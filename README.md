## Module 1
Nothing special - talks about client-server model using coffee shop analogy, elasticity (without mentioning the term), and pay as you use.

### What is Cloud Computing?
Cloud computing is the on-demand delivery of IT resources over the Internet with pay-as-you-go pricing. Instead of buying, owning, and maintaining physical data centers and servers, you can access technology services, such as computing power, storage, and databases, on an as-needed basis from a cloud provider like Amazon Web Services (AWS).

- Database installation etc. is not a core differentiator for business
    - repetitive tasks common to many businesses - no point in the business itself maintaining this
    - instead outsource this to cloud and concentrate on your core business development

### Deployment Models for Cloud Computing
While selecting a cloud stratgy, factors a company should consider (non-exhaustive)
    - What cloud application components are needed?
    - Preferred resource management tools
    - Legacy IT infra requirements

### Cloud computing models
- Infrastructure as a Service (IaaS)
- Platform as a Service (PaaS)
- Software as a Service (SaaS)
    - Software as a Service provides you with a completed product that is run and managed by the service provider
    - In most cases, people referring to Software as a Service are referring to end-user applications
    - With a SaaS offering you do not have to think about how the service is maintained or how the underlying infrastructure is managed

### Cloud computing deployment models
- cloud-based
    - Run all parts of the application in the cloud.
    - Migrate existing applications to the cloud.
    - Design and build new applications in the cloud.
- on-premises (aka private cloud)
    - Though this model is much like legacy IT infrastructure, its incorporation of application management and virtualization technologies helps to increase resource utilization.
- hybrid
    - Connect cloud-based resources to on-premises infrastructure
    - Integrate cloud-based resources with legacy IT applications
    - For example, you have legacy applications that are better maintained on premises, or government regulations require your business to keep certain records on premises.

### Benefits of cloud computing
- Trade upfront expense for variable expense
- Stop spending money to run and maintain data centers
- Stop guessing capacity
- Benefit from massive economies of scale
- Increase speed and agility (enables you to access new resources within minutes)
- Go global in minutes
    - Easily deploy your application in multiple regions around the world with just a few clicks

### AWS Customer Stories / Real-life case-studies
https://aws.amazon.com/solutions/case-studies/innovators/

## Module 2: Compute in the Cloud
- Elastic Compute Cloud (EC2)
    - compute power using virtual servers (servers that run on top of physical host machines using virtualization technology)
    - __Multitenancy__
        - __Hypervisor__ running on the host machines helps share physical resources between different virtual machines
        - The hypervisor ensures sandboxing of virtual machines and is managed by AWS
- Advantages
    - no upfront cost
    - no delays
    - you are not tied to the infra once you buy it
    - grow or shrink capacity
    - pay for what you use
    - in EC2 you only for for __running__ instances, not __stopped__ / __terminated__ instances

### Amazon EC2 Instance Types
- EC2 instance types are optimized for different tasks
- Consider the specific needs of your workloads and applications
    - compute
    - memory
    - storage capabilities
    - networking capacity
- Types of EC2 insrances
    - General purpose instances
        - application servers
        - gaming servers
        - backend servers for enterprise applications
        - small and medium databases
    - Compute optimized instances
        - like general purpose instances, you can use compute optimized instances for workloads such as web, application, and gaming servers
        - ideal for high-performance web servers, compute-intensive applications servers, scientific computing, and dedicated gaming servers
        - batch processing workloads that require processing many transactions in a single group
    - Memory optimized instances
        - workloads that process large datasets in memory
    - Accelerated computing instances
        - floating-point number calculations
        - GPU intensive tasks
        - data pattern matching (these also use hardware accelerators)
        - game streaming
        - application streaming
    - Storage optimized instances
        - high performance for locally store data
        - sequential read and write access to large datasets on local storage
        - distributed file systems
        - data warehousing applications
        - high-frequency online transaction processing (OLTP) systems
        - __Input/output Operations Per Second (IOPS)__ is a metric that measures the performance of a storage device
            - Storage optimized instances are designed to deliver tens of thousands of low-latency, random IOPS to applications

### EC2 pricing
__NOTE__: AWS Cost Explorer can analyze your Amazon EC2 usage over the past 7, 30, or 60 days. It provides customized recommendations for Savings Plans.

- _On-Demand_
    - Pay only for the duration you run it for (could be per hour / second depending on instance type)
    - ideal for short-term, irregular workloads
    - No upfront costs or minimum contracts apply
    - cannot be interrupted. Run continuously until you stop them.
    - not recommended for workloads that last a year or longer because these workloads can experience greater cost savings using Reserved Instances.
- _Savings plan_
    - Needs a commitment for 1 / 3 year term - savings upto 72%
    - Any usage up to the commitment is charged at the discounted Savings Plan rate (for example, $10 an hour)
    - Any usage beyond the commitment is charged at regular On-Demand rates
    - It applies to AWS Lambda and AWS Fargate as well
- _Reserved Instances_
    - _Reserved Instances are a __billing discount__ applied to the use of On-Demand Instances_ in your account
    - You can purchase for a 1-year or 3-year term
        - Standard Reserved
        - Convertible Reserved Instances
            - You have the flexibility to change families, operating system types, and tenancies
        - Scheduled Reserved Instances for a 1-year term
    - You realize greater cost savings with the 3-year option
    - At the end of a Reserved Instance term, you can continue using the Amazon EC2 instance without interruption. However, you are charged On-Demand rates until you terminate the instance, or purchase a new Reserved Instance that matches the instance attributes (instance type, Region, tenancy, and platform).
    - It does not apply to AWS Lambda and AWS Fargate (As environment for these cannot be inpected)
- Spot Instances
    - ideal for workloads
        - with flexible start and end times
        - that can withstand interruptions
            - Suppose that you have a _background processing job that can start and stop as needed_
    - use unused Amazon EC2 computing capacity and offer you cost savings at up to 90% off of On-Demand prices
    - If you make a Spot request and Amazon EC2 capacity is available, your Spot Instance launches. However, if you make a Spot request and Amazon EC2 capacity is unavailable, the request is not successful until capacity becomes available.
    - After you have launched a Spot Instance, if capacity is no longer available or demand for Spot Instances increases, your instance may be interrupted (with a __2 minute notice period__)
- Dedicated Hosts
    - physical servers with Amazon EC2 instance capacity that is fully dedicated to your use
    - You can use your existing __per-socket__, __per-core__, or __per-VM__ __software licenses__ to help maintain license compliance
    - You can purchase __On-Demand Dedicated Hosts__ and __Dedicated Hosts Reservations__. 
    - dedicated hosts form the most expensive option in EC2

### Scaling Amazon EC2 (Part 1, Part 2)
- automatically respond to changing demand by scaling out or in
    - both __vertical scaling__ (adding resources to existing instances) and horizontal scaling (increasing number of instances) are supported
    - called Amazon EC2 Auto Scaling
    - you are able to maintain a greater sense of application availability
    - Two approaches
        - __dynamic scaling__ responds to changing demand
        - __predictive scaling__ automatically schedules the right number of EC2 instances based on predicted demand
        - Dynamic scaling and predictive scaling can be used together to scale faster
- you pay for only the resources you use
- When you create an Auto Scaling Group (ASG)
    - set the __minimum capacity__, say, 1 EC2 instance
    - set the __desired capacity__, say, 2 EC2 instances
        - __Note__: If you do not specify the desired number of EC2 instances in an ASG, the desired capacity defaults to your minimum capacity
    - set the __maximum capacity__, say 4 EC2 instances.

### Directing Traffic with Elastic Load Balancing (ELB)
Elastic Load Balancing (ELB)
    - AWS service that automatically distributes incoming application traffic across multiple resources, such as EC2 instances
    - acts as a single point of contact for all incoming web traffic to your ASG
    - as you add or remove EC2 instances in response to the amount of incoming traffic, these requests route to the load balancer first
    - Although ELB and Auto Scaling are separate services, they work together to help ensure that applications running in EC2 can provide
        - high performance
        - high availability
    - ELB acts as a reverse proxy tp connect multiple frontend instances with multiple backend instances
        - without ELB you will end up with a bi-partite graph of frontend + backend instances, and auto-scaling requrieemtn would make it difficult to maintain this network
        - with ELB, all traffic from frontend to backend is routed via the ELB

### Messaging and Queueing
- Queues help achieve loosely coupled applications
    - When one application (say receiever) goes down, the other (say sender) still does not fail
        - it can continue to send messages, and they exist in the queue, till receiver application is up and running again and reads the messages
- Amazon SQS
    - Send messages
    - Store messages
    - Receive messages
    - ...At any volume!
    - reliable and scalable
- Amazon SNS
    - similar to SQS
        - can send messages to services
    - but it can also send notifications to end users!
        - mobile push, SMS, email supported
    - uses a pub-sub model
    - create SNS topics
        - a channel for messages to be delivered
        - subscribers subscribe to the topics and recieve messages published on that topic
            - basically the message published is __broadcast__ to all subscribers
    - subscribers can also be SQS queues, Lambda functions, web hooks!

### Monolithic Applications and Microservices
- Monolothic application
    - Application with tightly coupled components
        - databases
        - servers
        - user interface
        - business logic, and so on
    - if a single component fails, other components fail, and possibly the entire application fails
- Microservices
    - application components are loosely coupled
    - helps maintain application availability when a single component fails, because the functioning components are still communicating with each other
- Two services facilitate application integration (via microservices approach)
    - SQS
    - SNS

### Additional Computer Services
- With EC2 you need to take care of
    - patching instances' software
    - manage scaling instances
    - architect for high availability
- __AWS Lambda__ - (__serverless__)
    - zero administration - all the above are taken care
    - you do not need to provision or manage these servers
    - you cannot examine the underlying instances
    - for event-driven apps
    - you configure a __trigger__. When the trigger triggers, it runs a __lambda function__ in an AWS managed environment.
        - You upload your code to Lambda. 
        - You set your code to trigger from an event source. A event source can be for example,
            - an AWS service
            - a mobile applications
            - an HTTP endpoint
        - a simple Lambda function might involve automatically resizing uploaded images to the AWS Cloud. In this case, the function triggers when uploading a new image. 
    - Even with multiple simulatenous triggers (say thousands), AWS Lambda will scale automatically
        - can adjust the application's capacity by modifying the units of consumptions, such as throughput and memory
    - It is designed to run code in under 15 minutes
        - good for web backends, report generation etc.
        - not good for deep learning (long running tasks)
    - pay only for the compute time that you consume
- __AWS Serverless Application Repository (SAR)__
    - quickly deploy code samples, components, and complete applications for common use cases such as web and mobile backends, event and data processing, logging, monitoring, Internet of Things (IoT), and more
    - Each application is packaged with an __AWS Serverless Application Model (SAM)__ template that defines the AWS resources used
    - Use SAM to publish your own applications to SAR and share them within your team, across your organization, or with the community at large
- __Elastic Container Service (ECS)__, __Elastic Kubernetes Sevice (EKS)__ - Container Services 
    - Container orchestration tools
        - Helps manage a cluster of containers
        - you have to manage possibly hundreds of hosts with thousands of containers. -
        - monitor memory usage, security, logging, and so on.
    - Container = __Docker__ container
        - supports open-source Docker Community Edition
        - supports subscription-based Docker Enterprise Edition
    - you get access to underlying environment installed on EC2 instances
    - additionally you still get efficiency, portability
    - two modes - Fargate launch type and EC2 launch type
- __Amazon EC2 Image Builder__
    - reduces the effort of keeping images up-to-date and secure by providing a simple graphical interface, built-in automation, and AWS-provided security settings
    - no manual steps for updating an image nor do you have to build your own automation pipeline
- __AWS Fargate__
    - Use this if you want to host containerized apps using ECS/EKS but without access to the underlying environment (serverless)
    - you don't have to provision, configure, and scale clusters of VMs to run containers
- __Amazon Lightsail__
    - easiest way to launch and manage a virtual private server
    - plans include everything you need to jumpstart your project
        – Virtual Machine
        - SSD-based storage
        - data transfer
        - DNS management
        - static IP address – for a low, predictable price
- __AWS App Runner__
    - fully managed service that makes it easy for developers to quickly deploy containerized web applications and APIs, at scale
    - builds and deploys the web application and load balances traffic with encryption
    - scales up or down automatically
    - rather than thinking about servers or scaling, focus on your application
- __AWS Batch__
    - run hundreds of thousands of batch computing jobs
    - dynamically provisions the optimal quantity and type of compute resources based on the volume and specific resource requirements of the batch jobs submitted
    - plans, schedules, and runs your batch computing workloads across Amazon EC2 and Spot Instances
- __AWS Elastic Beanstalk__
    - easy-to-use service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and Internet Information Services (IIS).
    - You can simply upload your code, and AWS Elastic Beanstalk automatically handles
        - deployment, from capacity provisioning
        - load balancing, and auto scaling
        - application health monitoring
    - you retain full control over the AWS resources and can access the underlying resources
- __AWS Outposts__
    - bring native AWS services, infrastructure, and operating models to virtually any data center, co-location space, or on-premises facility
    - Two variants
        - VMware Cloud allows you to use the same VMware control plane and APIs you use to run your infrastructure
        - AWS-native variant allows you to use the same exact APIs and control plane you use to run in the AWS Cloud, but on-premises
- __AWS Wavelength__
    - infrastructure offering optimized for mobile edge computing applications
    - embed AWS compute and storage services within communications service providers' (CSP) datacenters at the edge of the 5G network, so application traffic from 5G devices can reach application servers running in Wavelength Zones without leaving the telecommunications network. This avoids the latency that would result from application traffic having to traverse multiple hops across the Internet to reach their destination, enabling customers to take full advantage of the latency and bandwidth benefits offered by modern 5G networks.
- __VMware Cloud on AWS__ 
    - an integrated cloud offering jointly developed by AWS and VMware delivering a highly scalable, secure and innovative service that allows organizations to seamlessly migrate and extend their on-premises VMware vSphere-based environments to the AWS Cloud running on next-generation Amazon Elastic Compute Cloud (Amazon EC2) bare metal infrastructure.
    - ideal for enterprise IT infrastructure and operations organizations looking to migrate their on-premises vSphere-based workloads to the public cloud
    - brings the broad, diverse and rich innovations of AWS services natively to the enterprise applications running on VMware's compute, storage and network virtualization platforms
        - integrate AWS infrastructure and platform capabilities such as AWS Lambda, Amazon Simple Queue Service (Amazon SQS), Amazon S3, Elastic Load Balancing, Amazon RDS, Amazon DynamoDB, Amazon Kinesis, and Amazon Redshift, among many others

## Module 3: Global Infrastructure and Reliability
- AWS has many data centers at different locations
- Advantages
    - High availability
    - Fault tolerance
    - Low latency (upto single-digit millisecond latency with __AWS Local Zones__ and __AWS Wavelength__)
- 32 Launched Regions each with multiple Availability Zones (AZs)
- 102 Availability Zones
- 600+ Points of Presence
- 13 Regional Edge Caches
- 36 Local Zones
    - Each AWS Local Zone location is an extension of an AWS Region where you can run your latency sensitive applications using AWS services such as Amazon Elastic Compute Cloud, Amazon Virtual Private Cloud, Amazon Elastic Block Store, Amazon File Storage, and Amazon Elastic Load Balancing in geographic proximity to end-users
- 29 Wavelength Zones (for ultralow latency applications)
- 245 Countries and Territories Served
- 115 Direct Connect Locations
    - https://aws.amazon.com/about-aws/global-infrastructure/
    - https://aws.amazon.com/about-aws/global-infrastructure/regions_az/
    - https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/

### Regions
- What to consider when determining the right Region for your services, data, and applications
    - Compliance with data governance and legal requirements
    - Proximity to your customers
    - Available services within a Region
        - AWS is frequently innovating by creating new services and expanding on features within existing services. However, making new services available around the world sometimes requires AWS to build out physical hardware one Region at a time. 
    - Pricing
        - the cost of services can vary from Region to Region
- __NOTE__:
    - Regions can be connected from region-to-region through a high-speed fiber network controlled by AWS.
    - Regional data sovereignty - Data stored in one region is not transferred to another region, unless the business owner explicitly transfer / allows transfer. Data is subject to the law of the land.

### Availability zone (AZ)
- A region is not a single data center. It is a collection of data centers tens of miles apart within a region called __Availability Zone (AZ)__
- The data centers in an AZ are far apart so that they don't fail together in the event of a natural calamity.
    - redundant power, networking, and connectivity in an AWS Region
    - AZs are fully isolated partitions of AWS infrastructure
    - to isolate any issues and achieve high availability, you can partition applications across multiple AZs in the same region
    - recommended that we run (for example) __EC2 instances across at least 2 AZs in a region__
        - For example, you can run in us-west-1a, us-west-1b AZs of Northern California region
- __Regionally scoped services__
    - Many AWS services run across AZs in a region without end user action / involvement. Eg. ELB, SQS, SNS

### Edge Locations
- An edge location is a site that __Amazon CloudFront__ uses to store cached copies of your content closer to your customers for faster delivery
- Suppose that your company’s data is stored in Brazil, and you have customers who live in China. To provide content to these customers, you don’t need to move all the content to one of the Chinese Regions. Instead of requiring your customers to get their data from Brazil, you can cache a copy locally at an edge location that is close to your customers in China.
- Some services that run on edge locations
    - Cloudfront (CDN)
    - Route 53 (DNS service)
- __AWS Outposts__
    - Helps run AWS services right on-premise in the organization! - edge devices
    - Owned and operated by AWS

### How to Provision AWS Resources
- Every AWS sercice is provisioned using an API. The ways to invoke these APIs
    - AWS Management Console
    - AWS CLI
    - AWS SDK kits for application programming
    - through other AWS services like AWS CloudFormation / AWS Elastic Beanstalk
        - AWS CloudFormation
            - __infrastructure as code__ tool
            - use JSON / YAML to define AWS resources (CloudFormation templates)
                - declarative - what you want to build, not how to (no need to know which underlying APIs are used)
        - AWS Elastic Beanstalk
            - supply app code + configuration
            - takes care of provisioning various AWS services
            - you can save the environment configurations and again spin up same environment again
            - you still get visibility and control of the underlying resources
- AWS Management Console
    - web-based interface
    - access recently used services and search for other services by name, keyword, or acronym
    - includes wizards and automated workflows that can simplify the process of completing tasks
    - also use the AWS Console mobile application to perform tasks such as
        - monitoring resources
        - viewing alarms
        - accessing billing information
    - Multiple identities can stay logged into the AWS Console mobile app at the same time
- AWS CLI
    - available for users on Windows, macOS, and Linux
    - automate the actions that your services and applications perform through scripts
    - also speeds up tasks
    - greatly reduces chances of human errors when using the AWS Management Console instead
- AWS SDKs
    - APIs designed for your programming language or platform
    - enable you to use AWS services with your existing applications or create entirely new applications that will run on AWS
    - provides documentation and sample code for each supported programming language
    - supports C++, Java, .NET, and more
    - https://aws.amazon.com/developer/tools/

## Module 4: Networking

### Connectivity to AWS
- __Virtual Private Cloud (VPC)__
    - Logically isolated section of the AWS Cloud
        - A VPC can span across multiple AZs of a region, but restricted to a single region
        - resembles a traditional network that you'd operate in your own data center
        - Resources in the network can be
            - public: public-facing
                - eg. load balancer for the frontend application server
            - private: no internet access
                - eg. database server for the application
    - https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html
    - __subnet__
        - a public or private grouping of resources in a VPC
        - group resources into subnets based on security or operational needs
        - a subnet has a range of IP addresses from the VPC for its resources
    - you can control what network traffic gets into a VPC
        - a public website has resources that are accessible by anyone
        - an enterprise app has only resources that are accessible by an employee logged into the private network
    - you can define how VPCs communicate with each other across accounts, Availability Zones, or AWS Regions
    - __Internet Gateway__
        - if a VPC has publicly accessible resources, it needs an internet gateway attached
    - __(Virtual) Private Gateway__
        - if a VPC has _only_ private resources, it needs an private gateway attached
            - allows only people coming in from an _approved network_ (approved network may for example be an on-premise data center, internal corporate network etc.)
            - allows to create a __VPN connection__ (_enabling encrypted communication_) between the approved network and the VPC
            - The VPN is encrypted and secure but is still over the internet, making it susceptible to internet slowdown (network bottlenecks, traffic etc.)
            - Alternative to VPN is __AWS Direct Connect__
                - dedicated physical connection between approved network and a VPC
                - low latency
                - highest security
                - meets high regulatory and compliance needs
    - A VPC may have multiple types of gateways attached for different types of resources (different subnets)
    - __Transit Gateway__
        - helps you design and implement networks at scale by acting as a __cloud router__
        - connects 1000s of VPCs and on-premises networks through a central hub
- __PrivateLink__
    - provides private connectivity between VPCs, supported AWS services, and on-premises networks without exposing traffic to the public internet
    - Interface VPC endpoints, powered by PrivateLink, connect you to services hosted by AWS Partners and supported solutions available in AWS Marketplace
    - Think of it like AWS Direct Connect but for connecting different VPCs, VPCs to AWS Marketplace applications / AWS services (not sure?!)
    - eliminates need for internet gateway, NAT (Network Address Translator), or a public IP address for a VPC
    - simplify network management and security of VPCs without use of firewall rules, proxy devices, or route tables
    - reduce vulnerabilities to security threats like man-in-the-middle attacks, brute-force etc.
    - also works with AWS Direct Connect
    - https://aws.amazon.com/privatelink/
- __VPC Lattice__
    - Simplify service-to-service connectivity, security, and monitoring
        - Connect thousands of services across VPCs and accounts without increasing network complexity (simplify service connectivity at scale)
        - Improve service-to-service security and support Zero Trust architectures with centralized access controls, authentication, and context-specific authorization
        - Apply granular traffic controls, such as request-level routing and weighted targets, for blue/green and canary deployments
        - Monitor and troubleshoot service-to-service communication for request type, traffic volume, errors, response time, and more.
- __App Mesh__
    - provides application-level networking so your services can communicate across multiple types of compute infrastructure
- __API Gateway__
    - a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale
    - API types
        - RESTful APIs
        - Web socket APIs
- __Cloud Map__
    - a cloud resource discovery service
    - you can define custom names for your application resources, and it maintains the updated location of these dynamically changing resources
        - register any application resources, such as databases, queues, microservices, and other cloud resources
    - increases your application availability because your web service always discovers the most up-to-date locations of its resources
    - checks the health of every IP-based component of your application to make sure the location is up-to-date
    - development teams don't have to constantly store, track, and update resource name and location information or make changes directly within the application code

### Subnets and Network Access Control Lists
- Gateway covers only a part of network security
- AWS tools that cover a range of security concerns
    - network hardening
    - application security
    - user identity
    - authentication and authorization
    - DDoS prevention
    - data integrity
    - encryption
- __Network Access Control List (ACL)__
    - provides __security at the subnet level__
    - controls which __data packet__ enters/leaves the subnet boundary
    - each AWS account includes a default network ACL
        - default network ACL allows all inbound and outbound traffic
    - when configuring your VPC, you can use your account's default network ACL or create custom network ACLs
        - for custom network ACLs, all inbound and outbound traffic is denied until you add rules to specify which traffic to allow
    - _stateless_
- __Security Group (SG)__
    - provides security at the __instance-level (EC2)__
    - controls which __request__ enters/leaves an EC2 instance
    - multiple Amazon EC2 instances within a subnet can use the same SG or use different SGs
    - the default SG for an EC2 instance
        - blocks all inbound traffic
        - allows all outbound traffic
    - you can allow traffic based on network protocol, IP address etc.
    - _stateful_
        - recognizes a response that returns to an instance after its corresponding request went out
        - if the request went out, then response is automatically accepted without further checks
            - this is regardless of inbound SG rules

### Global Networking
- __DNS server__
    - when user types website address in the browser, the browser communicates with a DNS server
    - DNS - phone book of the internet
    - __DNS resolution__ is the process of translating a domain name to an IP address
- __Route 53__
    - AWS' __Domain Name System (DNS)__ Service
        - reliable way to route end users to internet applications hosted in AWS
        - connects user to EC2 instances and load balancers
        - it can also route users to infrastructure outside of AWS
        - has the ability to manage the DNS records for domain names - you can register new domain names directly in Route 53
        - transfer DNS records for existing domain names managed by other domain registrars to Route 53 - enables you to manage all of your domain names within a single location
        - it can use several routing policies to redirect to different endpoints
            - Latency-based routing
            - Geolocation DNS
                - routing based on end user's location
            - Geoproximity routing
            - Weighted Round Robin
- How Amazon Route 53 and Amazon CloudFront deliver content
    - say, AnyCompany.com application is running on several Amazon EC2 instances. These instances are in an Auto Scaling group that attaches to an Application Load Balancer.
    - A customer requests data from the application by going to AnyCompany’s website
    - Amazon Route 53 uses DNS resolution to identify AnyCompany.com's corresponding IP address, 192.0.2.0. This information is sent back to the customer.
    - The customer's __request is sent to the nearest edge location through Amazon CloudFront__
    - __Amazon CloudFront connects to the Application Load Balancer, which sends the incoming packet to an Amazon EC2 instance__.

## Module 5: Storage and Databases

### Instance Stores and Amazon Elastic Block Store (Amazon EBS)
- EC2 gives access to storage
- Block-level storage
    - a place to store files
        - eg. hard drives
    - files are stored on blocks on the disk
        - whena file is updated, only the blocks of the file that changed are updated on the disk
    - __Instance Store Volume__
        - When you launch an EC2 instance, it comes with it
        - this is a part of the block storage (disk) attached to the host machine of the EC2 instance
        - The host machine of an EC2 instance (VM) can change when the EC2 instances is stopped and started!
            - Also all data on the attached instance store is deleted when the EC2 instance is stopped
        - The underlying instance store therefore cannot be maintained across restarts and is ephemeral
        - This is good only for temporary data (scratch data)
    - __Elastic Block Store (EBS)__
        - Virtual hard drives called __EBS Volumes__
        - Not tied to the EC2 instance's host
        - Different sizes and types
        - Persistent
        - __EBS snapshots__
                - for reliability - use the snapshot to restore data if it gets lost / corrupted etc.
                - is an incremental backup - the first backup taken of a volume copies all the data. For subsequent backups, only the blocks of data that have changed since the most recent snapshot are saved.

### Amazon Simple Storage Service (Amazon S3)
- __Object Storage__
    - service that provides object-level storage
    - each object consists of data, metadata, and a __key__
        - data might be an image, video, text document, or any other type of file
        - metadata contains information about what the data is, how it is used, the object size, and so on
        - key is the object's unique identifier
    - when you modify a file in block storage, only the pieces that are changed are updated. When a file in object storage is modified, the __entire object is updated__.
    __Features__
        - offers unlimited storage space
        - maximum file size for an object is 5 TB
        - set permissions to control visibility and access to an object
        - track changes to your objects over time using versioning
            - prevents accidental deletion (as you can now retrieve previous versions)
        - __Storage Classes__
            - you can stage data in different tiers
                - Based on
                    - how often you plan to retrieve your data
                        - data that needs to be accessed frequently vs data that is rarely accessed
                    - how available you need your data to be
                        - data that is to be retained for many years etc.
- __Bucket__
    - equivalent of a folder in a filesystem
        - but there is no underlying folder actually - S3 has a flat structure for buckets, objects
    - buckets cannot have buckets within
    - buckets can have folders within but the underlying stucture is actually flat - folder is only a virtual grouping in S3
    - __key prefix__
        - a string of characters that can be the complete path in front of the object name
        - if an object (123.txt) is stored as BucketName/Project/WordFiles/123.txt, then the prefix might be BucketName/Project/WordFiles/123.txt
    - implement access control at the bucket level
    - __it is the highest level for AWS namespaces__
        - makes it possible to uniquely identify objects in buckets, as the bucket name is used to create the URL (being a globally unique AWS namespace)
    - You can use an S3 bucket to host a static website
- __S3 Storage Classes__
    - __S3 Standard__
        - designed for frequently accessed data
        - stores data in a minimum of three AZs
        - provides high availability for objects. This makes it a good choice for a wide range of use cases, such as websites, content distribution, and data analytics. S3 Standard has a higher cost than other storage classes intended for infrequently accessed data and archival storage.
    - __S3 Standard-Infrequent Access (S3 Standard-IA)__
        - ideal for infrequently accessed data that needs to be highly available when needed
        - stores data in a minimum of three AZs
        - Similar to S3 Standard but has a lower storage price and higher retrieval price
    - __S3 One Zone-Infrequent Access (S3 One Zone-IA)__
        - stores data in a single AZ
        - has a lower storage price than S3 Standard-IA
        - use it if you can withstand the event of an AZ failure
    - __S3 Intelligent-Tiering__
        - __S3 Lifecycle Management__
        - Create __Lifecycle Policies__ to move data automatically between tiers
        - ideal for data with unknown or changing access patterns
        - Requires a small monthly fee per object to automatically monitor object access patterns
            - if you have not accessed an object for 30 consecutive days, it automatically moves it to the infrequent access tier, S3 Standard-IA
            - if you access an object in the infrequent access tier, Amazon S3 automatically moves it to the frequent access tier, S3 Standard
        - Also create fixed policies - keep objects in Standard for 30 days, then move to Standard 1A for 90 days, then Glacier Flexible retrieval etc.
    - __S3 Glacier__
        - low-cost storage designed for data archiving
        - able to retrieve objects within a few minutes to hours
        - you can store data in __vaults__
            - you can have a __vault lock policy__ for data that needs to be locked and stored for a certain number of years for compliance purposes
            - you can specify Write Once Read Many (WORM) ina vault lock policy - once locked such a policy can no longer be changed
    - __S3 Glacier Deep Archive__
        - lowest-cost object storage class ideal for archiving
        - able to retrieve objects within 12 hours

### Comparing Amazon EBS and Amazon S3
| __EBS__                                 | __S3__                              |
| :---:                                   | :---:                               |
| Block storage                           | Object storage                      |
| Sizes upto 16 TB                        | Unlimited with object upto 5 TB     |
| Survive termination of EC2 instance     | Not tied to EC2 instances           |
| Solid state with HDD options            | ?                                   |
| ?                                       | Specialize in Write Once Read Many  |
| Durable                                 | Highly durable - 99.99999999999%    |

- Use Cases
    - You have millions of photos that need to be indexed and viewed by thousands of users concurrently
        - S3
            - Is web-enabled - every object has a URL
            - Regionally distributed (3 AZs)
            - Very low cost
            - Works without a server! (think serverless as well)
    - 80GB video that is being processed - edited and stored, edited and stored...
        - EBS
            - Block storage - works with only poritions of the file - much faster
                - in S3 OTOH, the entire 80GB needs to be re-uploaded on every edit!
            - Low latency
    
### Amazon Elastic File System (Amazon EFS)
- __File Storage__
    - multiple clients (such as users, applications, servers, and so on) can access data that is stored in shared file folders
    - a storage server uses _block storage_ with a local file system to organize files
    - compared to block storage and object storage, file storage is ideal for use cases in which a large number of services and resources need to access the same data at the same time
- __Amazon Elastic File System (Amazon EFS)__
    - scalable file system used with _AWS Cloud services_ and _on-premises_ resources
        - as you add and remove files, Amazon EFS grows and shrinks automatically (to petabytes without disrupting applications!)
    - a Linux filesystem
    - great as a shared filesystem between applications
- EBS vs EFS
    - EBS
        - EBS is an AZ-level resource
        - to attach an Amazon EC2 instance to an EBS volume, both must reside within the same AZ
        - does not automatically scale
    - EFS
        - is a regional-level service
        - stores data in and across multiple AZs
        - enables concurrent access from all AZs in the Region where a file system is located
        - scales automatically
        - multiple EC2 instances can read/write simultaneously from/to it
- __Amazon File Cache__
    - High-speed cache for datasets stored anywhere, accelerate cloud bursting workloads

### Amazon Relational Database Service (Amazon RDS)
- __Amazon Relational Database Service__
    - enables you to run relational databases in the AWS Cloud
    - a managed service that automates
        - hardware provisioning
        - database setup
        - patching
        - backups
        - disaster recovery
    - integrate RDS with other services including AWS Lambda (to query your database from a serverless application)
    - different security options
        - encryption at rest (protecting data while it is stored)
        - encryption in transit (protecting data while it is being sent and received)
    - database engines
        - 6 database engines, which optimize for memory, performance, or input/output (I/O)
            - Amazon Aurora
            - PostgreSQL
            - MySQL
            - MariaDB
            - Oracle Database
            - Microsoft SQL Server
        - Amazon Aurora
            - enterprise-class relational database (basically custom MySQL and custom PostgreSQL)
            - compatible with MySQL and PostgreSQL databases
            - up to 5 times faster than standard MySQL databases and up to 3 times faster than standard PostgreSQL databases
            - 10% cost of standard DBs
            - helps to reduce your database costs by reducing unnecessary I/O operations, while ensuring that your database resources remain reliable and available
            - consider Amazon Aurora for highly available workloads
                - replicates 6 copies of your data across three AZs and continuously backs up your data to S3
                - supports up to 15 read replicase - thus enabling faster concurrent access
                - supports point-in-time recovery (recover data from a specific period)
- __Lift and shift migration__
    - A way to migrate your on-premises DB to EC2 (NOT RDS)
    - but this is unmanaged
    - You have control over the same variables as your on-premises DB - like similar OS, storage capacity etc.

### Amazon DynamoDB
- Non-relational DB
    - not every item in the table has to have the same attributes
- DynamoDB
    - a key-value database service
    - high throughput
    - petabytes size potential
    - serverless DB
        - means we do not need to provision / install / patch / manage the underlying instance
    - highly, and automatically, scalable
    - highly available
        - stores data redundantly across multiple AZs, and across multiple drives
    - low latency
    - in No SQL DBs, the queries generally are on one collection (table), not multiple ones (not joins)
        - In Dynamo DB queries are on certain keys (only?)

### Comparing Amazon RDS and Amazon DynamoDB
- Use Cases
    - Sales SCM, that is to be used to analyze for weak spots (sales SCM bottlenecks)
        - RDS
            - We need to make many (complex) joins for such complex reporting
            - RDBMS is built for business analytics
    - You just need to lookup attributes of an entity
        - no need for joins / complex joins in this case
        - Dynamo DB has high throughput
        - RDS will be slow in this case

### Amazon Redshift
- Data analytics with historical data is not easy with RDBMS, expecially when there are many data sources to collect data from
    - eg. how has production improved since the beginning of the company?
    - you decide till which period you consider the data - __data warehouse__ is best suited
    - when considering queries on up-to-date data - regular RDBMS is best
- __Amazon Redshift__
    - data warehousing service for __big data analytics__
    - ability to collect data from many sources and helps you to understand relationships and trends across your data
    - improve integration with __data lakes__ - build data lakes and perform real-time processing on change data from your data stores
    - handles common data warehouse tasks to keep it tuned, resilient and scalable
    - highly performant, highly scalable, and handles massive amounts of data

### AWS Database Migration Service (AWS DMS)
- helps migrate SQL, NoSQL DBs, and other types of data stores
- move data from source database to target database
    - source and target DBs can be of the same type or different types
        - if they are similar DBs, we called it a homogeneous database migration
            - For example from a MySQL DB stored on premises in an EC2 / RDS to an Amazon Aurora DB in RDS
            - schema structures, data types, database code is compatible
        - if they are dissimilar, we call it a heterogeneous database migration
            - has additional preparatory step of using AWS schema conversion tool to convert source DB schema, data types, code etc. to be compatible with that of the target.
    - during migration, the source DB remains operational
- Other use cases
    - Development and test DB migrations
        - enabling developers to test applications against production data without affecting production users (this can be done one-off or on a continuous basis!)
    - DB consolidation
        - combining several databases into a single database
    - Continuous replication
        - Sending ongoing copies of your data to other target sources instead of doing a one-time migration

### Additional Database Services and Database Accelerators
- __Amazon DocumentDB__
    - a document database service that supports MongoDB workloads
- __Amazon Neptune__
    - a graph database service
    - to run applications with highly connected datasets
        - recommendation engines, fraud detection, and knowledge graphs
- __Amazon Quantum Ledger Database (Amazon QLDB)__
    - ledger database service
    - to review a complete history of all the changes made to application data
    - like Blockchain but __NOT decentralized__
- __Amazon Managed Blockchain__
    - a service that you can use to create and manage blockchain networks with open-source frameworks
    - Blockchain is a distributed ledger system that lets multiple parties run transactions and share data without a central authority
- __Amazon ElastiCache__
    - a service that adds caching layers on top of your databases to help improve the read times of common requests
    - supports 2 types of data stores: __Redis__ and __Memcached__
- __Amazon DynamoDB Accelerator (DAX)__
    - an in-memory cache for DynamoDB
    - helps improve response times from single-digit milliseconds to microseconds

### Choosing the Right Database
| Database type     | Examples                                                                                                        | AWS Service                                   |
| :---:             | :---:                                                                         | :---:                           |
| Relational        | Traditional applications, enterprise resource planning (ERP), customer relationship management (CRM), ecommerce | Amazon Aurora  Amazon RDS  Amazon Redshift    |
| Key-value         | High-traffic web applications, ecommerce systems, gaming applications                                           | Amazon DynamoDB                               |
| In-memory         | Caching, session management, gaming leaderboards, geospatial applications                                       | Amazon ElastiCache  Amazon MemoryDB for Redis |
| Document          | Content management, catalogs, user profiles                                                                     | Amazon DocumentDB (with MongoDB compatibility)|
| Wide column       | High-scale industrial apps for equipment maintenance, fleet management, and route optimization                  | Amazon Keyspaces                              |
| Graph             | Fraud detection, social networking, recommendation engines                                                      | Amazon Neptune                                |
| Time series       | Internet of Things (IoT) applications, DevOps, industrial telemetry                                             | Amazon Timestream                             |
| Ledger            | Systems of record, supply chain, registrations, banking transactions                                            | Amazon Ledger Database Services (QLDB)        |

- https://aws.amazon.com/getting-started/decision-guides/databases-on-aws-how-to-choose/
- https://aws.amazon.com/products/databases/learn/#Getting_started_tutorials

## Module 6: Security
- Shared (security) Responsibility Model
    - AWS controls security __of the cloud__
        - Security of services - Compute, Storage, DB, Networking etc.
        - Security of AWS global infrastructure - Regions, AZs, Edge Locations etc.
    - Customers control security __in the cloud__
        - Security of platform, applications, IAM
        - OS, network, firewall configuration
        - Client-side data encryption, server-side data encryption, Network traffic protection


### Shared Responsibility Model
- AWS' responsibility
    - Physical layer - security of infrastructure - data centers etc.
    - Network layer,  Hypervisor
        - host operating system
        - AWS has re-invented network layer, hypervisor to make them faster, strong, tamper-proof
        - this is audited and compliance verified with a variety of computer security standards and regulations (by authorized third-parties)
    - AWS provides the right documentation for user security compliance
- Customer responsibility
    - OS - only the customer has access to keys to login to the EC2 instance (a root user account)
        - AWS cannot login to your EC2 instance!
        - customer selects, configures, and patches the operating systems that will run on Amazon EC2 instances, configuring security groups, and managing user accounts
        - AWS can only warn you if you don't update your EC2 OS with a new version for example
    - Application
    - Data
        - customer decides whether its only for self consumption (account-level), to authorized accounts only, to everyone (public) etc.
        - customer also (obviously) controls how access rights are granted, managed, and revoked

### User Permission and Access
- Root user
    - unrestricted access to any resource in the account
    - recommended to configure this account with MFA
    - even then it is recommended not to use root user account as a blunder by the root user can be disastrous (eg. terminating an important application)
    - __BEST PRACTICE__: create another IAM user and give it privileges to create more users. Use this to create more users with only those privileges they need for their tasks
    - Use the root user only for the limited number of tasks available only to the root user
        - changing your root user email address
        - changing your AWS support plan etc.
        - https://docs.aws.amazon.com/IAM/latest/UserGuide/root-user-tasks.html
- Identity and Access Management (IAM)
    - IAM Users
        - privileged user (root user is one) can create user accounts
        - by default IAM user has no permissions - they cannot even login to their AWS account! Forget spinning up an EC2 instances, creating an S3 bucket etc.
        - privileged user explicitly grants permissions to other users
            - __BEST PRACTICE__: Principle of Least Privilege used
                - give users access to only what they need (nothing more!)
            - this is done by associating an IAM policy to an IAM user
                - a JSON document that describes what API calls a user can and cannot make
                - Eg. __Allow__ user abc to __list bucket__ with URN __arn:aws:s3:::coffee_shop_reports__
                    ```
                    "Statement": {
                        "Effect": "Allow",
                        "Action": "s3:ListBucket",
                        "Resource": "arn:aws:s3:::coffee_shop_reports"
                    }
                    ```
                - The only possible _Effect_ (outcome) are "Allow" / "Deny"
                - The _Action_ is usually an API but here are permission-only actionsthat don't correspond to APIs
        - __BEST PRACTICE__: create individual IAM users for each person who needs to access AWS
    - IAM Groups
        - A category (group) of IAM users
        - makes it easy to create users with similar privileges
        - you can __attach a policy to a group instead of individually to users__
    - IAM Roles
        - same IAM user may take up different roles (for temporary periods of time)
        - privileges vary from role-to-role (for the same user)
        - an IAM role is similar to an IAM user, but without a username and password
        - a user can assume a role for a temporary period of time to gain access to temporary permissions - great for security of the system overall, as it grants permissions only when needed, for the period needed
        - a role can be granted temporarily to
            - IAM users
            - AWS resources
            - external identities
            - applications
            - AWS services
        - __the permissions for the role overrides the permissions for the user / AWS resource etc.__
        - __roles can be used to avoid creating unnecessary IAM accounts__ (since external identities can be assigned roles, a corporate user account can be added to a role when needed, for the period needed!)
        - __BEST PRACTICE__: are ideal for situations in which access to services or resources needs to be granted temporarily, instead of long-term

### AWS Organizations
- suppose that your company has multiple AWS accounts
- This is a service used to consolidate and manage multiple AWS accounts within a central location
- Helps group tons of AWS accounts according to business functions (HR, Legal, FInance, Engineering etc.) and manage accounts without much pain
- When you __create an organization__
    - automatically creates a __root__
        - the parent container for all the accounts in the organization
- __Service Control Policies (SCPs)__
    - centrally control permissions for the accounts in your organization using it
    - enable you to place restrictions on the AWS services, resources, and individual API actions that __users and roles in each account__ can access
- Consolidated billing is another feature
- __Organizational Units__
    - group accounts into _Organizational Units (OUs)__ to make it easier to manage accounts with similar business or security requirements
    - When you apply a policy to an OU, all the accounts in the OU automatically inherit the permissions specified in the policy
    - By organizing separate accounts into OUs, you can more easily isolate workloads or applications that have specific security requirements. For instance, if your company has accounts that can access only the AWS services that meet certain regulatory requirements, you can put these accounts into one OU. Then, you can attach a policy to the OU that blocks access to all other AWS services that do not meet the regulatory requirements.
- __Example__
    - Imagine that your company has separate AWS accounts for the finance, information technology (IT), human resources (HR), and legal departments. You decide to consolidate these accounts into a single organization so that you can administer them from a central location. When you create the organization, this establishes the root.
    - In designing your organization, you consider the business, security, and regulatory needs of each department. You use this information to decide which departments group together in OUs.
    - The finance and IT departments have requirements that do not overlap with those of any other department. You bring these accounts into your organization to take advantage of benefits such as consolidated billing, but you do not place them into any OUs.
    - The HR and legal departments need to access the same AWS services and resources, so you place them into an OU together. Placing them into an OU enables you to attach policies that apply to both the HR and legal departments' AWS accounts.
    - __Even though you have placed these accounts into OUs, you can continue to provide access for users, groups, and roles through IAM__
    - By grouping your accounts into OUs, you can more easily give them access to the services and resources that they need. You also prevent them from accessing any services or resources that they do not need.

### Compliance
- you may need to uphold specific standards
- an audit or inspection will ensure that the company has met those standards
- __AWS Artifact__
    - a service that provides on-demand access to AWS security and compliance reports and select online agreements
    - consists of two main sections
        - AWS Artifact Agreements
        - AWS Artifact Reports
- __AWS Artifact Agreements__
    - Suppose that your company needs to sign an agreement with AWS regarding your use of certain types of information throughout AWS services. You can do this through AWS Artifact Agreements.

In AWS Artifact Agreements, you can review, accept, and manage agreements for an individual account and for all your accounts in AWS Organizations. Different types of agreements are offered to address the needs of customers who are subject to specific regulations, such as the Health Insurance Portability and Accountability Act (HIPAA).

AWS Artifact Reports
Next, suppose that a member of your company’s development team is building an application and needs more information about their responsibility for complying with certain regulatory standards. You can advise them to access this information in AWS Artifact Reports. 

AWS Artifact Reports provide compliance reports from third-party auditors. These auditors have tested and verified that AWS is compliant with a variety of global, regional, and industry-specific security standards and regulations. AWS Artifact Reports remains up to date with the latest reports released. You can provide the AWS audit artifacts to your auditors or regulators as evidence of AWS security controls. 

The following are some of the compliance reports and regulations that you can find within AWS Artifact. Each report includes a description of its contents and the reporting period for which the document is valid. 



Customer Compliance Center
The Customer Compliance Center contains resources to help you learn more about AWS compliance. 

In the Customer Compliance Center, you can read customer compliance stories to discover how companies in regulated industries have solved various compliance, governance, and audit challenges.

You can also access compliance whitepapers and documentation on topics such as:

AWS answers to key compliance questions

An overview of AWS risk and compliance

An auditing security checklist


Additionally, the Customer Compliance Center includes an auditor learning path. This learning path is designed for individuals in auditing, compliance, and legal roles who want to learn more about how their internal operations can demonstrate compliance using the AWS Cloud.