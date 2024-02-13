## Domain 1: Design Secure Architectures 
- Design secure access to AWS resources
- Design secure workloads and applications
- Determine appropriate data security controls

## Domain 2: Design Resilient Architectures 
- Design scalable and loosely coupled architectures
- Design highly available and/or fault-tolerant architectures

## Domain 3: Design High-Performing Architectures 
- Determine high-performing and/or scalable storage solutions
- Design high-performing and elastic compute solutions
- Determine high-performing database solutions
- Determine high-performing and/or scalable network architectures
- Determine high-performing data ingestion and transformation solutions

## Domain 4: Design Cost-Optimized Architectures 
- Design cost-optimized storage solutions
- Design cost-optimized compute solutions
- Design cost-optimized database solutions
- Design cost-optimized network architectures

## IAM
- Global service
- Root account
- Users
- Groups only contain users, not other groups
- Users don't have to belong to groups, and can belong to multiple groups
- IAM Policies Sturcture
  -  Consists of
    -  Version:
    -  Id:
    -  Statement
  - Statements consists of
    - Sid:
    - Effect:whether the statement allows or denies access (Allow, Deny)
    - Principal:account/user/role to which this policy applied to
    - Action:list of actions this policy allows or denies
    - Resource:list of resources to which the actions applied to
    - Condition:conditions for when this policy is ineffect (optional)
- Role usually is for service account, such as for EC2 to run an AWS service.
- IAM Security Tools
  - IAM Credentials Report (account-level)
  - IAM Access Advisor (user-level)
 
## EC2
- EC2 Uer Data
  - bootstrapping our EC2 instances using an EC2 User data script
    - bootstrapping means launching commands when a achine starts
    - That cript is only run once at the instance first start
    - EC2 user data is used to automate boot tasks such as:
      - Installing updates
      - Installing software
      - Downloading common files from the internet
      - Anything you can think of
    - EC2 User data script is run as root user
- EC2 Instance Types
  - General Purpose
  - Compute Optimized
    - Batch jobs 
  - Memory Optimized
  - Storage Optimzed  







