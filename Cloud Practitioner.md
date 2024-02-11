- 8 core cold categories
  - Compute (oragne icons)
  - Storage (green icons)
  - Database (blue icons)
  - Networking (purple icons)

  - Security (red icons)
  - Application Integration
  - Management & Governance
    
  - Elasticity
    - The ability for the infrastructure supporting an application to grow and contract based on how much it is used at a point in time.   

 ## Global Infrasturction 
  - AWS Regions
    - Each region contains multiple datacenter clusters   
  - Availability Zones
    - Consists of one or more data centers
    - Multiple availability zones are included with each AWS Region
    - Locate within each geographic
    - HA concept - no signle fail point
  - Point of presence
    - edge location
    - reginal edge cache
    - these elements locate in near popular area
    - as node of global network node Content Delivery Network (CDN)
  - Local and Wavelength Zones
 
## Cloud Economics
  - Tag   
  - AWS Organizations
    - manage multiple accounts
    - provide single bill
  - Building the Business Case
    - AWS Pricing Calculator
      - Use for estimating future cost
      - AWS Simple Monthly Calculator (deprecated)
      - can use for one machine pricing calculating instead of migration project
    - Create a TCO - total cost
    - `AWS Migration Hub`
    - `Migration Evalutator`
  - AWS Budgets
  - AWS Cost Explorer
  - AWS Billing confuctor

## AWS Support
  - support from AWS resources
  - AWS Personal Health Dashboard
    - provide alerts and remediation guidline
  - AWS Trusted Advisor
    - Trusted Advisor Checks
      - Cost Optimization
      - Performance
      - Security
      - Fault Tolerance
      - Service Limits
  - AWS Support Plan
    - Differences
      - Communication Method
      - Response Time
      - Cost
      - Type of Guidance Offered
    - Plan types
      - Basic Support
        - 7 free core trust advisor checks
        - no human support 
      - Developer Support
        - can email human for support
        - responses time: 24, 12 hours
      - Business Support
        - can call human support
        - responses time: 24, 12, 4, 1 hours
      - Enterprise Support
        - designated Technical Advisor Manager (TAM)
        - responses time: 24, 12, 4, 1 hours, 15 minutes
  - Assistance for Cloud Workloads
    - AWS Quick Starts
    - AWS Partner Network Consulting Partners
    - AWS Professional Services
    - AWS Activate for Startups
    - AWS IQ
    - AWS Managed Service (AMS)
    - AWS Support

## Compute (orange icons)
  - EC2
    - Instance type
      - such as cpu, gpu etc.
    - EBS
      - persistent storage
    - Instance Store
      - in memery
    - Amazon Machine Image (AMI)
    - Purchase Options
      - On-Demand
      - Reserved
        - Standard
        - Convertible
        - Scheduled
      - Savings Plan
      - Spot Instances
        - up to 90% discount
      - Dedicated Host
        - per server license model
     
  - Beanstalk
    - Platform as a service (PaaS)
      - supported app platforms
        - Java, .NET, PHP, Node.js, Python, Docker, Ruby, Go
    - Monitoring included
    - Deployment
    - Scaling
    - allow EC2 Customization
  
  - Lambda
    - event-driven, serverless computing platform
    
  - Container Service 
    - AWS App Runner
    - Container Orchestration Services
      - ECS
        - natively integrates with many AWS services 
      - EKS
        - Kubernetes 
      - Compute Engines
        - EC2 
        - AWS Fargate
          - Serverless compute engine     

## Network & Content Delivery Services (blue icons) (6 core services)
  - Amazon Rotue 53
    - Amazon DNS server
    - Global AWS service (not regional)
    - Enables global resource routing 
  - Amazon VPC
  - AWS Direct Connect
    - establish a dedicated network connection form your data center to AWS   
  - Amazon API Gateway
    - can distribute from CloudFront
    - provides monitoring and metrics
    - supports VPC  
  - Amazon CloudFront
    - Content delivery network (CDN)
    - Enables usres to get content from server closest to them
    - use edge locations
  - Elastic Load Balancing
    - integrates with EC2, ECS and Lambda
    - support one or more availability zone in a region
    - 3 types of load balancers:
      - Application Load Balancer (ALB)
      - Network Load Balancer (NLB)
      - Classic Load Balancer (Classic or ELB)
    - Scaling EC2
      - Vertical Scaling
      - Horizontal Scaling
        - user load balancer to add more nodes       
  - AWS Global Accelerator
    - use Edge location
    - use AWS network instead of public internet
    - can use with AWS service, such as ALB, NLB,EC2, Elastic IP

## File Storage Services (green) (6 core services)
  - S3
    - stores files as objects in buckets
    - provides different storage classes
    - stores data across multiple availability zones
    - enables URL access
    - can serve as a static website host
    - S3 Non-Archival Storage classes
      - S3 Standard
        - frequently accessed data
      - S3 Express One Zone
        - most frequently accessed data
      - S3 Standard-IA (infrequently accessed data)
      - S3 One Zone-IA
      - S3 Intelligent-Tiering
        - Atuo adjust data storage
      - S3 Outposts
        - On premises storage
    
  - S3 lifecycle policies
    - transition can enable objects to another storage class based on time/version etc.
    -> S3 Standard
        -> S3 Standard-IA
          -> S3 Intelligent-Tiering
            -> S3 One Zone-IA
              -> S3 Glacier Instant Retrieval
                -> S3 Glacier Flexible Retrieval
                  -> S3 Glacier Deep Archive
      
  - S3 Transfer Acceleration
    - use edge location
        
  - S3 Glacier
    - archive storage
    - 3 classes
      - S3 Glacier Instant Retrieval
      - S3 Glacier Flexible Retrieval
      - S3 Glacier Deep Archive
        
  - Elastic Block Store (EBS)
    - used in EC2
    - provide multiple volume types:
      - General purpose SSD
      - Provisioned IOPS SSD - high performance
      - Throughput optimized HDD
      - Code HDD 
  - Elastic File System (EFS)
    - for Linux-based workloads
    - fully managed NFS file system (network file system)
    - support up to petabyte scale
    - 2 classes:
      - Standard
      - Infrequent access
  - Amazon FSx for Windows File Server
    - SMB support
    - Active Directory integration
    - Windows NTFS 
  - AWS Snowball
    - physically migrate petabyte-scale data to AWS
  - AWS Snowmobile
    - physically migrate exabyte scale data onto AWS

## AWS Databases & Related Services (Purple)
  - Amazon RDS
    - support MySQL, PostgreSQL, MariaDB, Oracle Database, SQL Server, Amazon Aurora 
  - Amazon Aurora
    - is a MySQL and PostgreSQL-compatible relational database 
  - Amazon DynamoDB
    - NoSQL database service;
    - SaaS
    - Good for gaming company
  - Amazon Redshift
    -  data warehouse service
    -  petabyte scale warehousing
  - Amazon Elasticache
    - in-memory
    - supports both Memcached and Redis
    - database layer caching  
  - Additional Database Services
    - DocumentDB -> MongoDB
    - Neptune -> Managed graph database
      - mapping relationships, such social network 
    - MemoryDB -> Redis in-memory DB
    - Timestream -> Serverless time series DB
    - DB migration tools
      - AWS Database Migration Service (DMS)
      - AWS Schema Conversion Tool   

## AWS App Integration Service
  - Amazon SNS (Simple Notification Service)
    - publish/subscrib message service
  - Amazon SQS (Simple Queue Service)
    - message queue service
  - AWS Step Functions
    - Serverless workflow management service
    - workflows
  - Amazon EventBridge
    - Serverless event bus for SaaS apps & AWS services 

## Management and Governance Services
  - AWS CloudTrail
    - audit trail
    - event history logs
    - in an S3
    - meets many compliance requirements
    - can be consolidated with AWS Control Tower
  - AWS CloudFormation
    - infrastructure automation
    - provisioning infrastruture based on templates
    - No additional charge
    - Templates can be YAML or JSON
    - Enable infrastucture as code
    - Provides drift detection to find changes in your infrastructure
  - AWS CloudWatch
    - track infrastuction
    - provides metrics, logs, and alarms for infrastructure
    - Monitoring and management service
  - AWS Config
    -  continually evaluates infrastructure against a set of rules
  - AWS Systems Manager
    - operational insights
    - provides operational data and automation across infrastucture
    - enables automation tasks for common maintenance actions
  - AWS OpsWorks
    - Provides managed instances of Chef and Puppet
    - Confguration is defined as code for servers
    - Chef and Puppet manage the lifecycle of those configuration changes with servers
    - Master-slave architecture
    - AWS OpsWorks for Chef Automate
    - AWS OpsWorks for Puppet Enterprise
    - AWS OpsWorks for Stacks
  - AWS Control Tower
    - Centralizes users across all AWS accounts
    - Provides a way to create new AWS accounts based on templates
    - Integrates Guardrails for accounts
    - Includes a dashboard 
  - AWS Organizations
    - Allows organizations to manage multiple accounts under a single master account

## Security and Architecture
  - AWS Shared Responsibility Model
  -  Pillars of the Well-architected Framework
    - Operational Excellence
    - Security
    - Reliability
    - Performance Efficiency
    - Cost Optimization
    - Sustainability
  - High-availability and Fault Tolerance
  - Compliance
    - AWS Config
      - conformance packs for standards 
    - AWS Artifact
      - self-service access to reports  
    - AWS GuardDuty
      - intelligent threat detection 

## AWS Identities and User Management
   -  AWS IAM (Identity and Access Management)
     - Identities
       - Users
       - Groups
       - Roles
     - Policies
       - JSON document that define permissions
     - Best practices
       - MFA
       - Least Privilege Access
   - Amazon Cognito
     - handle authentication and authorization for your custom web and mobile applications
     - SSO
       
## Data Architecture
  - On-premise Data Integration
    - AWS Storage Gateway
      - Integrates cloud storage into your local network
      - Deployed as a VM or specific hardware appliance
      - Supports 3 different gateway types:
        - Tape Gateway
          - virtual tapes 
        - Volume Gateway
          - cloud base iSCSI volumes to local applications 
        - File Gateway
            - Stores files in S3 with local cached
    - AWS DataSync
        - Integrates with S3, EFS, and FSx for Windows
        - charged per GB per data transform
 
  - Process Data
    - AWS Glue
      - Manage Extract, Transform and Load (ETL) Service
      - Supports RDS, DynamoDB, Redshift, and S3
    - AWS EMR (Elastic Map Reduce) (tool)
      - Big-data cloud processing on EC2 and S3
      - Supported tools
          - Apache Spark
          - Apache Hive
          - Apache HBase
          - Apache Flink
          - Apache Hudi
          - Presto 
    - AWS Data Pipeline (orchestration service)
      -  also for ETL
      -  upports RDS, EMR, DynamoDB, Redshift, and S3
    - Amazon Kinesis
      - Collect, process and analyze real-time video and data stream  
  
    - Data Analysis
      - Amazon Athena
        - enables querying of data stored in S3
        - can use SQL
        - charge by scanned data by query 
      - Amazon Quicksight
        - Business intelligence service
        - data dashboard
      - Amazon CloudSearch
 
    - AI and Machine Learning
      - Amazon Rekognition
        - image, video
        - identifies objects in images
        - facial recognition
      - Amazon Translate
        - text recognition 
      - Amazon Transcribe
        - speech recognition 

## Disaster Recovery
  - Disaster Recovery Architectures
    - Backup and Restore
    - Pilot light
    - Warm standby
    - Multi Site 
  - Select a Disaster Recovery Architecture
    - Recovery Time Objective (RTO)
      - Forcus on time 
    - Recovery Point Objective (RPO)
      - The amount of data loss
      - forcus on data
     
## Architecting Applicationson EC2
  - Scalling EC2
    - Horizontal vs Virtical (horizotal is good; scaling out not big)
  - EC2 Auto-Scaling Group
    - Launch template
    - Defines the minimum, maximum and desired number of instances
    - Performs health checks on each instance
    - Exists within 1 or more availability zones in a single region
    - Work on on-demain 
  - AWS Secrets Manager
    
  - Controlling Access to EC2 Instances
    - Security Groups
      - Serve as a firewall
      - control inbound and outbound traffic
      - Works at the instance level
      - EC2 instances can belong to multiple security groups
      - VPC have default security groups
      - Must be explicitly associated with an EC2 instance
      - By default all outbound traffic is allowed   
    - Network ACL's
      - Works at the subnet level with an VPC
      - Each VPC has a default ACL that allows all inbound and outbound traffic
      - Custom ACL deny all traffic until rules are added 
    - AWS VPN
      - Creates an encrypted tunnel into your VPC
      - Can be used to connect your data center
      - Supported in 2 services
        - Site-to-site VPN 
        - Client VPN
          
  - Protecting from attacks
    - AWS Shield
      - DDoS protection
      - 2 levels
        - standard
        - advance 
    - Amazon Macie
      - Data protection
      - classified the data
      - DLP
    - Amazon Inspector
      - Automated security assessment service
      - 2 types of rules packages
        - Network assessment
        - Host assessment
          
  - Deploying Pre-defined Solution
    - AWS Service Catalog
    - AWS Marketplace
      
  - Developer Tools
    - AWS CodeCommit
      - Git
      - Source control
      - control access with IAM policies
    - AWS AppConfig
    - AWS Cloud9
    - AWS CodeArtifact (Nexus repo) 
    - AWS CodeBuild
      - Build and continuous integration
      - CI 
    - AWS CodeDeploy
      - auto deploy 
    - AWS CodePipeline
      - Continueous Delivery 
    - AWS CodeStar
      - Workflow tool
      - Jenkins
    - AWS X-Ray
      - Analyze your code and debug
    - Amazon AppStream 2.0 (VDI desktop/Apps)
    - Amazon WorkSpaces
    - Amazon WorkSpaces Web
    - AWS Amplify
    - AWS AppSync
    - AWS IoT Core
    - AWS IoT Greengrass   

## AI
  - Amazon SageMaker
    - Build, train machine learning models 
  - Amazon Lex
    - Build voice or text chat bots 
  - Amazon Kendra
    - Enterprise search 
  - Amazon Athena
    - Query data in S3 with SQL 
  - Amazon Kinesis
  - AWS Glue
  - Amazon QuickSight


  









