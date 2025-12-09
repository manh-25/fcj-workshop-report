---
title: "Event 5"
weight: 1
chapter: false
pre: " <b> 4.5. </b> "
---

### **AWS Cloud Mastery Series #3: ​Theo AWS Well-Architected Security Pillar**

**Time:** 8:30AM – 12PM Saturday, November 29, 2025
**Location:** 26th Floor, Bitexco Financial Tower, HCMC


## **Event Objectives**

This workshop delivered an in-depth exploration of the **AWS Well-Architected Security Pillar**, focusing on how to design, deploy, and operate secure workloads on AWS.  
The session covered all **five security domains**—from identity management to incident response—while emphasizing **practical, real-world security best practices** applicable to day-to-day AWS operations.


## **Program Structure & Key Topics**

### **Opening & Security Foundations**

* Overview of the **Security Pillar** in the AWS Well-Architected Framework  
* Core security principles:
  * **Least Privilege**
  * **Zero Trust**
  * **Defense in Depth**
* Understanding the **AWS Shared Responsibility Model**


### **Pillar 1 — Identity & Access Management (IAM)**

* Modern IAM design:
  * Users vs Roles vs Policies
* **IAM Identity Center**:
  * Single Sign-On (SSO)
  * Permission sets
* Security best practices:
  * Multi-Factor Authentication (MFA)
  * Credential rotation
  * IAM Access Analyzer


### **Pillar 2 — Detection & Monitoring**

* Continuous detection using:
  * AWS CloudTrail  
  * Amazon GuardDuty  
  * AWS Security Hub  
* Logging at every layer:
  * VPC Flow Logs  
  * Application Load Balancer logs  
  * Amazon S3 access logs  
* Introduction to **Detection-as-Code** concepts


### **Pillar 3 — Infrastructure Protection**

* Network and workload security:
  * VPC segmentation strategies  
  * Security Groups vs Network ACLs  
* Layered perimeter defense:
  * AWS WAF  
  * AWS Shield  
  * AWS Network Firewall  


### **Pillar 4 — Data Protection**

* Encryption strategies:
  * Encryption at rest  
  * Encryption in transit  
* Key and secret management:
  * AWS KMS  
  * AWS Secrets Manager  
  * AWS Systems Manager Parameter Store  


### **Pillar 5 — Incident Response**

* Incident Response (IR) lifecycle and preparation  
* Incident Response playbooks:
  * Compromised IAM credentials  
  * Public S3 bucket exposure  
* Automated response mechanisms:
  * AWS Lambda  
  * AWS Step Functions  


### **Wrap-up & Q&A**

* Summary of key security concepts  
* Open discussion and real-world questions


## **What I Learned**

* **Least Privilege is the foundation**  
  * Always start with minimal permissions and expand only when necessary.

* **Zero Trust Architecture**  
  * Never assume trust—internal systems should be treated with the same caution as external ones.

* **Defense in Depth**  
  * Effective security requires multiple overlapping controls across all layers.

* **Automation in Detection**  
  * Security monitoring must be continuous and automated to be effective.

* **Prepared Incident Response**  
  * Playbooks are only useful if they are documented, tested, and regularly reviewed.


## **Applications to Work**

* Enable **IAM Access Analyzer** across current AWS accounts.  
* Centralize security visibility with **GuardDuty** and **Security Hub**.  
* Build and document **incident response playbooks** for common failure scenarios.  
* Audit and tighten **Security Group rules** following least-privilege principles.  
* Enforce encryption on all data stores:
  * Amazon S3  
  * Amazon RDS  
  * Amazon DynamoDB  


## **Event Experience**

Security used to feel abstract and overwhelming, but this workshop transformed it into **clear, scenario-driven problem solving**.

* Describing incidents such as **exposed access keys** or **public S3 buckets** showed how small misconfigurations can lead to serious security risks.  
* The **Zero Trust mindset** fundamentally changed how people think about system design—no component is trusted by default.  
* Services like **GuardDuty** and **Security Hub** feel like silent security sentinels, constantly monitoring the environment and reducing operational anxiety.


## **Key Takeaways**

* **Security by Design**  
  * Security must be embedded from the first architectural decision—not added later.

* **Least Privilege Saves You**  
  * While detailed IAM configuration is time-consuming, it drastically limits blast radius during incidents.

* **Always Be Ready to Respond**  
  * Incidents are inevitable.  
  * Well-prepared playbooks enable fast, calm, and systematic response instead of chaos.