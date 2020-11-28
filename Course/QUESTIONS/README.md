##Question 1

A solutions architect is designing a solution where users will be directed to a backup static error page if the primary website is unavailable. The primary website'sDNS records are hosted in Amazon Route 53 where their domain is pointing to an Application Load Balancer (ALB).Which configuration should the solutions architect use to meet the company's needs while minimizing changes and infrastructure overhead?

Answers
* A. Point a Route 53 alias record to an Amazon CloudFront distribution with the ALB as one of its origins. Then, create custom error pages for the distribution.
* B. Set up a Route 53 active-passive failover configuration. Direct traffic to a static error page hosted within an Amazon S3 bucket when Route 53 health checks determine that the ALB endpoint is unhealthy.
* C. Update the Route 53 record to use a latency-based routing policy. Add the backup static error page hosted within an Amazon S3 bucket to the record so the traffic is sent to the most responsive endpoints.
* D. Set up a Route 53 active-active configuration with the ALB and an Amazon EC2 instance hosting a static error page as endpoints. Route 53 will only send requests to the instance if the heal checks fail for the ALB.




---------------------
Question 2
A solutions architect is designing a high performance computing (HPC) workload on Amazon EC2. The EC2 instances need to communicate to each other frequently and require network performance with low latency and high throughput.Which EC2 configuration meets these requirements?

Answers
A. Launch the EC2 instances in a cluster placement group in one Availability Zone.
B. Launch the EC2 instances in a spread placement group in one Availability Zone.
C. Launch the EC2 instances in an Auto Scaling group in two Regions and peer the VPCs.
D. Launch the EC2 instances in an Auto Scaling group spanning multiple Availability Zones.


---------------------
Question 3
A company wants to host a scalable web application on AWS. The application will be accessed by users from different geographic regions of the world.Application users will be able to download and upload unique data up to gigabytes in size. The development team wants a cost-effective solution to minimize upload and download latency and maximize performance.What should a solutions architect do to accomplish this?

Answers
A. Use Amazon S3 with Transfer Acceleration to host the application.
B. Use Amazon S3 with CacheControl headers to host the application.
C. Use Amazon EC2 with Auto Scaling and Amazon CloudFront to host the application.
D. Use Amazon EC2 with Auto Scaling and Amazon ElastiCache to host the application.



---------------------
Question 4
A company is migrating from an on-premises infrastructure to the AWS Cloud. One of the company's applications stores files on a Windows file server farm that uses Distributed File System Replication (DFSR) to keep data in sync. A solutions architect needs to replace the file server farm.Which service should the solutions architect use?

Answers
A. Amazon EFS
B. Amazon FSx
C. Amazon S3
D. AWS Storage Gateway



---------------------
Question 5
A company has a legacy application that process data in two parts. The second part of the process takes longer than the first, so the company has decided to rewrite the application as two microservices running on Amazon ECS that can scale independently.How should a solutions architect integrate the microservices?

Answers
A. Implement code in microservice 1 to send data to an Amazon S3 bucket. Use S3 event notifications to invoke microservice 2.
B. Implement code in microservice 1 to publish data to an Amazon SNS topic. Implement code in microservice 2 to subscribe to this topic.
C. Implement code in microservice 1 to send data to Amazon Kinesis Data Firehose. Implement code in microservice 2 to read from Kinesis Data Firehose.
D. Implement code in microservice 1 to send data to an Amazon SQS queue. Implement code in microservice 2 to process messages from the queue.


---------------------
Question 6
A company captures clickstream data from multiple websites and analyzes it using batch processing. The data is loaded nightly into Amazon Redshift and is consumed by business analysts. The company wants to move towards near-real-time data processing for timely insights. The solution should process the streaming data with minimal effort and operational overhead.Which combination of AWS services are MOST cost-effective for this solution? (Choose two.)

Answers
A. Amazon EC2
B. AWS Lambda
C. Amazon Kinesis Data Streams
D. Amazon Kinesis Data Firehose
E. Amazon Kinesis Data Analytics



---------------------
Question 7
A company's application runs on Amazon EC2 instances behind an Application Load Balancer (ALB). The instances run in an Amazon EC2 Auto Scaling group across multiple Availability Zones. On the first day of every month at midnight, the application becomes much slower when the month-end financial calculation batch executes. This causes the CPU utilization of the EC2 instances to immediately peak to 100%, which disrupts the application.What should a solutions architect recommend to ensure the application is able to handle the workload and avoid downtime?

Answers
A. Configure an Amazon CloudFront distribution in front of the ALB.
B. Configure an EC2 Auto Scaling simple scaling policy based on CPU utilization.
C. Configure an EC2 Auto Scaling scheduled scaling policy based on the monthly schedule.
D. Configure Amazon ElastiGache to remove some of the workload from the EC2 instances.


---------------------
Question 8
A company runs a multi-tier web application that hosts news content. The application runs on Amazon EC2 instances behind an Application Load Balancer. The instances run in an EC2 Auto Scaling group across multiple Availability Zones and use an Amazon Aurora database. A solutions architect needs to make the application more resilient to periodic increases in request rates.Which architecture should the solutions architect implement? (Choose two.)

Answers
A. Add AWS Shield.
B. Add Aurora Replica.
C. Add AWS Direct Connect.
D. Add AWS Global Accelerator.
E. Add an Amazon CloudFront distribution in front of the Application Load Balancer.


---------------------
Question 9
An application running on AWS uses an Amazon Aurora Multi-AZ deployment for its database. When evaluating performance metrics, a solutions architect discovered that the database reads are causing high I/O and adding latency to the write requests against the database.What should the solutions architect do to separate the read requests from the write requests?

Answers
A. Enable read-through caching on the Amazon Aurora database.
B. Update the application to read from the Multi-AZ standby instance.
C. Create a read replica and modify the application to use the appropriate endpoint.
D. Create a second Amazon Aurora database and link it to the primary database as a read replica.



---------------------
Question 10
A recently acquired company is required to build its own infrastructure on AWS and migrate multiple applications to the cloud within a month. Each application has approximately 50 TB of data to be transferred. After the migration is complete, this company and its parent company will both require secure network connectivity with consistent throughput from their data centers to the applications. A solution architect must ensure one-time data migration and ongoing network connectivity.Which solution will meet these requirements?

Answers
A. AWS Direct Connect for both the initial transfer and ongoing connectivity.
B. AWS Site-to-Site VPN for both the initial transfer and ongoing connectivity.
C. AWS Snowball for the initial transfer and AWS Direct Connect for ongoing connectivity.
D. AWS Snowball for the initial transfer and AWS Site-to-Site VPN for ongoing connectivity.

---------------------
Question 11
A company serves content to its subscribers across the world using an application running on AWS. The application has several Amazon C2 instances in a private subnet behind an Application Load Balancer (ALB). Due to a recent change in copyright restrictions, the chief information officer (CIO) wants to block access for certain countries.Which action will meet these requirements?

Answers
A. Modify the ALB security group to deny incoming traffic from blocked countries.
B. Modify the security group for EC2 instances to deny incoming traffic from blocked countries.
C. Use Amazon CloudFront to serve the application and deny access to blocked countries.
D. Use ALB listener rules to return access denied responses to incoming traffic from blocked countries.

---------------------
Question 12
A product team is creating a new application that will store a large amount of data. The data will be analyzed hourly and modified by multiple Amazon EC2 Linux instances. The application team believes the amount of space needed will continue to grow for the next 6 months.Which set of actions should a solutions architect take to support these needs?

Answers
A. Store the data in an Amazon EBS volume. Mount the EBS volume on the application instances.
B. Store the data in an Amazon EFS file system. Mount the file system on the application instances.
C. Store the data in Amazon S3 Glacier. Update the vault policy to allow access to the application instances.
D. Store the data in Amazon S3 Standard-Infrequent Access (S3 Standard-IA). Update the bucket policy to allow access to the application instances.


---------------------
Question 13
A company is migrating a three-tier application to AWS. The application requires a MySQL database. In the past, the application users reported poor application performance when creating new entries. These performance issues were caused by users generating different real-time reports from the application during working hours.Which solution will improve the performance of the application when it is moved to AWS?

Answers
A. Import the data into an Amazon DynamoDB table with provisioned capacity. Refactor the application to use DynamoDB for reports.
B. Create the database on a compute optimized Amazon EC2 instance. Ensure compute resources exceed the on-premises database.
C. Create an Amazon Aurora MySQL Multi-AZ DB cluster with multiple read replicas. Configure the application reader endpoint for reports.
D. Create an Amazon Aurora MySQL Multi-AZ DB cluster. Configure the application to use the backup instance of the cluster as an endpoint for the reports.


---------------------
Question 14
A solutions architect is deploying a distributed database on multiple Amazon EC2 instances. The database stores all data on multiple instances so it can withstand the loss of an instance. The database requires block storage with latency and throughput to support several million transactions per second per server.Which storage solution should the solutions architect use?

Answers
A. Amazon EBS
B. Amazon EC2 instance store
C. Amazon EFS
D. Amazon S3


---------------------
Question 15
Organizers for a global event want to put daily reports online as static HTML pages. The pages are expected to generate millions of views from users around the world. The files are stored in an Amazon S3 bucket. A solutions architect has been asked to design an efficient and effective solution.Which action should the solutions architect take to accomplish this?

Answers
A. Generate presigned URLs for the files.
B. Use cross-Region replication to all Regions.
C. Use the geoproximity feature of Amazon Route 53.
D. Use Amazon CloudFront with the S3 bucket as its origin.


---------------------
Question 16
A solutions architect is designing a new service behind Amazon API Gateway. The request patterns for the service will be unpredictable and can change suddenly from 0 requests to over 500 per second. The total size of the data that needs to be persisted in a database is currently less than 1 GB with unpredictable future growth. Data can be queried using simple key-value requests.Which combination of AWS services would meet these requirements? (Choose two.)

Answers
A. AWS Fargate
B. AWS Lambda
C. Amazon DynamoDB
D. Amazon EC2 Auto Scaling
E. MySQL-compatible Amazon Aurora


---------------------
Question 17
A start-up company has a web application based in the us-east-1 Region with multiple Amazon EC2 instances running behind an Application Load Balancer across multiple Availability Zones. As the company's user base grows in the us-west-1 Region, it needs a solution with low latency and high availability.What should a solutions architect do to accomplish this?

Answers
A. Provision EC2 instances in us-west-1. Switch the Application Load Balancer to a Network Load Balancer to achieve cross-Region load balancing.
B. Provision EC2 instances and an Application Load Balancer in us-west-1. Make the load balancer distribute the traffic based on the location of the request.
C. Provision EC2 instances and configure an Application Load Balancer in us-west-1. Create an accelerator in AWS Global Accelerator that uses an endpoint group that includes the load balancer endpoints in both Regions.
D. Provision EC2 instances and configure an Application Load Balancer in us-west-1. Configure Amazon Route 53 with a weighted routing policy. Create alias records in Route 53 that point to the Application Load Balancer.


---------------------
Question 18
A solutions architect is designing a solution to access a catalog of images and provide users with the ability to submit requests to customize images. Image customization parameters will be in any request sent to an AWS API Gateway API. The customized image will be generated on demand, and users will receive a link they can click to view or download their customized image. The solution must be highly available for viewing and customizing images.What is the MOST cost-effective solution to meet these requirements?

Answers
A. Use Amazon EC2 instances to manipulate the original image into the requested customization Store the original and manipulated images in Amazon S3. Configure an Elastic Load Balancer in front of the EC2 instances.
B. Use AWS Lambda to manipulate the original image to the requested customization. Store the original and manipulated images in Amazon S3. Configure an Amazon CloudFront distribution with the S3 bucket as the origin.
C. Use AWS Lambda to manipulate the original image to the requested customization. Store the original images in Amazon S3 and the manipulated images in Amazon DynamoDB. Configure an Elastic Load Balancer in front of the Amazon EC2 instances.
D. Use Amazon EC2 instances to manipulate the original image into the requested customization. Store the original images in Amazon S3 and the manipulated images in Amazon DynamoDB. Configure an Amazon CloudFront distribution with the S3 bucket as the origin.


---------------------
Question 19
A company is planning to migrate a business-critical dataset to Amazon S3. The current solution design uses a single S3 bucket in the us-east-1 Region with versioning enabled to store the dataset. The company's disaster recovery policy states that all data multiple AWS Regions.How should a solutions architect design the S3 solution?

Answers
A. Create an additional S3 bucket in another Region and configure cross-Region replication.
B. Create an additional S3 bucket in another Region and configure cross-origin resource sharing (CORS).
C. Create an additional S3 bucket with versioning in another Region and configure cross-Region replication.
D. Create an additional S3 bucket with versioning in another Region and configure cross-origin resource (CORS).


---------------------
Question 20
A company has application running on Amazon EC2 instances in a VPC. One of the applications needs to call an Amazon S3 API to store and read objects. The company's security policies restrict any internet-bound traffic from the applications.Which action will fulfill these requirements and maintain security?

Answers
A. Configure an S3 interface endpoint.
B. Configure an S3 gateway endpoint.
C. Create an S3 bucket in a private subnet.
D. Create an S3 bucket in the same Region as the EC2 instance.


---------------------
Question 21
A company's web application uses an Amazon RDS PostgreSQL DB instance to store its application data. During the financial closing period at the start of every month. Accountants run large queries that impact the database's performance due to high usage. The company wants to minimize the impact that the reporting activity has on the web application.What should a solutions architect do to reduce the impact on the database with the LEAST amount of effort?

Answers
A. Create a read replica and direct reporting traffic to the replica.
B. Create a Multi-AZ database and direct reporting traffic to the standby.
C. Create a cross-Region read replica and direct reporting traffic to the replica.
D. Create an Amazon Redshift database and direct reporting traffic to the Amazon Redshift database.

---------------------
Question 22
A company wants to migrate a high performance computing (HPC) application and data from on-premises to the AWS Cloud. The company uses tiered storage on premises with hot high-performance parallel storage to support the application during periodic runs of the application, and more economical cold storage to hold the data when the application is not actively running.Which combination of solutions should a solutions architect recommend to support the storage needs of the application? (Choose two.)

Answers
A. Amazon S3 for cold data storage
B. Amazon EFS for cold data storage
C. Amazon S3 for high-performance parallel storage
D. Amazon FSx for Lustre for high-performance parallel storage
E. Amazon FSx for Windows for high-performance parallel storage

---------------------
Question 23
A company's application is running on Amazon EC2 instances in a single Region. In the event of a disaster, a solutions architect needs to ensure that the resources can also be deployed to a second Region.Which combination of actions should the solutions architect take to accomplish this? (Choose two.)

Answers
A. Detach a volume on an EC2 instance and copy it to Amazon S3.
B. Launch a new EC2 instance from an Amazon Machine Image (AMI) in a new Region.
C. Launch a new EC2 instance in a new Region and copy a volume from Amazon S3 to the new instance.
D. Copy an Amazon Machine Image (AMI) of an EC2 instance and specify a different Region for the destination.
E. Copy an Amazon Elastic Block Store (Amazon EBS) volume from Amazon S3 and launch an EC2 instance in the destination Region using that EBS volume.

---------------------
Question 24
A solutions architect needs to ensure that API calls to Amazon DynamoDB from Amazon EC2 instances in a VPC do not traverse the internet.What should the solutions architect do to accomplish this? (Choose two.)

Answers
A. Create a route table entry for the endpoint.
B. Create a gateway endpoint for DynamoDB.
C. Create a new DynamoDB table that uses the endpoint.
D. Create an ENI for the endpoint in each of the subnets of the VPC.
E. Create a security group entry in the default security group to provide access.


---------------------
Question 25
A company's legacy application is currently relying on a single-instance Amazon RDS MySQL database without encryption. Due to new compliance requirements, all existing and new data in this database must be encrypted.How should this be accomplished?

Answers
A. Create an Amazon S3 bucket with server-side encryption enabled. Move all the data to Amazon S3. Delete the RDS instance.
B. Enable RDS Multi-AZ mode with encryption at rest enabled. Perform a failover to the standby instance.
C. Take a Snapshot of the RDS instance. Create an encrypted copy of the snapshot. Restore the RDS instance from the encrypted snapshot.
D. Create an RDS read replica with encryption at rest enabled. Promote the read replica to master and switch the over to the new master. Delete the old RDS instance.

---------------------
Question 26
A manufacturing company wants to implement predictive maintenance on its machinery equipment. The company will install thousands of IoT sensors that will send data to AWS in real time. A solutions architect is tasked with implementing a solution that will receive events in an ordered manner for each machinery asset and ensure that data is saved for further processing at a later time.Which solution would be MOST efficient?

Answers
A. Use Amazon Kinesis Data Streams for real-time events with a partition for each equipment asset. Use Amazon Kinesis Data Firehose to save data to Amazon S3.
B. Use Amazon Kinesis Data Streams for real-time events with a shard for each equipment asset. Use Amazon Kinesis Data Firehose to save data to Amazon EBS.
C. Use an Amazon SQS FIFO queue for real-time events with one queue for each equipment asset. Trigger an AWS Lambda function for the SQS queue to save data to Amazon EFS.
D. Use an Amazon SQS standard queue for real-time events with one queue for each equipment asset. Trigger an AWS Lambda function from the SQS queue to save data to Amazon S3.


---------------------
Question 27
A company's website runs on Amazon EC2 instances behind an Application Load Balancer (ALB). The website has a mix of dynamic and static content. Users around the globe are reporting that the website is slow.Which set of actions will improve website performance for users worldwide?

Answers
A. Create an Amazon CloudFront distribution and configure the ALB as an origin. Then update the Amazon Route 53 record to point to the CloudFront distribution.
B. Create a latency-based Amazon Route 53 record for the ALB. Then launch new EC2 instances with larger instance sizes and register the instances with the ALB.
C. Launch new EC2 instances hosting the same web application in different Regions closer to the users. Then register instances with the same ALB using cross- Region VPC peering.
D. Host the website in an Amazon S3 bucket in the Regions closest to the users and delete the ALB and EC2 instances. Then update an Amazon Route 53 record to point to the S3 buckets.


---------------------
Question 28
A company has been storing analytics data in an Amazon RDS instance for the past few years. The company asked a solutions architect to find a solution that allows users to access this data using an API. The expectation is that the application will experience periods of inactivity but could receive bursts of traffic within seconds.Which solution should the solutions architect suggest?

Answers
A. Set up an Amazon API Gateway and use Amazon ECS.
B. Set up an Amazon API Gateway and use AWS Elastic Beanstalk.
C. Set up an Amazon API Gateway and use AWS Lambda functions.
D. Set up an Amazon API Gateway and use Amazon EC2 with Auto Scaling.


---------------------
Question 29
A company must generate sales reports at the beginning of every month. The reporting process launches 20 Amazon EC2 instances on the first of the month. The process runs for 7 days and cannot be interrupted. The company wants to minimize costs.Which pricing model should the company choose?

Answers
A. Reserved Instances
B. Spot Block Instances
C. On-Demand Instances
D. Scheduled Reserved Instances

---------------------
Question 30
A gaming company has multiple Amazon EC2 instances in a single Availability Zone for its multiplayer game that communicates with users on Layer 4. The chief technology officer (CTO) wants to make the architecture highly available and cost-effective.Which should a solutions architect do to meet these requirements? (Choose two.)?

Answers
A. Increase the number of EC2 instances.
B. Decrease the number of EC2 instances.
C. Configure a Network Load Balancer in front of the EC2 instances.
D. Configure an Application Load Balancer in front of the EC2 instances.
E. Configure an Auto Scaling group to add or remove instances in multiple Availability Zones automatically.

---------------------
Question 31
A company currently operates a web application backed by an Amazon RDS MySQL database. It has automated backups that are run daily and are not encrypted. A security audit requires future backups to be encrypted and the unencrypted backups to be destroyed. The company will make at least one encrypted backup before destroying the old backups.What should be done to enable encryption for future backups?

Answers
A. Enable default encryption for the Amazon S3 bucket where backups are stored.
B. Modify the backup section of the database configuration to toggle the Enable encryption check box.
C. Create a snapshot of the database. Copy it to an encrypted snapshot. Restore the database from the encrypted snapshot.
D. Enable an encrypted read replica on RDS for MySQL. Promote the encrypted read replica to primary. Remove the original database instance.


---------------------
Question 32
A company is hosting a website behind multiple Application Load Balancers. The company has different distribution rights for its content around the world. A solutions architect needs to ensure that users are served the correct content without violating distribution rights.Which configuration should the solutions architect choose to meet these requirements?

Answers
A. Configure Amazon CloudFront with AWS WAF.
B. Configure Application Load Balancers with AWS WAF.
C. Configure Amazon Route 53 with a geolocation policy.
D. Configure Amazon Route 53 with a geoproximity routing policy.


---------------------
Question 33
A solution architect has created a new AWS account and must secure AWS account root user access.Which combination of actions will accomplish this? (Choose two.)

Answers
A. Ensure the root user uses a strong password.
B. Enable multi-factor authentication to the root user.
C. Store root user access keys in an encrypted Amazon S3 bucket.
D. Add the root user to a group containing administrative permissions.
E. Apply the required permissions to the root user with an inline policy document.


---------------------
Question 34
A solutions architect at an ecommerce company wants to back up application log data to Amazon S3. The solutions architect is unsure how frequently the logs will be accessed or which logs will be accessed the most. The company wants to keep costs as low as possible by using the appropriate S3 storage class.Which S3 storage class should be implemented to meet these requirements?

Answers
A. S3 Glacier
B. S3 Intelligent-Tiering
C. S3 Standard-Infrequent Access (S3 Standard-IA)
D. S3 One Zone-Infrequent Access (S3 One Zone-IA)


---------------------
Question 35
A company's website is used to sell products to the public. The site runs on Amazon EC2 instances in an Auto Scaling group behind an Application Load Balancer(ALB). There is also an Amazon CloudFront distribution, and AWS WAF is being used to protect against SQL injection attacks. The ALB is the origin for theCloudFront distribution. A recent review of security logs revealed an external malicious IP that needs to be blocked from accessing the website.What should a solutions architect do to protect the application?

Answers
A. Modify the network ACL on the CloudFront distribution to add a deny rule for the malicious IP address.
B. Modify the configuration of AWS WAF to add an IP match condition to block the malicious IP address.
C. Modify the network ACL for the EC2 instances in the target groups behind the ALB to deny the malicious IP address.
D. Modify the security groups for the EC2 instances in the target groups behind the ALB to deny the malicious IP address.

---------------------
Question 36
A solutions architect is designing an application for a two-step order process. The first step is synchronous and must return to the user with little latency. The second step takes longer, so it will be implemented in a separate component. Orders must be processed exactly once and in the order in which they are received.How should the solutions architect integrate these components?

Answers
A. Use Amazon SQS FIFO queues.
B. Use an AWS Lambda function along with Amazon SQS standard queues.
C. Create an SNS topic and subscribe an Amazon SQS FIFO queue to that topic.
D. Create an SNS topic and subscribe an Amazon SQS Standard queue to that topic.


---------------------
Question 37
A web application is deployed in the AWS Cloud. It consists of a two-tier architecture that includes a web layer and a database layer. The web server is vulnerable to cross-site scripting (XSS) attacks.What should a solutions architect do to remediate the vulnerability?

Answers
A. Create a Classic Load Balancer. Put the web layer behind the load balancer and enable AWS WAF.
B. Create a Network Load Balancer. Put the web layer behind the load balancer and enable AWS WAF.
C. Create an Application Load Balancer. Put the web layer behind the load balancer and enable AWS WAF.
D. Create an Application Load Balancer. Put the web layer behind the load balancer and use AWS Shield Standard.


---------------------
Question 38
A company's website is using an Amazon RDS MySQL Multi-AZ DB instance for its transactional data storage. There are other internal systems that query this DB instance to fetch data for internal batch processing. The RDS DB instance slows down significantly the internal systems fetch data. This impacts the website's read and write performance, and the users experience slow response times.Which solution will improve the website's performance?

Answers
A. Use an RDS PostgreSQL DB instance instead of a MySQL database.
B. Use Amazon ElastiCache to cache the query responses for the website.
C. Add an additional Availability Zone to the current RDS MySQL Multi.AZ DB instance.
D. Add a read replica to the RDS DB instance and configure the internal systems to query the read replica.


---------------------
Question 39
An application runs on Amazon EC2 instances across multiple Availability Zones. The instances run in an Amazon EC2 Auto Scaling group behind an ApplicationLoad Balancer. The application performs best when the CPU utilization of the EC2 instances is at or near 40%.What should a solutions architect do to maintain the desired performance across all instances in the group?

Answers
A. Use a simple scaling policy to dynamically scale the Auto Scaling group.
B. Use a target tracking policy to dynamically scale the Auto Scaling group.
C. Use an AWS Lambda function to update the desired Auto Scaling group capacity.
D. Use scheduled scaling actions to scale up and scale down the Auto Scaling group.

---------------------
Question 40
A company runs an internal browser-based application. The application runs on Amazon EC2 instances behind an Application Load Balancer. The instances run in an Amazon EC2 Auto Scaling group across multiple Availability Zones. The Auto Scaling group scales up to 20 instances during work hours, but scales down to2 instances overnight. Staff are complaining that the application is very slow when the day begins, although it runs well by mid-morning.How should the scaling be changed to address the staff complaints and keep costs to a minimum?

Answers
A. Implement a scheduled action that sets the desired capacity to 20 shortly before the office opens.
B. Implement a step scaling action triggered at a lower CPU threshold, and decrease the cooldown period.
C. Implement a target tracking action triggered at a lower CPU threshold, and decrease the cooldown period.
D. Implement a scheduled action that sets the minimum and maximum capacity to 20 shortly before the office opens.


---------------------
Question 41
A financial services company has a web application that serves users in the United States and Europe. The application consists of a database tier and a web server tier. The database tier consists of a MySQL database hosted in us-east-1. Amazon Route 53 geoproximity routing is used to direct traffic to instances in the closest Region. A performance review of the system reveals that European users are not receiving the same level of query performance as those in the UnitedStates.Which changes should be made to the database tier to improve performance?

Answers
A. Migrate the database to Amazon RDS for MySQL. Configure Multi-AZ in one of the European Regions.
B. Migrate the database to Amazon DynamoDB. Use DynamoDB global tables to enable replication to additional Regions.
C. Deploy MySQL instances in each Region. Deploy an Application Load Balancer in front of MySQL to reduce the load on the primary instance.
D. Migrate the database to an Amazon Aurora global database in MySQL compatibility mode. Configure read replicas in one of the European Regions.


---------------------
Question 42
A company hosts a static website on-premises and wants to migrate the website to AWS. The website should load as quickly as possible for users around the world. The company also wants the most cost-effective solution.What should a solutions architect do to accomplish this?

Answers
A. Copy the website content to an Amazon S3 bucket. Configure the bucket to serve static webpage content. Replicate the S3 bucket to multiple AWS Regions.
B. Copy the website content to an Amazon S3 bucket. Configure the bucket to serve static webpage content. Configure Amazon CloudFront with the S3 bucket as the origin.
C. Copy the website content to an Amazon EBS-backed Amazon EC2 instance running Apache HTTP Server. Configure Amazon Route 53 geolocation routing policies to select the closest origin.
D. Copy the website content to multiple Amazon EBS-backed Amazon EC2 instances running Apache HTTP Server in multiple AWS Regions. Configure Amazon CloudFront geolocation routing policies to select the closest origin.


---------------------
Question 43
A solutions architect is designing storage for a high performance computing (HPC) environment based on Amazon Linux. The workload stores and processes a large amount of engineering drawings that require shared storage and heavy computing.Which storage option would be the optimal solution?

Answers
A. Amazon Elastic File System (Amazon EFS)
B. Amazon FSx for Lustre
C. Amazon EC2 instance store
D. Amazon EBS Provisioned IOPS SSD (io1)


---------------------
Question 44
A company is performing an AWS Well-Architected Framework review of an existing workload deployed on AWS. The review identified a public-facing website running on the same Amazon EC2 instance as a Microsoft Active Directory domain controller that was install recently to support other AWS services. A solutions architect needs to recommend a new design that would improve the security of the architecture and minimize the administrative demand on IT staff.What should the solutions architect recommend?

Answers
A. Use AWS Directory Service to create a managed Active Directory. Uninstall Active Directory on the current EC2 instance.
B. Create another EC2 instance in the same subnet and reinstall Active Directory on it. Uninstall Active Directory.
C. Use AWS Directory Service to create an Active Directory connector. Proxy Active Directory requests to the Active domain controller running on the current EC2 instance.
D. Enable AWS Single Sign-On (AWS SSO) with Security Assertion Markup Language (SAML) 2.0 federation with the current Active Directory controller. Modify the EC2 instance's security group to deny public access to Active Directory.


---------------------
Question 45
A company hosts a static website within an Amazon S3 bucket. A solutions architect needs to ensure that data can be recovered in case of accidental deletion.Which action will accomplish this?

Answers
A. Enable Amazon S3 versioning.
B. Enable Amazon S3 Intelligent-Tiering.
C. Enable an Amazon S3 lifecycle policy.
D. Enable Amazon S3 cross-Region replication.


---------------------
Question 46
A company's production application runs online transaction processing (OLTP) transactions on an Amazon RDS MySQL DB instance. The company is launching a new reporting tool that will access the same data. The reporting tool must be highly available and not impact the performance of the production application.How can this be achieved?

Answers
A. Create hourly snapshots of the production RDS DB instance.
B. Create a Multi-AZ RDS Read Replica of the production RDS DB instance.
C. Create multiple ROS Read Replicas of the production RDS DB instance. Place the Read Replicas in an Auto Scaling group.
D. Create a Single-AZ RDS Read Replica of the production RDS DB instance. Create a second Single-AZ RDS Read Replica from the replica.


---------------------
Question 47
A company runs an application in a branch office within a small data closet with no virtualized compute resources. The application data is stored on an NFS volume. Compliance standards require a daily offsite backup of the NFS volume.Which solution meet these requirements?

Answers
A. Install an AWS Storage Gateway file gateway on premises to replicate the data to Amazon S3.
B. Install an AWS Storage Gateway file gateway hardware appliance on premises to replicate the data to Amazon S3.
C. Install an AWS Storage Gateway volume gateway with stored volumes on premises to replicate the data to Amazon S3.
D. Install an AWS Storage Gateway volume gateway with cached volumes on premises to replicate the data to Amazon S3.


---------------------
Question 48
A company's web application is using multiple Linux Amazon EC2 instances and storing data on Amazon EBS volumes. The company is looking for a solution to increase the resiliency of the application in case of a failure and to provide storage that complies with atomicity, consistency, isolation, and durability (ACID).What should a solutions architect do to meet these requirements?

Answers
A. Launch the application on EC2 instances in each Availability Zone. Attach EBS volumes to each EC2 instance.
B. Create an Application Load Balancer with Auto Scaling groups across multiple Availability Zones. Mount an instance store on each EC2 instance.
C. Create an Application Load Balancer with Auto Scaling groups across multiple Availability Zones. Store data on Amazon EFS and mount a target on each instance.
D. Create an Application Load Balancer with Auto Scaling groups across multiple Availability Zones. Store data using Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA).


---------------------
Question 49
A security team to limit access to specific services or actions in all of the team's AWS accounts. All accounts belong to a large organization in AWS Organizations.The solution must be scalable and there must be a single point where permission can be maintained.What should a solutions architect do to accomplish this?

Answers
A. Create an ACL to provide access to the services or actions.
B. Create a security group to allow accounts and attach it to user groups.
C. Create cross-account roles in each account to deny access to the services or actions.
D. Create a service control policy in the root organizational unit to deny access to the services or actions.

---------------------
Question 50
A data science team requires storage for nightly log processing. The size and number of logs is unknown and will persist for 24 hours only.What is the MOST cost-effective solution?

Answers
A. Amazon S3 Glacier
B. Amazon S3 Standard
C. Amazon S3 Intelligent-Tiering
D. Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA)


---------------------
Question 51
A company is hosting a web application on AWS using a single Amazon EC2 instance that stores user-uploaded documents in an Amazon EBS volume. For better scalability and availability, the company duplicated the architecture and created a second EC2 instance and EBS volume in another Availability Zone, placing both behind an Application Load Balancer. After completing this change, users reported that, each time they refreshed the website, they could see one subset of their documents or the other, but never all of the documents at the same time.What should a solutions architect propose to ensure users see all of their documents at once?

Answers
A. Copy the data so both EBS volumes contain all the documents.
B. Configure the Application Load Balancer to direct a user to the server with the documents.
C. Copy the data from both EBS volumes to Amazon EFS. Modify the application to save new documents to Amazon EFS.
D. Configure the Application Load Balancer to send the request to both servers. Return each document from the correct server.

---------------------
Question 52
A company is planning to use Amazon S3 to store images uploaded by its users. The images must be encrypted at rest in Amazon S3. The company does not want to spend time managing and rotating the keys, but it does want to control who can access those keys.What should a solutions architect use to accomplish this?

Answers
A. Server-Side Encryption with keys stored in an S3 bucket
B. Server-Side Encryption with Customer-Provided Keys (SSE-C)
C. Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)
D. Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS)


---------------------
Question 53
A company is running an ecommerce application on Amazon EC2. The application consists of a stateless web tier that requires a minimum of 10 instances, and a peak of 250 instances to support the application's usage. The application requires 50 instances 80% of the time.Which solution should be used to minimize costs?

Answers
A. Purchase Reserved Instances to cover 250 instances.
B. Purchase Reserved Instances to cover 80 instances. Use Spot Instances to cover the remaining instances.
C. Purchase On-Demand Instances to cover 40 instances. Use Spot Instances to cover the remaining instances.
D. Purchase Reserved Instances to cover 50 instances. Use On-Demand and Spot Instances to cover the remaining instances.


---------------------
Question 54
A company has deployed an API in a VPC behind an internet-facing Application Load Balancer (ALB). An application that consumes the API as a client is deployed in a second account in private subnets behind a NAT gateway. When requests to the client application increase, the NAT gateway costs are higher than expected. A solutions architect has configured the ALB to be internal.Which combination of architectural changes will reduce the NAT gateway costs? (Choose two.)

Answers
A. Configure a VPC peering connection between the two VPCs. Access the API using the private address.
B. Configure an AWS Direct Connect connection between the two VPCs. Access the API using the private address.
C. Configure a ClassicLink connection for the API into the client VPC. Access the API using the ClassicLink address.
D. Configure a PrivateLink connection for the API into the client VPC. Access the API using the PrivateLink address.
E. Configure an AWS Resource Access Manager connection between the two accounts. Access the API using the private address.


---------------------
Question 55
A solutions architect is tasked with transferring 750 TB of data from a network-attached file system located at a branch office Amazon S3 Glacier. The solution must avoid saturating the branch office's low-bandwidth internet connection.What is the MOST cost-effective solution?

Answers
A. Create a site-to-site VPN tunnel to an Amazon S3 bucket and transfer the files directly. Create a bucket VPC endpoint.
B. Order 10 AWS Snowball appliances and select an S3 Glacier vault as the destination. Create a bucket policy to enforce VPC endpoint.
C. Mount the network-attached file system to Amazon S3 and copy the files directly. Create a lifecycle policy to S3 objects to Amazon S3 Glacier.
D. Order 10 AWS Snowball appliances and select an Amazon S3 bucket as the destination. Create a lifecycle policy to transition the S3 objects to Amazon S3 Glacier.


---------------------
Question 56
A company has a two-tier application architecture that runs in public and private subnets. Amazon EC2 instances running the web application are in the public subnet and a database runs on the private subnet. The web application instances and the database are running in a single Availability Zone (AZ).Which combination of steps should a solutions architect take to provide high availability for this architecture? (Choose two.)

Answers
A. Create new public and private subnets in the same AZ for high availability.
B. Create an Amazon EC2 Auto Scaling group and Application Load Balancer spanning multiple AZs.
C. Add the existing web application instances to an Auto Scaling group behind an Application Load Balancer.
D. Create new public and private subnets in a new AZ. Create a database using Amazon EC2 in one AZ.
E. Create new public and private subnets in the same VPC, each in a new AZ. Migrate the database to an Amazon RDS multi-AZ deployment.


---------------------
Question 57
A solutions architect is implementing a document review application using an Amazon S3 bucket for storage. The solution must prevent an accidental deletion of the documents and ensure that all versions of the documents are available. Users must be able to download, modify, and upload documents.Which combination of actions should be taken to meet these requirements? (Choose two.)

Answers
A. Enable a read-only bucket ACL.
B. Enable versioning on the bucket.
C. Attach an IAM policy to the bucket.
D. Enable MFA Delete on the bucket.
E. Encrypt the bucket using AWS KMS.


---------------------
Question 58
An application hosted on AWS is experiencing performance problems, and the application vendor wants to perform an analysis of the log file to troubleshoot further. The log file is stored on Amazon S3 and is 10 GB in size. The application owner will make the log file available to the vendor for a limited time.What is the MOST secure way to do this?

Answers
A. Enable public read on the S3 object and provide the link to the vendor.
B. Upload the file to Amazon WorkDocs and share the public link with the vendor.
C. Generate a presigned URL and have the vendor download the log file before it expires.
D. Create an IAM user for the vendor to provide access to the S3 bucket and the application. Enforce multi-factor authentication.


---------------------
Question 59
A solutions architect is designing a two-tier web application. The application consists of a public-facing web tier hosted on Amazon EC2 in public subnets. The database tier consists of Microsoft SQL Server running on Amazon EC2 in a private subnet. Security is a high priority for the company.How should security groups be configured in this situation? (Choose two.)

Answers
A. Configure the security group for the web tier to allow inbound traffic on port 443 from 0.0.0.0/0. B. Configure the security group for the web tier to allow outbound traffic on port 443 from 0.0.0.0/0.
B. Configure the security group for the database tier to allow inbound traffic on port 1433 from the security group for the web tier.
C. Configure the security group for the database tier to allow outbound traffic on ports 443 and 1433 to the security group for the web tier.
D. Configure the security group for the database tier to allow inbound traffic on ports 443 and 1433 from the security group for the web tier.

---------------------
Question 60
A company allows its developers to attach existing IAM policies to existing IAM roles to enable faster experimentation and agility. However, the security operations team is concerned that the developers could attach the existing administrator policy, when would allow the developers to circumvent any other security policies.How should a solutions architect address this issue?

Answers
A. Create an Amazon SNS topic to send an alert every time a developer creates a new policy.
B. Use service control policies to disable IAM activity across all account in the organizational unit.
C. Prevent the developers from attaching any policies and assign all IAM duties to the security operations team.
D. Set an IAM permissions boundary on the developer IAM role that explicitly denies attaching the administrator policy.


---------------------
Question 61
A company has a multi-tier application that runs six front-end web servers in an Amazon EC2 Auto Scaling group in a single Availability Zone behind anApplication Load Balancer (ALB). A solutions architect needs to modify the infrastructure to be highly available without modifying the application.Which architecture should the solutions architect choose that provides high availability?

Answers
A. Create an Auto Scaling group that uses three instances across each of two Regions.
B. Modify the Auto Scaling group to use three instances across each of two Availability Zones.
C. Create an Auto Scaling template that can be used to quickly create more instances in another Region.
D. Change the ALB in front of the Amazon EC2 instances in a round-robin configuration to balance traffic to the web tier.

---------------------
Question 62
A company runs an application on a group of Amazon Linux EC2 instances. The application writes log files using standard API calls. For compliance reasons, all log files must be retained indefinitely and will be analyzed by a reporting tool that must access all files concurrently.Which storage service should a solutions architect use to provide the MOST cost-effective solution?

Answers
A. Amazon EBS
B. Amazon EFS
C. Amazon EC2 instance store
D. Amazon S3

---------------------
Question 63
A media streaming company collects real-time data and stores it in a disk-optimized database system. The company is not getting the expected throughput and wants an in-memory database storage solution that performs faster and provides high availability using data replication.Which database should a solutions architect recommend?

Answers
A. Amazon RDS for MySQL
B. Amazon RDS for PostgreSQL.
C. Amazon ElastiCache for Redis
D. Amazon ElastiCache for Memcached


---------------------
Question 64
A company hosts its product information webpages on AWS. The existing solution uses multiple Amazon C2 instances behind an Application Load Balancer in anAuto Scaling group. The website also uses a custom DNS name and communicates with HTTPS only using a dedicated SSL certificate. The company is planning a new product launch and wants to be sure that users from around the world have the best possible experience on the new website.What should a solutions architect do to meet these requirements?

Answers
A. Redesign the application to use Amazon CloudFront.
B. Redesign the application to use AWS Elastic Beanstalk.
C. Redesign the application to use a Network Load Balancer.
D. Redesign the application to use Amazon S3 static website hosting.


---------------------
Question 65
A solutions architect is designing the cloud architecture for a new application being deployed on AWS. The process should run in parallel while adding and removing application nodes as needed based on the number of jobs to be processed. The processor application is stateless. The solutions architect must ensure that the application is loosely coupled and the job items are durably stored.Which design should the solutions architect use?

Answers
A. Create an Amazon SNS topic to send the jobs that need to be processed. Create an Amazon Machine Image (AMI) that consists of the processor application. Create a launch configuration that uses the AMI. Create an Auto Scaling group using the launch configuration. Set the scaling policy for the Auto Scaling group to add and remove nodes based on CPU usage.
B. Create an Amazon SQS queue to hold the jobs that need to be processed. Create an Amazon Machine Image (AMI) that consists of the processor application. Create a launch configuration that uses the AMI. Create an Auto Scaling group using the launch configuration. Set the scaling policy for the Auto Scaling group to add and remove nodes based on network usage.
C. Create an Amazon SQS queue to hold the jobs that need to be processed. Create an Amazon Machine Image (AMI) that consists of the processor application. Create a launch template that uses the AMI. Create an Auto Scaling group using the launch template. Set the scaling policy for the Auto Scaling group to add and remove nodes based on the number of items in the SQS queue.
D. Create an Amazon SNS topic to send the jobs that need to be processed. Create an Amazon Machine Image (AMI) that consists of the processor application. Create a launch template that uses the AMI. Create an Auto Scaling group using the launch template. Set the scaling policy for the Auto Scaling group to add and remove nodes based on the number of messages published to the SNS topic.