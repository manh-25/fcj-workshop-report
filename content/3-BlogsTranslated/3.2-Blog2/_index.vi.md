---
title: "Blog 2"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
# Tổng quan về các dịch vụ bảo mật có sẵn trong AWS Dedicated Local Zones

Tác giả: Lakshmi VP và Enrico Liguori | Ngày 10/09/2025 | Phân loại:  [Intermediate (200)](https://aws.amazon.com/blogs/security/category/learning-levels/intermediate-200/), [Security, Identity, & Compliance](https://aws.amazon.com/blogs/security/category/security-identity-compliance/), [Technical How-to](https://aws.amazon.com/blogs/security/category/post-types/technical-how-to/) | [Permalink](https://aws.amazon.com/blogs/security/overview-of-security-services-available-in-aws-dedicated-local-zones/)

Khi hiện đại hóa các ứng dụng, khách hàng trong các ngành có quy định nghiêm ngặt như chính phủ, tài chính, và nghiên cứu đối mặt với một thách thức quan trọng: làm thế nào để chuyển đổi hệ thống của họ trong khi vẫn đáp ứng các yêu cầu nghiêm ngặt về chủ quyền số và tuân thủ bảo mật. Một hiểu lầm phổ biến gắn liền với việc này là dữ liệu phải được chuyển sang một AWS Region để có thể sử dụng đầy đủ các dịch vụ bảo mật của [Amazon Web Services (AWS)](https://aws.amazon.com/).

Trong bài viết này, chúng tôi giải thích hiểu lầm đó bằng cách chỉ ra cách sử dụng các dịch vụ bảo mật theo Region trong khi giữ dữ liệu của bạn bên trong [AWS Dedicated Local Zones](https://aws.amazon.com/dedicatedlocalzones/). 

* AWS Nitro System cung cấp bảo mật nền tảng  
* [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms) và [AWS Certificate Manager (ACM)](https://aws.amazon.com/acm) hỗ trợ mã hóa mạnh mẽ  
* [Amazon Inspector](https://aws.amazon.com/inspector), [Amazon GuardDuty](https://aws.amazon.com/guardduty/), và [AWS Shield](https://aws.amazon.com/shield) hoạt động phối hợp để bảo vệ workloads  
* [AWS CloudTrail](https://aws.amazon.com/cloudtrail) duy trì quản trị thông qua việc giám sát và kiểm toán

Dedicated Local Zones là cơ sở hạ tầng do AWS quản lý, tại chỗ (on-premises), được cấu hình dành riêng cho bạn. Chúng giúp đáp ứng các yêu cầu quản lý quy định cụ thể đồng thời cung cấp các lợi ích của điện toán đám mây như độ co giãn, mở rộng, và tính phí theo nhu cầu. Bạn có thể đặt dữ liệu tại vị trí bạn chọn và sử dụng nó với các tính năng bảo mật và quản trị nâng cao cung cấp bởi AWS để theo dõi và kiểm soát truy cập ứng dụng, đồng thời đảm bảo cô lập dữ liệu, lưu trữ dữ liệu tại quốc gia, chủ quyền số, và đáp ứng các yêu cầu tuân thủ.

**AWS Nitro System**

Nhiều tổ chức với yêu cầu nghiêm ngặt về tuân thủ và chủ quyền dữ liệu ngần ngại khi chuyển các workloads bảo mật sang đám mây. Những lo ngại của họ là hợp lý và cụ thể: họ cần một giải pháp cung cấp sự bảo vệ có thể kiểm chứng độc lập và sự cô lập khỏi truy cập dữ liệu bởi các bên có đặc quyền, kể cả nhân sự nhà cung cấp đám mây. Những tổ chức này cũng cần sự đảm bảo rằng truy cập trái phép qua cloud control plane là không khả thi về mặt kỹ thuật, chứ không chỉ bị ngăn cấm bằng hợp đồng.

Có lẽ điều quan trọng nhất, họ cần có sự bảo vệ kênh phụ để đảm bảo rằng dữ liệu nhạy cảm không bị rò rỉ qua bộ nhớ hoặc phương tiện khác sang các tenants hypervisor khác sử dụng chung phần cứng vật lý. Các phương pháp bảo mật cloud truyền thống thường dựa vào kiểm soát vận hành và cam kết, thay vì sự bất khả thi về mặt kỹ thuật, điều mà không đáp ứng được các yêu cầu khắt khe mà những tổ chức này phải đối mặt.

 [AWS Nitro System](https://aws.amazon.com/ec2/nitro/), là nền tảng cho các [Amazon Elastic Compute Cloud (Amazon EC2)](https://aws.amazon.com/ec2) instances thế hệ mới chạy trong Dedicated Local Zone và parent Region của nó, giải quyết tất cả những lo ngại này thông qua kiến trúc của nó. Kết hợp phần cứng và phần mềm chuyên dụng tạo ra một secure enclave bảo vệ dữ liệu của bạn khỏi truy cập trái phép trong quá trình xử lý trên EC2 instances.

Các EC2 instance chạy trong Dedicated Local Zones của bạn được xây dựng dựa trên AWS Nitro System, được thiết kế để cung cấp bảo mật mạnh mẽ cho workloads tính toán. Nó sử dụng các thành phần phần cứng và phần mềm chuyên biệt để giúp bảo vệ dữ liệu của bạn khỏi truy cập trái phép trong quá trình xử lý trên Amazon EC2.

Ba thành phần chính của Nitro System bao gồm: Nitro cards chuyên dụng, Nitro Security Chip, và Nitro Hypervisor. Cả ba thành phần này [được thiết kế để thực thi các hạn chế](https://docs.aws.amazon.com/whitepapers/latest/security-design-of-aws-nitro-system/security-design-of-aws-nitro-system.html) và cung cấp các ranh giới bảo mật vật lý và logic để không ai, kể cả nhân viên AWS, có thể truy cập workloads hoặc dữ liệu khách hàng đang chạy trên Amazon EC2 mà không có quyền cho phép rõ ràng từ bạn.

[Nitro System whitepaper](https://docs.aws.amazon.com/whitepapers/latest/security-design-of-aws-nitro-system/security-design-of-aws-nitro-system.html) trình bày chi tiết cách Nitro System, theo thiết kế, loại bỏ khả năng truy cập của quản trị viên tới EC2 instance, thiết kế giao tiếp thụ động tổng thể và quy trình quản lý thay đổi của Nitro System. Thiết kế bảo mật của Nitro System cũng đã được xác thực độc lập bởi NCC Group trong một [báo cáo công khai](https://aws.amazon.com/vi/blogs/compute/aws-nitro-system-gets-independent-affirmation-of-its-confidential-compute-capabilities/).

## **AWS Key Management Service**

Khi làm việc với khách hàng, chúng tôi nhận thấy một trong những nguồn gây hiểu lầm và lo ngại dai dẳng không chỉ là liệu dữ liệu của họ có được mã hóa hay không, mà là ai kiểm soát các khóa bảo vệ việc mã hóa đó. Nhiều tổ chức đấu tranh với một mâu thuẫn cơ bản: họ muốn lợi ích vận hành của điện toán đám mây, nhưng họ cũng cần duy trì kiểm soát nghiêm ngặt các khóa mã hóa của mình để đáp ứng các yêu cầu tuân thủ.

Điều này đặc biệt nhạy cảm đối với các tổ chức trong các ngành công nghiệp thuộc phạm vi quản lý, nơi họ thường đặt các câu hỏi như “Chính xác thì khóa mã hóa của tôi đang được lưu ở nơi nào?” và “Ai có thể truy cập khóa của tôi?” [AWS KMS](https://aws.amazon.com/kms/) giải quyết điều này bằng cách cung cấp nhiều cách quản lý khóa, mỗi cách được thiết kế cho các yêu cầu bảo mật và vận hành khác nhau. Dịch vụ cung cấp sự kiểm soát tập trung đối với lifecycle và quyền truy cập của các khóa mã hóa để bạn có thể tạo khóa mới khi cần và kiểm soát truy cập quản lý khóa tách biệt với chính sách khóa (key policies).

Mặc định, khách hàng Dedicated Local Zones có thể sử dụng tích hợp AWS KMS trong parent Region để lưu trữ và kiểm soát các khóa mã hóa. Bạn sau đó có thể sử dụng các khóa này để mã hóa dữ liệu được lưu [cục bộ trong Amazon EBS và Amazon S3 trong Dedicated Local Zones](https://aws.amazon.com/vi/dedicatedlocalzones/features/).

Nếu trường hợp sử dụng của bạn yêu cầu một kho lưu trữ khóa mã hóa bên ngoài để duy trì yêu cầu chủ quyền dữ liệu nghiêm ngặt, thì kết hợp giữa Dedicated Local Zones và [AWS KMS external key store](https://docs.aws.amazon.com/kms/latest/developerguide/keystore-external.html) có thể cung cấp giải pháp mạnh mẽ.

Khi sử dụng external key store trong Dedicated Local Zones, bạn có thể lưu trữ external hardware security module (HSM) chứa các khóa mã hóa của bạn on-premises hoặc đồng bộ cùng với hạ tầng khác của bạn. Bằng cách này, bạn vẫn duy trì toàn quyền kiểm soát đối với bảo mật vật lý và việc quản lý HSM, đồng thời tận dụng được khả năng truy cập độ trễ thấp và năng lực xử lý dữ liệu của Dedicated Local Zones.

Các thành phần chính của kiến trúc AWS KMS external key store bao gồm:

* **XKS proxy server**: Bạn cấp phát một external key store proxy (XKS proxy) server trong trung tâm dữ liệu on-premises của bạn (thể hiện trong Figure 1\) hoặc trong Dedicated Local Zones. Vai trò của XKS proxy là làm trung gian giữa AWS KMS và HSM on-premises của bạn. Proxy XKS phải được đăng ký làm mục tiêu của [Network Load Balancer (NLB)](https://aws.amazon.com/elasticloadbalancing/application-load-balancer/) trong Region, điều này có nghĩa là nếu được lưu trữ trên trung tâm dữ liệu on-premises của bạn, thì NLB  [Amazon Virtual Private Cloud (Amazon VPC)](https://aws.amazon.com/vpc) phải có kết nối riêng với mạng on-premises thông qua VPN site-to-site hoặc kết nối [AWS Direct Connect](https://aws.amazon.com/directconnect).  
* **HSM on-premises**: Bạn cấu hình HSM on-premises để lưu trữ khóa gốc (root encryption keys) sẽ được dùng để bảo vệ các khóa mã hóa dữ liệu (data encryption keys) của bạn.  
* **External key store**: Bạn tạo một tài nguyên external key store trong AWS KMS, ánh xạ tới HSM on-premises thông qua XKS proxy.

<img src="/images/3-Blog/3.2-Blog2/fig-1.png" width="800">

*Figure 1: AWS KMS external key store trong một Dedicated Local Zone*

Luồng hoạt động như sau:

1. [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) hoặc [Amazon Elastic Block Store (Amazon EBS)](https://aws.amazon.com/ebs) triển khai cục bộ trong Dedicated Local Zones cần phải mã hóa dữ liệu, yêu cầu AWS KMS tạo một khóa mã hóa dữ liệu (data encryption key) mới.  
2. AWS KMS gửi một yêu cầu tới XKS proxy, proxy này giao tiếp với HSM on-premises để tạo khóa gốc (root key).  
3. AWS KMS sử dụng root key này để mã hóa data encryption key trước khi trả về cho dịch vụ yêu cầu và lưu trữ data encryption key đã mã hóa cùng với dữ liệu đã mã hóa trong Amazon S3 hoặc Amazon EBS.  
4. Cho các lần thao tác mã hóa/giải mã trong tương lai, dịch vụ AWS sử dụng data encryption key đã được tạo và mã hóa bởi AWS KMS trước đó mà không cần tương tác với HSM on-premises.

**Lưu ý:** HSM on-premises chỉ tham gia vào quá trình tạo root key ban đầu để bảo vệ data encryption key, không tham gia vào các hoạt động mã hóa/giải mã khối lượng lớn trên chính dữ liệu.

Kiến trúc này mang lại hai lợi ích chính:

* Bạn duy trì quyền kiểm soát hoàn toàn các khóa mã hóa bằng cách lưu chúng trong trung tâm dữ liệu của bạn, giúp đáp ứng yêu cầu tuân thủ bảo mật.  
* Dedicated Local Zones giữ dữ liệu của bạn được cô lập tại vị trí bạn chọn, cung cấp độ trễ thấp cho người dùng của bạn.

Điều quan trọng cần lưu ý là việc sử dụng AWS KMS external key store đòi hỏi bạn phải quản lý các tác vụ vận hành bổ sung ngoài AWS KMS tiêu chuẩn. Để duy trì truy cập liên tục tới dữ liệu được mã hóa, bạn phải cung cấp HSM on-premises hoạt động 24/7 của bạn, giám sát hiệu suất cơ sở hạ tầng XKS proxy, thực hiện kiểm soát bảo mật mạnh mẽ, tạo quy trình sao lưu và phục hồi.

Vì sự cố hệ thống có thể cản trở truy cập tới dữ liệu được mã hóa, chúng tôi khuyến nghị bạn phát triển các sổ tay vận hành (operational runbooks) chi tiết, thiết lập hệ thống giám sát toàn diện, kiểm thử quy trình phục hồi của bạn thường xuyên và duy trì các hệ thống dự phòng khi có thể.

Để biết thêm thông tin về tương tác giữa AWS KMS và external key store, xem [Announcing AWS KMS External Key Store (XKS)](https://aws.amazon.com/blogs/aws/announcing-aws-kms-external-key-store-xks/).

## **Amazon Inspector**

Một lo ngại phổ biến mà chúng tôi nghe từ các tổ chức đang đánh giá Dedicated Local Zones là liệu họ có cần phải hy sinh năng lực bảo mật để duy trì lưu giữ dữ liệu. Thực tế là các dịch vụ bảo mật của AWS chạy trong Region, như Amazon Inspector, được đặc biệt thiết kế để cung cấp bảo vệ toàn diện trong khi tôn trọng yêu cầu vị trí dữ liệu của bạn.

Các tổ chức chạy ứng dụng được quản lý (regulated applications) trong Dedicated Local Zones cần có sự bảo vệ mạnh mẽ trước các lỗ hổng zero-day, ưu tiên khắc phục bản vá và quản lý lỗ hổng tự động để đáp ứng các yêu cầu tuân thủ. Amazon Inspector đáp ứng những nhu cầu này bằng cách liên tục quét workloads để phát hiện các lỗ hổng phần mềm và nguy cơ mạng ngoài ý muốn mà không yêu cầu di chuyển dữ liệu từ vị trí bạn đã chọn.

Amazon Inspector giúp bảo vệ workloads của bạn thông qua hai chế độ quét riêng biệt: hybrid scanning và agent-based scanning. Tuy nhiên, trong bài viết này, chúng ta chỉ xem xét chế độ agent-based scanning.

Để đáp ứng an toàn các yêu cầu lưu giữ dữ liệu trong Dedicated Local Zones, bật chế độ agent-based scanning trên các [instances được quản lý bởi AWS Systems Manager (AWS SSM)](https://docs.aws.amazon.com/inspector/latest/user/scanning-ec2.html#agent-based) trong tài khoản của bạn. Đây là chế độ mặc định cho các tài khoản mới, cung cấp bảo mật nâng cao thông qua quét liên tục, phản ứng ngay lập tức với các lỗ hổng và sự phơi bày phổ biến (CVEs) mới và thay đổi của instance. Nó cũng cho phép khả năng kiểm tra sâu cho các instance đủ điều kiện, cung cấp đánh giá lỗ hổng toàn diện.

Kiến trúc tham chiếu trong Figure 2 cho thấy:

1. Agent của Amazon Inspector chạy trên các instances quản lý bởi AWS SSM, giữ dữ liệu ứng dụng của bạn bên trong Dedicated Local Zones.  
2. Amazon Inspector đánh giá và tạo ra [findings](https://docs.aws.amazon.com/inspector/latest/user/findings-types.html) cho các lỗ hổng được phát hiện.

<img src="/images/3-Blog/3.2-Blog2/fig-2.png" width="1000">

*Figure 2: Amazon Inspector trong Dedicated Local Zones*

## **Amazon GuardDuty**

Duy trì chủ quyền dữ liệu với Dedicated Local Zones không có nghĩa là từ bỏ các năng lực bảo mật cao cấp. [GuardDuty](https://aws.amazon.com/guardduty/) cho thấy cách phát hiện mối đe dọa tinh vi có thể hoạt động hiệu quả trong khi tôn trọng các yêu cầu lưu giữ dữ liệu nghiêm ngặt.

Bảo vệ workloads AI của bạn khỏi ransomware và các mối đe dọa bảo mật nâng cao yêu cầu một giải pháp tình báo mối đe dọa tích hợp AI và Machine Learning (AI/ML) có thể phát hiện hoạt động đáng ngờ và phản ứng nhanh. GuardDuty sử dụng phát hiện mối đe dọa dựa trên AI/ML và tình báo mối đe dọa tích hợp từ AWS và các bên thứ ba hàng đầu để bảo vệ tài khoản AWS, workloads và dữ liệu của bạn. Nó liên tục giám sát hoạt động độc hại, đưa ra các phát hiện bảo mật chi tiết, và bạn có thể sử dụng thông tin được cung cấp để phản ứng nhanh với các mối đe dọa.

Với [GuardDuty EKS Protection](https://docs.aws.amazon.com/guardduty/latest/ug/kubernetes-protection.html), giám sát Kubernetes audit logs để phát hiện mối đe dọa. Điểm chính cần lưu ý là [dữ liệu của bạn được lưu tại vị trí bạn đã chọn](https://aws.amazon.com/vi/compliance/data-privacy-faq/#topic-1) và parent Region chỉ xử lý dữ liệu log.

[GuardDuty Runtime Monitoring](https://docs.aws.amazon.com/guardduty/latest/ug/runtime-monitoring.html) quan sát và phân tích các operating system, networking, và file events để phát hiện các mối đe dọa tiềm năng trong workloads AWS của bạn. Parent Region chỉ nhận các báo cáo mối đe dọa trong khi Dedicated Local Zones giữ dữ liệu gốc.

Kiến trúc tham chiếu trong Figure 3 cho thấy cách GuardDuty giúp bảo vệ dữ liệu của bạn trong Dedicated Local Zones:

1. GuardDuty giám sát EC2 instances trong khi dữ liệu của bạn vẫn ở trong Dedicated Local Zones.  
2. GuardDuty phân tích các nguồn dữ liệu từ [AWS CloudTrail](https://aws.amazon.com/cloudtrail) event logs, management events, và Amazon VPC flow logs mà tài khoản AWS của bạn thu thập trong Region.

<img src="/images/3-Blog/3.2-Blog2/fig-3.png" width="1000">

*Figure 3: Amazon GuardDuty trong Dedicated Local Zones*

## **AWS Certificate Manager**

Các tổ chức thường bày tỏ lo ngại về độ phức tạp trong quản lý chứng chỉ khi triển khai ứng dụng trong Dedicated Local Zones. [AWS Certificate Manager (ACM)](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html), hoạt động tại parent Region, giải quyết những thách thức này bằng cách đóng vai trò là dịch vụ chính mà khách hàng dùng để cấp phát, quản lý, và triển khai các chứng chỉ cho cả workloads công khai lẫn workloads trong private Dedicated Local Zones.

ACM tích hợp liền mạch với ALBs trong Dedicated Local Zones để quản lý toàn bộ vòng đời chứng chỉ (certificate lifecycle), như được thể hiện ở Figure 4.

<img src="/images/3-Blog/3.2-Blog2/fig-4.png" width="1000">

*Figure 4: ACM trong Dedicated Local Zones*

Thực hiện các bước sau để triển khai chứng chỉ TLS trong Dedicated Local Zones:

1. Cấp phát hoặc nhập chứng chỉ qua ACM trong parent Region.  
2. Liên kết chứng chỉ với các ALB HTTPS listeners trong Dedicated Local Zones để cho phép SSL/TLS termination an toàn, độ trễ thấp gần người dùng.

ACM tự động gia hạn chứng chỉ, tránh các nhiệm vụ quản lý thủ công, và duy trì tính khả dụng của dịch vụ HTTPS liên tục. Sự tích hợp này mang lại bảo mật cấp doanh nghiệp với dữ liệu của bạn lưu trữ cục bộ trong Dedicated Local Zones. Nó cũng cung cấp hiệu suất được cải thiện và giảm độ trễ nhờ sự gần gũi với người dùng.

**AWS Shield**

Các ứng dụng quan trọng đối với doanh nghiệp trong Dedicated Local Zones cần tính khả dụng và phản hồi tối đa. [AWS Shield](https://aws.amazon.com/shield/) Standard, một dịch vụ bảo vệ chống từ chối dịch vụ phân tán (DDoS) được quản lý, chạy tại edge của AWS, tự động giúp bảo vệ ứng dụng của bạn bằng cách phát hiện và giảm thiểu các cuộc tấn công DDoS mạng (Layer 3) và transport (Layer 4) ngay cả trước khi chúng tới được workloads của bạn.

## **AWS CloudTrail**

Một mối lo ngại phổ biến khi triển khai workloads trong Dedicated Local Zones là liệu các tổ chức có thể duy trì cùng mức quản trị và giám sát tuân thủ như họ mong đợi từ các triển khai AWS truyền thống hay không. CloudTrail thể hiện cách khả năng kiểm toán toàn diện có thể mở rộng liền mạch qua cơ sở hạ tầng phân tán trong khi vẫn tôn trọng các yêu cầu về lưu trữ dữ liệu.

Chạy trong parent Region, [CloudTrail](https://aws.amazon.com/cloudtrail) cho phép quản trị, tuân thủ, kiểm toán vận hành, và kiểm toán rủi ro cho tài khoản AWS của bạn, cung cấp cho bạn bản ghi hợp nhất các sự kiện đa nguồn tại một nơi duy nhất. Điều này bao gồm lịch sử chi tiết AWS API calls cho tài khoản của bạn, bao gồm các API calls thực hiện qua AWS Management Console, AWS SDKs, command line tools và các dịch vụ AWS cấp cao hơn được ứng dụng sử dụng trong Dedicated Local Zones. Chỉ có logs được lưu trữ ở parent Region, trong khi dữ liệu của bạn vẫn nằm trong Dedicated Local Zones. AWS CloudTrail giúp bạn kích hoạt kiểm toán vận hành và rủi ro, quản trị và tuân thủ cho tài khoản AWS của bạn.

## **Kết luận**

Dedicated Local Zones cung cấp một giải pháp mạnh mẽ để chạy các workloads có quy định nghiêm ngặt cho mọi ngành, để đáp ứng các yêu cầu khắt khe về lưu trữ dữ liệu và chủ quyền số. Thông qua các dịch vụ bảo mật tích hợp như AWS Nitro System, AWS KMS External Key Store, ACM, AWS Shield, Amazon GuardDuty, Amazon Inspector và AWS CloudTrail, tổ chức của bạn có thể đạt được mức độ tuân thủ bảo mật mạnh hơn cho các ứng dụng mission-critical chạy trong AWS Dedicated Local Zones.

Để tìm hiểu thêm về việc triển khai các giải pháp bảo mật này trong bản triển khai Dedicated Local Zones của bạn, hãy liên hệ AWS account team của bạn.

Nếu bạn có góp ý cho bài viết này, gửi comment trong phần Comments bên dưới. Nếu bạn có thắc mắc về bài viết, xin vui lòng [liên hệ AWS Support.](https://console.aws.amazon.com/support/home).

---

| <img src="/images/3-Blog/3.2-Blog2/author-1.png" width="200"> | **Lakshmi VP** - Lakshmi là Solutions Architect tại AWS WWPS-Canada và chuyên về các các giải pháp Hybrid Edge — Outposts, Local Zones và Dedicated Local Zones. Với hơn 16 năm kinh nghiệm hỗ trợ nhiều ngành công nghiệp khác nhau trên toàn cầu, Lakshmi đam mê công nghệ và các giải pháp thiết thực cho khách hàng. Ngoài công việc, cô thích xem phim hoạt hình và đi bộ đường dài. |
| :---- | :---- |
| <img src="/images/3-Blog/3.2-Blog2/author-2.png" width="200"> |**Enrico Liguori** - Enrico là Specialist Solutions Architect tập trung vào networking và hybrid cloud. Anh làm việc tại Worldwide Public Sector Solutions Architecture, nơi anh tận dụng chuyên môn của mình để thiết kế các giải pháp  networking và hybrid cloud có tính khả dụng cao, khả năng mở rộng, bảo mật và tiết kiệm chi phí. Khi Enrico không đắm chìm trong trách nhiệm nghề nghiệp của mình, Enrico dành thời gian khám phá những điều kỳ diệu của thế giới dưới nước thông qua hoạt động lặn biển. |

TAGS: [Digital Sovereignty](https://aws.amazon.com/blogs/security/tag/digital-sovereignty/)

---

### **Resources**

[AWS Cloud Security](https://aws.amazon.com/security?sc_ichannel=ha&sc_icampaign=acq_awsblogsb&sc_icontent=security-resources)  
[AWS Compliance](https://aws.amazon.com/compliance?sc_ichannel=ha&sc_icampaign=acq_awsblogsb&sc_icontent=security-resources)  
[AWS Security Reference Architecture](https://docs.aws.amazon.com/prescriptive-guidance/latest/security-reference-architecture/welcome.html?secd_ip5)  
[Best Practices](https://aws.amazon.com/architecture/security-identity-compliance)  
[Data Protection at AWS](https://aws.amazon.com/compliance/data-protection/)  
[Zero Trust on AWS](https://aws.amazon.com/security/zero-trust/)  
[Cryptographic Computing](https://aws.amazon.com/security/cryptographic-computing/)