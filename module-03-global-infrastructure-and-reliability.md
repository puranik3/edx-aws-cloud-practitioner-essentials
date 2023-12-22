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

### Resources
- [Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)
- [Regions and Availability Zones](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/)
- [AWS Networking and Content Delivery Blog](https://aws.amazon.com/blogs/networking-and-content-delivery/)
- [Tools to Build on AWS](https://aws.amazon.com/developer/tools/)