---
title: "Blog 1"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# DISA STIG cho Amazon Linux 2023 hiện đã được phát hành

Tác giả: Mahak Arora | Ngày 10/09/2025 | Phân loại: [Announcements](https://aws.amazon.com/blogs/compute/category/post-types/announcements/), [Compute](https://aws.amazon.com/blogs/compute/category/compute/), [Intermediate (200)](https://aws.amazon.com/blogs/compute/category/learning-levels/intermediate-200/) | [Permalink](https://aws.amazon.com/blogs/compute/disa-stig-for-amazon-linux-2023-is-now-available/) 

Hôm nay, chúng tôi xin thông báo về việc phát hành Security Technical Implementation Guide (STIG) cho [Amazon Linux 2023 (AL2023)](https://aws.amazon.com/linux/amazon-linux-2023/), được phát triển thông qua sự hợp tác giữa Amazon Web Services (AWS) và [Defense Information Systems Agency](http://public.cyber.mil/stigs/) (DISA). Hướng dẫn STIG đóng vai trò quan trọng đối với các khách hàng thuộc [U.S. Department of Defense](https://www.war.gov/) (DOD) và các cơ quan Liên bang cần tuân thủ nghiêm ngặt các tiêu chuẩn bảo mật được xây dựng dựa trên [National Institute of Standards and Technology (NIST) 800-53](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) và các tài liệu liên quan. Tài liệu hướng dẫn triển khai kỹ thuật mới này cung cấp các cấu hình tăng cường bảo mật chi tiết cho Operating System (OS) dành cho các tổ chức triển khai AL2023 trong môi trường của DOD hoặc các cơ quan khác yêu cầu tuân thủ DISA STIG.

AL2023 STIG cung cấp cho khách hàng quyền truy cập vào tài liệu hướng dẫn OS đáp ứng các tiêu chuẩn bảo mật nghiêm ngặt của chính phủ. Hướng dẫn triển khai các cấu hình STIG này sẽ giúp đơn giản hóa quy trình bảo mật cho các tổ chức muốn thiết lập hệ thống kiểm soát an ninh mạng mạnh mẽ, dù là để duy trì tuân thủ quy định của DOD hay chủ động áp dụng các biện pháp bảo mật tốt nhất nhằm tăng cường mức độ bảo mật tổng thể.

**Triển khai AL2023 DISA STIG với AWS**

AWS Systems Manager (SSM) và EC2 Image Builder cung cấp các giải pháp gốc giúp triển khai cấu hình AL2023 DISA STIG trong môi trường của bạn. Đối với khách hàng đang vận hành workload AL2023 EC2, có thể sử dụng AWS Systems Manager (SSM) để đơn giản hóa việc triển khai STIG. Còn với khách hàng muốn xây dựng các AL2023 EC2 instances tuân thủ STIG để dùng trong triển khai, có thể tận dụng EC2 Image Builder và tự động hóa quá trình áp dụng AL2023 DISA STIG.

**Xây dựng Image tuân thủ STIG bằng EC2 Image Builder**

Khách hàng có thể sử dụng EC2 Image Builder để tăng cường và đơn giản hóa việc triển khai AL2023 DISA STIG. Cách tiếp cận tích hợp này giúp giảm đáng kể khối lượng công việc vận hành thường gắn liền với việc duy trì tuân thủ STIG. Nhờ đó, khách hàng của chúng tôi có thể tập trung vào nhiệm vụ cốt lõi của mình trong khi vẫn duy trì các tiêu chuẩn bảo mật cao nhất. Khách hàng của chúng tôi có thể sử dụng các thành phần tăng cường bảo mật Linux hiện có của AWS EC2 Image Builder, hiện đã hỗ trợ phát hiện AL2023 Category I, II, và III để tự động tạo các AL2023 EC2 images tuân thủ STIG với thao tác thủ công tối thiểu. Việc tự động hóa này giúp giảm đáng kể thời gian và công sức cần thiết cho việc triển khai tăng cường bảo mật. Thành phần tăng cường bảo mật EC2 Image Builder Linux mở rộng các khả năng đã được chứng minh của mình sang AL2023, cung cấp quy trình cấu hình bảo mật đơn giản tương tự cho các bản phân phối Linux khác. Để biết thêm thông tin, vui lòng tham khảo [Image Builder documentation.](https://docs.aws.amazon.com/imagebuilder/latest/userguide/ib-stig.html)

**Tự động hóa STIG cho các fleet hiện có bằng Systems Manager**

Đối với các AL2023 EC2 instances hiện có, bạn có thể sử dụng AWS-managed SSM command documents để tự động hóa việc triển khai các cấu hình STIG.  
 Các command document này có thể được thực thi thông qua SSM Console, API, hoặc AWS Command Line Interface (AWS CLI). Cơ chế chính ở đây là AWS managed Systems Manager command document chứa sẵn các cấu hình STIG được định nghĩa trước. Bằng cách tận dụng các command document này thông qua khả năng thực thi của Systems Manager, khách hàng có thể triển khai và duy trì cấu hình AL2023 STIG một cách có hệ thống trên toàn bộ các EC2 instances. Điều này tạo ra các security baselines nhất quán đáp ứng yêu cầu của chính phủ và doanh nghiệp. Giải pháp này đặc biệt hiệu quả đối với các môi trường đã có sẵn AL2023 EC2 instances, vì nó cho phép khách hàng triển khai các STIG controls mà không cần phải xây dựng lại hoặc redeploy instance. Để biết thêm thông tin về command document, vui lòng tham khảo mục [*Apply STIG settings with Systems Manager*](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-stig-ssm-cmd-doc.html) trong EC2 User Guide.

AL2023 STIG thể hiện cam kết liên tục của Amazon Linux trong việc cung cấp cho khách hàng các công cụ bảo mật và hướng dẫn cần thiết để thành công trong các môi trường được quản lý nghiêm ngặt. Amazon Linux, hợp tác với DISA, mang đến cho khách hàng quyền truy cập vào các cấu hình bảo mật được chính phủ xác thực và đáp ứng các yêu cầu tuân thủ khắt khe nhất.

Bạn đã sẵn sàng triển khai AL2023 STIG trong môi trường của mình chưa? Hãy khám phá tài liệu hướng dẫn đầy đủ của chúng tôi và bắt đầu hành trình đơn giản hóa tuân thủ bảo mật ngay hôm nay. Để tìm hiểu thêm về STIG hardening cho EC2 instances, tham khảo [STIG compliance for your EC2 instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-configure-stig.html) và đối với STIG settings được áp dụng cho các phiên bản EC2 Linux, hãy tham khảo [STIG settings for EC2 Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-stig-settings.html#ec2-linux-os-stig). Để áp dụng các STIG settings cho AL2023 EC2 instance của bạn, [tải AL2023 DISA STIG](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-stig-downloads.html).

---

**Resources**  
[Serverless Computing and Applications](https://aws.amazon.com/serverless/?sc_ichannel=ha&sc_icampaign=acq_awsblogsb&sc_icontent=compute-resources)  
[Amazon Container Services](https://aws.amazon.com/containers/?sc_ichannel=ha&sc_icampaign=acq_awsblogsb&sc_icontent=compute-resources)  
[AWS Messaging](https://aws.amazon.com/messaging/?sc_ichannel=ha&sc_icampaign=acq_awsblogsb&sc_icontent=compute-resources)  
[Cloud Compute with AWS](https://aws.amazon.com/products/compute/?sc_ichannel=ha&sc_icampaign=acq_awsblogsb&sc_icontent=compute-resources)  
[Desktop and Application Streaming](https://aws.amazon.com/products/end-user-computing/)