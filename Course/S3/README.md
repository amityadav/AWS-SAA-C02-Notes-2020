# CHAPTER 3 | S3 Object Storage and CDN

## S3

### [What's S3](https://aws.amazon.com/s3/)

* Object-based storage: you can save only object, you can't, for example, install an OS (In this case you need block-based storage).
* Files can save from 0 Bytes to 5 TB.
* No storage Limits.
* Files are stored in Buckets (a folder in a cloud).
* S3 is a universal namespace, the name must be unique globally. So you **cannot** have the same name as someone else.
* Sample of an S3 URL: ```https://s3-eu-west-1.amazonaws.com/yourbucket```.
* When you upload an object in S3 you get an HTTP 200 OK code back.

### Data Consistency for S3

* It's consistent in reads after a write on new objects.
* It's eventually consistent for overwriting and deletes (this means it can take some time to propagate)
* S3 is spread across multiple AZ's

### Components

* S3 is an object. Objects consist of:
  * Key (name of the object)
  * Value (data)
  * Version ID (Used on versioning)
  * Metadata (a set of data that describes and gives information about the object data.)
  * Subresources:
    * Access Control List (Decide who can access files)
    * Torrent (Not an exam topic)

### Basics

* S3 SLA: 99.9% availability
* S3 is built for 99.99%
* S3 guarantees 11x9s (99.999999999) durability for S3 information.
* Tiered Storage (classes) available
* You can have lifecycle management
* Versioning
* Supports [multi-part upload](https://docs.aws.amazon.com/AmazonS3/latest/dev/mpuoverview.html)
* Encryption
* Access control (permissions on single files) and bucket policies (permissions on buckets)

### [S3 Storage Tiers](https://aws.amazon.com/s3/storage-classes/)

* S3 standard: 99.99% availability 11x9s durability (it sustains the loss of 2 facilities concurrently)
* S3 IA: (Infrequently Accessed): For data that is accessed less frequently, but needs rapid access. You are charged a retrieval fee per GB retrieved
* S3 One Zone IA: Like S3 IA but data is stored only in one AZ
* Glacier: Most cheap, used for archival only.
  * Expedited: few minutes for retrieval
  * Standard: 3-5 hours for retrieval
  * Bulk: 5-12 hours for retrieval
  * It encrypts data by default
  * Regionally availability
  * Designed with 11x9s durability, like S3

|Storage Class | Designed For | Availability Zone | Min Storage Duration | Min Billable Object size|
|---|---|---|---|---|
| Standard  | Frequently accessed data  | >=3  | -  | 128 KB  |
| Standard-IA  | Long-lived, infrequently accessed data  | >=3  | 30 Days  | 128 KB  |
| One Zone-IA  | Long-lived, infrequently accessed, non-critical data  | 1  |  30 Days | 128 KB  |
| Reduced redundancy  | Frequently accessed, non-critical data  | >=3  |   |   |
|  Intelligent-Tiering | Long-lived data with changing or unknown access patterns  | >=3  | 30 Days  |   |
| Glacier  | Long-term data archiving with retrieval times ranging from minutes to hours  | >=3  | 90 Days  |   |
| Glacier Deep Archive  | Long-term data archiving with retrieval times within 12 hours  | >=3  | 180 Days  | -  ||


### [Charges](https://aws.amazon.com/s3/pricing/)

S3 is charged for:

* Storage
* Requests
* Storage management pricing
* Data Transfer Pricing
* Transfer acceleration (it's using CloudFront the AWS CDN) using edge locations

### [Server side Encryption and ACL](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)

* AES-256 Use Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)
* AWS-KMS Use Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS)
* Server-Side Encryption with Customer-Provided Keys (SSE-C)

* Control access to the bucket using bucket ACL or Bucket policies
* By default all buckets and objects within are private

### [S3 Version Control](https://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html)

* Once you enable versioning, you can't disable it, you can only suspend it. A way of disabling it is to delete the bucket and re-create it
* Every time you update an object, it will become private by default.
* It integrates with Lifecycle rules.
* You pay for each version you have
* Delete an object:

    Once you delete a file inside a versioned bucket, you don't delete the file, you simply add a Delete Marker (this basically creates a new version of the object)
    If you delete the version with the Detele Marker you will basically restore the object.

    If you want to permanently delete the object, you have to delete all the Versions of the object.

    You can optionally add another layer of security by configuring a bucket to enable MFA Delete

    More info about versioning:
    [ObjectVersioning](https://docs.aws.amazon.com/AmazonS3/latest/dev/ObjectVersioning.html)
    and
    [Versioning](https://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html)

### [S3 Cross region replication](https://docs.aws.amazon.com/AmazonS3/latest/dev/crr.html)

* Regions must be unique
* Cross region replication doesn't replicate existing object by default, only new ones (after the replicate is set) will be replicated automatically.
* In order to replicate the existing objects, you need to do a `cp` using the aws cli:

    `aws s3 cp --recursive s3://alessio-casco-versioning s3://alessio-casco-versioning-replica-sydney`
* If you delete an object in the primary bucket, the delete action and markers won't be done or replicated in your remote bucket, this is a security function.
Only creations and modifications are replicated to the bucket in the other regions NOT the delete
* You can't replicate over multiple buckets, the maps are always 1-to-1

## [CloudFront](https://aws.amazon.com/cloudfront/)

### [What's a CDN](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/)

* A content delivery network or content distribution network is a geographically distributed network of proxy servers and their data centres

* Key terminology about CloudFront:
  * Edge Location: Is the location where the content is cached (separate from AWS AZ's or regions)
    Be aware that you can also write on edge locations, is not ready only.
  * Invalidating (erasing) the cache costs money.
  * Origin: Is the source of the files the CDN will distribute. An origin can be an EC2 instance, an S3 bucket, an Elastic Load Balancer or Route53, you can also have your own origin, it not mandatory that is within AWS.
  * Distribution: Is the name AWS calls CDN's.
    * You can Have two types: Web that is for generic web contents and RTMP that is for video streaming
    * TTL: time to live of the cached object.

### [S3 Security & Encryption](https://aws.amazon.com/blogs/aws/new-amazon-s3-encryption-security-features/)

* You can configure S3 to create access logs for requests made to the S3 bucket
* Access control for buckets:
  * Bucket policies: Permission bucket wide
  * Access control list: Permissions that can be applied to the single object

* Encryption:
  * In transit: from to your bucket, HTTPS for example
  * At rest:
    * Server-side encryption:
      * S3 Managed Keys: SSE-S3 (Keys are managed by S3)
      * Key Management Service: SS3-KMS the customer manages the keys
      * Server-side encryption: Here you manage the keys, and Amazon manage the writes
  * Client-side Encryption: You encrypt the data and you upload it encrypted to S3

## S3 Object lock & Glacier Vault Lock

* YS# Object Lock to store Objects using a Write Once, Read Many (WORM) model
* This helps prevents objects from being deleted or modified for a fixed amount of timeor indefinitely
* S3 Object loc can be used to meet regulatory compliance requirements
  * ### Governance Mode - Users can't overwrite or delete an object version or alter its lock settings unless they have special permissions. With governance mode, you protect objects against being deleted by most users, but you can still grant some users permissing to alter trhe retention settings or delete the object if necessary
  * ### Compliance Mode - A protecte object version can't be overritten or deleted by any user, including the root user. When object is locked in compliance mode, its retention mode can't be changed and its retention period can't be shortened. Compliance mode ensures an object version can't be overwritten or deleted for the duration of the retention period by any user
* Glacier Valut Lock - S3 Glacier vault lock allows you to deploy and enforce compliance controls for individual S3 glaciers valuts within a vauly lock policy. Once locksed the policy can't be changed

## S3 performance
* S3 has extremely low latency. You can get the first byte out of S3 within 100-200 milliseconds
* You can also achieve a high number of request: 3,500 PUT/COPY/POST/DELETE and 5,500 GET/HEAD requests per second per prefix
* The more prefix we have the more performance we have for S3
* The performance is impacted if we are using KMS as that it will encrypt & decrypt files when uploading and downloading
* Use Multipart uploads - Recomended for files over 100 MB & required for files over 5 GB
* S3 byte-Rance Fetches for downloads

### S3 Select
* S3 select enables apps to retrieve only a subset of data from an object by using simple SQL expressions, This will help in achieving drastic performance increases

### 3 Diff ways to share S3 bucets across accounts (IMPORTANT)
* Using Bucket Policies & IAM (applies across thge entire bucket). Programmatic Access Only
* Using Bucket ACLs & IAM (Individual objects). Programmatic Access Only
* Cross-accountIAM Roles. programmatic AND Consold access

## [Amazon Storage](https://aws.amazon.com/products/storage/)

### [Amazon Storage Gateway](https://aws.amazon.com/storagegateway/)

What's an Amazon Storage Gateway: AWS Storage Gateway connects an on-premises software appliance with cloud-based storage to provide seamless integration with data security features between your on-premises IT environment and the AWS storage infrastructure.

* File Gateway: For flat files, stored directly in S3. You can NFS Mount points
* VOlume gateway (iSCSI): Block-based storage
  * Store volume (you keep all your data on prem)
  * Cached Volumes (you keep only the most recent data on prem)
Tape Gateway (VTL): Virtual tapes

### [Snowball](https://aws.amazon.com/snowball/)

Import Export is still available and was the first version of snowball, you used to ship your drives to AWS

Snowball is (an appliance) a petabyte-scale data transport solution that uses devices designed to be secure to transfer large amounts of data into and out of the AWS Cloud

Snowball edge: is a 100TB data transfer device with onboard storage-computer capabilities. It's like an AWS DC in a box

Snowmobile: AWS Snowmobile is an Exabyte-scale data transfer service used to move extremely large amounts of data to AWS. A truck full of disks basically.

## [S3 Transfer Acceleration](https://docs.aws.amazon.com/AmazonS3/latest/dev/transfer-acceleration.html)

Instead of uploading files directly to your S3 bucket, you can use the AWS edge network.
Using a specific URL, you upload the file to your local edge and then the file will be uploaded to S3
an example or URL:  alessio-casco-accelerate.s3-accelerate.amazonaws.com

## [Static Website Using S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html)

* You can use bucket policies to make entire S3 buckets public
* You can use S3 to host only static websites.
* S3 Scales automatically to meet demand

[Permissions Required for Website Access](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteAccessPermissionsReqd.html)

On console: Amazon S3 => Your_Bucket => Permissions => Bucket Policy

```json
{
  "Version":"2012-10-17",
  "Statement":[{
    "Sid":"PublicReadGetObject",
        "Effect":"Allow",
      "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::example-bucket/*"
      ]
    }
  ]
}
```

_[!!! Read the S3 FAQs before the exam !!!](https://aws.amazon.com/s3/faqs/)_



## Additional Topics that needs to be looked at
* AWS Organization
* DataSync
    - DataSync automatically encrypts data and accelerates transfer over the WAN. DataSync performs automatic data integrity checks in-transit and at -rest
    - DataSync seamlessly and securly connects to Amazon S3, EFS, or FSx for windows File Server to copy data and metadata to and from AWS
    - DataSync agent is deployed as an agent on a server and connects to your NAS or file system to copy data to AWS and write data to AWS
    - Used to move large amount of data from on-premises to AWS
    - Used with NFS and SMB compatible file systems
    - Replication can be done hourly, daily, or weekly
    
* CloudFront & CloudFront Signed URL
    - Edge Location - This is the location where content will be cached. This is a different than an AWS Region/AZ
     - Distribution - This is the name given the CDN, which consists of collection of edge locations
     - Origin - This is the origin of all the files that CDN will distribute. This can be either an S3 bucket, an EC2 instance, an Elastic Load Balancer, or Route 53
     - Web Distribution - Typically used for websites
     - RTMP - Used for media Streaming
     - Signed URL v/s Cookies 
        * A signed cookie or URL is used for providing access to premium content / paid users / authorized users
        * A signed URL is for individual file
        * A signed cookie is for multiple files
        * While creating a signed URl or Cookie we can attach a policy. A policy includes - URL Expiration, IP ranges & Trusted Signers (Which AWS accounts can create signed URL's)
        * If the origin is EC2 then use CloudFront signed URL and if the origin is S3 then use S3 signed URL
* Storage Gateway
    ![Diagram](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2019/11/23/Storage-Gateway-summary-picture.png)
    ![Storage Gareway](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2019/11/23/Use-case-1-More-on-premises-backups-to-the-cloud.png)
    - Its a Service that connects an on-prem software application with cloud-based storage to provide seamless and secure integration b/w an organization's on-prem IT environment and AWS storage infrastructure. This service enables you ro securely store data to the AWS cloud for scalable and cost effective storage
     - AWS Storage Gateway's s/w applicance is available for download as a VM inage that can be installed on the host in your dataventer. SG supports VMWare ESXi or Microsoft Hyper-V
     - Types of Storage Gateway
        * File Gateway - NFS & SMB - Files are stored as objects in S3 buckets, accessed through a NFS mount point. Once objects are transfered to S3 they can be manages as native S3 onjects
        ![File Gateway](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2019/11/23/File-Gateway-for-on-premises-backups.png)
        * Volume Gateway - iSCSI
          * Stored Volume
          * Cached Volume
          ![Volume Gateway](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2019/11/23/volume-gateway-for-on-premises-backups.png)
        * Tape Gateway - VTL
        ![Tape Gateway](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2019/11/23/Tape-Gateway-for-on-premises-backups.png)
* Athena & Macie