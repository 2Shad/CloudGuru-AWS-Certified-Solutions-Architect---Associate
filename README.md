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




# IAM Hands-On Lab: Managing Users, Groups, and Permissions

### Objective
Learn the foundations of AWS Identity and Access Management (IAM) by creating and managing users, groups, and permissions. Understand how IAM policies enforce access restrictions and how to simulate real-world scenarios.

---

### Steps Taken

1. **Exploring IAM Users and Groups**:
   - Reviewed user permissions and groups.
   - Verified no permissions were assigned to users initially.
   - Examined group policies:
     - **EC2-Admin**: Full access to start, stop, and view EC2 instances.
     - **EC2-Support**: Read-only EC2 access.
     - **S3-Support**: Read-only S3 access.

2. **Assigning Users to Groups**:
   - Added `user-1` to **S3-Support** (read-only access to S3).
   - Added `user-2` to **EC2-Support** (read-only access to EC2).
   - Added `user-3` to **EC2-Admin** (view, start, and stop EC2 instances).

3. **Testing Permissions**:
   - **Sign-in as `user-1`**:
     - Verified access to **S3**. Could not create a bucket (Access Denied).
     - Encountered API errors for EC2 (no permissions).
   - **Sign-in as `user-2`**:
     - Verified access to **EC2**. Could view instances but could not stop them (Access Denied).
     - Confirmed no access to **S3**.
   - **Sign-in as `user-3`**:
     - Verified full access to **EC2**. Successfully stopped a running instance.

4. **Access Control Insights**:
   - Explored IAM-managed policies and inline policies for groups and users.
   - Verified that group policies enforce user permissions.



# IAM Hands-On Lab: Create and Assume Roles in AWS

### Objective
Learn how to create and manage IAM policies and roles to restrict user access to specific AWS resources. Understand the concept of assuming roles and how it facilitates secure access control in AWS.

---

### Steps Taken

1. **Created a Custom IAM Policy**:
   - Navigated to S3 and identified buckets to restrict access (`appconfigprod` buckets).
   - Created the **S3RestrictedPolicy**:
     - Allowed all S3 actions but restricted resources to the two `appconfigprod` buckets.
     - Added the ARNs for the restricted buckets to the policy.
   - Attached the policy to `user1`.

2. **Created an IAM Role**:
   - Created the **S3RestrictedRole**:
     - Trusted entity: The current AWS account.
     - Attached the **S3RestrictedPolicy** to the role.

3. **Configured Trust Relationship**:
   - Allowed `user2` to assume the **S3RestrictedRole**:
     - Updated the trust policy for the role with `user2`'s ARN.

4. **Tested Policy and Role Configuration**:
   - **Signed in as `user1`**:
     - Confirmed no access to EC2 or `customerdata` buckets.
     - Verified access to the `appconfigprod` buckets.
   - **Signed in as `user2`**:
     - Confirmed no access to any buckets by default.
     - Used the "Switch Role" feature to assume the **S3RestrictedRole**:
       - Verified access to `appconfigprod` buckets.
       - Confirmed restricted access to `customerdata` buckets.




# AWS S3

#### **What is S3?**
- **S3** stands for **Simple Storage Service**, providing object-based storage in the cloud.
- **Features:**
  - Secure, durable, and highly scalable.
  - Allows storing and retrieving any amount of data from anywhere on the web at low costs.
  - Simple-to-use web interface.
  
#### **Key Characteristics of S3**
1. **Object-Based Storage**:
   - Stores files as objects rather than in file systems or data blocks.
   - Examples of file types: images, videos, documents, code, etc.
   - Not for operating systems or databases.
2. **Unlimited Storage**:
   - Unlimited number of objects with individual object sizes ranging from **0 bytes to 5 TB**.
3. **Buckets**:
   - Containers (similar to folders) where files (objects) are stored.
   - Must have **globally unique names** within the **S3 universal namespace**.
   - Example of bucket URL: `https://bucket-name.s3.Region.amazonaws.com/key-name`.
4. **Key-Value Storage**:
   - Key: Object name (e.g., `photo.jpg`).
   - Value: Actual data stored.
   - Includes **metadata** (data about data, e.g., content type, modification time).
   - Supports **versioning** to manage multiple object versions.

#### **Availability & Durability**
- **Designed for Availability**:
  - 99.95% to 99.99% depending on the S3 tier.
- **Durability**:
  - 99.999999999% (11 nines) durability, ensuring negligible data loss.
- Data is replicated across multiple devices and facilities (e.g., multiple Availability Zones).

#### **Storage Tiers**
- **Standard S3**:
  - Default tier for frequently accessed data.
  - Designed for high availability and durability.
  - Suitable for websites, content distribution, big data analytics, etc.
- **Lifecycle Management**:
  - Allows automatic transition of objects to cheaper tiers or deletion after a set period.
- **Versioning**:
  - Retains all versions of objects, including deleted ones.

#### **Securing Data in S3**
1. **Server-Side Encryption (SSE)**:
   - Encrypts objects as they are uploaded to buckets.
2. **Access Control Lists (ACLs)**:
   - Fine-grained permissions for specific AWS accounts or groups.
   - Can be applied to individual files within a bucket.
3. **Bucket Policies**:
   - JSON policies governing actions (e.g., `PUT`, `GET`) on a bucket-wide level.
   - Example: Granting user Alice permission to upload files but not delete them.

#### **Consistency Model**
- **Strong Read-After-Write Consistency**:
  - Any read request after uploading or modifying an object immediately retrieves the latest version.
  - Includes strong consistency for list operations (e.g., listing all objects in a bucket).

#### **Important Exam Tips**
- S3 is **object-based** storage for static files, not for operating systems or databases.
- Objects can be up to **5 TB** in size, and total storage is unlimited.
- Buckets must have **globally unique names**.
- Successful uploads via CLI/API return an **HTTP 200 status code**.
- Key S3 components include:
  - **Key**: Object name.
  - **Value**: Data stored.
  - **Version ID**: Tracks multiple versions of the same object.
  - **Metadata**: Information about the stored data.