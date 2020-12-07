 # FXs for Lustre
* A managed windows server that runs Windows Server Message Block (SMB)-based file services
* Designed for Windows and Windows applications
* Supports AD users, access control list, groups and security policies, along with Distributed File System (DFS) namespace and replication
* Built on Windows Server, delivering a wide range of administrative features such as user quotas, end-user file restore, ACLs and Microsoft Active Directory (AD) integration.
* Amazon FSx provides high levels of throughput and IOPS, and consistent sub-millisecond latencies
* Amazon FSx is accessible from Windows, Linux, and MacOS compute instances and devices
* Thousands of compute instances and devices can access a file system concurrently
* Amazon FSx can connect the file system to EC2, VMware Cloud on AWS, Amazon WorkSpaces, and Amazon AppStream 2.0 instances.
* Integrated with CloudWatch to monitor storage capacity and file system activity
* Integrated with CloudTrail to monitor all Amazon FSx API calls
* Amazon FSx was designed for use cases that require Windows shared file storage, like CRM, ERP, custom or .NET applications, home directories, data analytics, media and entertainment workflows, web serving and content management, software build environments, and Microsoft SQL Server
* Amazon FSx file systems is accessible from the on-premises environment using an AWS Direct Connect or AWS VPN connection
* Amazon FSx is accessible from multiple VPCs, AWS accounts, and AWS Regions using VPC Peering connections or AWS Transit Gateway
* Amazon FSx provides consistent sub-millisecond latencies with SSD storage, and single-digit millisecond latencies with HDD storage
* Amazon FSx grows the storage capacity of your existing file system without any downtime impact to your applications and users by adding larger disks, transparently migrating your data in the background from the original disks to the new ones, and then removing the original disks from your file system – the standard process for growing storage on a Windows File Server.


## FSx for Windows Security

* Amazon FSx works with Microsoft Active Directory (AD) to integrate with  existing Windows environments, which can either be an AWS Managed Microsoft AD or self-managed Microsoft AD

* Amazon FSx provides standard Windows permissions (full support for Windows Access Controls ACLS) for files and folders.
Amazon FSx for Windows File Server supports encryption at rest for the file system and backups using KMS managed keys

* Amazon FSx encrypts data-in-transit using SMB Kerberos session keys, when accessing the file system from clients that support SMB 3.0

* Amazon FSx supports file-level or folder-level restores to previous versions by supporting Windows shadow copies, which are snapshots of your file system at a point in time

* Amazon FSx supports Windows shadow copies to enable your end-users to easily undo file changes and compare file versions by restoring files to previous versions, and backups to support your backup retention and compliance needs.

## FSx for Windows Availability and durability
* Amazon FSx automatically replicates the data within an Availability Zone (AZ) to protect it from component failure

* Amazon FSx continuously monitors for hardware failures, and automatically replaces infrastructure components in the event of a failure

* Amazon FSx supports Multi-AZ deployment
    * automatically provisions and maintains a standby file server in a different Availability Zone.
    * Any changes written to disk in the file system are synchronously replicated across AZs to the standby.
    * helps enhance availability during planned system maintenance
    * helps protect the data against instance failure and AZ disruption.
    * In the event of planned file system maintenance or unplanned service disruption, Amazon FSx automatically fails over to the secondary file server, allowing data accessibility without manual intervention.
* Amazon FSx supports automatic backups of the file systems, which are incremental storing only the changes after the most recent backup
* Amazon FSx stores backups in Amazon S3.

Q: When should I use Amazon FSx Windows File Servers vs. Amazon EFS vs. Amazon FSx for Lustre?
---
A: For Windows-based applications, Amazon FSx provides fully managed Windows file servers with features and performance optimized for "lift-and-shift" business-critical application workloads including home directories (user shares), media workflows, and ERP applications. It is accessible from Windows and Linux instances via the SMB protocol. If you have Linux-based applications, Amazon EFS is a cloud-native fully managed file system that provides simple, scalable, elastic file storage accessible from Linux instances via the NFS protocol.

For compute-intensive and fast processing workloads, like high performance computing (HPC), machine learning, EDA, and media processing, Amazon FSx for Lustre, provides a file system that’s optimized for performance, with input and output stored on Amazon S3.

## Billing
* You pay only for the resources you use. You are billed hourly for your file systems, based on their deployment type (Single-AZ or Multi-AZ), storage type (SSD or HDD), storage capacity (priced per GB-month), and throughput capacity (priced per MBps-month). You are billed hourly for your backup storage (priced per GB-month).