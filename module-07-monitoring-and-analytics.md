## Module 7: Monitoring and Analytics
- continuously observing the system in action, automatically collecting/generating metrics, and using it as feedback to take immediate and necessary corrective action
- we monitor AWS resources to take action when needed
    - if EC2 instances are overloaded, we detect it and automatically scale up
    - if an application sends error responses frequently, we can alert someone to take a look into it

### Amazon CloudWatch
- a web service to monitor and manage various metrics
- AWS services send metrics to CloudWatch
- CloudWatch uses these metrics to create graphs plotted over time
- __CloudWatch Alarms__
    - configure alarm actions based on data from metrics
    - you can set up to receive a notification whenever this alarm is triggered (integrates wiith __SNS__)
    - example, if the developers forget to stop the instances it costs!
        - create a CloudWatch alarm that automatically stops an Amazon EC2 instance when the CPU utilization percentage has remained below a certain threshold for a specified period
    - reduce Mean Time To Resolution (MTTR) and improve (reduce) Total Cost Cost of Ownership (TCO)
- __CloudWatch Dashboard__
    - access all the metrics for your resources from a single location
        - Examples
            - CPU utilization of an Amazon EC2 instance
            - total number of requests made to an Amazon S3 bucket
    - is real-time - updates live!
    - customize separate dashboards based on
        - business purposes
        - applications
        - resources

### AWS CloudTrail
- AWS CloudTrail engine records every AWS service API call for your account (that are used to provision, manage, and configure your AWS resources etc.)
    - identity of caller
    - time of call
    - IP address of caller
    - what changed (if any)
    - was the request allowed / denied
    - etc.
- these details can also be captured in secure S3 buckets and locked in AWS Vault!
- events are typically updated in CloudTrail within 15 minutes after an API call
- __Example__
    - Q: Who, when, and which method created a new unexpected IAM account Mary
    - A: On January 1, 2020 at 9:00 AM, IAM user John created a new IAM user (Mary) through the AWS Management Console
- __CloudTrail Insights__
    - enabling CloudTrail Insights feature to automatically detect unusual API activities in your AWS account
    - For example, it might detect that a higher number of Amazon EC2 instances than usual have recently launched in your account

### AWS Trusted Advisor
- a web service that inspects your AWS environment and provides real-time recommendations in accordance with AWS best practices
- compares its findings to AWS best practices in 5 categories
    - cost optimization
    - performance
    - security
    - fault tolerance
    - service limits
- offers a list of recommended actions, additional resources to learn more about AWS best practices
- this can help
    - while you are creating new workflows and developing new applications
    - while you are making ongoing improvements to existing applications and resources
- can set up automatic notifications to concerned user accounts
- __AWS Trusted Advisor Dashboard__
    - review completed checks in the 5 categories
    - the green check indicates the number of items for which it detected __no problems__
    - the orange triangle represents the number of __recommended investigations__
    - Tte red circle represents the number of __recommended actions__

### Resources
- [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/)
- [Use Amazon CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html)
- [Using Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html)
- [Using Amazon CloudWatch dashboards](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Dashboards.html)
- [AWS CloudTrail](https://aws.amazon.com/cloudtrail/)
- [Logging Insights events](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/logging-insights-events-with-cloudtrail.html)
- [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/)
- [Management and Governance on AWS](https://aws.amazon.com/products/management-and-governance/)
- [Monitoring and Observability](https://aws.amazon.com/cloudops/monitoring-and-observability)
- [Configuration, Compliance, and Auditing](https://aws.amazon.com/cloudops/compliance-and-auditing)
- [AWS Management & Governance Blog](https://aws.amazon.com/blogs/mt/)
- [Whitepaper: AWS Governance at Scale](https://d1.awsstatic.com/whitepapers/Security/AWS_Governance_at_Scale.pdf)