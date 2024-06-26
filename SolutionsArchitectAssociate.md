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
- Ports:
  - MS SQL - 1433
  - MySQL - 3306
  - PostgreSQL - 5432
  - Oracle - 1521

## Route 53
- Hosted Zones
  - Public Hosted Zones
  - Private Hosted Zones 
- DNS record types
  - A
  - AAAA
  - CNAME
  - NS
- CNAME vs Alias
  - CNAME
    - Points a hostname to any other hostname
    - ONLY for non root domain
  - Alisa
    - Points a hostname to an AWS Resource
    - Works for ROOT Domain and NON ROOT Domain
    - Free of charge
    - Native health check
    - Alias Record is always of type A/AAAA for AWS resources
    - Alias Record can NOT set the TTL
    - You can NOT set an Alias Record for an EC2 DNS name
- Routing Policies - response to DNS queries 
  - Simple
    - route traffic to a single resource
    - can return multiple values in the same record. The client will random chose one.
    - can NOT be associated with Health Checks 
  - Weighted
    - Control the % of the requests that go to each specific resource
    - DNS name must have same name and type
    - Can be associated with Health Checks
    - Assign a weight of 0 to a record to stop sending traffic to a resource
    - If all records are 0, then will return equally. 
  - Failover
    - Health Checks
      - checks that monitor an endpoint (application, server, other AWS resource)
      - checks that monitor other health checks (Calculated Health Checks)
      - checks that monitor CloudWatch Alarms  
  - Latency based
    - Redirect to the resource that has the least latency close to us 
  - Geolocation
    - Base on user location
    - should create a "Default" record 
  - Multi-value Answer
    - allow Health Checking with multiple values return; Simple policy can NOT associated with Health Checks 
  - Geoproximity (using Route 53 Traffic Flow feature)
    - based on the geographic location of users and resources
  - IP-based Routing
- Domain Registar vs DNS Service

## S3
- Buckets
  - store objects(files) in "buckets" (directories)
  - Buckets must have a globally unique name (across all regions all accounts)
  - Buckets are defined at the region level
  - S3 look like a global service but buckets are created in a region
  - Naming convention
    - No uppercase, No underscore
    - 3 - 63 characters long
    - Not an IP
    - Must NOT start with the prefix xn--
    - Must NOT end with the uffix -s3alias
- Objects have a Key
  - The key is the FULL path
  - There is no dirtory concept
  - Object values are the content of the body
  - Max Object size is 5GB
  - If more than 5TB, must use "multi-part upload"
  - Metadata
  - Tags(Unicode ke/value pair - up to 10)
  - Version ID
- S3 - Security
  - User-Based
    - IAM policies
  - Resource-Based
    - Bucket Policies - bucket wide rules from the S3 console - allows cross account
    - Object Access Control List (ACL) - finer grain
    - Bucket Access Control List - less common
  - Note: an IAM principal can access an S3 object if
    - The user IAM permissions ALLOW it OR the resource policy ALLOW it
    - AND there's no explicit DENY  
  - Encryption: encrypt objects in Amazon S3 using encryption keys
  - S3 Bucket Policies
    - IAM JSON based policies
    - User - IAM Policy to allow
    - EC2 instance - IAM Role policy to allow
    - Block Public Access
      - specificly deny
      - allow Cross-Account

## Amazon FSx
- Launch 3rd party high-performance file systems on AWS
- FSx for Lustre
  - Linux and Cluster
  - is used to Machine Learning, High Performance Computing (HPC)
  - Video Processing, Financial Modeling, Electronic Design Automation
  - Seamless integration with S3
    - Can "read S3" as a file system (through FSx)
    - Can write the output of the computations back to S3 (through FSx)  
- FSx for Windows File Serer
  - Supports SMB, Windows NTFS, Active Directory, ACLs
  - Can be mounted on Linux EC2 instance
  - Supports MS Distributed File System (DFS) Namespaces (group files across multiple FS) 
- FSx for NetApp ONTAP
  - support NFS, SMB, iSCSI
  - Move workloads running on ONTAP or NASto AWS
  - Point-in-time instananceous cloning 
- FSx for OpenZFS
  - only support NFS
  - Move workloads running on ZFS to AWS
  - Point-in-time instananceous cloning 

## Storage Gateway
- for Hybrid Cloud for Storage
- AWS Storage Cloud Native Options
  - Block (EBS, EC2 instance store)
  - File (EFS, FSx)
  - Object (S3, Glacier)
- AWS Storage Gateway
  - Bridge between on-premises data and cloud data
  - S3 File Gateway
    - Not Glacier; only S3
    - using NFS or SMB protocol
    - Need to create IAM role for each gateway; also need to integrate with AD to access on-premises data
  - FSx File Gateway
    - Native access to Amazon FSx for Windows File Server
    - Local cache for frequently accessed data
    - Windows native compatibility (SMB, NTFS, Active Directory...) 
  - Volume Gateway
    - Block storage using iSCSI protocol backed by S3
    - Backed by EBS snapshots which can help restore on-premises volumes
    - Cached volumes: low latency access to most recent data
    - Stored volumes: entire dataset is on premise, scheduled backups to S3 
  - Tape Gateway
    - Virtual Tape Library (VTL) backed by Amazon S3 and Glacier
    - Back up data using existing tape-based processes (and iSCSI interface)
     
## DataSync
- Move large data to and from
  - out side AWS -> need agent
  - in AWS -> no agent needed (even Glacier)
- Replication tasks can be scheduled hourly, daily, weekly -> NOT real time / NOT continuely
- File permisions and metadata are preserved 

## CloudFront & AWS Global Acceslerator

## Decoupling applications: SQS, SNS, Kinesis, Active MQ

## Containers on AWS: ECS, Fargate, ECR & EKS

## Serviceless Overviews from a Solution Architect Perspective
- Lambda
- DynamoDB
- API Gateway
- Step Functions
- Amazon Cognito
 
## Database
- RDBMS - great for joins; RDS, Aurora (OLTP; Online Transaction Processing)
- NoSQL - no joins, no SQL; DynamoDB (~json), ElastiCache (key/value pairs), Neptune (graphs); DocumentDB(mongoDB); Amazon Keyspaces(Apache Cassandra)
  - DocuentDB doesn't have serverless and is not global -> need use DynamoDB 
- Object Store: S3
- Data Warehouse - SQL Analytics/ BI; Redshift (OLAP; Online Analytical Processing), Athena, EMR
- Search: OpenSearch (JSON)
- Graphs: Amazon Neptune
- Ledger: Amazon Quantum Ledger Database (Amazon QLDB)
- Time series: Amazon Timestream

## Data Analysis
- Amazon Athena
  - Servreless query in S3
  - Uses standard SQL
  - Commonly used with Amazon Quicksight for reporting
  - Performance Improvement
    - Use columnar data for cost-saving
    - Apache Parquet or ORC is recommended
    - Compress data for smaller retrievals
    - Partition dataset in S3
    - Use large file (>128M) in S3 instead of many small files in S3
    - Use Federated Queries -> Use Data Source Connectors that run on AWS Lambda to run Federated Queries
      
- Redshift
  - based on PostgreSQL, but is OLAP not OLTP.
  - analytics and data warehousing
  - Redshift has index, but Athena doesn't
  - Loading data into Redshift
    - Amazon Kinesis Data Firehose
    - S3 using COPY command
      - Through internet -> without Enhanced VPC Routing
      - Through VPC -> with Enhanced VPC Routing 
    - EC2 instance JDBC driver
    - Large inserts is better
  - Query -> Amazon Redshift Cluster (Leader Node -> Compute Nodes) -> Redshift Spectrum(s) -> S3

- OpenSearch (ElasticSearch)
  - With OpenSearch, you can search any field, even partially matches
  - Does not natively support SQL (can be enabled via a plugin)
  - DynamoDB Table -> Dynamo DB Stream -> Lambda Function -> Amazon OpenSearch
    - Then, applicaiton API to search items in OpenSearch to get id, then go to DynamoDB Table to retrieve items
  - Inject CloudWatch Logs
 
- EMR (Elastic MapReduce)
  - EMR helps creating Hadoop clusters (Big Data) to analyze and process vast amount of data
  - The clusters can be made of hundreds of EC2 instances
  - EMR comes bundled with Apache Spark, HBase, Presto, Flink
  - Node types & purchasing
    - Master Node - long running
    - Core Node - long running
    - Task Node - usually Spot
    - Purchasing options
      - On-demand: reliable, predictable, won't be terminated
      - Reserved (min 1 year): cost savings (EMR will automatically use if available)
      - Spot INstances: cheaper, can be terminated, less reliable
    - Can have long-running cluster, or transient (temporary) cluster

- Amazon QuickSight
  - Servless machine learning-powered business intelligence service
  - In-memory computation using SPICE engine if data is imported into QuickSight
  - Enterprise edition: Possibility to setup Column-Level security (CLS)
  - Define Users and Groups -> these are not IAM, only exist in QuickSight

- AWS Glue ETL
  - For ETL service
  - Fully serverless service
  - Need to write code
  - AWS Glue - convert data into Parquest format
  - Glue Data Catalog: catalog of datasets
    - AWS Glue Data Crawler -> writes metadata -> AWS Glue Data Catalog
    - Then, data discovery by Amazon Athena or Amazon Redshift Spectrum or Amazon EMR
  - Glue Job Bookmarks: prevent re-processing old data
  - Glue Elastic Views:
    - Combine and repllicate data across multiple data stores
  - Glue DataBrew: clean and normalize data
  - Glue Studio: new GUI to create, run and monitor ETL jobs
  - Glue Streaming ETL (built on Apache Spark Structured Streaming)
 
- AWS Lake Formation
  - Data lke = central place to have all your data for analytics purposes
  - Out-of-the-box source blueprints: S3, RDS, Relational & NOoSQL DB ...
  - Fine-grained Access Control for your applications
  - Built on top AWS Glue
  - Create Data Lake (stored in S3)
  - Centralized Permissions -> so manay data sources, hard to do access control -> using Lake Formation to inject data to S3 (Data Lake) to manage ACL

- Amaon Kinesis Data Analytics
  - Kinesis Data Analytics for SQL applications
    - Use SQL
       
  - Kinesis Data Analytics for Apache Flink
    - Use Flink to process and analyze steaming data
    - Run any Apache Flink application on a managed cluster on AWS
      - Flink is much powerful than SQL
    - Flink (Java, Scala or SQL) only read from Kinesis Data Streams or Amazon MSK
    - Flink does NOT read from Firehose (use Kinesis Analytics for SQL instead)
   
- Amazon Managed Streaming for Apache Kafka (Amazon MSK)
  - Alternative to Amazon Kinesis
  - Option to use MSK Serverless

- Big Data Ingestion Pipeline
  - IoT Devices -> real time sent data -> Amazon Kinesis Data Streams -> Amazon Kinesis Data Firehose -> S3 -> trigger SQS -> trigger Lambda -> trigger Athena query (pull data from S3) -> another S3 -> QuickSight or Redshift dataware house 
![Screenshot 2024-03-17 at 10 47 34 PM](https://github.com/vancouver-sky/AWS/assets/71688244/2b420ccd-b7bf-459c-9300-975c53eec83d)

- VPN
 - Transit Gateway is the only AWS service which supports **IP Multicast**
 - ECMP - Equal-cost multi-path routing
