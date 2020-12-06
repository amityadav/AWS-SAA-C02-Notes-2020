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
    

* Athena & Macie

## Provisioned Capacity Unit (PCU) 
* Provisioned Capacity guarantees that your retrieval capacity for Expedited retrievals will be available when you need it. 
* Each unit of capacity ensures that at least 3 expedited retrievals can be performed every 5 minutes and provides up to 150MB/s of retrieval throughput.
* Without provisioned capacity, Expedited retrieval requests will be accepted if capacity is available at the time the request is made.
# Billing

* Some prices vary across Amazon S3 Regions. 
* Billing prices are based on the location of your bucket. 
* There is no Data Transfer charge for data transferred within an Amazon S3 Region via a COPY request. 
* Data transferred via a COPY request between AWS Regions is charged. 
* There is no Data Transfer charge for data transferred between Amazon EC2 and Amazon S3 within the same region, for example, data transferred within the US East (Northern Virginia) Region. However, data transferred between Amazon EC2 and Amazon S3 across all other regions is charged, for example, data transferred between Amazon EC2 US East (Northern Virginia) and Amazon S3 US West (Northern California). 
* For S3 on Outposts pricing, please visit the Outposts pricing page.


Q:  How will I be charged and billed for my use of Amazon S3?
---
* Storage Used - The volume of storage billed in a month is based on the average storage used throughout the month.
* Network Data Transfer In - This represents the amount of data sent to your Amazon S3 buckets. 
* Network Data Transfer Out - This charge applies whenever data is read from any of your buckets from a location outside of the given Amazon S3 Region.

Q: How am I charged for using Versioning?
---
* Normal Amazon S3 rates apply for every version of an object stored or requested.
* For example, let’s look at the following scenario to illustrate storage costs when utilizing Versioning (let’s assume the current month is 31 days long):

1) Day 1 of the month: You perform a PUT of 4 GB (4,294,967,296 bytes) on your bucket.
2) Day 16 of the month: You perform a PUT of 5 GB (5,368,709,120 bytes) within the same bucket using the same key as the original PUT on Day 1.

When analyzing the storage costs of the above operations, please note that the 4 GB object from Day 1 is not deleted from the bucket when the 5 GB object is written on Day 15. Instead, the 4 GB object is preserved as an older version and the 5 GB object becomes the most recently written version of the object within your bucket. At the end of the month:

Total Byte-Hour usage
[4,294,967,296 bytes x 31 days x (24 hours / day)] + [5,368,709,120 bytes x 16 days x (24 hours / day)] = 5,257,039,970,304 Byte-Hours.


Q:  How does S3 Intelligent-Tiering work?
---
S3 Intelligent-Tiering works by storing objects in four access tiers: two low latency access tiers optimized for frequent and infrequent access, and two opt-in archive access tiers designed for asynchronous access that are optimized for rare access. Objects uploaded or transitioned to S3 Intelligent-Tiering are automatically stored in the Frequent Access tier. S3 Intelligent-Tiering works by monitoring access patterns and then moving the objects that have not been accessed in 30 consecutive days to the Infrequent Access tier. Once you have activated one or both of the archive access tiers, S3 Intelligent-Tiering will automatically move objects that haven’t been accessed for 90 consecutive days to the Archive Access tier and after 180 consecutive days of no access to the Deep Archive Access tier. If the objects are accessed later, the objects are moved bacck to the Frequent Access Tier. There are no retrieval fees, so one won’t see unexpected increases in storage bills when access patterns change. There is no minimum billable object size in S3 Intelligent-Tiering, but objects smaller than 128KB are not eligible for auto-tiering.

Q:  Is there a minimum duration for S3 Intelligent-Tiering?
---
Yes. The S3 Intelligent-Tiering storage class has a minimum storage duration of 30 days, which means that data that is deleted, overwritten, or transitioned to a different S3 Storage Class before 30 days will incur the normal usage charge plus a pro-rated charge for the remainder of the 30-day minimum.

Q:  What are S3 object tags?
---
S3 object tags are key-value pairs applied to S3 objects which can be created, updated or deleted at any time during the lifetime of the object. With these, you’ll have the ability to create Identity and Access Management (IAM) policies, setup S3 Lifecycle policies, and customize storage metrics. These object-level tags can then manage transitions between storage classes and expire objects in the background.Up to ten tags can be added to each S3 object.

Q:  What is Storage Class Analysis?
---
With Storage Class Analysis, you can analyze storage access patterns and transition the right data to the right storage class. This new S3 feature automatically identifies infrequent access patterns to help you transition storage to S3 Standard-IA. Configure a Storage Class Analysis policy to monitor an entire bucket, prefix, or object tag.

Q:  What is S3 Inventory?
---
The S3 Inventory report provides a scheduled alternative to Amazon S3’s synchronous List API. You can configure S3 Inventory to provide a CSV, ORC, or Parquet file output of your objects and their corresponding metadata on a daily or weekly basis for an S3 bucket or prefix. S3 Inventory report files can be encrypted by SSE-S3 or SSE-KMS.

Q:  What is S3 Batch Operations?
---
S3 Batch Operations is a feature that you can use to automate the execution, management, and auditing of a specific S3 request or Lambda function across many objects stored in Amazon S3. 

Q:  Why should I use S3 Batch Operations?
---
You should use S3 Batch Operations if you want to automate the execution of a single operation (like copying an object, or executing an AWS Lambda function) across many objects. With S3 Batch Operations, you can, with a few clicks in the S3 console or a single API request, make a change to billions of objects without having to write custom application code or run compute clusters for storage management applications. Not only does S3 Batch Operations administer your storage operation across many objects, S3 Batch Operations manages retries, displays progress, delivers notifications, provides a completion report, and sends events to AWS CloudTrail for all operations performed on your target objects. If you are interested in learning more about S3 Batch Operations, go to the Amazon S3 features page.

Q: What is Amazon S3 Storage Lens?
---
Amazon S3 Storage Lens provides organization-wide visibility into object storage usage and activity trends, as well as actionable recommendations to improve cost efficiency and apply data protection best practices. Storage Lens offers an interactive dashboard containing a single view of your object storage usage and activity across tens or hundreds of accounts in your organization, with the ability to drill-down to generate insights at the account, bucket, or even prefix level. This includes metrics like bytes, object counts, and requests, as well as metrics detailing S3 feature utilization, such as encrypted object counts and delete marker counts. S3 Storage Lens also delivers contextual recommendations to find ways for you to reduce storage costs and apply best practices on data protection across tens or hundreds of accounts and buckets.

Q: How does S3 Storage Lens work?
---
S3 Storage Lens aggregates your storage usage and activity metrics on a daily basis to be visualized in the S3 Storage Lens interactive dashboard, or available as a metrics export in CVS or Parquet file format. A default dashboard is created for you automatically at the account level, and you have the option to create additional custom dashboards scoped to your AWS organization or specific accounts, Regions, or buckets. In configuring your dashboard you can use the default metrics selection, or receive advanced metrics and recommendations for an additional cost. S3 Storage Lens provides recommendations contextually with storage metrics in the dashboard, so you can take action to optimize your storage based on the metrics.

Q: What is the difference between S3 Storage Lens and S3 Storage Class Analysis (SCA)?
---
S3 Storage Class Analysis provides recommendations for an optimal storage class by creating object age groups based on object-level access patterns within an individual bucket/prefix/tag for the previous 30-90 days. S3 Storage Lens provides daily organization level recommendations on ways to improve cost efficiency and apply data protection best practices, with additional granular recommendations by account, region, storage class, bucket or prefix.  