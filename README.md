- 4 core cold service
  - Compute (oragne icons)
  - Storage (green icons)
  - Database (blue icons)
  - Networking (purple icons)

  - Security (red icons)
  - Elasticity
    - The ability for the infrastructure supporting an application to grow and contract based on how much it is used at a point in time.   

- Global Infrasturction 
  - AWS Regions
    - Each region contains multiple datacenter cluster   
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
 
- Cloud Economics
  - Tag   
  - AWS Organizations
    - manage multiple accounts
    - provide single bill
  - Building the Business Case
    - AWS Pricing Calculate
      - AWS Simple Monthly Calculator (deprecated)
      - can use for one machine pricing calculating instead of migration project
    - Create a TCO - total cost
    - AWS Migration Hub
    - Migration Evalutator

- AWS Support
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

- Compute (orange icons)
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

- Network & Content Delivery Services (blue icons)
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
    











