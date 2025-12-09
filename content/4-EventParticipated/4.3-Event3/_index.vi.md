---
title: "Event 3"
weight: 1
chapter: false
pre: " <b> 4.3. </b> "
---

# Workshop AI/ML/GenAI trên AWS

**Thời gian:** Thứ Bảy, ngày 15 tháng 11 năm 2025, 8:30 – 12:00
**Địa điểm:** Văn phòng AWS Vietnam

## **Mục tiêu sự kiện**

* Cung cấp trải nghiệm thực hành với các dịch vụ **AI/ML trên AWS** cho cả machine learning truyền thống và generative AI.  
* Giúp người tham gia hiểu quy trình **ML end-to-end trên Amazon SageMaker**.  
* Giới thiệu **các năng lực Generative AI trên Amazon Bedrock**, bao gồm foundation models và kiến trúc agent.  
* Trình bày cách triển khai thực tế **ứng dụng AI theo mô hình RAG** trên AWS.  
* Nâng cao nhận thức về **an toàn, quản trị và kiểm soát nội dung AI** thông qua Bedrock Guardrails.


## **Cấu trúc chương trình & Nội dung nổi bật**

### **Khai mạc & Giới thiệu workshop**

* Đăng ký và giao lưu kết nối.  
* Giới thiệu agenda và mục tiêu học tập của workshop.  
* Tổng quan ngắn gọn về **hệ sinh thái AI/ML tại Việt Nam** và vai trò của AWS.


### **Tổng quan dịch vụ AI/ML trên AWS – Amazon SageMaker**

#### **Amazon SageMaker – Nền tảng ML toàn diện**

* **Chuẩn bị & gán nhãn dữ liệu**  
  * Làm sạch dữ liệu, feature engineering và các khả năng gán nhãn tự động.  

* **Huấn luyện, tinh chỉnh & triển khai mô hình**  
  * Hạ tầng huấn luyện được quản lý  
  * Hyperparameter tuning  
  * Các hình thức triển khai: real-time inference và batch inference  

* **Năng lực MLOps tích hợp**  
  * Quản lý phiên bản mô hình  
  * Giám sát và phát hiện drift  
  * Pipeline tái huấn luyện tự động  

#### **Demo trực tiếp – SageMaker Studio**

* Môi trường phát triển ML hợp nhất  
* Tích hợp Jupyter Notebook  
* Theo dõi thí nghiệm (experiment tracking)  
* Visual workflow builder  

→ Thể hiện cách SageMaker đơn giản hóa toàn bộ vòng đời ML so với việc thiết lập môi trường cục bộ thủ công.


### **Generative AI với Amazon Bedrock**

#### **Foundation Models trên Bedrock**

* **Claude, Llama, Titan** – so sánh các mô hình  
* Hướng dẫn lựa chọn dựa trên:
  * Use case  
  * Hiệu năng  
  * Chi phí  

#### **Prompt Engineering & Kỹ thuật suy luận**

* Best practices trong thiết kế prompt  
* **Chain-of-Thought reasoning** để dẫn dắt mô hình suy luận từng bước  
* **Few-shot learning** nhằm cải thiện chất lượng đầu ra  

#### **Retrieval-Augmented Generation (RAG)**

* Tổng quan kiến trúc RAG  
* Kết hợp truy xuất dữ liệu và sinh nội dung để tạo câu trả lời chính xác, cập nhật  
* Tích hợp knowledge base với:
  * Amazon OpenSearch  
  * Amazon Kendra  

#### **Bedrock Agents & Guardrails**

* Kiến trúc agent điều phối các quy trình nhiều bước  
* **Bedrock Guardrails** giúp:
  * Đảm bảo an toàn nội dung  
  * Thực thi chính sách  
  * Đáp ứng yêu cầu tuân thủ  

#### **Demo trực tiếp – Xây dựng chatbot GenAI trên Bedrock**

* Lựa chọn và cấu hình foundation model  
* Triển khai RAG  
* Sử dụng Bedrock Agents  
* Áp dụng Guardrails để kiểm soát nội dung  


## **Những điều học được**

* Amazon SageMaker cung cấp **nền tảng ML toàn diện**, giúp giảm đáng kể độ phức tạp vận hành.  
* Việc chọn foundation model cần cân đối giữa **năng lực, chi phí và bài toán thực tế**.  
* **Prompt engineering là kỹ năng cốt lõi** ảnh hưởng trực tiếp đến chất lượng kết quả.  
* RAG là kiến trúc thiết yếu cho các ứng dụng AI cần truy cập **dữ liệu nội bộ hoặc thông tin thường xuyên thay đổi**.  
* An toàn và quản trị AI cần được **thiết kế ngay từ đầu**, không phải bổ sung sau.


## **Ứng dụng vào công việc**

* Thử nghiệm **SageMaker Studio** cho các bài toán phân tích dữ liệu và ML nội bộ.  
* Xây dựng **ứng dụng GenAI theo mô hình RAG** với Amazon Bedrock cho hệ thống tài liệu nội bộ.  
* Xây dựng các **template prompt và best practices** dùng chung.  
* Tích hợp **Bedrock Guardrails** để đảm bảo an toàn và tuân thủ cho ứng dụng GenAI.


## **Trải nghiệm sự kiện**

Đây là một trong những workshop AI mang tính **thực hành cao nhất** mà tôi từng tham dự.  
Việc tự tay xây dựng chatbot theo kiến trúc **RAG trên Amazon Bedrock** giúp tôi “giải mã” nhiều khái niệm GenAI vốn chỉ quen thuộc trên lý thuyết.

* Giao diện SageMaker Studio rất trực quan, giúp quản lý vòng đời ML dễ dàng hơn nhiều so với việc tự thiết lập môi trường cục bộ.  
* Phần ấn tượng nhất là cách **Bedrock Agents** xử lý các tác vụ nhiều bước, giống như việc “dạy AI suy nghĩ và hành động” theo một quy trình mong muốn.  
* Việc hiểu rõ Guardrails giúp tôi tự tin hơn trong việc kiểm soát nội dung do AI sinh ra trong các ứng dụng thực tế.


## **Kết luận chính**

* **RAG là cầu nối giữa GenAI và dữ liệu doanh nghiệp**: giúp AI truy cập tri thức nội bộ mà không cần tái huấn luyện tốn kém.  
* **Prompt engineering vừa là nghệ thuật vừa là kỹ năng kỹ thuật**: cần luyện tập thường xuyên để đạt hiệu quả cao.  
* **An toàn & bảo mật AI là yếu tố bắt buộc**: Guardrails nên là thành phần đầu tiên trong quá trình xây dựng ứng dụng GenAI, không phải phần bổ sung sau cùng.
