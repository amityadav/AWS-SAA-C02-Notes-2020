# CHAPTER 4 | EC2 The Backbone of AWS

## EC2

### [What's EC2](https://aws.amazon.com/ec2/)

Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers.

### [EC2 Options](https://aws.amazon.com/ec2/pricing/)

* [On demand](https://aws.amazon.com/ec2/pricing/on-demand/): 
    - Users who wants the low cost & flexibility of Amazon Ec2 without any upfront payment or long-term commitment
    - Applications with short-term, spiky or unpredictable load that connot be interrupted
    - Applications being developed or tested for the first time on EC2
    - You pay for computing capacity by per hour or per second depending on which instances you run.
* [Reserved Instance (RI)](https://aws.amazon.com/ec2/pricing/reserved-instances/): 
    - Applications who have predictable loads or steady state
    - Provide a significant discount (up to 75%) compared to On-Demand pricing and provide a capacity reservation when used in a specific Availability Zone. You have to enter a contract.
        * Standard Reserved Instances - Payupfront abd long tern contract
        * Convertible Reserved Instances - Capability to change the attributes of RI as long as the exchange results in the cerations of RI's equal or greater value
        * Scheduled Reserved Instances - Available to launch within the time windows you reserved
* [Spot](https://aws.amazon.com/ec2/spot/): Amazon EC2 Spot instances allow you to request spare Amazon EC2 computing capacity for up to 90% off the On-Demand price.

  * If you terminate an instance, you will pay for the complete hour.
  * If Amazon terminates the instance, you won't pay for the complete hour.
  * The following are the possible reasons that Amazon EC2 might [interrupt your Spot Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-interruptions.html):
    * Price – The Spot price is greater than your maximum price.
    * Capacity – If there are not enough unused EC2 instances to meet the demand for Spot Instances, Amazon EC2 interrupts Spot Instances. The order in which the instances are interrupted is determined by Amazon EC2.
    * Constraints – If your request includes a constraint such as a launch group or an Availability Zone group, these Spot Instances are terminated as a group when the constraint can no longer be met.



* [Dedicated Hosts](https://aws.amazon.com/ec2/dedicated-hosts/): 
  - Is a physical server with EC2 instance capacity fully dedicated to your use.
  - Useful for regulatory requirements
  - Can be purchased on-demand
  - Great for licencing which does not support multi-tenancy or cloud deployments

### [What's EBS](https://aws.amazon.com/ebs/)

Provides persistent block storage volumes for use with Amazon EC2 instances in the AWS Cloud. EBS is automatically replicated within its AZ

### [Amazon EBS Volume Types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumeTypes.html)

#### SSD

SSD are good for random access.

* General Purpose SSD (GP2): General purpose SSD volume that balances price and performance. 3 [IOPS](https://en.wikipedia.org/wiki/IOPS) per GB, up to 10k IOPS
* Provisioned IOPS SSD (io1): Designed for IO intensive, use it if you need more than 10k IOPS

#### HDD (Magnetic)

Are great for sequential access (processing log files, bigdata work flows as an example).

* Throughput Optimized HDD (st1): Magnetic disk, this can't be a boot volume (root volume).
* Cold HDD (sc1): Lower cost storage, like file servers, can't be a boot volume.
* Magnetic (standard): Lowest cost per gigabyte of all EBS. It's bootable and it's from the previous storage generation.

|                                |                                                                                                              | Solid State Drives (SSD)                                                              | Hard Disk Drives (HDD)                                                                                   |                                                                                      |                                                                        |
|--------------------------------|--------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| Volume Type                    | EBS Provisioned IOPS SSD (io2)                                                                               | EBS Provisioned IOPS SSD (io1)                                                        | EBS General Purpose SSD (gp2)*                                                                           | Throughput Optimized HDD (st1)                                                       | Cold HDD (sc1)                                                         |
| Short Description              | Highest performance and highest durability SSD volume designed for latency-sensitive transactional workloads | Highest performance SSD volume designed for latency-sensitive transactional workloads | General Purpose SSD volume that balances price performance for a wide variety of transactional workloads | Low cost HDD volume designed for frequently accessed, throughput intensive workloads | Lowest cost HDD volume designed for less frequently accessed workloads |
| Durability                     | 100.00%                                                                                                      | 99.8% - 99.9% durability                                                              | 99.8% - 99.9% durability                                                                                 | 99.8% - 99.9% durability                                                             | 99.8% - 99.9% durability                                               |
| Use Cases                      | I/O-intensive NoSQL and relational databases                                                                 | I/O-intensive NoSQL and relational databases                                          | Boot volumes, low-latency interactive apps, dev and test                                                 | Big data, data warehouses, log processing                                            | Colder data requiring fewer scans per day                              |
| API Name                       | io2                                                                                                          | io1                                                                                   | gp2                                                                                                      | st1                                                                                  | sc1                                                                    |
| Volume Size                    | 4 GB – 16 TB                                                                                                 | 4 GB - 16 TB                                                                          | 1 GB - 16 TB                                                                                             | 500 GB - 16 TB                                                                       | 500 GB - 16 TB                                                         |
| Max IOPS**/Volume              | 64,000                                                                                                       | 64,000                                                                                | 16,000                                                                                                   | 500                                                                                  | 250                                                                    |
| Max Throughput***/Volume       | 1,000 MB/s                                                                                                   | 1,000 MB/s                                                                            | 250 MB/s                                                                                                 | 500 MB/s                                                                             | 250 MB/s                                                               |
| Max IOPS/Instance              | 160,000                                                                                                      | 160,000                                                                               | 160,000                                                                                                  | 160,000                                                                              | 160,000                                                                |
| Max Throughput/Instance        | 4,750 MB/s                                                                                                   | 4,750 MB/s                                                                            | 4,750 MB/s                                                                                               | 4,750 MB/s                                                                           | 4,750 MB/s                                                             |
| Price                          | $0.125/GB-month                                                                                              | $0.125/GB-month                                                                       | $0.10/GB-month                                                                                           | $0.045/GB-month                                                                      | $0.025/GB-month                                                        |
|                                |                                                                                                              |                                                                                       |                                                                                                          |                                                                                      |                                                                        |
|                                | $0.065/provisioned IOPS                                                                                      | $0.065/provisioned IOPS                                                               |                                                                                                          |                                                                                      |                                                                        |
| Dominant Performance Attribute | IOPS and volume durability                                                                                   | IOPS                                                                                  | IOPS                                                                                                     | MB/s                                                                                 | MB/s                                                                   |




* Termination Protection is turned off byt default
* On an EBS backed instance, the default action is for the root EBS volumen to be deleted when the instance is terminated
* EBS Root volume of the default AMI's can be encrypted. You can also use third party tools like Bitlocker to encrypt the root volume or can also be done while creating the AMI's in the AWS console or by using API's
* Additional volums can be encrypted


### [RAID Arrays using EBS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/raid-config.html)

As you would do in a bare-metal server, you can also create [RAID](https://en.wikipedia.org/wiki/RAID) arrays within AWS EC2 boxes using EBS volumes.

* Remeber that the RAID available in AWS is only **software**
* You can have two types of RAID:

  * [RAID 0](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_0) – splits ("stripes") data evenly across two or more disks. When I/O performance is more important than fault tolerance; for example, as in a heavily used database (where data replication is already set up separately). You can use RAID 0 configurations in scenarios where you are using heavy databases with perhaps mirroring and replication.
  * [RAID 1](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_1) – consists of an exact copy (or mirror) of a set of data on two or more disks. When fault tolerance is more important than I/O performance; for example, as in a critical application. With RAID 1 you get more data durability in addition to the replication features of the AWS cloud.
  * RAID 5 and RAID 6 are not recommended for Amazon EBS because the parity write operations of these RAID modes consume some of the IOPS available to your volumes. Depending on the configuration of your RAID array, these RAID modes provide 20-30% fewer usable IOPS than a RAID 0 configuration. Increased cost is a factor with these RAID modes as well; when using identical volume sizes and speeds, a 2-volume RAID 0 array can outperform a 4-volume RAID 6 array that costs twice as much.

Remember also that you can create [snapshots of your RAID arrays](https://aws.amazon.com/premiumsupport/knowledge-center/snapshot-ebs-raid-array/)

### Launch an EC2 Instance - Lab

* Termination protection is turned off by default.
* The EBS root volume by default is deleted at termination.
* Default AMI's (provided by Amazon) can be encrypted.
* Additional volumes can be encrypted.

## Security groups - Lab

### [What's a security group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)

A security group acts as a virtual firewall for your instance to control inbound and outbound traffic.

* All Inbound traffic is Blocked by Default.
* All Outbound traffic is Blocked by Default.
* All security groups changes are applied immediately.
* Security groups are stateful. For example, if you allow the request to come in, automatically responses can go out even if you don't have anything on the outbound section of your security group.
* You can specify only allow rules, not deny rules.
* You can add multiple security groups to the same EC2 instance
* You can also attach same security groups to multiple EC2 instances

## EBS Volumes & Encrypt Root Device Volume - Lab

* Instances and Volumes MUST be in the same AZ
* Snapshots exists in S3.
* Snapshots are a point in time copies of Volumes.
* Snapshots are incremental (only differences are saved)
* Snapshot of root volumes require the instance to be stopped.
* _You can't delete a snapshot of an EBS volume that is used as the root device of a registered AMI._
* You can change EBS volumes size and type on the fly.
* To move an EC2 volume from one AZ/Region to another, take a snap or an image of it, then you can copy them to the new AZ/Region.
* Snapshots of encrypted volumes are encrypted automatically
* Volumes restored from an encrypted snapshot will be encrypted as well.
* You can share snapshots only if they are not encrypted, these snapshots can be made public.

### [AMI - Amazon Machine Image](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)
An Amazon Machine Image (AMI) provides the information required to launch an instance. You must specify an AMI when you launch an instance. You can launch multiple instances from a single AMI when you need multiple instances with the same configuration. You can use different AMIs to launch instances when you need instances with different configurations.

An AMI includes the following:

 - One or more EBS snapshots, or, for instance-store-backed AMIs, a template for the root volume of the instance (for example, an operating system, an application server, and applications).

 - Launch permissions that control which AWS accounts can use the AMI to launch instances.

 - A block device mapping that specifies the volumes to attach to the instance when it's launched.

* ![Using an AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/ami_lifecycle.png)

### [AMI Types](https://aws.amazon.com/amazon-linux-ami/instance-type-matrix/)

* [EBS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html): Amazon EBS provides durable, block-level storage volumes that you can attach to a running instance
  * EBS takes less time to provision.
  * EBS volumes can be kept once the instance is terminated.
* [Instance Store / Ephemeral storage](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html): This storage is located on disks that are physically attached to the host computer

  * Instance Store Volumes can't be stopped, if the host fails, you lose data.
  * You can reboot the instance without losing data.
  * You can not detach Instance Store Volumes.
  * Instance store volumes cannot be kept once the instance is terminated.

 - For EBs Volums: The root device for an instance launched from the AMIis an Amazon EBS volume created from an Amazon EBS snapshot
 - For Instance Store Volumes: The root device for an instance launched from the AMI is an instnace store volume created from a template stored in Amzaom S3


## <u>ENI v/s EMA v/s EFA</u>

[ENI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) - Elastic Network Interface - A virtual network card
n elastic network interface is a logical networking component in a VPC that represents a virtual network card. It can include the following attributes:

 - A primary private IPv4 address from the IPv4 address range of your VPC
 - One or more secondary private IPv4 addresses from the IPv4 address range of your VPC
 - One Elastic IP address (IPv4) per private IPv4 address
 - One public IPv4 address
 - One or more IPv6 addresses
 - One or more security groups
 - A MAC address
 - A source/destination check flag
 - A description

Scenarios for network interfaces
Attaching multiple network interfaces to an instance is useful when you want to:
 - Create a management network.
 - Use network and security appliances in your VPC.
 - Create dual-homed instances with workloads/roles on distinct subnets.
 - Create a low-budget, high-availability solution.


[ENA](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/enhanced-networking.html) - Enhanced Networkling. Uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities on supported instance types (All current generation instance types support enhanced networking, except for T2 instances.)

You can enable enhanced networking using one of the following mechanisms:

* <u>Elastic Network Adapter (ENA)</u>
The Elastic Network Adapter (ENA) supports network speeds of up to 100 Gbps for supported instance types.

  - The current generation instances use ENA for enhanced networking, except for C4, D2, and M4 instances smaller than m4.16xlarge.

* <u>Intel 82599 Virtual Function (VF) interface</u>
  - The Intel 82599 Virtual Function interface supports network speeds of up to 10 Gbps for supported instance types.

   - The following instance types use the Intel 82599 VF interface for enhanced networking: C3, C4, D2, I2, M4 (excluding m4.16xlarge), and R3.

[EFA](https://aws.amazon.com/hpc/efa/) - Elastic Fabric Adapter - A n/w device that you can attach to your Amazon EC2 instance to accelerate High Performance Computing (HPC) and maching learning applications. Elastic Fabric Adapter (EFA) is a network interface for Amazon EC2 instances that enables customers to run applications requiring high levels of inter-node communications at scale on AWS. Its custom-built operating system (OS) bypass hardware interface enhances the performance of inter-instance communications, which is critical to scaling these applications. With EFA, High Performance Computing (HPC) applications using the Message Passing Interface (MPI) and Machine Learning (ML) applications using NVIDIA Collective Communications Library (NCCL) can scale to thousands of CPUs or GPUs. As a result, you get the application performance of on-premises HPC clusters with the on-demand elasticity and flexibility of the AWS cloud.

## Spot Inatances and Spot Fleets
* Spot Instances save up tp 90% of the cost of on-demand inatances
* Useful for any type of computing where you don't need persistent storage
* You can block Spot from terminating by using Spot block
* A Spot Fleet is a collection of Spot instances and optionally on-demand instances

Spot Instances are userful for
* Big data & analytics
* Containerized workloads
* CI/CD & testing
* Web Services
* Image & meria rendering
* High-performinance computing

Spot Fleet
* A Spot Fleet is a collection of Spot instances and optionally on-demand instances
* CapacityOptimized - Spot instance conme from a pool with optimal capacity for the number of instances launching
* LowestPrice - Spot instance come from the pool with the lowest price. This is the default strategy
* Diversified - Spot instances are distributed across all pools
* InstancePoolsToUseCount - Spot instances are distributed across the number of Sport instance pools you specify. The parameter is valid only when used in combination with lowestPrice

## EC2 Hibernate
When you hibernate an instance, Amazon EC2 signals the operating system to perform hibernation (suspend-to-disk). Hibernation saves the contents from the instance memory (RAM) to your Amazon Elastic Block Store (Amazon EBS) root volume. Amazon EC2 persists the instance's EBS root volume and any attached EBS data volumes. When you start your instance:
* The EBS root volume is restored to its previous state
* The RAM contents are reloaded
* The processes that were previously running on the instance are resumed
* Previously attached data volumes are reattached and the instance retains its instance ID
* You can hibernate an instance only if it's enabled for hibernation and it meets the hibernation prerequisites.
* In order to use Hibernation the root device volume should be encrypted
* Instances cannot be hibernated more than 60 days
![Ec2 Hibernation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/hibernation-flow.png)

## Elastic Load Balancers

### [What's an Elastic Load Balancer](https://aws.amazon.com/elasticloadbalancing/)

Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, and others.

### [Types of loadbalancers](https://aws.amazon.com/elasticloadbalancing/features/#Details_for_Elastic_Load_Balancing_Products)

* Application Load balancers: Best for load balancing HTTP & HTTPS traffic. They operate at layer 7.
* Network Load Balancer: Loadbalancing TCP traffic where extreme performance is needed. They operate at layer 4.
* Classic Load Balancer: Legacy ELB, mostly operate at layer 4, but can go up to 7.

### X-Forwarded-For

(XFF) The HTTP header field is a common method for identifying the originating IP address of a client connecting to a web server through an HTTP proxy or load balancer.

### Load Balancers - Lab

* You must set up health checks in order to let the load balancer to understand if the instances are up and running
* Load balancers won't expose any IP, instead they expose DNS names.

```bash
dig +short MyClassicELB-57286656.eu-west-2.elb.amazonaws.com
35.176.153.196
35.176.224.44
```

_At the time of writing, the lab instructs you to create one EC2 instance and configure the load balancer to simply point against it.
My suggestion is to create 2 instances instead and change the `index.html` in something like `instance_1` and `instance_2` so you can see what box the load balancer decides to send your requests. Doing so, allows you to also confirm that if an instance is down, the load balancer automatically forwards traffic to the remaining one still online._

### CloudWatch - Lab

* Standard monitoring is 5 min and * Detailed monitoring is 1 min (you will be charged for it)
* Dashboard used to visualize what's happening with your AWS environment.
* Alarms can be set to notify when a specific threshold is hit
* Events can be used to perform actions when state changes happen in your AWS resources.
* Logs can be aggregated in a single place to better troubleshoot. Remember that you need to install an agent on the EC2 instance.
* By default, Matrics on EC2 instances are: CPU related, Disk related, Network related and Status check related.

Remember that:

* CloudWatch: is for monitoring resources
* CloudTrail: is for auditing

### IAM Roles with EC2 - Lab

* Roles avoid you to store credentials inside EC2 instances in order to communicate with other AWS services
* Roles can be assigned after an EC2 instance it has been provisioned
* Roles are universal, you can use them in any region.

### [EC2 Instance Metadata](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)

Within your local instance run:

 ```http://169.254.169.254/latest/meta-data```

 This will give you the top level metadata items, something like this.

 ```text
 [ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/
ami-id
ami-launch-index
ami-manifest-path
block-device-mapping/
events/
hostname
iam/
instance-action
instance-id
instance-type
local-hostname
local-ipv4
mac
metrics/
network/
placement/
profile
public-hostname
public-ipv4
public-keys/
reservation-id
security-groups
services/
```

If you want to access a specific item, simply add it at the end of your request:

```bash
[ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/ami-id
ami-12345678
```

There is also one URL for user data

```bash
[ec2-user ~]$ curl http://169.254.169.254/latest/user-data/
```

### [Lanch configurations](https://docs.aws.amazon.com/autoscaling/ec2/userguide/LaunchConfiguration.html) and [Autoscaling Groups](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html)

* A launch configuration is an instance configuration template that an Auto Scaling group uses to launch EC2 instances
* An Auto Scaling group contains a collection of Amazon EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management.

Autoscaling group will automatically spread evenly on the number of instances across the AZ you selected once you configured it. So 3 AZ with 3 as group size, means 1 box in each AZ

### [Placement Groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html)

You can launch or start instances in a placement group, which determines how instances are placed on the underlying hardware. When you create a placement group, you specify one of the following strategies for the group:

* Cluster – clusters instances into a low-latency group in a single Availability Zone.

  ![](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/placement-group-cluster.png)
* Spread – spreads instances across underlying hardware and can spread in multiple Availability Zones.
  ![](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/placement-group-spread.png)
* Partition – spreads instances across logical partitions, ensuring that instances in one partition do not share underlying hardware with instances in other partitions.
  ![](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/placement-group-partition.png)

Some notes about placement groups:

* The name you specify for a placement group must be unique within your AWS account.
* Only specific types of instances can be launched in a placement group.
* You can't merge placement groups.
* You can't move an existing instance into a placement group.
* If the exam refers to placement groups, without mentioning which type, it's most probably talking about the Cluster ones since those are the old ones.

## [EFS](https://aws.amazon.com/efs/)

Amazon EFS provides scalable file storage for use with Amazon EC2. You can create an EFS file system and configure your instances to mount the file system

* Supports NFSv4.
* You only pay for the storage you use.
* Scale up to petabytes.
* Can support thousands of concurrent connections.
* Data is stored across multiple AZ.
* Read after write consistency.

* You need to make sure that the EC2 instance that needs to connect with the EFS volume, is associated with the same security group you have on the EFS volume.
* You can assign permissions at the file level and at the folder level.
![EFS](https://d1.awsstatic.com/r2018/b/EFS/product-page-diagram-Amazon-EFS-Launch_How-It-Works.cf947858f0ef3557b9fc14077bdf3f65b3f9ff43.png)


## AWS Storage Types - S3, EFS, & EBS
Lets talk about AWS Storage for a moment.

There have been a number of questions about the different storage types, which are Block storage which are Object storage and where EFS fits into the mix.  Below I hope to shed some light on the important differences so that you can make wise choices between them.

Storage 
Ultimately all storage has "block storage" at he lowest level (even SSDs which emulate disk blocks). The terminology used is not as important as understanding the distinctions in how the storage is interacted with. Rather than trying to memorize that this service has this title, or that service has that title, it is more useful to understand how they are used and the advantages and limitations that imposes​.

* S3, files on S3 can only be addressed as objects. You cannot interact with the contents of the object until you have extracted the object from S3  (GET). It cannot be edited in-place, you must extract it, change it, and them put it back to replace the original (PUT). What this comes down to is that here is no user "locking" functionality as might be offered by a 'file system' This is why it is called "Object storage".

* EFS is basically NFS (Network File System) which is an old and still viable Unix technology. As the title implies it is a "File System" and offers more capabilities than "Object Storage" .  The key to these is grades of 'File Locking' which makes it suitable for shared use. This is what makes it suitable for a share NETWORK file system. It is important to note that like Object Stores, you are still restricted to handling the file as a complete object. You can lock it so that you can write back to it, but you are restricted in the extent that you do partial content updates based on blocks. This gets a bit grey as there are ways to do partial updates, but they are limited.

* EBS is closer to locally attached disk whether that be IDE, SAS, SCSI (or it's close cousin iSCSI/Fibre Channel, which is in reality just SCSI over a pipe). With Locally attached disk you have better responsiveness and addressing. This allows you to use File Systems that can address the disk at a block level. This includes part reads, part writes, read ahead, delayed writes, file system maintenance where you swap block under the file, block level cloning, thin provisioning, deduplication etc. As noted above, Block Storage sits underneath both NFS and Object stores, but as a consumer you are abstracted away and cannot make direct use of them.

## [Amazon FSx for Windwos File Server](https://aws.amazon.com/fsx/windows/)
* Provides a full managed native Microsoft Windows file system so you can move your windows apps that require file storage to AWS. Amazon FSx is built on Windows Server
* A managed Windows server that runs Windows Server Message Block (SMB) based file services
* Designed for Windows and Windows applications
* Support AD users, access control lists, groups & security policies, along with Distributed File System (DFS) namespaces and replication
* It offers single-AZ and multi-AZ deployment options, fully managed backups, and encryption of data at rest and in transit
* Amazon FSx file storage is accessible from Windows, Linux, and MacOS compute instances and devices running on AWS or on premises. 
![FSX for Windows](https://d1.awsstatic.com/r2018/b/FSx-Windows/FSx_Windows_File_Server_How-it-Works.9396055e727c3903de991e7f3052ec295c86f274.png)

## [Amazon FSx for Lustre](https://aws.amazon.com/fsx/lustre/)
Amazon FSx for Lustre is a fully managed service that provides cost-effective, high-performance storage for compute workloads. Many workloads such as machine learning, high performance computing (HPC), video rendering, and financial simulations depend on compute instances accessing the same set of data through high-performance shared storage.
Powered by Lustre, the world's most popular high-performance file system, FSx for Lustre offers sub-millisecond latencies, up to hundreds of gigabytes per second of throughput, and millions of IOPS. It provides multiple deployment options and storage types to optimize cost and performance for your workload requirements.

FSx for Lustre file systems can also be linked to Amazon S3 buckets, allowing you to access and process data concurrently from both a high-performance file system and from the S3 API.


## [Lambda](https://aws.amazon.com/lambda/)

AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume - there is no charge when your code is not running.
Lambda basically is based on triggers.

You can use lambda in two ways:

* Event-driven based: Lambda runs your code based on events, such, new file on S3 or a new alarm on cloudwatch
* Compute-service based: Lambda runs your code based on HTTP requests using an API Gateway or API calls made using AWS SDKs.

AWS lambda, supports: C#, Node.js, Python, and Java

Lambda is charged as follow:

* First 1M requests per month are free. $0.20 PER 1M requests thereafter
* Duration: You are charged for the amount of memory you allocate on your functions. First 400,000 GB-seconds per month, up to 3.2M seconds of computing time, are free.
* Your functions can't go over 5 minutes in run-time.

_Make sure you have a look at what [CORS](https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html) is._


## [HPC on AWS - Component Services](https://aws.amazon.com/hpc/)
* Data Management & Transfer
  - [AWS DataSync](https://aws.amazon.com/datasync/)
  - [AWS Snowball](https://aws.amazon.com/snowball/)
  - [AWS Snowmobile](https://aws.amazon.com/snowmobile/)
  - [AWS DirectConnect](https://aws.amazon.com/directconnect/)
* Compute & Networking
  - [Amazon EC2 instances(CPU, CPU, FPGA)](https://aws.amazon.com/ec2/)
  - [Amazon EC2 spot](https://aws.amazon.com/ec2/spot/)
  - [AWS Auto scaling](https://aws.amazon.com/autoscaling/)
  - [Placement groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html)
  - [Enhanced Networking](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/enhanced-networking.html)
  - [Elastic Fabric Adapter](https://aws.amazon.com/hpc/efa/)
  - [AWS VPC](https://aws.amazon.com/vpc/)
* Storage
  - [Amazon EBS with provisioned IOPS](https://aws.amazon.com/ebs/)
  - [Amazon Fsx for Lustre](https://aws.amazon.com/fsx/lustre/)
  - [Amazon EFS](https://aws.amazon.com/efs/)
  - [Amazon S3](https://aws.amazon.com/s3/)
* Automation & Orchestration
  - [AWS Batch](https://aws.amazon.com/batch/)
  - [AWS ParallelCliuster](https://aws.amazon.com/hpc/parallelcluster/)
  - [NICE EnginFrame](https://www.nice-software.com/download/enginframe-on-aws)
* Visualization
  - [NICE DCV](https://aws.amazon.com/hpc/dcv/)
  - [Amazon AppStream 2.0](https://aws.amazon.com/appstream2/)
* Operation & Management
  - [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/)
  - [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/)
* Security & Compliance
  - [AWS Identity & Access Management](https://aws.amazon.com/iam/)

## [AWS WAF](https://aws.amazon.com/waf/)
  AWS WAF is a web application firewall that helps protect your web applications or APIs against common web exploits that may affect availability, compromise security, or consume excessive resources. AWS WAF gives you control over how traffic reaches your applications by enabling you to create security rules that block common attack patterns, such as SQL injection or cross-site scripting, and rules that filter out specific traffic patterns you define. You can get started quickly using Managed Rules for AWS WAF, a pre-configured set of rules managed by AWS or AWS Marketplace Sellers. The Managed Rules for WAF address issues like the OWASP Top 10 security risks. These rules are regularly updated as new issues emerge. AWS WAF includes a full-featured API that you can use to automate the creation, deployment, and maintenance of security rules.

With AWS WAF, you pay only for what you use. The pricing is based on how many rules you deploy and how many web requests your application receives. There are no upfront commitments.

You can deploy AWS WAF on Amazon CloudFront as part of your CDN solution, the Application Load Balancer that fronts your web servers or origin servers running on EC2, or Amazon API Gateway for your APIs.
![AWS WAF](https://d1.awsstatic.com/products/WAF/product-page-diagram_AWS-WAF_How-it-Works@2x.452efa12b06cb5c87f07550286a771e20ca430b9.png)