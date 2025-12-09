---
title: "Blog 2"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
# Overview of security services available in AWS Dedicated Local Zones

by Lakshmi VP và Enrico Liguori | on 10 SEP 2025 | in [Intermediate (200)](https://aws.amazon.com/blogs/security/category/learning-levels/intermediate-200/), [Security, Identity, & Compliance](https://aws.amazon.com/blogs/security/category/security-identity-compliance/), [Technical How-to](https://aws.amazon.com/blogs/security/category/post-types/technical-how-to/) | [Permalink](https://aws.amazon.com/blogs/security/overview-of-security-services-available-in-aws-dedicated-local-zones/)

When modernizing applications, customers in regulated industries like government, financial, and research face a critical challenge: how to transform their systems while meeting strict digital sovereignty and security compliance requirements. A common misconception tied to this is that data must be moved to an AWS Region to fully use [Amazon Web Services (AWS)](https://aws.amazon.com/) security services.

In this blog post, we dispel that misconception by addressing how to use the following Region-based AWS security services while keeping your data within [AWS Dedicated Local Zones](https://aws.amazon.com/dedicatedlocalzones/).

*   AWS Nitro System provides foundational security
*   [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms) and [AWS Certificate Manager (ACM)](https://aws.amazon.com/acm) enable robust encryption
*   [Amazon Inspector](https://aws.amazon.com/inspector), [Amazon GuardDuty](https://aws.amazon.com/guardduty/), and [AWS Shield](https://aws.amazon.com/shield) work together to help protect workloads
*   [AWS CloudTrail](https://aws.amazon.com/cloudtrail) maintains governance through monitoring and auditing

Dedicated Local Zones are AWS-managed on-premises infrastructure configured for your exclusive use. They help meet specific regulatory requirements while providing cloud benefits such as elasticity, scalability, and pay-as-you-grow pricing. You can place data in your chosen location and use it with enhanced security and governance features provided by AWS to monitor and control application access while maintaining data isolation, in-country data residency, digital sovereignty, and meeting compliance requirements.

### AWS Nitro System

Many organizations with strict compliance and data sovereignty requirements are understandably hesitant about moving confidential workloads to the cloud. Their concerns are legitimate and specific: they need a solution that provides independently verifiable protection and isolation from data access by privileged parties, including cloud provider personnel. These organizations also require assurance that unauthorized data access through the cloud control plane is technically impossible, not just contractually prohibited.

Perhaps most critically, they need side-channel protection to help make sure that sensitive data cannot leak through memory or other means to other hypervisor tenants sharing the same physical infrastructure. Traditional cloud security approaches often rely on operational controls and promises rather than technical impossibility, which doesn’t meet the stringent requirements these organizations face.

The [AWS Nitro System](https://aws.amazon.com/ec2/nitro/), which is the foundation of AWS next generation [Amazon Elastic Compute Cloud (Amazon EC2)](https://aws.amazon.com/ec2) instances that run in a Dedicated Local Zone and its parent Region, addresses each of these concerns through its architecture. This purpose-built combination of specialized hardware and software creates a secure enclave that shields your data from unauthorized access during processing on EC2 instances.

The EC2 instances that run in your Dedicated Local Zones are based on AWS Nitro System, which is designed to provide robust security for compute workloads. It uses specialized hardware and software components to help protect your data from unauthorized access during processing on Amazon EC2.

The three key components of Nitro System include a purpose-built Nitro cards, the Nitro Security Chip, and a Nitro Hypervisor. Together, these three components are [designed to enforce restrictions](https://docs.aws.amazon.com/whitepapers/latest/security-design-of-aws-nitro-system/security-design-of-aws-nitro-system.html) and provide physical and logical security boundaries so that no one, including AWS employees, can access customer workloads or data running on Amazon EC2 without your explicit authorization.

The [Nitro System whitepaper](https://docs.aws.amazon.com/whitepapers/latest/security-design-of-aws-nitro-system/security-design-of-aws-nitro-system.html) details how the Nitro System, by design, removes the possibility of administrator access to an EC2 instance, the overall passive communications design of the Nitro System, and the Nitro System change management process. The security design of the Nitro System has also been independently validated by the NCC Group in a [public report](https://aws.amazon.com/vi/blogs/compute/aws-nitro-system-gets-independent-affirmation-of-its-confidential-compute-capabilities/).

### AWS Key Management Service

Working with customers, we’ve noticed that one of the most persistent sources of confusion and concern isn’t just about whether their data is encrypted, but about who controls the keys that protect that encryption. Many organizations struggle with a fundamental tension: they want the operational benefits of cloud computing, but they also need to maintain strict control over their encryption keys to meet compliance requirements.

This concern is particularly acute for organizations in regulated industries, which often ask pointed questions like “Where exactly are my encryption keys stored?” and “Who can access my keys?” [AWS KMS](https://aws.amazon.com/kms/) addresses this by offering multiple approaches to key management, each designed for different security and operational requirements. The service provides centralized control over the lifecycle and permissions of encryption keys, so you can create new keys whenever needed and control key management access separate from key policies

By default, Dedicated Local Zones customers can use the integration with AWS KMS in the parent Region to store and control encryption keys. You can then use these encryption keys to encrypt your data stored [locally in Amazon EBS, and Amazon S3 in the Dedicated Local Zones](https://aws.amazon.com/vi/dedicatedlocalzones/features/).

If your use cases require an external encryption key store to maintain strict data sovereignty requirements, then the combination of Dedicated Local Zones and an [AWS KMS external key store](https://docs.aws.amazon.com/kms/latest/developerguide/keystore-external.html) can provide a robust solution.

Using an external key store in Dedicated Local Zones, you can host the external hardware security module (HSM) that stores your encryption keys on-premises or colocated with your other infrastructure. By doing this, you maintain full control over the physical security and management of the HSM, while benefiting from the low-latency access and data processing capabilities of Dedicated Local Zones.

The main components of AWS KMS external key store architecture are:

*   **XKS proxy server:** You provision an external key store proxy (XKS proxy) server within your on-premises data center (as shown in Figure 1) or within the Dedicated Local Zones. The role of the XKS proxy is to act as the intermediary between AWS KMS and your on-premises HSM. The XKS proxy must be registered as target of a [Network Load Balancer (NLB)](https://aws.amazon.com/elasticloadbalancing/application-load-balancer/) in Region, this means that if it’s hosted on your on-premises data center, then NLB [Amazon Virtual Private Cloud (Amazon VPC)](https://aws.amazon.com/vpc) must have private connectivity to the on-premises network through a site-to-site VPN or [AWS Direct Connect](https://aws.amazon.com/directconnect) connection.
*   **On-premises HSM:** You configure your on-premises HSM to securely store the root encryption keys that will be used to protect your data encryption keys.
*   **External key store:** You create an external key store resource in AWS KMS, which maps to your on-premises HSM through the XKS proxy.

<img src="/images/3-Blog/3.2-Blog2/fig-1.png" width="800">

*Figure 1: AWS KMS external key store trong một Dedicated Local Zone*

The workflow is as follows:

1.  [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) or [Amazon Elastic Block Store (Amazon EBS)](https://aws.amazon.com/ebs) deployed locally in the Dedicated Local Zones needs to encrypt data, it requests AWS KMS to generate a new data encryption key.
2.  AWS KMS sends a request to the XKS proxy, which communicates with your on-premises HSM to generate the root key material.
3.  AWS KMS uses this root key to encrypt the data encryption key before returning it to the requesting service and stores the encrypted data encryption key alongside the encrypted data in Amazon S3 or Amazon EBS.
4.  For future encrypt/decrypt operations, the AWS service uses the previously generated and AWS KMS-encrypted data encryption key, without needing to interact with the on-premises HSM.

**Note**: The on-premises HSM only participates in the initial root key generation to protect the data encryption key, not in the high-volume encrypt/decrypt operations on the data itself.

This architecture delivers two key benefits:

*   You maintain complete control of your encryption keys by storing them in your data center, helping you meet security compliance requirements.
*   Dedicated Local Zones keep your data isolated in your chosen location, providing low latency for your users.

It’s important to note that using an AWS KMS external key store requires you to manage additional operational tasks beyond standard AWS KMS. To maintain continuous access to your encrypted data, you must provide 24/7 availability of your on-premises HSM, monitor XKS proxy infrastructure performance, implement robust security controls, and create backup and recovery procedures.

Because system outages can prevent access to your encrypted data, we recommend that you develop detailed operational runbooks, set up comprehensive monitoring, test your recovery procedures regularly, and maintain redundant systems where possible.

For more information about the interactions between AWS KMS and the external key store, see [Announcing AWS KMS External Key Store (XKS)](https://aws.amazon.com/blogs/aws/announcing-aws-kms-external-key-store-xks/).

### Amazon Inspector

Another common concern we hear from organizations evaluating Dedicated Local Zones is whether they’ll need to compromise on security capabilities to maintain data residency. The reality is that AWS security services running in a Region, such as Amazon Inspector, are specifically designed to provide comprehensive protection while respecting your data location requirements.

Organizations running regulated applications in Dedicated Local Zones require robust protection from zero-day vulnerabilities, prioritized patch remediation, and automated vulnerability management to meet compliance requirements. Amazon Inspector addresses these needs by continuously scanning your workloads to detect software vulnerabilities and unintended network exposure without requiring data movement from your chosen location.

Amazon Inspector helps protect your workloads through two distinct scanning modes: hybrid scanning and agent-based scanning. However, for the context of this blog, let’s consider only agent-based scanning mode.

To securely meet data residency requirements in Dedicated Local Zones, enable agent-based scanning mode on [AWS Systems Manager (AWS SSM)-managed instances](https://docs.aws.amazon.com/inspector/latest/user/scanning-ec2.html#agent-based) in your account. It’s the default mode for new accounts offering enhanced security through continuous scanning, immediately responding to new common vulnerabilities and exposures (CVEs) and instance changes. It also enables deep inspection capabilities for eligible instances, providing comprehensive vulnerability assessment.

The reference architecture in Figure 2 shows:

*   Amazon Inspector agent running on AWS SSM managed instances, keeping your application data within Dedicated Local Zones.
*   Amazon Inspector evaluates and generates [findings](https://docs.aws.amazon.com/inspector/latest/user/findings-types.html) for detected vulnerabilities.

<img src="/images/3-Blog/3.2-Blog2/fig-2.png" width="1000">

*Figure 2: Amazon Inspector trong Dedicated Local Zones*

### Amazon GuardDuty

Maintaining data sovereignty with Dedicated Local Zones doesn’t mean sacrificing advanced security capabilities. [GuardDuty](https://aws.amazon.com/guardduty/) demonstrates how sophisticated threat detection can operate effectively while honoring strict data residency requirements.

Protecting your AI workloads from ransomware and advanced security threats requires an AI and machine learning (AL/ML)-integrated threat intelligence solution that can detect suspicious activity and respond proactively. GuardDuty uses AI/ML-based threat detection and integrated threat intelligence from AWS and leading third parties to protect your AWS accounts, workloads, and data. It continuously monitors malicious activity, delivers detailed security findings, and you can use the information it provides to respond quickly to threats.

With [GuardDuty EKS Protection](https://docs.aws.amazon.com/guardduty/latest/ug/kubernetes-protection.html), monitors Kubernetes audit logs to detect threats. The key point to note is that [your data is stored in your chosen location](https://aws.amazon.com/vi/compliance/data-privacy-faq/#topic-1) and the parent Region only processes log data.

[GuardDuty Runtime Monitoring](https://docs.aws.amazon.com/guardduty/latest/ug/runtime-monitoring.html) observes and analyzes operating system, networking, and file events to detect potential threats in your AWS workloads. The parent Region receives only threat reports while Dedicated Local Zones retain your data.

The reference architecture in Figure 3 shows how GuardDuty helps protect your data in a Dedicated Local Zones:

1. GuardDuty monitors EC2 instances while your data stays in Dedicated Local Zones.
2. GuardDuty analyzes data sources from [AWS CloudTrail](https://aws.amazon.com/cloudtrail) event logs, management events, and Amazon VPC flow logs that your AWS account captures in the Region.

<img src="/images/3-Blog/3.2-Blog2/fig-3.png" width="1000">

*Figure 3: Amazon GuardDuty trong Dedicated Local Zones*

### AWS Certificate Manager

Organizations frequently express concern about certificate management complexity when deploying applications in Dedicated Local Zones. [AWS Certificate Manager (ACM)](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html), which operates in the parent Region, addresses these challenges by serving as the primary service that customers use to provision, manage, and deploy certificates for use in both public-facing and private Dedicated Local Zones workloads.

ACM integrates seamlessly with ALBs in Dedicated Local Zones to manage your complete certificate lifecycle, as shown in Figure 4.

<img src="/images/3-Blog/3.2-Blog2/fig-4.png" width="1000">

*Figure 4: ACM trong Dedicated Local Zones*

Follow these steps to implement TLS certificates in Dedicated Local Zones:

1.  Provision or import certificates through ACM in the parent Region.
2.  Associate your certificates with ALB HTTPS listeners in Dedicated Local Zones to enable secure, low-latency SSL/TLS termination near your users.

ACM renews certificates automatically, avoids manual management tasks, and maintains continuous HTTPS service availability. This integration delivers enterprise-grade security with your data residing locally in Dedicated Local Zones. It also provides enhanced performance and reduced latency through proximity to users.

### AWS Shield

Business-critical applications in Dedicated Local Zones need maximum availability and responsiveness. [AWS Shield](https://aws.amazon.com/shield/) Standard, a managed distributed denial of service (DDoS) protection service that runs at the AWS edge, automatically helps protect your applications by detecting and mitigating network (Layer 3) and transport (Layer 4) DDoS attacks even before they reach your workloads.

### AWS CloudTrail

A common concern when deploying workloads in Dedicated Local Zones is whether organizations can maintain the same level of governance and compliance oversight they expect from traditional AWS deployments. CloudTrail demonstrates how comprehensive auditing capabilities can extend seamlessly across distributed infrastructure while respecting data residency requirements.

[CloudTrail](https://aws.amazon.com/cloudtrail), running in the parent Region, enables governance, compliance, operational auditing, and risk auditing of your AWS account providing you aggregated and consolidated record of multisource events in a single place. This includes a detailed history of AWS API calls for your account, including API calls made using the AWS Management Console, the AWS SDKs, the command line tools, and higher-level AWS services used by the applications running in your Dedicated Local Zones. Only the logs are stored in the parent Region, while your data remains within the Dedicate Local Zones. AWS CloudTrail helps you to enable operational and risk auditing, governance, and compliance of your AWS accounts.

### Conclusion

Dedicated Local Zones provide a robust solution for running regulated workloads for all industries, to meet strict data residency and digital sovereignty. Through integrated security services like AWS Nitro System, AWS KMS External Key Store, ACM, AWS Shield, Amazon GuardDuty, Amazon Inspector, and AWS CloudTrail, your organization can achieve stronger security compliance for their mission-critical applications running in AWS Dedicated Local Zones.

To learn more about implementing these security solutions in your Dedicated Local Zones deployment, contact your AWS account team.

If you have feedback about this post, submit comments in the Comments section below. If you have questions about this post, [contact AWS Support](https://console.aws.amazon.com/support/home).

---

| <img src="/images/3-Blog/3.2-Blog2/author-1.png" width="200"> |**Lakshmi VP** - Lakshmi is a Solutions Architect at AWS WWPS-Canada and specializes in hybrid edge solutions—Outposts, Local Zones and Dedicated Local Zones. With over 16 years of global supporting various industries, Lakshmi is passionate about technology and practical solutions for customers. Outside work, she enjoys watching animated movies and hiking. |
| :---- | :---- |
| <img src="/images/3-Blog/3.2-Blog2/author-2.png" width="200"> |**Enrico Liguori** - Enrico is a Specialist Solutions Architect focused on networking and hybrid cloud. He works within the Worldwide Public Sector Solutions Architecture organization, where he leverages his expertise to design highly available, scalable, secure, and cost-effective networking and hybrid cloud solutions. When Enrico isn’t immersed in his professional responsibilities, he indulges in exploring the wonders of the underwater world through scuba diving. |

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