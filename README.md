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

# Key Services to Know for the Exam
- **Compute**: EC2, Lambda, Elastic Beanstalk
- **Storage**: S3, EBS, EFS, FSx, Storage Gateway
- **Databases**: RDS, DynamoDB, Redshift
- **Networking**: VPCs, Direct Connect, Route 53, API Gateway, AWS Global Accelerator

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

### Shared Responsibility Model

#### Customer Responsibility (IN the Cloud)
| **Responsibility for Security IN the Cloud**                                                                                           |
|----------------------------------------------------------------------------------------------------------------------------------------|
| **Customer Data**                                                                                                                      |
| **Platform, Applications, Identity & Access Management**                                                                              |
| **Operating System, Network & Firewall Configuration**                                                                                 |
| **Client-Side Data Encryption** | **Server-Side Encryption (File System and/or Data)** | **Networking Traffic Protection (Encryption, Integrity, Identity)** |

#### AWS Responsibility (OF the Cloud)
| **Responsibility for Security OF the Cloud** |
|-----------------------------------------------|
| **Software**                                  |
| - Compute                                     |
| - Storage                                     |
| - Database                                    |
| - Networking                                  |
| **Hardware / AWS Global Infrastructure**      |
| - Regions                                     |
| - Availability Zones                          |
| - Edge Locations                              |

#### Can you do this yourself in the AWS Management Console?

- **If yes, you are likely responsible.**  
  Security groups, IAM users, patching EC2 operating systems, patching databases running on EC2, etc.
- **If not, AWS is likely responsible.**  
  Management of data centers, security cameras, cabling, patching RDS operating systems, etc.
- **Encryption is a shared responsibility.**
---

### Six Pillars of the Well-Architected Framework

- **Operational Excellence**  
  Running and monitoring systems to deliver business value, and continually improving processes and procedures.
- **Security**  
  Protecting information and systems.
- **Reliability**  
  Ensuring a workload performs its intended function correctly and consistently when it’s expected to.
- **Performance Efficiency**  
  Using IT and computing resources efficiently.
- **Cost Optimization**  
  Avoiding unnecessary costs.
- **Sustainability**  
  Minimizing the environmental impacts of running cloud workloads.

**Read this whitepaper before the exam:**  
[Well-Architected Framework Whitepaper](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html?did=wp_card&trk=wp_card)
---


# What is IAM?

**IAM (Identity and Access Management)** allows you to manage users and their level of access to the AWS console.

### Key Features:
- Create users and grant permissions to those users.
- Create groups and roles.
- Control access to AWS resources.
---


# What is the Root Account?

The **root account** is the email address you used to sign up for AWS. The root account has **full administrative access** to AWS.  
For this reason, it is important to secure this account.

# 4 Steps to Secure Your AWS Root Account
1. Enable multi-factor authentication (MFA) on the root account.
2. Create an admin group for your administrators and assign the appropriate permissions to this group.
3. Create user accounts for your administrators.
4. Add your users to the admin group.


## **Steps for Managing IAM Users, Groups, and Policies**

#### **1. Creating a User**
- Navigate to **IAM** in the AWS Management Console.
- Select **Create User**.
- Provide the username.
- Choose:
  - **AWS Management Console Access** (e.g., set/generate password).
  - Optionally enforce the user to change the password on first login.
- Download or save the credentials (username and temporary password) securely.

#### **2. Creating a Group**
- During user creation or separately, create a **Group**.
- Assign a group name based on job function (e.g., Admins).
- Attach an **IAM Policy** to the group, such as:
  - **Administrator Access** for admins.
  - Predefined AWS policies for job functions (e.g., Database Administrator, Network Administrator).

#### **3. Adding Users to Groups**
- Add users to groups for them to **inherit group permissions**.
- Groups simplify permission management compared to assigning policies to individual users.


#### **4. User Without Group or Permissions**
- A user **without a group or policy**:
  - Can log in but has no permissions except to **change their password**.
  - Cannot perform any actions in AWS.

#### **5. Tagging Users**
- Add **tags** during user creation (e.g., department, Employee_ID).
- Tags help with auditing and tracking resources created by specific users.

### **1. Creating AWS CLI Keys**
- To enable programmatic access (e.g., AWS CLI):
  - Select the user.
  - Create an **Access Key** and **Secret Access Key**.
  - Save or download the keys securely. They can only be viewed once.
- **Note**: CLI keys are separate from console passwords and used for automation/scripts.

### **Password Policy**
- Customize password settings:
  - Minimum length (e.g., 8 characters).
  - Require uppercase, lowercase, numbers, and special characters.
  - Prevent password reuse (e.g., last 10 passwords).
  - Enforce periodic password rotation.


### **Best Practices**
1. **Use Groups**:
   - Apply policies at the group level for easier management.
   - Users inherit permissions from their groups.
2. **Least Privilege Principle**:
   - Assign only the minimum permissions required for a user's role.
3. **Avoid Shared User Accounts**:
   - Each user should have their own account for accountability.
4. **Secure Root Account**:
   - Enable MFA and avoid using the root account for day-to-day activities.
5. **AWS Policy Library**:
   - Leverage predefined AWS-managed policies for common roles (e.g., Administrator Access, View-Only Access).
