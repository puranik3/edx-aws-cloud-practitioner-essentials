## Module 10: The Cloud Journey
How do we know that our arhitecture for apps in the AWS Cloud is good? What standards exist to evaluate it against? Enter, the __AWS Well-Architected Framework__

### The AWS Well-Architected Framework
- helps you understand how to design and operate reliable, secure, efficient, and cost-effective systems in the AWS Cloud
- consistently measure architecture against best practices and design principles, and identify areas for improvement
- Based on __6 pillars__
    - __Operational excellence__
        - the ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures
        - design principles for operational excellence in the cloud include performing operations as code, annotating documentation, anticipating failure, and frequently making small, reversible changes
        - eg. automatic deployment using popelines, responding to event triggers
    - __Security__
        - ability to protect information, systems, and assets while delivering business value through risk assessments and mitigation strategies
        - Best practices
            - automate security best practices when possible
            - apply security at all layers
            - protect data in transit and at rest
    - __Reliability__
        - Reliability is the ability of a system to
            - recover from infrastructure or service disruptions
            - dynamically acquire computing resources to meet demand
            - mitigate disruptions such as misconfigurations or transient network issues
        - Reliability includes testing recovery procedures, scaling horizontally to increase aggregate system availability, and automatically recovering from failure
        - eg. recovering from EC2 failure
    - __Performance efficiency__
        - ability to use computing resources efficiently to meet system requirements and maintain that efficiency as demand changes and technologies evolve
        - evaluating the performance efficiency of your architecture includes experimenting more often, using serverless architectures, and designing systems to be able to go global in minutes
        - eg. using the right EC2 instance types based on workload and memory requirements
    - __Cost optimization__
        - ability to run systems to deliver business value at the lowest price point
        - includes adopting a consumption model, analyzing and attributing expenditure, and using managed services to reduce the cost of ownership
    - __Sustainability__
        - minimizing the environmental impacts of running workloads
        - focuses on reducing energy consumption, increasing efficiency
- __The AWS Well-Architected Tool__
    - create a workload and run it against the AWS account to generate a report on the areas to address

### Benefits of the AWS Cloud
- Operating in the AWS Cloud offers benefits over in on-premises or hybrid environments
    - Trade upfront expense for variable expense
        - data centers, physical servers, and other resources that you would need to invest in
        - instead you can pay-as-you-use, only for what you use
    - Benefit from massive economies of scale
        - achieve a lower variable cost than you can get on your own, because usage from hundreds of thousands of customers aggregates in the cloud
    - Stop guessing capacity
        - eg. you can launch Amazon EC2 instances when needed and pay only for the compute time you use, and scale in or out in response to demand
    - Increase speed and agility
        - flexibility of cloud computing makes it easier for you to develop and deploy applications
        - this also provides your development teams with more time to experiment and innovate
        - so many start ups are spun-up in a day!
    - Stop spending money running and maintaining data centers
        - focus less on these tasks and more on your applications and customers
    - Go global in minutes

### Resources
- [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/)
- [Whitepaper: AWS Well-Architected Framework](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf)
- [AWS Architecture Center](https://aws.amazon.com/architecture)
- [Six Advantages of Cloud Computing](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html)
- [AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/)