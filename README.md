# CloudGuru-AWS-Certified-Solutions-Architect---Associate
##### My notes following the **AWS-Certified-Solutions-Architect - Associate** course avaliable on CloudGuru
---

# Exam Guide

### Exam Overview
- **Exam Format:**
  - Score range: 100–1,000
  - Minimum passing score: 720
  - Total questions: 65
  - Time allotted: 130 minutes

### Response Types
- **Scenario-based questions:**
  - Real-world scenarios requiring interpretation of keywords and requirements.
- **Multiple choice:**
  - One correct response among distractors.
- **Multiple response:**
  - Two correct responses out of five options.

### Exam Domains and Weights
1. **Design Resilient Architectures (26%):**
   - Design multi-tier, scalable, fault-tolerant solutions.
   - Implement decoupling mechanisms like message queues.
   - Select appropriate resilient storage solutions.
2. **Design High-Performing Architectures (24%):**
   - Identify elastic and scalable compute solutions (e.g., auto-scaling groups).
   - Select optimal networking solutions (e.g., VPN vs Direct Connect).
   - Choose high-performing database solutions.
3. **Design Secure Architectures (30%):**
   - Design secure access with IAM and encryption methods.
   - Implement secure application tiers.
4. **Design Cost-Optimized Architectures (20%):**
   - Identify cost-effective storage and compute options (e.g., S3 tiers, spot instances).
   - Optimize network architectures for cost.
---

# Key AWS Components

- **Region**
  - A physical location in the world that consists of two or more Availability Zones (AZs).
- **Availability Zone (AZ)**
  - One or more discrete data centers — each with redundant power, networking, and connectivity — housed in separate facilities.
- **Edge Locations**
  - Endpoints for AWS that are used for caching content.
  - Typically consists of **CloudFront**, Amazon's Content Delivery Network (CDN).
---

# Shared Responsibility Model

| **Customer Responsibility (IN the Cloud)**                                 | **AWS Responsibility (OF the Cloud)**             |
|-----------------------------------------------------------------------------|---------------------------------------------------|
| **Customer Data**                                                           | **Software**                                      |
| **Platform, Applications, Identity & Access Management**                   | - Compute                                         |
| **Operating System, Network & Firewall Configuration**                     | - Storage                                         |
| **Client-Side Data Encryption & Data Integrity Authentication**            | - Database                                        |
| **Server-Side Encryption (File System and/or Data)**                       | - Networking                                      |
| **Networking Traffic Protection (Encryption, Integrity, Identity)**        | **Hardware / AWS Global Infrastructure**          |
|                                                                             | - Regions                                         |
|                                                                             | - Availability Zones                              |
|                                                                             | - Edge Locations                                  |

### Can you do this yourself in the AWS Management Console?

- **If yes, you are likely responsible.**  
  Security groups, IAM users, patching EC2 operating systems, patching databases running on EC2, etc.
- **If not, AWS is likely responsible.**  
  Management of data centers, security cameras, cabling, patching RDS operating systems, etc.
- **Encryption is a shared responsibility.**
---
