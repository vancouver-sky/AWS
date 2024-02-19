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
- EC2 Plancement Groups
  - Cluster - clusters instances into a low-latency group in a single AZ - high performance; high risk
    - same rack
    - same AZ
    - 10 Gvps bandwidth bewtween instances 
  - Spread - spreads instances across underlying hardware (max 7 instances per group per AZ) - critical applications
    - each instance on different hardware/rack 
  - Partition - spreads instances across many different partitions (which rely on different sets of racks) whithin an AZ. Scales to 100s of EC2 instances per group (Hadoop, Cassandra, Kafka)
    - each partition presents a single rack
    - up to 7 partitions per AZ
- Elastic Network Interfaces (ENI)
  - represents a virtual network card
  - bound to single AZ; can NOT attach to another AZ
 
## EBS
  - Network drive
    - so can be detached and attached to another EC2 instance 
  - bound to single AZ
    - if wants to move to other AZ, we can snapshot it first 
  - have a provisioned capacity *aize in GBs, and IOPS)

## Load Balancer
- NLB has one static IP per AZ
- Gateway Load Balancer - Uses the GENEVE protocol on port 6081
- Sticky Session (Session Affinity)
  
- SSL - Server Name Indication (SNI)
  - SNI solves the problem of loading multiple SSL certificate onto one web server (to serve multiple websites)
  - It is a "newer" protocol, and requires the client to indicate the hostname of the target server in the initial SSL handshake.
  - The server will then find the correct certificate, or return the default one.
  - Only works for ALB & NLB, CloudFront
  - Does not work for CLB
 
- Connection Draining
  - Feature naming
    - Connection Draining - for CLB
    - Deregistration Dely - for ALB & NLB 
  - Time to complee "in-flight requests" while the instance is de-registering or unhealthy
  - Stopes sending new requests to the EC2 instance which is de-registering
  - Between 1 to 3600 seconds (default: 300 seconds)
  - Can be disabled (set value to 0)

- Auto Scaling Group (ASG)
  - is free
  - very powerful combinding with Load Balancer
  - ASG Launch Template
  - Dynamic Scaling
    - Target Tracking Scaling -> set-up, such as average CPU to stay around 40%
    - Simple/Step Scaling -> CloudWatch alarm 
  - Scheduled Scaling
  - Predictive scaling - predict usage and scheduled the scaling
  - Scaling Cooldowns
    - Default 300 secounds 

  ## RDS
  - Support
    - Oracle
    - IBM DB2
    - MS SQL Server
    - PostgreSQL
    - MySQL
    - Amazon Aurora
    - Maria DB
  - RDS Read Replicas for read scalability
    - Up to 15 Read Replicas
    - 3 options
      - Winthin AZ
      - Cross AZ
      - Cross Region 
    -  Replication is ASYNC so reads are eventually consistent
    -  Replicas can be promoted to their own DB
    -  Applications must update the connection string to leverage read replicas
    -  Use Cases: report servers
    - Network Cost
      - In AWS, there is a network cost when data goes from one AZ to another
      - For Read Replicas within the same region, you don't pay that fee
      - Cross region will incur a fee
    - RDS Multi AZ
      - for Disaster Recovery
      - SYNC replication
      - One DNS name - automatic app failover to standby
      - Increase availability
      - Failover in case of loss of AZ, loss of network, instance or stroage failure
      - No manual intervention in apps
      - Not used for scaling
      - Note: The Read Replicas CAN be setup as Multi AZ for Disaster Recovery
    - RDS - From Single-AZ to Multi-AZ
      - Zero downtime opertaion
      - Just click on "modify" for the database
      - A snapshot is taken -> A new DB is restored from the snapshot in a new AZ -> Sync is established between the 2 DBs.
  - Aurora
    - 6 copies of your data across 3 AZ
    - One Aurora Instance thakes writes (master)
    - Automated failover for master in less than 30 seconds
    - Master + up to 15 Aurora Read Replicas serve reads
    - Support for Cross Region Replication
    - Auto Expanding from 10G to 128 TB
    - Client always points to the Writer Endpoint which points to the master which has ONE and only ONE.
    - Because the Auto Scaling, it is hard to tracking the Read Replica, -> Reader Endpoint is a Connection Load Balancing to all of Read Replica
      - The Load Balancer is on connection level not the statement level  





