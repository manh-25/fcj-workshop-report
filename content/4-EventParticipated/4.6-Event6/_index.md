---
title: "Event 6"
weight: 1
chapter: false
pre: " <b> 4.6. </b> "
---
# **BUILDING AGENTIC AI - Context Optimization with Amazon Bedrock**

**Location**: 26th Floor, Bitexco Financial Tower, HCMC  
**Time**: 9AM Friday, December 05, 2025

## **Event Objectives**

* Introduce AWS’s vision for Agentic AI and the Amazon Bedrock AgentCore service.

* Present agentic solutions from partners Diaflow and CloudThinker along with real-world case studies.

* Discuss architecture and best practices for building Agentic AI systems.

## **Speaker List**

* **Nguyen Gia Hung** – Head of Solutions Architect, AWS

* **Kien Nguyen** – Solutions Architect, AWS

* **Viet Pham** – Founder & CEO, Diaflow

* **Thang Ton** – Co-founder & COO, CloudThinker

* **Henry Bui** – Head of Engineering, CloudThinker

* **Kha Van** – Community Leader, AWS

## **Key Highlights**

### **Opening – Nguyen Gia Hung**

* Introduced the workshop objectives: understanding Agentic AI on AWS, how it operates, and how to build real-world workflows.

### **Amazon Bedrock AgentCore – Kien Nguyen**

#### **1\. Evolution of Agentic AI**

* From chatbot → agent → multi-agent.

* AWS vision: build the best platform for developing and scaling AI agents.

* Framework ecosystem: CrewAI, Google ADK, LangGraph, LangChain, LlamaIndex, OpenAI Agents SDK, Strands Agents.

#### **2\. AgentCore Architecture:**

**I. Enhance with tools & memory**

* **Memory:** contextual \+ long-term; supports self-managed storage.

* **Gateway:** convert API/Lambda into tools; supports MCP \+ IAM.

* **Browser Tool:** allows agents to access permitted web/resources.

* **Interpreter:** sandbox compute environment for data analysis, code generation, and safe script execution.

**II. Deploy securely at scale**

* **Runtime:** serverless, supports long-running workloads, cost-optimized, session isolation.

* **Identity:** manage agent identities, permissions, audit, and control allowed tools/APIs.

**III. Agentic operations**

* **Observability:** trace plan → tool calls; metrics (token, latency); detailed logs.

#### **3\. Key Benefits**

* No infrastructure management required.

* Optimized performance – scalability – security – governance.

* Standardized multi-agent for enterprise.

* Partner solutions available on AWS Marketplace.

* Demo/POC: [agentcore.builderstudio.marketing.aws.dev](http://agentcore.builderstudio.marketing.aws.dev)

### **Diaflow – Use Case – Viet Pham**

#### **1\. Business Problems**

* Time-consuming repetitive tasks.

* Data privacy concerns when using external AI.  
   ➡ Diaflow runs directly within enterprise infrastructure → data never leaves the internal environment.

#### **2\. Architecture**

* Multi-agent architecture.

* User-defined workflows aligned with enterprise processes.

* Easy to package into widgets or integrate directly.

#### **3\. Key Highlights**

* Automates repetitive tasks → increases efficiency.

* Cost saving: reduces processing time and manual errors.

* Fast deployment.

* Easy to use, suitable for non-technical users.

#### **4\. Case Studies**

* Data extraction \+ automated analysis.

* Procurement automation.

* Clinical workflow automation.

* Vital metrics digitization from legacy systems.

* Automation of online payments.

### **CloudThinker**

#### **CloudThinker Intro – Thang Ton**

**Focus:** Agentic AI for Cloud Operations  
 **Capabilities:** collaboration, automation, optimization, continuous learning, multi-cloud support  
 **Features:** code review, incident response, operation automation, infra observability (Coming soon: Kubernetes management, Cloud Keeper)

#### **CloudThinker Agentic Orchestration & Context Optimization – Henry Bui**

**1\. Comparison: Chatbot – Agent – Multi-Agent**

* Chatbot: reactive, rule-based.

* Agent: planning \+ tool use.

* Multi-agent: coordinated roles for complex tasks.

**2\. Getting started with agents**

* Start with simple architectures like ReAct.

* Set up evals & observability from the beginning.

* Tool design strongly impacts output quality.

* Apply “quick win techniques.”

**3\. When a single agent hits limitations**

* When complexity increases → multi-agent or multi-session single-agent is needed.  
   **Multi-agent components:** supervisor, transfer architecture, specialized agents.

**4\. Context Optimization Techniques**

* Prompt caching.

* Context compaction.

* Tool consolidation (reports, dashboards, slideshows).

* Parallel tool calling.

#### **CloudThinker Hack: Hands-on Workshop – Kha Van**

Hands-on practice using CloudThinker with various use cases.

## **Key Learnings**

##### **About AgentCore**

A powerful platform enabling enterprises to build AI agents that are secure, flexible, and infrastructure-free.

##### **About Diaflow**

Clear effectiveness in automating repetitive workflows, ensuring data privacy, and reducing costs.

##### **About CloudThinker**

Optimizing cloud ops through agentic orchestration & multi-agent optimization.

##### **About Technical Practices**

* Start with simple architectures.

* Focus on evals and observability.

* Optimize context (caching, compaction, parallel calling).

## **Applications to Work**

* Experiment with Amazon Bedrock AgentCore for multi-step agentic AI requiring scalability and security.

* Use Diaflow to automate enterprise workflows with high privacy requirements.

* Use CloudThinker for cloud ops (cost, security, infra optimization).

* When building complex agentic systems: start modular, use memory \+ observability early for easy scaling.

## **Event Experience**

The workshop provided a comprehensive view of the Agentic AI landscape, including AWS vision, AgentCore architecture, Diaflow and CloudThinker solutions, and hands-on practice.

### **Some photos from the event**

* Add your images here