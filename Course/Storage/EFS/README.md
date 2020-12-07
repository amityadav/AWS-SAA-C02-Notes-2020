# EFS (Elastic File System)
* EFS is a file storage service for Amazon Elastic Cloud Compute instances
* EFS is easy to use and provies a simple interface that allow you to create and configure file system quickly and easily
* Fully managed
* Storage capacity is elastic, growing and shrinking automatically based on your usage
* Can be used to share files between multiple instances
* Replicated across multiple AZ's
* We can enable automatic lifecycle management
* Stopping EFS lifecycle management will no longer move infrequent accessed file to EFS IA but existing files will remain as-is
* File size smaller than 128 KiB are not eligible for Lifecycle Management
* Based on NFS v4 protocol (Port 2049)
* Encryption at rest and in-transit
* 1000 file systems per regions is the limit
* Amazon EFS is designed to burst to allow high throughput levels for periods of time
* consistent baseline performance of 50 MB/s per TB of Standard class storage, all file systems (regardless of size) can burst to 100 MB/s
* You can use EFS with only LINUX based EC2 instances

## Use Cases
* Big Data & analytics
* Media processing workflows
* content management
* web servicing
* home directories

## Loading data to EFS
* use AWS DataSync
* AWS VPN
* AWS Direct Connect

## Storage Classes
* Standard Access Storage
    * Designed for active file system workloads
    * Pay only for the file system storage usage per month
* Infrequent Access Storage
    * Lower cost-optimized
    * Used for files not accessed every day
    * Costs 85% less than the standard storage class
    * Use case - satisfying audits, performing historical analysis, backup or recovery etc.

## Durability & Availability
* Every file system object is redundantly stored across multiple AZ
* Can be accessed concurrently from all AZ within a region where it is located. So we can architect it for failover from one AZs to other
* Use AWS Backup to schedule automatic backup, incremental backup

## Provisioned Throughput
* Provisioned Throughput enables Amazon EFS customers to provision their file system’s throughput independent of the amount of data stored, optimizing their file system throughput performance to match their application’s needs
* Billed
    * Storage(per GB-Month)
    * Throughput (per MB/s-Month)

## Security
* Controle EC2 instance access to EFS using VPC security group rules & IAM policies
* IAM policies can be used for disabiling root access, enforcing readonly access, enforcing encrypted connection
* use IAM roles for advanced policies
* Ability to encrypt data at rest and in-transit
* Automatically encrypt data while reads and writes. Encryption keys are managed by KMS
* Data in-transit is encrypted uses TLS 1.2

## Billing
* Provisioned Throughput you pay for the throughout you provision per month. No minimum fee.
* EFS IA - amount of storeage used and the amount of data accessed
* EFS Standard - Storage and amount of data accessed 

## Accessibility
* Can be accessed from
    * EC2
    * ECS
    * EKS
    * AWS Lambda
    * AWS SageMaker