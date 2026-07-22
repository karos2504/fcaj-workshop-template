---
title: "AWS ARCHITECTURE CASE STUDY – Samsung Giải Quyết Bài Toán Đồng Bộ Giá Với AWS Lambda Response Streaming"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AWS ARCHITECTURE CASE STUDY – Từ Cache Theo Giờ Đến Real-Time Pricing: Samsung Giải Quyết Bài Toán Đồng Bộ Giá Với AWS Lambda Response Streaming

Xin chào mọi người!

Trong thương mại điện tử (E-Commerce), giá sản phẩm là một trong những dữ liệu quan trọng nhất. Chỉ cần giá hiển thị trên trang danh mục/chi tiết khác với giá tại bước thanh toán (Checkout), trải nghiệm khách hàng có thể bị ảnh hưởng nghiêm trọng và làm suy giảm niềm tin vào thương hiệu.

Hôm nay, mình muốn chia sẻ một bài phân tích kiến trúc rất thú vị từ **AWS Architecture Blog** về cách **Samsung** cải tiến toàn bộ hệ thống định giá trên trang thương mại điện tử **Samsung.com** bằng cách kết hợp **AWS Lambda Response Streaming** và **Amazon CloudFront**. 

Đây là một Case Study điển hình về việc lựa chọn tư duy kiến trúc phù hợp (Source of Truth) thay vì chỉ tập trung lạm dụng việc lưu trữ bộ nhớ tạm (Cache).

---

### 1. BÀI TOÁN KINH DOANH VÀ THỬ THÁCH VẬN HÀNH

**Samsung.com** là kênh bán hàng trực tiếp (D2C) của Samsung, phục vụ hàng triệu người dùng với dải sản phẩm đa dạng từ điện thoại, máy tính bảng, TV đến thiết bị gia dụng và phụ kiện.

Trong các sự kiện mua sắm lớn như **Black Friday** hay **Flash Sale**:
* Một trang danh sách sản phẩm (Product Listing Page) có thể phải hiển thị đồng thời giá của hơn **30 SKU khác nhau**.
* Mỗi sản phẩm lại có hàng loạt biến thể phức tạp: *Màu sắc, dung lượng bộ nhớ, chương trình khuyến mãi theo thời điểm, ưu đãi theo khu vực địa lý hoặc đối tác*.

Điều này khiến việc truy vấn và tính toán giá chính xác theo thời gian thực (Real-time) trở thành một thách thức cực kỳ lớn về cả hiệu năng lẫn chi phí.

---

### 2. KIẾN TRÚC CŨ VÀ NHỮNG HẠN CHẾ CỐT LÕI

Trong kiến trúc cũ, Samsung xây dựng một tầng trung gian **Data Aggregation Layer** nằm giữa hệ thống tính giá **Pricing Engine** và mạng phân phối nội dung **Amazon CloudFront**. 

Một **Cron Job** tự động sẽ chạy định kỳ mỗi giờ một lần để:
1. Đọc toàn bộ dữ liệu sản phẩm từ Pricing Engine.
2. Tính toán trước (Pre-compute) tất cả các tổ hợp giá có thể xảy ra.
3. Ghi kết quả đã tính sẵn vào bộ nhớ tạm (Cache) để phục vụ request của người dùng.

Mặc dù mô hình này giúp tốc độ đọc dữ liệu vô cùng nhanh, nhưng nó lại gây ra hai điểm nghẽn nghiêm trọng:

#### A. Bùng nổ tổ hợp dữ liệu (Permutation Explosion)
Khi số lượng sản phẩm và các thuộc tính biến thể tăng lên, số lượng tổ hợp giá phải tính trước tăng theo **cấp số nhân**. 
> *Ví dụ:* 30 sản phẩm × nhiều phiên bản bộ nhớ × nhiều màu sắc × hàng chục mã giảm giá có thể tạo ra **hàng chục nghìn bản ghi** cần tiền xử lý. Hệ thống tiêu tốn lượng lớn tài nguyên tính toán và lưu trữ cho những dữ liệu mà người dùng thậm chí không bao giờ click xem.

#### B. Độ trễ đồng bộ dữ liệu (Synchronization Lag)
Đây là vấn đề ảnh hưởng trực tiếp đến doanh thu. Vì Cron Job chỉ chạy **60 phút/lần**, dữ liệu giá trong Cache có thể bị chậm hơn giá thực tế tới 1 tiếng đồng hồ. 
> *Kịch bản sự cố:* Nếu chương trình Flash Sale bắt đầu lúc **10:05**, khách hàng truy cập lúc **10:15** vẫn sẽ nhìn thấy giá gốc chưa giảm cho tới khi Cron Job tiếp theo chạy vào lúc **11:00**.
> * **Hệ quả:** Giá hiển thị sai lệch, khách hàng bất ngờ/thất vọng khi bấm thanh toán, gia tăng tỷ lệ hủy giỏ hàng và làm mất uy tín thương hiệu.

---

### 3. GIẢI PHÁP MỚI VỚI AWS LAMBDA RESPONSE STREAMING

Thay vì tiếp tục tối ưu hóa tầng Cache phức tạp, Samsung đã đưa ra quyết định kiến trúc táo bạo: **Loại bỏ hoàn toàn tầng Data Aggregation trung gian**.

Kiến trúc mới được xây dựng theo nguyên tắc: **Luôn truy vấn dữ liệu từ nguồn gốc chính xác nhất (Source of Truth) ngay tại thời điểm người dùng gửi yêu cầu.**

```
[User Browser] ➔ [Amazon CloudFront Edge] ➔ (Cache Miss) ➔ [AWS Lambda Function URL] 
                                                                    │
                                            ┌───────────────────────┴───────────────────────┐
                                            ▼                                               ▼
                              [Fan-out API Request 1]                         [Fan-out API Request 2]
                                            │                                               │
                                            └───────────────────────┬───────────────────────┘
                                                                    ▼
                                                         [Pricing Engine Service]
                                                                    │
                                                (Stream chunks via Response Streaming)
                                                                    ▼
                                                     [Stream Response back to Client]
```

#### Quy trình xử lý theo thời gian thực:
1. Người dùng truy cập trang sản phẩm trên Samsung.com.
2. **Amazon CloudFront** kiểm tra Cache tại Edge Location.
3. Nếu Cache Miss, request được chuyển tiếp ngay tới **AWS Lambda** (thông qua Function URL).
4. Hàm Lambda thực hiện kỹ thuật **Fan-out**, phát các request song song tới **Pricing Engine** để lấy giá cho 30+ sản phẩm cùng lúc.
5. Ngay khi từng phần dữ liệu giá của sản phẩm đầu tiên được Pricing Engine trả về, Lambda sử dụng **Response Streaming** để đẩy ngay các mảng dữ liệu (chunks) về cho phía Client mà không cần chờ tính xong toàn bộ 30 sản phẩm.
6. CloudFront tiếp tục cache nhẹ kết quả trong khoảng thời gian ngắn để tối ưu các request trùng lặp tiếp theo.

---

### 4. VÌ SAO AWS LAMBDA RESPONSE STREAMING LÀ "KEY-ENABLE"?

Thông thường, một hàm AWS Lambda phải chờ toàn bộ tiến trình xử lý hoàn tất rồi mới đóng gói toàn bộ JSON payload trả về cho client. Nếu phải gọi nhiều API bên ngoài, thời gian chờ (Latency) sẽ bị cộng dồn.

Với **AWS Lambda Response Streaming**:
* **Trả về dữ liệu tức thì (Stream Payload):** Lambda gửi các HTTP response chunk đầu tiên về trình duyệt ngay khi nhận được dữ liệu từ Pricing Engine.
* **Giảm chỉ số TTFB (Time To First Byte):** Trình duyệt của khách hàng có thể bắt đầu render khung giao diện và hiển thị giá của những sản phẩm đầu tiên ngay lập tức.
* **Đơn giản hóa hạ tầng:** Không cần duy trì cụm máy chủ Redis/ElastiCache đắt đỏ hay xây dựng kịch bản đồng bộ dữ liệu phức tạp.

---

### 5. CÁC DỊCH VỤ AWS TRONG KIẾN TRÚC

| Dịch Vụ AWS | Vai Trò Trong Hệ Thống Samsung.com |
| :--- | :--- |
| **Amazon CloudFront** | Mạng phân phối nội dung Edge, cache dữ liệu trong thời gian ngắn và bảo mật đường truyền. |
| **AWS Lambda** | Đóng vai trò làm Serverless Compute Engine thực hiện Fan-out request tính giá song song. |
| **Lambda Response Streaming** | Cơ chế stream HTTP Response theo dạng chunks để tối ưu chỉ số TTFB cho người dùng. |
| **Lambda Function URL** | Endpoint HTTPS trực tiếp kích hoạt hàm Lambda với chi phí và độ trễ thấp nhất. |
| **Provisioned Concurrency** | Duy trì sẵn các hàm Lambda ở trạng thái Warm, loại bỏ hoàn toàn Cold Start trong giờ cao điểm. |

---

### 6. BÀI HỌC KIẾN TRÚC RÚT RA (ARCHITECTURAL INSIGHTS)

Điều giá trị nhất từ Case Study của Samsung không chỉ nằm ở tính năng Lambda Response Streaming, mà là **Tư duy thiết kế hệ thống**:

1. **Bộ nhớ tạm (Cache) không phải là "viên đạn bạc":** Cache rất tốt cho tốc độ, nhưng trong các bài toán mà tính chính xác của dữ liệu (Data Accuracy) quan trọng hơn tốc độ thuần túy, Cache có thể trở thành nguyên nhân gây ra lỗi nghiệp vụ nghiêm trọng.
2. **Ưu tiên nguồn dữ liệu gốc (Source of Truth):** Với các hệ thống liên quan đến tài chính, giá bán, kho hàng, luôn truy vấn từ nguồn dữ liệu gốc tại thời điểm thực hiện giao dịch.
3. **Sức mạnh của Serverless Streaming:** Serverless hiện đại không chỉ xử lý các request ngắn dạng REST API, mà còn có khả năng xử lý và tổng hợp dữ liệu quy mô lớn theo dạng luồng (Streaming).
4. **Triết lý "Less is More":** Một kiến trúc đơn giản, ít tầng trung gian sẽ dễ bảo trì, ít điểm lỗi (Single Point of Failure) và mang lại tin cậy cao hơn một hệ thống nhiều tầng phức tạp.

---

* Bài viết gốc trên AWS Blog: [How Samsung achieved real-time pricing with AWS Lambda Response Streaming](https://aws.amazon.com/vi/blogs/architecture/how-samsung-achieved-real-time-pricing-with-aws-lambda-response-streaming/)

`#AWS` `#Serverless` `#AWSLambda` `#LambdaResponseStreaming` `#AmazonCloudFront` `#CloudArchitecture` `#SystemDesign` `#CaseStudy` `#DevOps`
