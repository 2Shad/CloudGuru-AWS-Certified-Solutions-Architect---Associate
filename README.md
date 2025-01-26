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

## Securing S3 Buckets with Block Public Access

This exercise focused on understanding and applying access control for S3 buckets, particularly using the **S3 Block Public Access** feature. By default, S3 buckets are private, and this exercise demonstrated how to securely modify settings to allow or restrict public access at both the bucket and object levels. Explored **Access Control Lists (ACLs)** and **Bucket Policies**, understanding their use cases and limitations while managing object permissions.

#### Steps Taken
1. **Create an S3 Bucket**:
   - Navigated to the AWS Management Console and selected S3.
   - Created a new, uniquely named S3 bucket in the `us-east-1` region with default settings (private access by default).

2. **Upload Files**:
   - Uploaded two files to the S3 bucket and confirmed successful uploads via HTTP `200` response codes.

3. **Test Default Permissions**:
   - Attempted to access the files via their object URLs but received "Access Denied" errors, as the bucket and objects were private by default.

4. **Modify Bucket Permissions**:
   - Edited **Block Public Access settings** in the Permissions tab:
     - Disabled blocking public access to the bucket.
   - Adjusted **Object Ownership settings** to enable the use of ACLs by unchecking the "Bucket owner enforced" option.

5. **Make Individual Objects Public**:
   - Used **Object ACLs** to make the uploaded files public.
   - Verified access by testing the object URLs and confirming public access.

6. **Key Learnings**:
   - Buckets and objects are private by default, and explicit permissions must be configured for public access.
   - **Object ACLs** allow permissions at the object level, while **Bucket Policies** can grant permissions for the entire bucket.
   - Proper testing ensures that access changes are reflected accurately and securely.


## Hosting a Static Website Using S3

This exercise demonstrates how to host a static website using Amazon S3. Static websites consist of files such as HTML and CSS, which do not rely on backend processing or databases. S3 is particularly suited for hosting static sites due to its scalability and simplicity, automatically handling varying traffic loads without manual intervention. 

---

### Steps Taken

1. **Preparing Website Files:**
   - Downloaded a zip file containing `index.html`, `error.html`, and a JSON policy for bucket permissions.
   - `index.html` was the main homepage file, while `error.html` displayed a message for incorrect or unavailable URLs.

2. **Creating the S3 Bucket:**
   - Navigated to the S3 console in AWS.
   - Created a new bucket with a unique name.
   - Unchecked the "Block all public access" setting to allow public access.
   - Acknowledged the warning about public access for the bucket and its contents.

3. **Configuring Static Website Hosting:**
   - Navigated to the bucket's properties and enabled "Static website hosting."
   - Set the `index.html` as the default document and `error.html` as the error document.

4. **Uploading Website Files:**
   - Uploaded the `index.html` and `error.html` files into the S3 bucket.
   - Verified that the files were successfully uploaded.

5. **Making the Bucket Public:**
   - Edited the bucket policy by pasting a predefined JSON policy.
   - Updated the `Resource` field in the policy to include the specific bucket's ARN (Amazon Resource Name).
   - Saved the policy to make the entire bucket public.

6. **Testing the Website:**
   - Accessed the website via the provided bucket website endpoint.
   - Verified the functionality of `index.html` as the homepage.
   - Tested the error-handling functionality by navigating to an incorrect URL, which correctly displayed `error.html`.


## S3 Versioning Lab

#### Introduction
This exercise focused on **versioning in Amazon S3**, a feature that allows you to maintain multiple versions of objects within an S3 bucket. Versioning is particularly useful for object recovery, backup, and accidental deletion prevention. The lab demonstrated how to enable versioning, manage versions, and leverage delete markers, while emphasizing its benefits and relevance for AWS certification exams.

#### Steps Taken
1. **Understanding Versioning**:
   - Versioning was introduced as a tool for maintaining multiple versions of objects in S3, including deleted objects.
   - Key advantages:
     - Backup for all writes, even deletions.
     - Cannot be disabled once enabled, only suspended.
     - Integration with lifecycle rules.
     - Multi-Factor Authentication (MFA) support.

2. **Enabling Versioning**:
   - Navigated to the S3 Management Console.
   - Selected the bucket used for the exercise.
   - Enabled versioning under the bucket’s **Properties** section.

3. **Viewing and Managing Versions**:
   - Observed the "Show versions" option after enabling versioning.
   - Demonstrated:
     - Uploading modified versions of a file (e.g., `index.html` with changes to indicate Version 2 and Version 3).
     - Accessing specific versions using unique version IDs.

4. **Handling Deletions**:
   - Deleted an object, which resulted in a **delete marker** being applied.
   - Explored how delete markers hide objects from the user interface while retaining their previous versions.
   - Restored an object by removing its delete marker using the "Permanently delete" action.

5. **Exam Tips and Best Practices**:
   - Highlighted the benefits of versioning, including its backup capabilities and integration with lifecycle rules.
   - Explained scenarios where enabling versioning and MFA can prevent accidental deletions.
   - Reinforced that versioning cannot be completely disabled once activated, ensuring data safety.



Got it! Here's a more concise and test-focused version of the notes:

---

### **S3 Storage Classes**

#### **S3 Standard**
- High availability (99.99%) and durability (99.999999999% or "11 nines").
- Redundant storage across multiple AZs (≥3).
- Designed for frequent access.
- Suitable for websites, mobile apps, big data analytics, and content distribution.

#### **S3 Standard-Infrequent Access (IA)**
- Lower storage cost for infrequent access but requires rapid retrieval.
- 99.9% availability and 99.999999999% durability.
- Includes per-GB retrieval fees.
- Use cases: Backups, disaster recovery, long-term storage.

#### **S3 One Zone-Infrequent Access**
- Similar to Standard-IA, but data is stored in a single AZ.
- 99.5% availability and 99.999999999% durability.
- Costs ~20% less than Standard-IA.
- Use case: Non-critical, long-lived, infrequently accessed data.

#### **S3 Intelligent-Tiering**
- Automatically optimizes cost by moving data between frequent and infrequent access tiers.
- Monitoring and automation fee applies.
- No retrieval fees in frequent/infrequent tiers.
- Ideal for data with unpredictable access patterns.

#### **S3 Glacier**
- **Glacier Instant Retrieval**: Archival storage with millisecond access time.
- **Glacier Flexible Retrieval**: Lower cost, flexible retrieval within minutes to 12 hours.
- **Glacier Deep Archive**: Cheapest option for long-term retention (7–10 years); retrieval times 12–48 hours.
- Use cases: Compliance archives, disaster recovery, rarely accessed data.


### ** S3 Glacier Tiers**

#### **1. Glacier Instant Retrieval**
- **Purpose**: Long-term archival storage with fast retrieval (millisecond access).
- **Cost**: 
  - Storage: $0.004 per GB per month.
  - Retrieval: Minimal fees for instant access.
- **Use Cases**:
  - Archiving active data that needs quick access occasionally.
  - Media assets, medical imaging, or long-term project data requiring immediate availability.

#### **2. Glacier Flexible Retrieval**
- **Purpose**: Lower-cost archival storage with flexible retrieval options.
- **Retrieval Time**:
  - Standard: Minutes to hours.
  - Bulk: Up to 12 hours for large datasets.
- **Cost**:
  - Storage: $0.0036 per GB per month.
  - Retrieval:
    - Standard: Free for up to 5% of your stored data per month.
    - Additional requests incur fees.
- **Use Cases**:
  - Disaster recovery.
  - Backup systems where immediate access isn't critical.
  - Periodic access to large datasets.

#### **3. Glacier Deep Archive**
- **Purpose**: Cheapest archival storage for infrequent, long-term retention (e.g., regulatory compliance).
- **Retrieval Time**:
  - Standard: 12 hours.
  - Bulk: 48 hours.
- **Cost**:
  - Storage: $0.00099 per GB per month.
  - Retrieval:
    - Bulk retrieval has lower fees compared to Instant or Flexible tiers.
- **Use Cases**:
  - Regulatory compliance (e.g., legal or healthcare).
  - Data retention for 7–10 years or longer.
  - Historical archives and long-term backups with rare retrieval requirements.

#### **Comparison of Glacier Tiers**
| **Feature**               | **Glacier Instant**    | **Glacier Flexible** | **Glacier Deep Archive** |
|---------------------------|------------------------|-----------------------|---------------------------|
| **Retrieval Time**        | Milliseconds          | Minutes to 12 hours  | 12–48 hours              |
| **Cost (per GB/month)**   | $0.004                | $0.0036              | $0.00099                 |
| **Storage Use Cases**     | Active archival data  | Backups, DR          | Long-term, infrequent    |
| **Durability**            | 99.999999999% (11 9's)| Same                 | Same                     |
| **Lifecycle Transition** | Supported             | Supported            | Supported                |



## Lifecycle Management in S3

#### What is Lifecycle Management?
- **Definition**: Automates moving objects between different storage tiers to maximize cost efficiency.
- **Purpose**: Saves money by transitioning objects that are not frequently accessed to cheaper storage tiers.

#### Example Workflow:
1. **S3 Standard**: Objects are stored here initially.
2. **S3 Infrequent Access (S3 IA)**: After 30 days of inactivity, objects are moved here.
3. **Glacier**: After 90 days, objects are archived to Glacier for long-term storage at lower cost.

#### Combining with Versioning:
- Lifecycle Management can move **different versions** of objects to different storage tiers, offering further cost-saving opportunities.
- Example: Keep the latest version in **Standard** and older versions in **Glacier**.


### Steps for Configuring Lifecycle Management in AWS S3

1. **Create a Bucket**:
   - Go to the AWS Management Console.
   - Navigate to **S3** and create a new bucket (e.g., `acloudgurulifecycle`).
   - Use default settings for the bucket.

2. **Upload Objects**:
   - Add objects to the newly created bucket (e.g., upload three sample photos).

3. **Access Lifecycle Rules**:
   - Go to the **Management** tab within the bucket.
   - Click on **Lifecycle Rules** to define automated actions for object storage.

4. **Create a Lifecycle Rule**:
   - Click **Create Lifecycle Rule** and give it a name (e.g., `Rule1`).
   - Apply the rule to all objects in the bucket or filter specific objects.
   - Acknowledge the warning message.

5. **Define Actions**:
   - Select actions such as:
     - Transition **current versions** of objects between storage classes.
     - Transition **non-current versions** of objects (if versioning is enabled).
     - Set expiration rules to permanently delete objects after a specified period.
   - Example:
     - Transition objects to **S3 Infrequent Access** after 30 days.
     - Transition objects to **Glacier Instant Retrieval** after 60 days.

6. **Visualize the Rule**:
   - A timeline map will display the flow:
     - Day 0: Object is uploaded.
     - Day 30: Moved to **S3 IA**.
     - Day 60: Moved to **Glacier**.
   - Click **Create Rule** to save.

7. **Enable Versioning (Optional)**:
   - Go to the **Properties** tab in the bucket and enable versioning.
   - This allows applying lifecycle rules to **specific object versions**.


### Exam Tips:
1. **Understand the Automation**:
   - Lifecycle Management rules automate cost-saving transitions across storage tiers.
2. **Versioning Integration**:
   - Rules can be applied to current and previous versions of objects.
3. **Key Use Case**:
   - Moving infrequently accessed files to cheaper tiers (e.g., S3 IA or Glacier) to minimize costs.
4. **Scenario-Based Questions**:
   - Expect scenarios about managing costs by transitioning files effectively using lifecycle rules.



### S3 Object Lock and Glacier Vault Lock

#### **S3 Object Lock**
- **Purpose**: 
  - Use a Write Once, Read Many (WORM) model.
  - Prevents objects from being deleted or modified for a fixed time or indefinitely.
  - Helps meet regulatory requirements or add an extra layer of protection against changes/deletions.
  
- **Modes**:
  1. **Governance Mode**:
     - Prevents overwriting, deleting, or altering lock settings unless users have special permissions.
     - Allows certain users to alter retention settings or delete objects if necessary.
     - **Use Case**: Scenarios where some users need to modify or delete objects.
  2. **Compliance Mode**:
     - Protected objects cannot be overwritten or deleted by any user, including the root user.
     - Retention mode and period cannot be changed once set.
     - **Use Case**: Scenarios requiring strict, unalterable protection.

- **Retention Periods**:
  - Protects an object version for a specified time (e.g., 10 days, 1 year).
  - Retention metadata stored in the object indicates when the retention period expires.
  - After expiration, objects can be modified or deleted unless a legal hold is applied.

- **Legal Holds**:
  - Prevents overwriting or deleting objects.
  - Does not have an associated retention period; remains in effect until manually removed.
  - Requires the `s3:PutObjectLegalHold` permission to place or remove holds.

#### **Glacier Vault Lock**
- **Purpose**: 
  - Enforce compliance controls for Glacier vaults using a vault lock policy.
  - Uses the WORM model.
  
- **Features**:
  - Specify controls (e.g., WORM) in a vault lock policy.
  - Policies are locked from future edits once set.
  - Ensures long-term compliance and data immutability.

#### **Exam Tips**:
1. **WORM Model**:
   - For S3: Use S3 Object Lock.
   - For Glacier: Use Glacier Vault Lock.
2. **Modes Recap**:
   - **Governance Mode**: Allows limited modification or deletion by specific users.
   - **Compliance Mode**: No user (even root) can modify or delete objects.
3. **Object Lock Scope**:
   - Can apply to individual objects or entire buckets.
4. **Glacier Vault Lock**:
   - Think of this for compliance needs in Glacier.



## Encryption in Amazon S3

#### Types of Encryption
1. **Encryption in Transit**
   - Secures data while being transferred to/from the bucket.
   - Utilizes **SSL/TLS** or **HTTPS** (port 443).
   - Prevents eavesdroppers from accessing data in transit.

2. **Encryption at Rest**
   - Protects data stored in S3.
   - **Server-Side Encryption (SSE)**:
     - **SSE-S3**:
       - Managed by Amazon S3.
       - Uses AES 256-bit encryption.
       - Default for all new buckets.
     - **SSE-KMS**:
       - Managed with AWS Key Management Service (KMS).
       - User manages key permissions via KMS.
     - **SSE-C**:
       - Customer-provided keys.
       - S3 manages encryption/decryption using customer keys.
   - **Client-Side Encryption**:
     - Users encrypt data locally before uploading.
     - Users manage both encryption and decryption processes.

#### Enforcing Encryption
- Encryption is **enabled by default** for all new buckets (with SSE-S3).
- To enforce specific encryption policies:
  - Add `x-amz-server-side-encryption` to **PUT request headers**.
    - Options:
      - `AES256` (SSE-S3).
      - `aws:kms` (SSE-KMS).
  - Create a **bucket policy** to deny PUT requests without the encryption parameter:
    - Example:
      - Deny requests lacking `x-amz-server-side-encryption`.

#### Steps for Setting Encryption in the AWS Console
1. Navigate to **S3** in the AWS Management Console.
2. Click **Create Bucket**.
3. In the **Encryption** section:
   - Encryption is enabled by default.
   - Choose between:
     - **SSE-S3** (Amazon S3-managed keys).
     - **SSE-KMS** (AWS Key Management Service-managed keys).
     - **Dual-layer encryption** (SSE-KMS with extra layers of key management, optional).
4. Complete the bucket creation process.
5. View encryption settings:
   - Open an existing bucket.
   - Select an object.
   - Scroll to **Server-Side Encryption Settings** to view the applied encryption type.

#### Key Notes for Exam Preparation
- Encryption at Rest is **enabled by default**.
- **Three types of server-side encryption**: SSE-S3, SSE-KMS, and SSE-C.
- **Client-side encryption** requires user-managed keys.
- Enforce encryption:
  - **Bucket policies** can deny PUT requests without encryption headers.
- Common headers in PUT requests:
  - `x-amz-server-side-encryption`:
    - `AES256` (SSE-S3).
    - `aws:kms` (SSE-KMS).

With encryption now being default, most exam scenarios focus on **enforcing specific policies** and understanding the **different encryption methods available**.



## Optimizing S3 Performance

#### S3 Prefixes
- **Definition**: Folders and subfolders inside an S3 bucket. Does not include the object name or file type.
  - Example:
    - `mybucket/folder1/subfolder1/myfile.jpg` → Prefix: `/folder1/subfolder1`
    - `mybucket/folder2/subfolder1/myfile.jpg` → Prefix: `/folder2/subfolder1`
- **Performance Benefits**:
  - More prefixes → Better performance.
  - Request limits:
    - **3,500** requests per second for PUT/COPY/POST/DELETE.
    - **5,500** GET/HEAD requests per second per prefix.
  - Example:
    - Using **2 prefixes** → 11,000 GET requests per second.
    - Using **4 prefixes** → 22,000 GET requests per second.
- **Tip**: Distribute data across multiple prefixes to improve performance.

---

#### S3 Performance for Uploads
- **Multipart Uploads**:
  - Recommended for files **>100MB**.
  - Required for files **>5GB**.
  - **How It Works**:
    - Large files are split into chunks.
    - Chunks are uploaded in parallel, increasing efficiency.
- **Scenario**:
  - For optimizing upload performance in a test, consider **Multipart Uploads**.

---

#### S3 Performance for Downloads
- **Byte-Range Fetches**:
  - Enables parallel downloads by specifying byte ranges.
  - Benefits:
    - Faster downloads.
    - Fault tolerance: Failure only affects specific byte ranges.
  - Example:
    - A **5GB** file can be split into 5 **1GB chunks**, downloaded simultaneously.

---

#### Limitations with SSE-KMS (Key Management Service)
- **Built-In Limits**:
  - Region-specific request limits: **5,500**, **10,000**, or **30,000** requests per second.
  - Both uploading and downloading count towards this quota.
- **Quota Restrictions**:
  - Quotas cannot be increased.
- **Tips**:
  - For encryption-related scenarios, consider S3 native encryption if hitting KMS limits.


### Exam Tips

- **Prefixes for Performance:**
  - Distribute traffic across multiple prefixes (e.g., `/folder1/subfolder1`) to increase throughput.
  - Each prefix supports **3,500 PUT/POST/DELETE** and **5,500 GET/HEAD requests/sec**.

- **Multipart Uploads:**
  - Boost efficiency by splitting files into parts for parallel uploads.
  - Recommended for files over **100 MB**; required for files over **5 GB**.

- **Byte-Range Fetches:**
  - Enhance download performance by retrieving specific file ranges.
  - Fault-tolerant: retries occur only for the failed byte range.

- **KMS Quotas:**
  - SSE-KMS encryption requests are subject to regional quotas (5,500, 10,000, or 30,000 requests/sec).
  - Quotas cannot be increased, so plan workloads accordingly.

- **Encryption Overhead:**
  - Using SSE-KMS incurs additional API calls for encryption (`GenerateDataKey`) and decryption (`Decrypt`), potentially creating bottlenecks.

- **Performance Optimization:**
  - Combine prefixes, multipart uploads, and byte-range fetches for scalable, efficient S3 operations.


## S3 Replication

#### Key Features:
1. **Replication Functionality**:
   - Replicate objects between two buckets (either within the same region or cross-region).
   - Versioning must be enabled on both the source and destination buckets.

2. **Behavior**:
   - Existing objects in the bucket are **not replicated automatically** when replication is enabled. You need to create a batch job for existing objects.
   - Delete markers are **not replicated by default**.

3. **Use Cases**:
   - Backup and disaster recovery across regions or within the same region.
   - Compliance with data residency regulations.
   - Ensures resiliency by replicating data to geographically diverse regions.

#### How to Enable S3 Replication:
1. **Create Two Buckets**:
   - Define a source and a destination bucket.
   - Enable versioning on both buckets.

2. **Upload Files to Source Bucket**:
   - Add objects before or after turning on replication.

3. **Enable Replication Rules**:
   - Access the source bucket's management section.
   - Create replication rules and apply them to specific prefixes or all objects.
   - Choose a destination bucket (within the same account or a different account).
   - Configure IAM roles for permissions (create a new role or select an existing one).

4. **Handle Existing Objects**:
   - Optionally enable replication of existing objects via a batch job.

5. **Verify Replication**:
   - Check the destination bucket for replicated objects. Note that batch replication may take a few minutes.

#### Exam Tips:
- Remember the requirement to enable **versioning** on both buckets.
- Replication works for new objects automatically but requires manual intervention for existing objects.
- Delete markers and individual object deletions are **not replicated by default** unless explicitly configured.
- Use cases often involve cross-region replication for resilience against natural disasters or compliance with regulations.


# S3 Summary for Exam Preparation

#### S3 Basics:
- **Object-Based Storage:** Designed for uploading and storing files in the cloud.
- **Limitations:** Not suitable for operating systems or databases.
- **Storage Limits:** Files can range from 0 bytes to 5 TB, with unlimited storage capacity.
- **Universal Namespace:** Bucket names are unique globally and form part of the bucket URL (e.g., `bucket-name.s3.region.amazonaws.com/key-name`).
- **Successful Uploads:** HTTP 200 status code indicates success.

#### S3 Objects:
- **Key:** The file name (e.g., `Ralphie.jpg`).
- **Value:** The file data, represented as bytes.
- **Version ID:** Tracks different versions of the same object.
- **Metadata:** Information about the object, such as content type or last-modified date.

#### Security:
- **Default Privacy:** Buckets and objects are private by default.
- **Object ACLs:** Grant access to individual objects.
- **Bucket Policies:** Control access at the bucket level (e.g., public access for static websites).
- **Static Websites:** S3 supports hosting static websites with automatic scaling.

#### Versioning:
- **Backup Tool:** Stores all versions of objects, including deleted ones (via delete markers).
- **Non-Disabling:** Can only be suspended, not turned off.
- **Integration:** Works with lifecycle rules and supports multi-factor authentication.

#### Storage Classes:
1. **S3 Standard:** General-purpose for most workloads.
2. **S3 Standard-Infrequent Access (IA):** For less frequently accessed critical data.
3. **S3 One Zone-IA:** Cost-effective for non-critical, infrequently accessed data in one availability zone.
4. **S3 Glacier:** For archiving with retrieval times of hours.
5. **S3 Glacier Deep Archive:** Lowest-cost archival with 12+ hour retrieval times.
6. **S3 Intelligent-Tiering:** Uses machine learning for cost optimization based on access patterns.

#### Lifecycle Management:
- **Automation:** Moves objects between storage tiers.
- **Integration:** Works with versioning for managing current and previous versions.
- **Applications:** Ideal for long-term cost management.

#### Object Lock & Glacier Vault Lock:
- **Object Lock (WORM):** Write Once, Read Many (WORM) model for immutability.
  - **Governance Mode:** Restricts overwrites/deletions with limited permissions.
  - **Compliance Mode:** Full protection, including root user restrictions.
- **Glacier Vault Lock:** Enforces compliance rules like WORM for Glacier storage, locking policies permanently once applied.

#### Encryption:
- **In Transit:** SSL/TLS or HTTPS ensures data security while transferring.
- **At Rest (Server-Side Encryption):**
  - **SSE-S3:** Managed by S3 using AES-256.
  - **SSE-KMS:** Managed by AWS Key Management Service.
  - **SSE-C:** Customer-managed encryption keys.
- **Client-Side Encryption:** Files are encrypted before upload.
- **Bucket Policies for Enforcement:** Deny PUT requests without encryption.

#### Performance Optimization:
- **Prefixes:** Separate prefixes (folders/subfolders) increase request throughput (e.g., 3,500 PUT/POST/DELETE and 5,500 GET/HEAD requests/sec per prefix).
- **Multipart Uploads:** For files over 100 MB (mandatory for >5 GB) to boost upload efficiency.
- **Byte-Range Fetches:** Parallelize downloads by specifying byte ranges, improving speed and fault tolerance.

#### Replication:
- **Replication Scope:** Replicates objects between buckets, both within the same region and across regions.
- **Versioning Requirement:** Both source and destination buckets must have versioning enabled.
- **Replication Rules:**
  - Existing objects are not automatically replicated.
  - Delete markers are not replicated by default (configurable).
