---
title: "AWS COST OPTIMIZATION – Tối ưu chi phí Amazon EBS: Vì sao doanh nghiệp nên chuyển từ gp2 sang gp3?"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# AWS COST OPTIMIZATION – Tối ưu chi phí Amazon EBS: Vì sao doanh nghiệp nên chuyển từ gp2 sang gp3?

Xin chào mọi người!

Amazon EBS (Elastic Block Store) là dịch vụ lưu trữ block storage được sử dụng phổ biến cùng Amazon EC2 trong nhiều hệ thống Production. Qua nhiều năm, không ít doanh nghiệp vẫn đang vận hành khối lượng lớn EBS Volume sử dụng loại **gp2 (General Purpose SSD)** bởi đây từng là lựa chọn mặc định của AWS.

Tuy nhiên, kể từ khi **gp3** được giới thiệu, AWS đã nhiều lần khuyến nghị người dùng chuyển đổi sang loại ổ đĩa thế hệ mới này. Không chỉ có chi phí thấp hơn, gp3 còn mang đến hiệu năng ổn định và khả năng cấu hình linh hoạt hơn đáng kể. Theo **AWS Cost Optimization Hub**, chỉ riêng việc chuyển đổi từ gp2 sang gp3 có thể giúp doanh nghiệp **tiết kiệm tới 20% chi phí lưu trữ EBS**, đồng thời cải thiện hiệu năng của hệ thống mà không cần thay đổi kiến trúc ứng dụng hay gián đoạn dịch vụ.

---

### 1. SO SÁNH KIẾN TRÚC VÀ HIỆU NĂNG: gp2 VS gp3

Sự khác biệt cốt lõi giữa hai thế hệ ổ đĩa nằm ở cơ chế phân bổ hiệu năng:

* **gp2 (Hiệu năng phụ thuộc Dung lượng):** Hiệu năng của ổ đĩa bị khóa chặt với dung lượng lưu trữ (3 IOPS/GB). Nếu ứng dụng yêu cầu nhiều IOPS hơn, bạn buộc phải tăng dung lượng Volume (ví dụ: muốn có 3.000 IOPS thì ổ đĩa phải đạt từ 1.000 GB trở lên), gây lãng phí chi phí cho phần dung lượng không thực sự sử dụng.
* **gp3 (Tách biệt Dung lượng và Hiệu năng):** Thiết kế độc lập hoàn toàn giữa Dung lượng, IOPS và Throughput. Một Volume gp3 mặc định đã cung cấp sẵn **3.000 IOPS** và **125 MB/s Throughput** hoàn toàn miễn phí mà không phụ thuộc vào kích thước ổ đĩa. Khi cần hiệu năng cao hơn, bạn chỉ cần mua thêm IOPS hoặc Throughput riêng lẻ mà không cần mở rộng dung lượng.

#### So sánh nhanh:

* **Đơn giá lưu trữ:** gp3 thấp hơn tới 20% so với gp2 trên tất cả các Region.
* **Mức Baseline mặc định:** gp2 đạt 3 IOPS/GB (tối đa 16.000 IOPS), trong khi gp3 cung cấp sẵn 3.000 IOPS cố định (tối đa 16.000 IOPS).
* **Throughput mặc định:** gp2 từ 128 MB/s đến 250 MB/s (tùy dung lượng), còn gp3 cố định 125 MB/s (có thể chủ động nâng lên 1.000 MB/s).
* **Cơ chế mở rộng:** gp2 buộc phải mua thêm GB để tăng hiệu năng, còn gp3 cho phép tùy chỉnh độc lập GB, IOPS và Throughput.

---

### 2. LỢI ÍCH CỐT LÕI VÀ CÁC WORKLOAD ƯU TIÊN

* **Tối ưu ngân sách FinOps ngay lập tức:** Đơn giá GB/tháng của gp3 thấp hơn khoảng 20% so với gp2. Với các hệ thống vận hành hàng trăm hoặc hàng nghìn Volume, việc chuyển đổi mang lại khoản tiết kiệm chi phí vận hành hàng tháng rất lớn.
* **Chuyển đổi Zero-Downtime:** Nhờ tính năng Amazon EBS Elastic Volumes, việc chuyển từ gp2 sang gp3 diễn ra trực tiếp trên Volume đang hoạt động. Máy chủ EC2 tiếp tục chạy bình thường, không cần reboot, không cần restore dữ liệu và không ảnh hưởng tới ứng dụng.

#### Các Workload ưu tiên chuyển đổi:

* Web Application & API Server
* Database cỡ nhỏ và trung bình (MySQL, PostgreSQL, MongoDB, SQL Server)
* Bastion Host, Monitoring Server (Prometheus, Zabbix)
* CI/CD Workers (Jenkins, GitLab Runner)
* File Server & Storage Node

---

### 3. QUY TRÌNH RÀ SOÁT, TỰ ĐỘNG HÓA VÀ THEO DÕI CHO DEVOPS

Để triển khai chuyển đổi hàng loạt một cách an toàn và hiệu quả, đội ngũ DevOps có thể thực hiện theo quy trình kỹ thuật sau:

* **Bước 1: Rà soát các Volume gp2 hiện có**  
  Sử dụng các công cụ quản trị như AWS Cost Optimization Hub, AWS Cost Explorer hoặc AWS CLI để định danh các Volume cần nâng cấp và ước tính chi phí tiết kiệm.

* **Bước 2: Tự động hóa quá trình chuyển đổi (IaC & Automation)**  
  Thay vì thao tác thủ công từng Volume trên AWS Management Console, nên sử dụng AWS Systems Manager (SSM) Automation, Lambda để gọi API `ModifyVolume` nâng cấp hàng loạt. Đối với Infrastructure as Code (Terraform / CloudFormation / AWS CDK), cập nhật thuộc tính `volume_type = "gp3"` trong mã nguồn quản lý hạ tầng để tránh việc IaC ghi đè lại cấu hình cũ trong các lần deploy sau.

* **Bước 3: Theo dõi CloudWatch Metrics sau chuyển đổi**  
  Sau khi nâng cấp, cần theo dõi các chỉ số quan trọng trên Amazon CloudWatch trong khoảng 7–14 ngày:
  * `VolumeReadOps` và `VolumeWriteOps`: Tính toán tổng IOPS thực tế sử dụng.
  * `VolumeThroughputPercentage`: Kiểm tra mức tiêu thụ băng thông.
  * `VolumeConsumedReadWriteOps`: Kiểm tra xem hệ thống có bị nghẽn (throttling) do vượt quá mức 3.000 IOPS mặc định hay không. Nếu có, chủ động cấu hình tăng thêm IOPS cho Volume đó.

---

### KẾT LUẬN

Chuyển đổi từ gp2 sang gp3 là một trong những hành động tối ưu chi phí (Quick Win) có tỷ lệ lợi ích trên chi phí cao nhất trên AWS. Doanh nghiệp vừa cắt giảm ngay 20% chi phí lưu trữ, vừa sở hữu hiệu năng linh hoạt và độc lập hơn mà không phải chấp nhận bất kỳ khoảng thời gian dừng hệ thống (downtime) nào. Nếu hạ tầng của bạn vẫn còn các ổ đĩa gp2, đây là thời điểm thích hợp nhất để tự động hóa quá trình nâng cấp này.

* Nguồn tham khảo: [AWS Storage Blog - Migrate your Amazon EBS volumes from gp2 to gp3 and save up to 20% on costs](https://aws.amazon.com/blogs/storage/migrate-your-amazon-ebs-volumes-from-gp2-to-gp3-and-save-up-to-20-on-costs/)

`#AWS` `#AmazonEBS` `#AWSStorage` `#CostOptimization` `#FinOps` `#AmazonEC2` `#CloudComputing` `#DevOps`
