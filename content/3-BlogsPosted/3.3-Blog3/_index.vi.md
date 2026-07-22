---
title: "Tối Ưu Chi Phí Amazon EBS: Vì Sao Doanh Nghiệp Nên Chuyển Từ gp2 Sang gp3?"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Tối Ưu Chi Phí Amazon EBS: Vì Sao Doanh Nghiệp Nên Chuyển Từ gp2 Sang gp3?

Amazon EBS (Elastic Block Store) là dịch vụ lưu trữ block storage được sử dụng phổ biến cùng Amazon EC2 trong hầu hết các hệ thống Production. Qua nhiều năm, không ít doanh nghiệp vẫn đang vận hành khối lượng lớn EBS Volume sử dụng loại **gp2 (General Purpose SSD)** bởi đây từng là lựa chọn mặc định của AWS.

Tuy nhiên, kể từ khi loại ổ đĩa thế hệ mới **gp3** được ra mắt, AWS đã liên tục khuyến nghị người dùng chuyển đổi. Không chỉ cắt giảm ngay **20% chi phí lưu trữ**, gp3 còn mang lại hiệu năng baseline cao hơn và khả năng cấu hình linh hoạt tuyệt đối.

Đây là một trong những chiến dịch tối ưu hóa ngân sách (Quick Win) có tỷ lệ ROI cao nhất dành cho các đội ngũ Cloud Operations và FinOps.

---

### BÀI TOÁN

Trong mô hình vận hành hạ tầng đám mây quy mô lớn (với hàng trăm đến hàng nghìn máy chủ EC2), chi phí lưu trữ Amazon EBS chiếm một tỷ trọng đáng kể trong hóa đơn AWS hàng tháng.

Khi doanh nghiệp vẫn duy trì loại ổ đĩa thế hệ cũ gp2, hệ thống phải đối mặt với các bài toán:

* **Chi phí lưu trữ cao hơn 20%:** Đơn giá GB/tháng của gp2 cao hơn khoảng 20% so với gp3 trên tất cả các AWS Region.
* **Mối liên kết cứng giữa Dung lượng và Hiệu năng (IOPS):** Để có hiệu năng IOPS cao hơn cho ứng dụng, doanh nghiệp buộc phải mua thêm dung lượng lưu trữ (GB) không cần thiết.
* **Lãng phí tài nguyên:** Nhiều ứng dụng cần IOPS cao nhưng dung lượng dữ liệu nhỏ (như DB logs, caching nodes) bị buộc phải phình to kích thước ổ đĩa để lấy IOPS.

---

### KIẾN TRÚC CŨ (gp2) VÀ VẤN ĐỀ PHÁT SINH

Trong kiến trúc của gp2, hiệu năng ổ đĩa được phân bổ theo tỷ lệ cố định **3 IOPS cho mỗi 1 GB dung lượng**.

Mô hình này tạo ra hai hạn chế kỹ thuật lớn:

#### 1. Lãng phí chi phí khi mua thêm GB chỉ để lấy IOPS (Capacity Coupling)
*Ví dụ:* Một ứng dụng Database cần 3.000 IOPS để xử lý giao dịch. Với gp2, ổ đĩa bắt buộc phải có kích thước tối thiểu **1.000 GB** (1.000 GB × 3 = 3.000 IOPS). Nếu dữ liệu thực tế chỉ dùng 100 GB, doanh nghiệp đang phải trả tiền thừa cho 900 GB lưu trữ lãng phí mỗi tháng.

#### 2. Giới hạn Throughput phụ thuộc vào kích thước
Throughput của gp2 được tính toán dựa trên kích thước Volume. Các ổ đĩa nhỏ (dưới 170 GB) bị giới hạn băng thông truy xuất, dễ dẫn tới hiện tượng thắt cổ chai (throttling) khi I/O tăng đột biến.

---

### GIẢI PHÁP MỚI VỚI AMAZON EBS gp3

Dịch vụ ổ đĩa thế hệ mới **gp3** giải quyết hoàn toàn rào cản này bằng kiến trúc **Tách biệt độc lập giữa Dung lượng, IOPS và Throughput**.

**Quy trình chuyển đổi Zero-Downtime:**
1. Rà soát danh sách các Volume gp2 trên hệ thống bằng **AWS Cost Optimization Hub** hoặc **AWS CLI**.
2. Thực hiện lệnh `ModifyVolume` chuyển đổi kiểu ổ đĩa từ `gp2` sang `gp3` trực tiếp trên Volume đang chạy.
3. Nhờ tính năng **Amazon EBS Elastic Volumes**, quá trình chuyển đổi diễn ra trực tiếp trong ngầm mà không cần dừng máy chủ EC2, không cần reboot và không ảnh hưởng tới ứng dụng.
4. Cập nhật mã nguồn Infrastructure as Code (Terraform / CloudFormation) với thuộc tính `volume_type = "gp3"`.

---

### VÌ SAO AMAZON EBS gp3 PHÙ HỢP?

* **Tiết kiệm ngay 20% chi phí:** Đơn giá GB của gp3 rẻ hơn 20% so với gp2 trên tất cả các Region.
* **Baseline IOPS cao miễn phí:** gp3 mặc định cung cấp sẵn **3.000 IOPS** và **125 MB/s Throughput** hoàn toàn miễn phí cho mọi kích thước ổ đĩa (ngay cả với Volume 10 GB).
* **Cấu hình độc lập linh hoạt:** Khi ứng dụng cần 10.000 IOPS, bạn chỉ cần mua thêm IOPS riêng lẻ mà không cần tăng dung lượng đĩa.

---

### NHỮNG DỊCH VỤ AWS XUẤT HIỆN TRONG KIẾN TRÚC

* **Amazon EBS (Elastic Block Store):** Ổ đĩa lưu trữ khối thế hệ mới gp3.
* **Amazon EC2:** Máy chủ tính toán đang gắn ổ đĩa EBS.
* **AWS Cost Optimization Hub & Cost Explorer:** Công cụ rà soát và ước tính chi phí tiết kiệm.
* **AWS Systems Manager (SSM) & AWS Lambda:** Tự động hóa quy trình chuyển đổi hàng loạt.
* **Amazon CloudWatch:** Giám sát các chỉ số I/O (`VolumeReadOps`, `VolumeWriteOps`, `VolumeThroughputPercentage`).

---

### BÀI HỌC RÚT RA TỪ CASE STUDY

Chuyển đổi từ gp2 sang gp3 là một ví dụ điển hình về tối ưu hóa FinOps mang lại hiệu quả tức thì mà không đánh đổi bằng rủi ro hạ tầng.

**Bài học rút ra:**
* Luôn rà soát và cập nhật các thế hệ tài nguyên AWS mới (Resource Modernization) để tận hưởng đơn giá thấp hơn và hiệu năng tốt hơn.
* Kiến trúc tách biệt (Decoupled Performance) giúp doanh nghiệp kiểm soát ngân sách chính xác theo đúng nhu cầu sử dụng thực tế.
* Tận dụng tối đa tính năng Zero-Downtime (Elastic Volumes) để thực hiện cải tiến hạ tầng liên tục mà không gây gián đoạn dịch vụ.

* Bài viết gốc: [AWS Storage Blog - Migrate your Amazon EBS volumes from gp2 to gp3 and save up to 20% on costs](https://aws.amazon.com/blogs/storage/migrate-your-amazon-ebs-volumes-from-gp2-to-gp3-and-save-up-to-20-on-costs/)

`#AWS` `#AmazonEBS` `#AWSStorage` `#CostOptimization` `#FinOps` `#AmazonEC2` `#CloudComputing` `#DevOps`
