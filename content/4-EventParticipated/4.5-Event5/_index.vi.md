---
title: "Event 5"
weight: 1
chapter: false
pre: " <b> 4.5. </b> "
---
# **AWS Cloud Mastery Series #3: ​Theo AWS Well-Architected Security Pillar**

**Thời gian:** 8:30 – 12:00 Thứ Bảy, ngày 29 tháng 11 năm 2025
**Địa điểm:** AWS Event Hall, Tầng 26 – Bitexco Tower, TP. Hồ Chí Minh

## **Mục tiêu sự kiện**

Workshop này mang đến cái nhìn **chuyên sâu và toàn diện về trụ cột Security trong AWS Well-Architected Framework**, tập trung vào cách thiết kế, triển khai và vận hành hệ thống an toàn trên AWS.  
Nội dung bao phủ **đầy đủ 5 miền bảo mật**, từ quản lý danh tính đến ứng phó sự cố, với trọng tâm là **các best practices có thể áp dụng ngay trong thực tế**.


## **Cấu trúc chương trình & Nội dung chính**

### **Khai mạc & Nền tảng bảo mật**

* Tổng quan về **Security Pillar** trong AWS Well-Architected Framework  
* Các nguyên tắc cốt lõi:
  * **Least Privilege**  
  * **Zero Trust**  
  * **Defense in Depth**  
* Hiểu rõ **AWS Shared Responsibility Model**


### **Pillar 1 — Identity & Access Management (IAM)**

* Thiết kế IAM hiện đại:
  * Users – Roles – Policies  
* **IAM Identity Center**:
  * Single Sign-On (SSO)  
  * Permission sets  
* Best practices:
  * Multi-Factor Authentication (MFA)  
  * Credential rotation  
  * IAM Access Analyzer  


### **Pillar 2 — Detection & Monitoring**

* Phát hiện và giám sát liên tục với:
  * AWS CloudTrail  
  * Amazon GuardDuty  
  * AWS Security Hub  
* Logging ở mọi lớp:
  * VPC Flow Logs  
  * Application Load Balancer logs  
  * Amazon S3 access logs  
* Giới thiệu khái niệm **Detection-as-Code**


### **Pillar 3 — Infrastructure Protection**

* Bảo mật mạng và workload:
  * Chiến lược phân tách VPC  
  * So sánh Security Groups và Network ACLs  
* Phòng thủ nhiều lớp:
  * AWS WAF  
  * AWS Shield  
  * AWS Network Firewall  


### **Pillar 4 — Data Protection**

* Chiến lược mã hóa dữ liệu:
  * Mã hóa at-rest  
  * Mã hóa in-transit  
* Quản lý khóa và secrets:
  * AWS KMS  
  * AWS Secrets Manager  
  * AWS Systems Manager Parameter Store  


### **Pillar 5 — Incident Response**

* Vòng đời xử lý sự cố (Incident Response lifecycle)  
* Playbook ứng phó sự cố:
  * IAM key bị lộ  
  * S3 bucket public ngoài ý muốn  
* Tự động phản ứng sự cố bằng:
  * AWS Lambda  
  * AWS Step Functions  


### **Tổng kết & Hỏi đáp**

* Tóm tắt các ý chính  
* Thảo luận các tình huống thực tế


## **Những điều học được**

* **Least Privilege là nền tảng**  
  * Luôn bắt đầu với quyền tối thiểu, chỉ mở rộng khi thực sự cần.

* **Zero Trust Architecture**  
  * Không mặc định tin tưởng bất kỳ thành phần nào, kể cả trong mạng nội bộ.

* **Defense in Depth**  
  * Bảo mật hiệu quả phải được triển khai đồng thời ở nhiều lớp.

* **Tự động hóa phát hiện sự cố**  
  * Hệ thống phát hiện cần hoạt động liên tục và tự động.

* **Chuẩn bị Incident Response**  
  * Playbook cần được tài liệu hóa, kiểm thử và cập nhật thường xuyên.


## **Ứng dụng vào công việc**

* Triển khai **IAM Access Analyzer** cho các AWS account hiện tại.  
* Thiết lập **GuardDuty** và **Security Hub** để giám sát tập trung.  
* Xây dựng **playbook ứng phó sự cố** cho các kịch bản phổ biến.  
* Rà soát và siết chặt **Security Group rules** theo nguyên tắc least privilege.  
* Bật mã hóa cho toàn bộ data store:
  * Amazon S3  
  * Amazon RDS  
  * Amazon DynamoDB  


## **Trải nghiệm sự kiện**

Trước đây, bảo mật luôn là chủ đề khô khan và khó tiếp cận, nhưng workshop này đã biến nó thành **những tình huống “chiến đấu” rất thực tế**.

* Việc mô tả các kịch bản như **lộ access key** hay **S3 bucket bị public** chỉ ra mức độ nguy hiểm của những lỗi tưởng chừng rất cơ bản.  
* Tư duy **Zero Trust** làm thay đổi hoàn toàn cách thiết kế kiến trúc hệ thống – không còn tin tưởng bất kỳ thành phần nào.  
* Các dịch vụ như **GuardDuty** hay **Security Hub** mang lại sự yên tâm khi vận hành hệ thống trên Cloud.


## **Kết luận chính**

* **Security by Design**  
  * Bảo mật phải được tính toán ngay từ đầu, không phải là phần bổ sung sau khi sản phẩm hoàn thành.

* **Nguyên tắc Least Privilege**  
  * Dù việc cấu hình IAM chi tiết tốn nhiều công sức, đây vẫn là “điểm chặn” quan trọng nhất để giảm thiểu thiệt hại khi sự cố xảy ra.

* **Luôn sẵn sàng ứng phó**  
  * Sự cố có thể xảy ra bất cứ lúc nào.  
  * Việc chuẩn bị playbook giúp đội ngũ xử lý vấn đề một cách bình tĩnh, có hệ thống và nhanh chóng hơn.

### Hình ảnh sự kiện

![img](/images/4-Event/Event-5/z7309533778160_d73d04090668200f3e05d45a25f251ba.jpg)
![img](/images/4-Event/Event-5/z7309533786182_0826a264ad96bc67fdfcc6cec7146286.jpg)
![img](/images/4-Event/Event-5/z7309533793690_64f27fd001e9424f6b408301a5a19bcc.jpg)