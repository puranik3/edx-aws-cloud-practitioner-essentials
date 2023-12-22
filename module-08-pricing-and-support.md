## Module 8: Pricing and Support

### AWS Free Tier
- enables you to begin using __certain services__ without having to worry about incurring costs for the specified period
- https://aws.amazon.com/free
- Three types of offers are available
    - __Always Free__
        - _do not expire and are available to all AWS customers_
        - AWS Lambda allows 1 million free requests and up to 3.2 million seconds of compute time per month
        - Amazon DynamoDB allows 25 GB of free storage per month
    - __12 Months Free__
        - free for 12 months following your initial sign-up date to AWS
        - specific amounts of Amazon S3 Standard Storage
            - 5 GB of Standard Storage
            - 20,000 Get Requests
            - 2,000 Put Requests
        - thresholds for monthly hours of Amazon EC2 compute time
        - amounts of Amazon CloudFront data transfer out
    - __Trials__
        - short-term free trial offers start from the date you activate a particular service
        - length of each trial might vary by number of days or the amount of usage in the service
        - Amazon Inspector offers a 90-day free trial
        - Amazon Lightsail offers 750 free hours of usage over a 30-day period (you can, say, deploy a Wordpress blog with Amazon Lightsail)
- For each offer, make sure to review the specific details about exactly which resource types are included

### AWS Pricing Concepts
- How pricing works
    - __Pay for what you use__
        - pay for exactly the amount of resources that you actually use - no long-term contracts or complex licensing
    - __Pay less when you reserve__
        - reservation options that provide a significant discount compared to On-Demand Instance pricing
        - eg. EC2 Instance Savings Plan (upto 72% savings)
    - __Pay less with volume-based discounts when you use more__
        - tiered pricing, so the per-unit cost is incrementally lower with increased usage
        - the more Amazon S3 storage space you use, the less you pay for it per GB
    - view the __itemized charges for a service by region__
- __Pricing Calculator__
    - lets you explore AWS services and create an estimate for the cost of your use cases
    - organize your AWS estimates by __groups__ that reflect how your company is organized (cost centers)
    - create an estimate, save it, and generate a link to share it with others!
    - eg. you need to use EC2, but not sure which AWS Region or instance type is cost-effective
        - enter details like OS, memory, and I/O requirements - you will get a comparison for different EC2 instance types, across AWS Regions!
- __Pricing Examples__
    - __Lambda Pricing__
        - number of requests
        - running time of functions
        - Free tier limits: 1 million free requests and up to 3.2 million seconds of compute time per month
        - pay less when you reserve (commit to a certain usage over a 1-year or 3-year term)
    - __EC2 Pricing__
        - pay for compute time while instances are running
        - reduce EC2 costs by using Spot Instances (upto 90% savings) - interruptible workloads
        - or reduce costs using Savings Plans and Reserved Instances - non-interruptible workloads
        - has price for
            - each Amazon EC2 instance type used
            - amount of EBS storage space
            - length of time ELB is used
    - __S3 Pricing__
        - storage you use
        - objects' sizes
        - storage classes
        - how long each object is stored in the month
        - number and type of requests / data retrievals for objects and buckets
            - eg. every time a visitor requests the website that includes photos stored in S3, it counts towards requests!
        - storage management features enabled on your account's Amazon S3 buckets
            - inventory
            - analytics
            - object tagging (wow! tagging is not free!!)
        - pay for data that you transfer into and out of Amazon S3, with a few exceptions. No cost for data transferred...
            - into Amazon S3 from the internet
            - out to Amazon CloudFront
            - _between different Amazon S3 buckets_ or _from Amazon S3 to other services (like EC2) within the __same AWS Region___

### Billing Dashboard
- __Billing & Cost Management Dashboard__
    - pay bills
    - monitor usage
    - analyze and control costs
- compare bills month-on-month
- forecast for next month based on current usage
- month-to-date spend by service
    - view Free Tier usage by service
- access __Cost Explorer__ and create __budgets__
- purchase and manage Savings Plans
- publish AWS Cost and Usage Reports

### Consolidated Billing
- AWS Organizations provides the option for consolidated billing
    - single bill for all AWS accounts in your organization
    - easily track the combined costs of all the linked accounts in your organization
    - benefit by sharing bulk discount pricing
        - eg. in S3, after customers have transferred 10 TB of data in a month, they pay a lower per-GB transfer price for the next 40 TB of data transferred. If ou have 3 accounts (in an organization) with transfers of 2, 5, and 7 TB in a month
            - though each does not qualify individually for the discount, with consolidated billing you will!
            - AWS allocates each linked account a portion of the overall volume discount based on the account's usage
    - Savings Plan, Reserved Instance can be shared across the accounts in an organization, bringing costs down
- review itemized charges incurred by each account
- consolidated billing is a free feature - you have nothing to lose by using it
- default maximum number of accounts allowed for an organization is 4, but you can contact AWS Support to increase your quota

### AWS Budgets
- create budgets to plan
    - service usage
    - service costs
    - instance reservations
- information in AWS Budgets updates 3 times a day
- set custom alerts when your usage exceeds (or is forecasted to exceed) the budget
    - eg. if you set a budget of $200 for Amazon EC2, you could set AWS Budget to notify you when the usage has reached half of the amount ($100)
    - allows you to receive an alert and decide how you would like to proceed with your continued use of Amazon EC2

### AWS Cost Explorer
- visualize, understand, and manage your AWS costs and usage over time
    - 12 months of historical data
- includes a default report of the costs and usage for your top 5 cost-accruing AWS services
- apply custom filters and groups to analyze your data
    - eg. view resource usage at the hourly level, by tag name etc.
- granular
    - separates costs for different Amazon EC2 instance types (such as t2.micro or m3.large)

### AWS Support Plans
- 4 types with __increasing support levels__ (__Basic < Developer < Business < Enterprise__)
    - __Basic__
        - free for all AWS customers
        - access tp
            - whitepapers
            - documentation
            - support communities
        - contact AWS for billing questions and service limit increases
        - access to limited selection of AWS Trusted Advisor checks
        - use the AWS Personal Health Dashboard
            - provides alerts and remediation guidance when AWS is experiencing events that may affect you
    - __Developer__
        - paid
        - open an unrestricted number of technical support cases
        - email support with
            - 24 hour response time
            - 12 hours if your business is impaired
        - best practice guidance
        - client-side diagnostic tools
        - __Building-block architecture support__ - guidance for how to use AWS offerings, features, and services together
        - great when building Proof-of-concept (PoCs)
    - __Business__
        - paid
        - direct phone access to cloud support engineers
            - 4 hour support time if production system is impaired
            - 1 hour support time if production system is down
        - all AWS Trusted Advisor checks
        - __Infrastructure event management__ supported?? (not sure - need to check this)
        - __Use-case guidance__ - identify AWS offerings, features, and services that can best support your specific needs
        - limited support for third-party software, such as common operating systems and application stack components
            - Suppose that your company wants to install a common third-party OS onto EC2 instances. Use AWS Support for assistance in installing, configuring, and troubleshooting the OS. For advanced topics such as optimizing performance, using custom scripts, or resolving security issues, you may need to contact the third-party software provider directly.
    - __Enterprise__
        - 2 types
        - __Enterprise On-Ramp__
            - paid
            - 30 minute response time for business and mission critical workloads
            - access to a pool of __Technical Account Manager (TAMs)__
                - engagement with TAMs is __rate-limited__
        - __Enterprise__
            - paid
            - 15 minute response time for business and mission critical workloads
            - access to corrective reviews, workshops and deep dives
            - __Application architecture guidance__ - a consultative relationship to support your company's specific use cases and applications
            - __Infrastructure event management__ - A short-term engagement with AWS Support that helps your company gain a better understanding of your use cases. This also provides your company with architectural and scaling guidance.
            - includes access to a __designated__ __Technical Account Manager (TAM)__
                - engagement with TAM is __NOT ____rate-limited__
                - TAM is your primary point of contact at AWS - provides guidance, architectural reviews, and ongoing communication with your company as you plan, deploy, and optimize your applications
                - TAM provides expertise across the full range of AWS services - helps you design solutions that efficiently use multiple services together through an integrated approach (say, helping you achieve the goal through that new application you are building)
                - TAM reviews architecture using the _AWS Well-Architected Framework_, i.e. it is checked against these 6 pillars
                    - Operational excellence
                    - Security
                    - Reliability
                    - Performance efficiency
                    - Cost-optimization
                    - Sustainability


### AWS Marketplace
- a digital catalog that includes thousands of software listings from independent software vendors
- find, test, and buy software that runs on AWS
- access detailed information on pricing options, available support, and reviews from other AWS customers
- one-click deployment!
- many solutions include free trials, pay-as-you-go options, custom terms and pricing
- explore software solutions by
    - industry
    - use case
    - eg. for healthcare industry, you can review use cases that software helps you to address, such as 
        - implementing solutions to protect patient records
        - using machine learning models to analyze a patient's medical history and predict possible health risks
- __AWS Marketplace Categories__
    - AWS Marketplace offers products in several categories (with subcategories), such as Infrastructure Products, Business Applications, Data Products, and DevOps
    - narrow search within a category / subcategories
- __Enterprise-focused features of the AWS Marketplace__
    - custom terms and pricing for solutions on the marketplace
    - ability to create a __Private marketplace__ with a custom catalog of only those solutions that meet the legal / security standards of the enterprise
    - integration into procurement systems of the enterprise
    - a range of cost management tools

### AWS Cloud Financial Management Services
| Use Cases | Capabilities | AWS Resources |
| :---: | :---: | :---: |
| Organize | Construct your cost allocation strategy that aligns with your business logic | AWS Billing Conductor, AWS Cost Allocation Tags, AWS Cost Categories |
| Report | Raise awareness and accountability of your cloud spend with the detailed, allocable cost data | AWS Cost Explorer, AWS Cost and Usage Report, AWS Application Cost Profiler |
| Access | Track billing information across the organization in a consolidated view	AWS Consolidated Billing | AWS Purchase Order Management, AWS Credits |
| Control | Establish effective governance mechanisms with the right guardrails in place | AWS Cost Anomaly Detection, AWS Identity and Access Management, AWS Organizations, AWS Control Tower, AWS Service Catalog |
| Forecast | Estimate your resource utilization and spend with forecast dashboards that you create | AWS Cost Explorer (Self-Service), AWS Budgets (Event-Driven) |
| Budget | Keep your spend in check with custom budget threshold and auto alert notification | AWS Budgets, AWS Budget Actions, AWS Service Catalog |
| Purchase | Leverage free trials and programmatic discounts based on your workload pattern and needs | AWS Free Tier, AWS Reserved Instances, AWS Savings Plans, AWS Spot Instances, Amazon DynamoDB On-demand |
| Elasticity | Scale and schedule your services based on your expected utilization pattern and needs | AWS Instance Scheduler, Amazon Redshift pause and resume, EC2 Auto Scaling, AWS Trusted Advisor |
| Rightsize | Align your service allocation size to your actual workload demand	AWS Cost Explorer Right Sizing Recommendations | AWS Compute Optimizer, Amazon Redshift resize, Amazon S3 Intelligent Tiering |
| Inspect | Stay up-to-date with your resource deployment and cost optimization opportunities | AWS Cost Explorer |

### Resources
- [AWS Free Tier](https://aws.amazon.com/free)
- [AWS Pricing Calculator](https://calculator.aws)
- [What is AWS Billing and Cost Management?](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html)
- [What are AWS Cost and Usage Reports?](https://docs.aws.amazon.com/cur/latest/userguide/what-is-cur.html)
- [Consolidated billing for AWS Organizations](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html)
- [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/)
- [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/)
- [Compare AWS Support Plans](https://aws.amazon.com/premiumsupport/plans/)
- [AWS Marketplace](https://aws.amazon.com/marketplace)
- [AWS Pricing](https://aws.amazon.com/pricing)
- [AWS Cost Management](https://aws.amazon.com/aws-cost-management/)
- [Whitepaper: How AWS Pricing Works](https://d1.awsstatic.com/whitepapers/aws_pricing_overview.pdf)
- [Whitepaper: Introduction to AWS Economics](https://d1.awsstatic.com/whitepapers/introduction-to-aws-cloud-economics-final.pdf)
- [AWS Support](https://aws.amazon.com/premiumsupport/)
- [AWS Knowledge Center](https://repost.aws/knowledge-center)