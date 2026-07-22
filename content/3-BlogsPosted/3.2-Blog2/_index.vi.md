---
title: "AWS BACKUP – AWS Backup bổ sung Item-Level Recovery cho Amazon EBS và Amazon S3"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# AWS BACKUP – AWS Backup bổ sung Item-Level Recovery cho Amazon EBS và Amazon S3: Khôi phục đúng tệp cần thiết thay vì toàn bộ Backup

Xin chào mọi người!

Một trong những tình huống khá phổ biến khi vận hành hệ thống là người dùng hoặc ứng dụng vô tình xóa nhầm dữ liệu. Đó có thể chỉ là một file cấu hình, một file log, một tài liệu PDF hoặc một video được lưu trên Amazon EBS hay Amazon S3. Tuy nhiên, trước đây việc khôi phục lại đúng một tệp như vậy lại không hề đơn giản.

Đối với Amazon EBS Snapshot hoặc các bản sao lưu được quản lý bởi AWS Backup, quản trị viên thường phải khôi phục toàn bộ volume, gắn volume vào EC2 rồi mới tìm và sao chép lại đúng file cần thiết. Quy trình này vừa mất thời gian, vừa phát sinh thêm chi phí lưu trữ và tài nguyên tính toán.

Để giải quyết vấn đề này, AWS đã giới thiệu **AWS Backup Search** và **Item-Level Recovery**, cho phép tìm kiếm và khôi phục trực tiếp từng file riêng lẻ từ các bản sao lưu của Amazon EBS và Amazon S3.

---

### 1. ITEM-LEVEL RECOVERY LÀ GÌ VÀ CÁC TRƯỜNG HỢP SỬ DỤNG THỰC TẾ

**Item-Level Recovery (ILR)** là khả năng khôi phục dữ liệu ở cấp độ từng đối tượng (file hoặc object) thay vì phải khôi phục toàn bộ bản sao lưu. Điều này đồng nghĩa với việc nếu chỉ cần lấy lại một file duy nhất, bạn không còn phải restore cả một EBS Volume dung lượng hàng trăm GB hoặc nhiều TB nữa.

Tính năng này giải quyết hiệu quả các bài toán thực tế:

* **Khôi phục file bị xóa nhầm:** Khi nhân viên vô tình xóa file cấu hình của ứng dụng hoặc một tài liệu quan trọng trên volume của EC2, quản trị viên chỉ cần tìm đúng file đó trong AWS Backup và thực hiện Item-Level Restore chỉ trong vài phút.
* **Phục vụ Audit và điều tra sự cố:** Dễ dàng truy xuất các tài liệu cũ như file PDF hợp đồng, báo cáo Excel, video giám sát hay file CSV xuất dữ liệu mà không cần mount snapshot hay restore cả volume.
* **Rút ngắn thời gian phục hồi (RTO):** Giúp rút ngắn thời gian downtime của các hệ thống Production từ hàng giờ xuống chỉ còn vài phút khi sự cố mất file xảy ra.

---

### 2. CƠ CHẾ HOẠT ĐỘNG VÀ CÁC BƯỚC CHUẨN BỊ CHO DEVOPS / OPERATIONS

Để hệ thống có thể xác định đúng file cần phục hồi mà không phải quét toàn bộ snapshot, AWS Backup dựa trên cơ chế lập chỉ mục (Indexing) metadata của các file trong quá trình tạo Backup.

Các lưu ý và bước triển khai quan trọng:

1. **Bật Backup Indexing:** Đây là điều kiện tiên quyết khi tạo Backup Plan hoặc chạy On-Demand Backup để AWS lập chỉ mục dữ liệu.
2. **Sử dụng Tag hợp lý:** Gắn Tag nhất quán giữa EC2 Instance, Amazon EBS Volume và Backup Vault để dễ dàng quản lý cũng như tìm kiếm trong môi trường nhiều workload.
3. **Sử dụng AWS Backup Search:** Truy vấn trực tiếp file cần tìm theo tên file, đường dẫn, định dạng, khoảng thời gian hoặc metadata rồi thực hiện Item-Level Restore.
4. **Tối ưu vận hành và bảo vệ dữ liệu:** Kết hợp thiết lập Backup Plan phù hợp, kiểm thử khả năng Restore định kỳ và áp dụng AWS Backup Vault Lock để tăng cường khả năng chống ransomware.

---

### KẾT LUẬN

AWS Backup Search và Item-Level Recovery là một cải tiến đáng giá dành cho các đội DevOps và Cloud Operations. Thay vì phải khôi phục toàn bộ Snapshot chỉ để lấy lại một file nhỏ, giờ đây bạn có thể tìm kiếm và phục hồi chính xác dữ liệu cần thiết trong thời gian ngắn hơn rất nhiều, giúp giảm chi phí vận hành và cải thiện đáng kể chỉ số RTO.

* Nguồn tham khảo: [AWS Storage Blog - AWS Backup Search and item-level restore](https://aws.amazon.com/blogs/storage/aws-backup-search-and-item-level-restore/)

`#AWS` `#AWSBackup` `#AmazonEBS` `#AmazonS3` `#DisasterRecovery` `#DataProtection` `#DevOps` `#CloudComputing`
