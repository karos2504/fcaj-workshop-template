---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Blog 1: Những điều Developer và DevOps cần biết

Xin chào mọi người!

Amazon S3 từ lâu đã là một trong những dịch vụ lưu trữ phổ biến nhất trên AWS, được sử dụng trong rất nhiều hệ thống từ website tĩnh, data lake, backup cho đến các ứng dụng AI/ML. Bên cạnh khả năng mở rộng gần như không giới hạn, bảo mật dữ liệu luôn là một trong những yếu tố được AWS ưu tiên hàng đầu.

Mới đây, AWS đã công bố một thay đổi quan trọng liên quan đến cơ chế mã hóa **Server-Side Encryption with Customer-Provided Keys (SSE-C)**. Bắt đầu từ tháng 04/2026, các S3 General Purpose Bucket mới sẽ không còn hỗ trợ SSE-C theo mặc định. Đây là thay đổi có thể ảnh hưởng trực tiếp đến các ứng dụng đang sử dụng phương thức mã hóa này.

---

### 1. NHỮNG THAY ĐỔI CỐT LÕI VÀ NGUYÊN NHÂN TỪ AWS

Mặc dù SSE-C cho phép doanh nghiệp hoàn toàn kiểm soát khóa mã hóa, nhưng điều này đồng nghĩa với việc toàn bộ trách nhiệm quản lý khóa thuộc về phía ứng dụng. Nếu khóa bị mất hoặc gửi sai, dữ liệu sẽ không thể được giải mã.

Theo thông báo từ AWS, kể từ tháng 04/2026:

* **Vô hiệu hóa trên Bucket mới:** Các General Purpose Bucket mới sẽ mặc định không hỗ trợ SSE-C.
* **Áp dụng cho Account chưa sử dụng:** Với những AWS Account chưa từng lưu dữ liệu được mã hóa bằng SSE-C, các bucket hiện có cũng sẽ bị vô hiệu hóa tính năng này.
* **Trả về lỗi HTTP 403 Access Denied:** Nếu ứng dụng vẫn gửi request `PutObject` kèm các header của SSE-C mà bucket chưa được cấu hình lại (`x-amz-server-side-encryption-customer-algorithm`, `x-amz-server-side-encryption-customer-key`, `x-amz-server-side-encryption-customer-key-MD5`), Amazon S3 sẽ chặn và trả về lỗi ngay lập tức.

Thay đổi này nhằm mục đích giảm nguy cơ cấu hình sai cho người dùng mới, đồng thời thúc đẩy các hệ thống dịch chuyển sang giải pháp quản lý khóa tập trung an toàn hơn như **SSE-KMS**.

---

### 2. KỸ THUẬT VẬN HÀNH VÀ HƯỚNG XỬ LÝ CHO DEVELOPER / DEVOPS

Để tránh nguy cơ gián đoạn dịch vụ đối với các hệ thống như pipeline backup, upload tài liệu, dịch vụ chia sẻ file hay Data Lake sử dụng SDK cũ, anh em cần chủ động thực hiện các bước sau:

1. **Kích hoạt thủ công nếu bắt buộc dùng SSE-C:** Quản trị viên cần chủ động bật lại tính năng SSE-C thông qua API hoặc cập nhật kịch bản Infrastructure as Code (IaC) như AWS CloudFormation, Terraform, AWS CDK, AWS CLI trước khi triển khai.
2. **Rà soát toàn bộ hệ thống:** Kiểm tra lại toàn bộ S3 Bucket, kiểm tra mã nguồn ứng dụng hoặc SDK có đang gửi Customer-Provided Keys hay không.
3. **Lộ trình chuyển đổi sang SSE-S3 hoặc SSE-KMS:**
   * **Sử dụng SSE-S3:** Nếu cần giải pháp đơn giản nhất, không tốn thêm chi phí và được bật mặc định cho đa số ứng dụng.
   * **Sử dụng SSE-KMS:** Đối với môi trường Production yêu cầu mức độ bảo mật cao, cần phân quyền IAM, theo dõi lịch sử truy cập bằng CloudTrail, tự động xoay vòng khóa và đáp ứng các tiêu chuẩn như PCI DSS, HIPAA, ISO 27001.

---

### KẾT LUẬN

Thay đổi này rất quan trọng đối với các hệ thống đang sử dụng SSE-C. Việc rà soát cấu hình, cập nhật Infrastructure as Code và cân nhắc chuyển sang SSE-KMS sẽ giúp hệ thống hoạt động ổn định hơn, hạn chế tối đa nguy cơ gián đoạn dịch vụ khi AWS chính thức áp dụng chính sách mới.

* Nguồn tham khảo: [AWS Storage Blog - Amazon S3 security updates: Disabling SSE-C by default](https://aws.amazon.com/blogs/storage/amazon-s3-security-updates-disabling-sse-c-by-default/)

`#AWS` `#AmazonS3` `#CloudSecurity` `#SSEKMS` `#SSEC` `#DevOps` `#CloudComputing` `#AWSStorage`
