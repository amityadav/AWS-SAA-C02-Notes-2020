# CHAPTER 6 | Databases

## Databases 101

_You won't be questioned in the exam about the next sections (up to AWS Databases).
It's just for your knowledge and very good for better understanding the course._

### [What is a relational DataBase](https://www.codecademy.com/articles/what-is-rdbms-sql)

A relational database is a type of database. It uses a structure that allows us to identify and access data in relation to another piece of data in the database. Often, data in a relational database is organized into tables.

### [What is a non relational DataBase](https://www.mongodb.com/scale/what-is-a-non-relational-database)

A non-relational database is any database that does not follow the relational model provided by traditional relational database management systems. This category of databases also referred to as NoSQL databases, has seen steady adoption growth in recent years with the rise of Big Data applications.

### [What is data warehousing](https://en.wikipedia.org/wiki/Data_warehouse)

Is a system used for reporting and data analysis, and is considered a core component of business intelligence.

### [OLTP vs. OLAP](https://www.datawarehouse4u.info/OLTP-vs-OLAP.html)

We can divide IT systems into transactional (OLTP) and analytical (OLAP). In general, we can assume that OLTP systems provide source data to data warehouses, whereas OLAP systems help to analyze it.

### [AWS Databases](https://aws.amazon.com/products/databases/)

### Relations ones

* SQL
* MySQL
* PostgreSQL
* Oracle
* Aurora
* MariaDB

# [Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
* Amazon Relational Database Service (Amazon RDS) is a web service that makes it easier to set up, operate, and scale a relational database
* When you buy a server, you get CPU, memory, storage, and IOPS, all bundled together. With Amazon RDS, these are split apart so that you can scale them independently. If you need more CPU, less IOPS, or more storage, you can easily allocate them.
* Amazon RDS manages backups, software patching, automatic failure detection, and recovery.
* To deliver a managed service experience, Amazon RDS doesn't provide shell access to DB instances. It also restricts access to certain system procedures and tables that require advanced privileges.
* You can have automated backups performed when you need them, or manually create your own backup snapshot. You can use these backups to restore a database. The Amazon RDS restore process works reliably and efficiently.
* You can use the database products you are already familiar with: MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL Server.
* You can get high availability with a primary instance and a synchronous secondary instance that you can fail over to when problems occur. You can also use MariaDB, Microsoft SQL Server, MySQL, Oracle, and PostgreSQL read replicas to increase read scaling.
* In addition to the security in your database package, you can help control who can access your RDS databases by using AWS Identity and Access Management (IAM) to define users and permissions. You can also help protect your databases by putting them in a virtual private cloud.
* A security group controls the access to a DB instance. It does so by allowing access to IP address ranges or Amazon EC2 instances that you specify

### RDS Instance Class Types
---
  * CPU optimized
  * Memory optimized
  * Burstable perofmance
* You can change the CPU and memory available to a DB instance by changing its DB instance class

### Amazon RDS storage types
---
* General purpose SSD
  * General Purpose SSD volumes offer cost-effective storage that is ideal for a broad range of workloads
  * Deliver single-digit millisecond latencies and the ability to burst to 3,000 IOPS for extended periods of time
* Provisioned IOPS
  * Provisioned IOPS storage is designed to meet the needs of I/O-intensive workloads, particularly database workloads, that require low I/O latency and consistent I/O throughput
* Magnetic 
  * Amazon RDS also supports magnetic storage for backward compatibility

### High availability (Multi-AZ) for Amazon RDS
---
* Amazon RDS provides high availability and failover support for DB instances using Multi-AZ deployments for deployments for MariaDB, MySQL, Oracle, and PostgreSQL DB
* SQL Server DB instances use SQL Server Database Mirroring (DBM) or Always On Availability Groups (AGs)
* Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone
* The primary DB instance is synchronously replicated across Availability Zones to a standby replica to provide data redundancy, eliminate I/O freezes, and minimize latency spikes during system backups
* If you have a DB instance in a Single-AZ deployment and modify it to a Multi-AZ deployment
  * Amazon RDS takes a snapshot of the primary DB instance from your deployment
  * then restores the snapshot into another Availability Zone
  * New volumes created from existing EBS snapshots load lazily in the background
  * then sets up synchronous replication between your primary DB instance and the new instance
  * This action avoids downtime when you convert from Single-AZ to Multi-AZ, but you can experience a performance impact during and after converting to Multi-AZ
* **Failover** - In the event of a planned or unplanned outage of your DB instance, Amazon RDS automatically switches to a standby replica in another Availability Zone if you have enabled Multi-AZ

### Billing
---
DB instances are billed on the following components
* DB instance hours (per hour)
* Storage (per GiB per month)
* I/O requests (per 1 millisecond requests per month)
* Provisioned IOPS (per IOPS per month)
* Backup Storage (per GiB per month)
* GB transfer (per month)
* Amazon RDS provides the following purchasing options to enable you to optimize your costs based on your needs:
  * **On-Demand Instances** – Pay by the hour for the DB instance hours that you use. Pricing is listed on a per-hour basis, but bills are calculated down to the second and show times in decimal form. RDS usage is now billed in one second increments, with a minimum of 10 minutes.
  * **Reserved Instances** – Reserve a DB instance for a one-year or three-year term and get a significant discount compared to the on-demand DB instance pricing. Wi

### Security 
---
* Run your DB instance in a virtual private cloud (VPC) based on the Amazon VPC service for the greatest possible network access control 
* Use AWS Identity and Access Management (IAM) policies to assign permissions that determine who is allowed to manage Amazon RDS resources. For example, you can use IAM to determine who is allowed to create, describe, modify, and delete DB instances, tag resources, or modify security groups
* Use security groups to control what IP addresses or Amazon EC2 instances can connect to your databases on a DB instance. When you first create a DB instance, its firewall prevents any database access except through rules specified by an associated security group
* Use Secure Socket Layer (SSL) or Transport Layer Security (TLS) connections with DB instances running the MySQL, MariaDB, PostgreSQL, Oracle, or Microsoft SQL Server database engines
* Use Amazon RDS encryption to secure your DB instances and snapshots at rest. Amazon RDS encryption uses the industry standard AES-256 encryption algorithm to encrypt your data on the server that hosts your DB instance
* Use network encryption and transparent data encryption with Oracle DB instances; for more information, see Oracle native network encryption and Oracle Transparent Data Encryption
Use the security features of your DB engine to control who can log in to the databases on a DB instance

# [DynamoDB NoSQL](https://aws.amazon.com/dynamodb/)
* Amazon DynamoDB is a key-value and document database that delivers single-digit millisecond performance at any scale. 
* It's fully managed.
* Uses SSD storage
* Spread across 3 distinct data centres
* Eventual Consistent Reads (Default)
* Strongly Consistent Reads
* It's scalable
* DynamoDB can be very expensive for writes
* Amazon DynamoDB stores data in partitions. artitions are automatically replicated across multiple AZ's
* DynamoDB automatically particions and re-partitions your table as it grows in size

### DynamoDB Streams

DynamoDB Streams is an optional feature that captures data modification events in DynamoDB tables. The data about these events appear in the stream in near-real time, and in the order that the events occurred.

Each event is represented by a stream record. If you enable a stream on a table, DynamoDB Streams writes a stream record whenever one of the following events occurs:

* A new item is added to the table: The stream captures an image of the entire item, including all of its attributes.
* An item is updated: The stream captures the "before" and "after" image of any attributes that were modified in the item.
* An item is deleted from the table: The stream captures an image of the entire item before it was deleted.
Each stream record also contains the name of the table, the event timestamp, and other metadata. Stream records have a lifetime of 24 hours; after that, they are automatically removed from the stream.

You can use DynamoDB Streams together with AWS Lambda to create a trigger—code that runs automatically whenever an event of interest appears in a stream

### Read Consistency
* **Eventually Consistent Reads** - When you read data from a DynamoDB table, the response might not reflect the results of a recently completed write operation
* **Strongly Consistent Reads** - When you request a strongly consistent read, DynamoDB returns a response with the most up-to-date data, reflecting the updates from all prior write operations that were successful
  * A strongly consistent read might not be available if there is a network delay or outage. In this case, DynamoDB may return a server error (HTTP 500).
  * Strongly consistent reads may have higher latency than eventually consistent reads.
  * Strongly consistent reads are not supported on global secondary indexes.
  * Strongly consistent reads use more throughput capacity than eventually consistent reads

# [RedShift - OLAP - Used for DataWearhouse](https://aws.amazon.com/redshift/)

Amazon Redshift is a fast, scalable data warehouse that makes it simple and cost-effective to analyze all your data across your data warehouse.

Redshift stores data by [colums](https://en.wikipedia.org/wiki/Column-oriented_DBMS).  By storing data in columns rather than rows, the database can more precisely access the data it needs to answer a query rather than scanning and discarding unwanted data in rows. Query performance is increased for certain workloads.

Columnar data stores can be compressed much more than row-based data.

* Single node: You can start with a single node (Up to 160Gb of ram in one node)
* Multi-Node:
  * Leader node: Manages clients and distribute queries
  * Compute nodes: Store data and execute queries (up to 128 computer nodes max)

* Pricing:
  * You are charged for the total number of hours you run across all your compute nodes.
  * You are charged for backups
  * You are also charged for data transfer within a VPC

* Security:
  * Encrypted in transit using SSL
  * Encrypted at rest using AES-256 encryption
  * By default redshift takes care of key management.

* Availability:
  * Is available only in 1 AZ
  * Can restore the snapshot to new AZ's in the event of an outage.

# [RDS Aurora](https://aws.amazon.com/rds/aurora/)

Amazon Aurora is a MySQL and PostgreSQL-compatible relational database built for the cloud, that combines the performance and availability of traditional enterprise databases with the simplicity and cost-effectiveness of open source databases.

* Scaling:
  * Scales in 10GB Increments up to 64TB
  * Compute resources can scale up to 32vCPUs and 244GB of Memory
  * 2 Copies of your data are contained in each availability zone, with a minimum of 3 availability zones
  * Aurora handles the loss of up two to copies of data without affecting database **write** capability
  * Aurora handles the loss of up to three copies of data without affecting database **read** capability

* Replicas:
  * Aurora Replicas: Separate aurora replicas (up to 15 replicas)
  * MySQL Read replicas: (up to 5 replicas).
  * In case of loss of the primary aurora DB, failover will automatically occur on the Aurora replica, it will not in the MySQL read replica.

* Aurora global databases
  * An Aurora global database is a single database that spans multiple AWS Regions
  * enabling low-latency global reads and disaster recovery from any Region-wide outage
  * provides built-in fault tolerance for your deployment because the DB instance relies not on a single AWS Region, but upon multiple Regions and different Availability Zones

* Aurora Serverless
  * Aurora Serverless is an on-demand, auto-scaling feature designed to be a cost-effective approach to running intermittent or unpredictable workloads on Amazon Aurora
  * It automatically starts up, shuts down, and scales capacity up or down, as needed by your applications

* Amazon Aurora connection management
  * Amazon Aurora typically involves a cluster of DB instances instead of a single instance
  * When you connect to an Aurora cluster, the host name and port that you specify point to an intermediate handler called an endpoint
  * Aurora uses the endpoint mechanism to abstract these connections
  * For certain Aurora tasks, different instances or groups of instances perform different roles. For example, the primary instance handles all data definition language (DDL) and data manipulation language (DML) statements
    * Cluster endpoint
      * A cluster endpoint (or writer endpoint) for an Aurora DB cluster connects to the current primary DB instance for that DB cluster
      * Each Aurora DB cluster has one cluster endpoint and one primary DB instance
    * Reader endpoint
      * A reader endpoint for an Aurora DB cluster provides load-balancing support for read-only connections to the DB cluster
      * By processing those statements on the read-only Aurora Replicas, this endpoint reduces the overhead on the primary instance
    * Custom endpoint
      * A custom endpoint for an Aurora cluster represents a set of DB instances that you choose
      * You define which instances this endpoint refers to, and you decide what purpose the endpoint serves
      * An Aurora DB cluster has no custom endpoints until you create one
    * Instance endpoint
      * An instance endpoint connects to a specific DB instance within an Aurora cluster
      * Each DB instance in a DB cluster has its own unique instance endpoint. So there is one instance endpoint for the current primary DB instance of the DB cluster, and there is one instance endpoint for each of the Aurora Replicas in the DB cluster

![](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/images/AuroraArch001.png)


# Elasticache - In Memeory Caching
  * Redis
  * Memcached

|Database Type|Use Cases|AWS Service|
|--- |--- |--- |
|Relational|Traditional applications, ERP, CRM, e-commerce| Amazon Aurora,  Amazon RDS,  Amazon Redshift|
|Key-value|High-traffic web apps, e-commerce systems, gaming applications|Amazon DynamoDB|
|In-memory|Caching, session management, gaming leaderboards, geospatial applications|Amazon ElastiCache for Memcached, Amazon ElastiCache for Redis|
|Document|Content management, catalogs, user profiles|Amazon DocumentDB (with MongoDB compatibility)|
|Wide-column|High scale industrial apps for equipment maintenance, fleet management, and route optimization|Amazon Keyspaces (for Apache Cassandra)|
|Graph|Fraud detection, social networking, recommendation engines|Amazon Neptune|
|Time series|IoT applications, DevOps, industrial telemetry|Amazon Timestream|
|Ledger|Systems of record, supply chain, registrations, banking transactions|Amazon Quantum Ledger Database|

## [Use Cases]()
Internet scale applications
![](https://d1.awsstatic.com/webteam/category-pages/Databases/category-page-diagram_database_gaming.de2623720c885acfe788a9170db1837129758d8a.png)

Real-time applications
![](https://d1.awsstatic.com/webteam/category-pages/Databases/category-page-diagram_database_caching.959d5429c58d7a59fa08e3484ff7d43b4881ebdc.png)

Opensource application
![](https://d1.awsstatic.com/webteam/category-pages/Databases/category-page-diagram_database_open-source.b19513e06bb99e0cf4a9f98b389f3c891ebb2843.png)

Enterprise applications
![](https://d1.awsstatic.com/webteam/category-pages/Databases/Category-Page-Diagram_Datbases-on-AWS_Enterprise-Applications.fa44910d3054c6b9f6fc5140fb77b0e056dc8df7.png)

### [Automated Backups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html)

There are two different types of backups for AWS:

* Automated: Are enabled by default, data is stored in S3 and are enable automatically.
    If you delete the DB, the backup will de belated too
* Database snapshots: Need to be done manually, they are kept even if you remove the DB.

When you restore a backup or a snapshot, the restored version of the database will be in a new RDS instance, with a new DNS name

[Encryption](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html) You can encrypt your Amazon RDS DB instances and snapshots at rest by enabling the encryption option on your Amazon RDS DB instances.

### [RDS Multi-AZ](https://aws.amazon.com/rds/details/multi-az/)

When you provision a Multi-AZ DB Instance, Amazon RDS automatically creates a primary DB Instance and synchronously replicates the data to a standby instance in a different Availability Zone

* it's for disaster recovery not for scaling.

### [RDS Read Replicas](https://aws.amazon.com/rds/details/read-replicas/)

This feature makes it easy to elastically scale out beyond the capacity constraints of a single DB Instance for read-heavy database workloads
The read replica operates as a DB instance that allows only **read-only** connections

* It's used for scaling not for disaster recovery
* You need to have automatic backups on in order to have a read replica.
* You can have up to 5 read replicas of any DB at the time of writing.
* Each replica has its own DNS name.
* Replicas can become their own databases.
* You can have a replica in a second region.
* You can enable encryption on your replica even if your master is not.




### [Elasticache](https://aws.amazon.com/elasticache/)

Elasticache: Managed, Redis or Memcached-compatible in-memory data store. Basically, it's a DB that saves everything in memory to increases I/O performance.

* Types of Elasticache:
  * Memcached
  * Redis: In memory key-value store

