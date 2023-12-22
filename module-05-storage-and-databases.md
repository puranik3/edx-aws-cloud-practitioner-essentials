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
    - secure
        - data is encrypted
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
| :---:             | :---:                                                                                                           | :---:                                         |
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