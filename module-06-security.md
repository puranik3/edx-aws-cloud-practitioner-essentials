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
        - __AWS Artifact Agreements__
        - __AWS Artifact Reports__
    - __AWS Artifact Agreements__
        - used if a company needs to sign an agreement with AWS regarding use of certain types of information throughout AWS services
        - one can review, accept, and manage agreements for an individual account and for all accounts in AWS Organizations
        - different types of agreements are offered to address the needs of customers who are subject to specific regulations (eg. GDPA, HIPAA)
    - __AWS Artifact Reports__
        - if a member of your company's development team is building an application and needs more information about their responsibility for complying with certain regulatory standards, this can be accessed here
        - provides compliance reports from third-party auditors
        - tested and verified that AWS is compliant with a variety of global, regional, and industry-specific security standards and regulations
        - remains up to date with the latest reports released
        - provide the AWS audit artifacts to your auditors or regulators as evidence of AWS security controls
    - __Customer Compliance Center__
        - contains resources to help you learn more about AWS compliance
        - read customer compliance stories to discover how companies in regulated industries have solved various compliance, governance, and audit challenges
        - access compliance whitepapers and documentation on topics such as
            - AWS answers to key compliance questions
            - overview of AWS risk and compliance
            - an auditing security checklist
            - includes an auditor learning path

### Denial-of-Service Attacks
- A __Denial-of-Service (DoS) attack__ is a deliberate attempt to make a website or application unavailable to users
- In a __Distributed Denial-of-Service (DDoS) attack__, multiple sources are used to start an attack that aims to make a website or application unavailable. This can come from a group of attackers, or even a single attacker. The single attacker can use multiple infected computers (also known as "bots") to send excessive traffic to a website or application.
- __AWS Shield__
    - a service that protects applications against DDoS attacks
    - provides two levels of protection
        - __AWS Shield Standard__
            - automatically protects all AWS customers at no cost
            - protects AWS resources from the most common, frequently occurring types of DDoS attack
            - analyses network traffic into your applications, using a variety of analysis techniques to detect malicious traffic in real time and automatically mitigates it
        - __AWS Shield Advanced__
            - paid service that provides detailed attack diagnostics and the ability to detect and mitigate sophisticated DDoS attacks
            - integrates with other services such as Amazon CloudFront, Amazon Route 53, and Elastic Load Balancing
            - you can additionally integrate AWS Shield with AWS WAF by writing custom rules to mitigate complex DDoS attacks

### Additional Security Services
- __AWS Key Management Service (AWS KMS)__
    - to ensure that your application data is secure while in storage (encryption at rest) and while it is transmitted (encryption in transit)
    - enables you to perform encryption operations through the use of cryptographic keys
    - a cryptographic key is a random string of digits used for locking (encrypting) and unlocking (decrypting) data
    - use KMS to create, manage, and use cryptographic keys
    - control the use of keys across a wide range of services and in your applications
    - you can choose the specific levels of access control for the keys
        - specify which IAM users and roles are able to manage keys
        - temporarily disable keys so that they are no longer in use by anyone
- __AWS Web Application Firewall (AWS WAF)__
    - lets you monitor network requests that come into your web apps
    - works together with Amazon CloudFront and an __Application Load Balancer__ (a type of ELB)
    - AWS WAF works in a way similar to Network ACLs block or allow traffic. However, it does this by using a __Web Access Control List (ACL)__ to protect your AWS resources
        - Suppose an application has been receiving malicious network requests from several IP addresses
        - you configure the Web ACL to allow all requests except those from the IP addresses that you have specified
- __Amazon Inspector__
    - helps to improve the security and compliance of apps by running automated security assessments
    - checks applications for security vulnerabilities and deviations from security best practices, such as open access to Amazon EC2 instances and installations of vulnerable software versions
    - provides you with a list of security findings
        - prioritizes by severity level
        - detailed description of each issue
        - recommendation for how to fix it
            - However, AWS does not guarantee that following the provided recommendations resolves every potential security issue (customer is ultimately responsible for security of apps! under the Shared Responsibility Model)
    - Parts of the Amazon Inspector
        - Network configuration reachability piece
        - Amazon agent
        - Security assessment service
- __Amazon GuardDuty__
    - a service that provides intelligent threat detection for your AWS infrastructure and resources
    - identifies threats by continuously monitoring the network activity and account behavior within your AWS environment
    - analyzes data from multiple AWS sources, including AWS CloudTrail events, VPC Flow Logs and DNS logs
    - you can review detailed findings from the AWS Management Console
    - suggests recommended steps for remediation
    - you can also configure AWS Lambda functions to take remediation steps automatically in response to GuardDuty's security findings

### AWS Security, Identity, & Compliance services
| Category | What is it | AWS service |
| :---: | :---: | :---: |
| Identity and access management | Securely manage identities and access to AWS services and resources | AWS Identity and Access Management (IAM) |
| | Centrally manage workforce access to multiple AWS accounts and applications | AWS IAM Identity Center (successor to SSO) |
| | Implement secure, frictionless customer identity and access management that scales | Amazon Cognito |
| | Manage fine-grained permissions and authorization within custom applications | Amazon Verified Permissions |
| | Gain efficiency with a fully managed Microsoft Active Directory service	| AWS Directory Service |
| | Simply and securely share your AWS resources across multiple accounts | AWS Resource Access Manager |
| | Centrally manage your environment as you scale your AWS resources | AWS Organizations |
| Detection and response | Protect AWS accounts with intelligent threat detection | Amazon GuardDuty |
| | Automated and continual vulnerability management at scale | Amazon Inspector |
| | Automate AWS security checks and centralize security alerts | AWS Security Hub |
| | Automatically centralize your security data in a few steps | Amazon Security Lake |
| | Analyze and visualize security data to investigate potential security issues | Amazon Detective |
| | Assess, audit, and evaluate configurations of your resources | AWS Config |
| | Observe and monitor resources and applications on AWS, on premises, and on other clouds | Amazon CloudWatch |
| | Track user activity and API usage | AWS CloudTrail |
| | Security management across your IoT devices and fleets | AWS IoT Device Defender |
| | Scalable, cost-effective application recovery to AWS | AWS Elastic Disaster Recovery |
| Network and application protection | Centrally configure and manage firewall rules across your accounts | AWS Firewall Manager |
| | Deploy network firewall security across your VPCs | AWS Network Firewall |
| | Maximize application availability and responsiveness with managed DDoS protection | AWS Shield |
| | Provide secure access to corporate applications without a VPN | AWS Verified Access |
| | Protect your web applications from common exploits | AWS Web Application Firewall (WAF) |
| | Filter and control outbound DNS traffic for your VPCs | Amazon Route 53 Resolver DNS Firewall |
| Data protection | Discover and protect your sensitive data at scale | Amazon Macie |
| | Create and control keys to encrypt or digitally sign your data | AWS Key Management Service (AWS KMS) |
| | Manage single-tenant hardware security modules (HSMs) on AWS | AWS CloudHSM |
| | Provision and manage SSL/TLS certificates with AWS services and connected resources | AWS Certificate Manager |
| | Simplify cryptography operations in your cloud-hosted payment applications | AWS Payment Cryptography |
| | Create private certificates to identify resources and protect data | AWS Private Certificate Authority |
| | Centrally manage the lifecycle of secrets | AWS Secrets Manager |
| Compliance | No cost, self-service portal for on-demand access to AWS’ compliance reports | AWS Artifact |
| | Continually audit your AWS usage to simplify risk and compliance assessment | AWS Audit Manager |

### Resources
- [Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)
- [AWS Identity and Access Management](https://aws.amazon.com/iam/)
- [AWS account root user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html)
- [IAM user groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups.html)
- [IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)
- [Multi-Factor Authentication (MFA) for IAM](https://aws.amazon.com/iam/features/mfa/)
- [AWS Organizations](https://aws.amazon.com/organizations/)
- [Service control policies (SCPs)](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
- [AWS Artifact](https://aws.amazon.com/artifact/)
- [Customer Compliance Center](https://aws.amazon.com/compliance/customer-center/)
- [AWS Shield](https://aws.amazon.com/shield/)
- [AWS Key Management Service](https://aws.amazon.com/kms/)
- [AWS WAF](https://aws.amazon.com/waf/)
- [Web access control lists (web ACLs)](https://docs.aws.amazon.com/waf/latest/developerguide/web-acl.html)
- [Amazon Inspector](https://aws.amazon.com/inspector/)
- [Amazon GuardDuty](https://aws.amazon.com/guardduty/)
- [Security, Identity, and Compliance on AWS](https://aws.amazon.com/products/security/)
- [Whitepaper: Introduction to AWS Security](https://docs.aws.amazon.com/whitepapers/latest/introduction-aws-security/welcome.html)
- [Whitepaper: Amazon Web Services - Overview of Security Processes](https://docs.aws.amazon.com/pdfs/whitepapers/latest/aws-overview-security-processes/aws-overview-security-processes.pdf)
- [AWS Security Blog](https://aws.amazon.com/blogs/security/)
- [AWS Compliance](https://aws.amazon.com/compliance/)