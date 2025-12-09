---
title: "Event 6"
weight: 1
chapter: false
pre: " <b> 4.6. </b> "
---
# **BUILDING AGENTIC AI - Context Optimization with Amazon Bedrock**

**Địa điểm**: Tầng 26, Tòa nhà Bitexco Financial, TP.HCM
**Thời gian**: 9:00 Thứ Sáu, ngày 05 tháng 12 năm 2025

## **Mục Đích Của Sự Kiện**

* Giới thiệu tầm nhìn Agentic AI của AWS và dịch vụ Amazon Bedrock AgentCore.  
* Trình bày giải pháp agentic từ đối tác Diaflow và CloudThinker cùng các case study thực tế.  
* Thảo luận kiến trúc và best practices khi xây dựng hệ thống Agentic AI.

## **Danh Sách Diễn Giả**

* **Nguyen Gia Hung** – Head of Solutions Architect, AWS  
* **Kien Nguyen** – Solutions Architect, AWS  
* **Viet Pham** – Founder & CEO, Diaflow  
* **Thang Ton** – Co-founder & COO, CloudThinker  
* **Henry Bui** – Head of Engineering, CloudThinker  
* **Kha Van** – Community Leader, AWS

## **Nội Dung Nổi Bật**

### **Opening – Nguyen Gia Hung**

* Giới thiệu mục tiêu workshop: hiểu đúng về Agentic AI trên AWS, cách vận hành, và xây dựng workflow thực tế.

### **Amazon Bedrock AgentCore – Kien Nguyen**

#### **1\. Tiến hóa của Agentic AI**

* Từ chatbot → agent → multi-agent.  
* Tầm nhìn AWS: xây dựng nền tảng tốt nhất để phát triển và mở rộng AI agents.  
* Hệ sinh thái frameworks: CrewAI, Google ADK, LangGraph, LangChain, LlamaIndex, OpenAI Agents SDK, Strands Agents.

#### **2\. Kiến trúc AgentCore:**

**I. Enhance with tools & memory**

* **Memory:** contextual \+ long-term; hỗ trợ self-managed storage.  
* **Gateway:** chuyển API/Lambda thành tool; hỗ trợ MCP \+ IAM.  
* **Browser Tool:** cho phép agent truy xuất web/nguồn được phép.  
* **Interpreter:** môi trường tính toán sandbox để phân tích data, sinh mã, chạy script an toàn.

**II. Deploy securely at scale**

* **Runtime:** serverless, hỗ trợ long-running workloads, tối ưu chi phí, session isolation.  
* **Identity:** quản lý danh tính agent, phân quyền, audit, kiểm soát tool/API được phép gọi.

**III. Agentic operations**

* **Observability:** tracing plan → tool calls; metrics (token, latency); logs chi tiết.

#### **3\. Key Benefits**

* Không cần quản lý hạ tầng.  
* Tối ưu performance – scalability – security – governance  
* Chuẩn hóa multi-agent enterprise.  
* Có giải pháp partner sẵn trên AWS Marketplace.  
* Demo/POC: [agentcore.builderstudio.marketing.aws.dev](http://agentcore.builderstudio.marketing.aws.dev)

### **Diaflow – Use Case - Viet Pham**

#### **1\. Vấn đề doanh nghiệp**

* Tốn thời gian cho tác vụ lặp lại.  
* Lo ngại data privacy khi dùng AI bên ngoài.  
   ➡ Diaflow chạy trực tiếp trong hạ tầng doanh nghiệp → dữ liệu không rời môi trường nội bộ.

#### **2\. Kiến trúc**

* Multi-agent architecture.  
* User-defined workflows theo quy trình doanh nghiệp.  
* Dễ đóng gói thành widget hoặc tích hợp trực tiếp.

#### **3\. Điểm nổi bật**

* Tự động hóa tác vụ lặp lại → tăng hiệu suất.  
* Cost saving: giảm thời gian xử lý, giảm lỗi thủ công.  
* Triển khai nhanh.  
* Dễ sử dụng, phù hợp non-technical users.

#### **4\. Case Studies**

* Trích xuất dữ liệu \+ phân tích tự động.  
* Procurement automation.  
* Clinical workflow automation.  
* Vital metrics digitization from legacy systems.  
* Automation online payments.

### **CloudThinker**

#### **CloudThinker Intro – Thang Ton**

**Focus:** Agentic AI for Cloud Operations  
 **Capabilities:** collaboration, automation, optimization, continuous learning, multi-cloud support  
 **Features:** code review, incident response, operation automation, infra observability (Coming soon: Kubernetes management, Cloud Keeper)

#### **CloudThinker Agentic Orchestration & Context Optimization – Henry Bui**

**1\. So sánh Chatbot – Agent – Multi-Agent**
* Chatbot: reactive, rule-based.  
* Agent: planning \+ tool use.  
* Multi-agent: phối hợp vai trò xử lý nhiệm vụ phức tạp.

**2\. Getting started with agents**
* Bắt đầu với kiến trúc đơn giản như ReAct.  
* Thiết lập evals & observability ngay từ đầu.  
* Tool design ảnh hưởng mạnh đến chất lượng output.  
* Áp dụng “quick win techniques”.

**3\. Khi single-agent chạm giới hạn**
* Khi yêu cầu tăng độ phức tạp → cần multi-agent hoặc multi-session single-agent.  
   **Multi-agent components:** supervisor, transfer architecture, specialized agents.

**4\. Context Optimization Techniques**
* Prompt caching.  
* Context compaction.  
* Tool consolidation (reports, dashboards, slideshows).  
* Parallel tool calling.

#### **CloudThinker Hack: Hands-on Workshop – Kha Van**
Thực hành sử dụng CloudThinker với các use case.

## **Những Gì Học Được**
##### **Về AgentCore**

Nền tảng mạnh mẽ giúp doanh nghiệp xây AI agent an toàn, linh hoạt, không phải lo hạ tầng.

##### **Về Diaflow**

Hiệu quả rõ rệt trong tự động hóa quy trình lặp lại, bảo mật dữ liệu và tiết kiệm chi phí.

##### **Về CloudThinker**

Tối ưu hoá cloud ops thông qua agentic orchestration & multi-agent optimization.

##### **Về Technical Practices**

* Bắt đầu kiến trúc đơn giản.  
* Chú trọng evals và observability.  
* Tối ưu context (caching, compaction, parallel calling).

## **Ứng Dụng Vào Công Việc**

* Thử nghiệm Amazon Bedrock AgentCore cho agentic AI đa bước, yêu cầu scalability và security.  
* Dùng Diaflow để automate quy trình doanh nghiệp cần privacy cao.  
* Dùng CloudThinker cho cloud ops (cost, security, infra optimization).  
* Khi build agentic hệ thống phức tạp: bắt đầu modular, memory \+ observability từ đầu để dễ mở rộng.

## **Trải nghiệm trong event**

Buổi workshop mang đến góc nhìn toàn diện về xu hướng Agentic AI, gồm tầm nhìn AWS, kiến trúc AgentCore, giải pháp từ Diaflow và CloudThinker, cùng workshop thực hành.  

### **Một số hình ảnh khi tham gia sự kiện**
* Thêm các hình ảnh của các bạn tại đây

