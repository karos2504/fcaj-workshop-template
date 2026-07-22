---
title: "Blog 4"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

# Blog 4: Từ Cache Theo Giờ Đến Real-Time Pricing với AWS Lambda Response Streaming

Xin chào mọi người!

Trong thương mại điện tử, giá sản phẩm là một trong những dữ liệu quan trọng nhất. Chỉ cần giá hiển thị trên trang sản phẩm khác với giá tại bước thanh toán, trải nghiệm khách hàng có thể bị ảnh hưởng nghiêm trọng.

Gần đây mình đọc được một bài chia sẻ khá thú vị từ AWS Architecture Blog về cách **Samsung** cải tiến hệ thống định giá trên **Samsung.com** bằng **AWS Lambda Response Streaming** và **Amazon CloudFront**.

Đây là một case study rất hay về việc lựa chọn kiến trúc phù hợp thay vì chỉ tập trung vào tối ưu hiệu năng.

---

### 1. BÀI TOÁN KINH DOANH VÀ THÁCH THỨC TẠI SAMSUNG.COM

Samsung.com là kênh bán hàng trực tiếp của Samsung, cung cấp nhiều dòng sản phẩm như điện thoại, TV, thiết bị gia dụng và phụ kiện.

Trong các sự kiện lớn như Black Friday, một trang danh sách sản phẩm có thể phải hiển thị giá của hơn 30 SKU khác nhau cùng lúc. Mỗi sản phẩm lại có nhiều biến thể:

* Màu sắc & Phiên bản bộ nhớ
* Chương trình khuyến mãi & Voucher
* Ưu đãi theo từng khu vực địa lý

Điều này khiến việc truy vấn giá theo thời gian thực trở thành một thách thức lớn về hạ tầng và độ trễ.

---

### 2. KIẾN TRÚC CŨ VÀ CÁC VẤN ĐỀ PHÁT SINH

Trong kiến trúc cũ, Samsung sử dụng một lớp **Data Aggregation** nằm giữa Pricing Engine và CloudFront. Một Cron Job sẽ chạy mỗi giờ để:

1. Lấy toàn bộ dữ liệu sản phẩm từ Pricing Engine.
2. Tính toán trước các tổ hợp giá có thể xảy ra.
3. Lưu kết quả vào cache để phục vụ người dùng.

Mô hình này giúp tăng tốc độ đọc dữ liệu nhưng lại tạo ra hai vấn đề lớn:

#### 1. Permutation Explosion (Bùng nổ tổ hợp dữ liệu)
Khi số lượng sản phẩm và biến thể tăng lên, số lượng tổ hợp giá tăng theo cấp số nhân. Ví dụ: 30 sản phẩm × nhiều phiên bản × nhiều chương trình khuyến mãi có thể tạo ra hàng nghìn hoặc hàng chục nghìn bản ghi cần được tính toán trước. Kết quả là hệ thống tiêu tốn nhiều tài nguyên lưu trữ và xử lý cho những dữ liệu có thể không bao giờ được người dùng truy cập.

#### 2. Synchronization Lag (Độ trễ đồng bộ dữ liệu)
Đây là vấn đề nghiêm trọng hơn. Vì Cron Job chỉ chạy mỗi giờ một lần nên dữ liệu trong cache có thể chậm hơn dữ liệu thực tế tới 60 phút. Nếu một chương trình Flash Sale bắt đầu lúc 10:05 thì khách hàng vẫn có thể nhìn thấy giá cũ cho đến khi Cron Job tiếp theo chạy vào 11:00.

**Hệ quả:**
* Giá hiển thị không chính xác
* Khách hàng bất ngờ khi thanh toán
* Mất niềm tin vào hệ thống và ảnh hưởng trực tiếp đến doanh thu

---

### 3. GIẢI PHÁP MỚI VỚI AWS LAMBDA RESPONSE STREAMING

Thay vì tiếp tục tối ưu cache, Samsung quyết định loại bỏ hoàn toàn tầng Data Aggregation. Kiến trúc mới được xây dựng dựa trên nguyên tắc: **Luôn lấy dữ liệu từ nguồn chính (Source of Truth) tại thời điểm người dùng gửi yêu cầu.**

#### Quy trình hoạt động:
1. Người dùng gửi yêu cầu lấy giá sản phẩm.
2. **Amazon CloudFront** kiểm tra cache tại Edge Location.
3. Nếu cache miss, request được chuyển đến **AWS Lambda**.
4. Lambda thực hiện fan-out và gửi song song nhiều request tới **Pricing Engine**.
5. Kết quả được stream ngay về phía người dùng khi có dữ liệu trả về.
6. CloudFront tiếp tục cache kết quả trong thời gian ngắn để tối ưu hiệu năng.

#### Vì sao AWS Lambda Response Streaming phù hợp?
Thông thường, Lambda sẽ đợi xử lý xong toàn bộ dữ liệu rồi mới trả về response. Điều này làm tăng thời gian chờ khi cần tổng hợp dữ liệu từ nhiều nguồn khác nhau.

Với **Lambda Response Streaming**:
* Dữ liệu được gửi về ngay khi có kết quả đầu tiên
* Giảm **Time To First Byte (TTFB)** đáng kể
* Người dùng nhận được phản hồi sớm hơn
* Không cần xây dựng thêm lớp cache trung gian phức tạp

---

### 4. CÁC DỊCH VỤ AWS TRONG KIẾN TRÚC

* **Amazon CloudFront:** Phân phối nội dung và cache ngắn hạn tại Edge.
* **AWS Lambda:** Xử lý logic nghiệp vụ tính toán giá.
* **Lambda Response Streaming:** Gửi phản hồi dạng stream giảm độ trễ TTFB.
* **Lambda Function URL:** Endpoint gọi trực tiếp hàm Lambda từ CloudFront.
* **Provisioned Concurrency:** Giảm thiểu rủi ro Cold Start trong giờ cao điểm.

---

### KẾT LUẬN & BÀI HỌC KIẾN TRÚC

Điều thú vị nhất không nằm ở Lambda Response Streaming mà nằm ở tư duy kiến trúc. Cache thường được xem là giải pháp cho các vấn đề hiệu năng. Tuy nhiên, trong những bài toán mà tính chính xác của dữ liệu quan trọng hơn tốc độ truy xuất, cache đôi khi lại trở thành nguyên nhân gây ra lỗi nghiệp vụ.

Case study của Samsung cho thấy rằng:
* Không phải lúc nào thêm cache cũng là hướng đi đúng.
* **Source of Truth** cần được ưu tiên trong các hệ thống liên quan đến giá bán và thanh toán.
* Serverless có thể giải quyết hiệu quả các bài toán tổng hợp dữ liệu theo thời gian thực.
* Một kiến trúc đơn giản hơn đôi khi lại mang lại kết quả tốt hơn một hệ thống nhiều tầng trung gian.

* Nguồn tham khảo: [AWS Architecture Blog - How Samsung achieved real-time pricing with AWS Lambda Response Streaming](https://aws.amazon.com/vi/blogs/architecture/how-samsung-achieved-real-time-pricing-with-aws-lambda-response-streaming/)

`#AWS` `#LambdaResponseStreaming` `#AmazonCloudFront` `#Serverless` `#RealTimePricing` `#SoftwareArchitecture` `#DevOps`
