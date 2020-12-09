# EBS (Elastic Block Store) - Block Storage
EBS is an easy to use, high performance **block storage** designed for Amazon EC2.

It offers two variants
* SSD based
* HDD based

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

-------


* Amazon EBS provides highly available, reliable, durable, block-level storage volumes that can be attached to a running instance
* EBS as a primary storage device is recommended for data that requires frequent and granular updates for e.g. running a database or filesystems
* An EBS volume behaves like a raw, unformatted, external block device that can be attached to a single EC2 instance at a time
* EBS volume persists independently from the running life of an instance
* An EBS volume can be attached to any instance within the same Availability Zone, and can be used like any other physical hard drive
* EBS volumes allows encryption using the EBS encryption feature. All data stored at rest, disk I/O, and snapshots created from the volume are encrypted. Encryption occurs on the EC2 instance, providing encryption of data-in-transit from EC2 to the EBS volume
* EBS volumes can be backed up by creating a snapshot of the volume, which is stored in S3. EBS volumes can be created from a snapshot & can be attached to an another instance within the same region
* EBS volumes are created in a specific Availability Zone, and can then be attached to any instances in that same Availability Zone. To make a volume available outside of the Availability Zone, create a snapshot and restore that snapshot to a new volume anywhere in that region
* Snapshots can also be copied to other regions and then restored to new volumes, making it easier to leverage multiple AWS regions for geographical expansion, data center migration, and disaster recovery.
* General Purpose (SSD) volumes support up to 10,000 16000 IOPS and 160 250 MB/s of throughput and Provisioned IOPS (SSD) volumes support up to 20,000 64000 IOPS and 320 1000 MB/s of throughput.

### [RAID Arrays using EBS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/raid-config.html)

As you would do in a bare-metal server, you can also create [RAID](https://en.wikipedia.org/wiki/RAID) arrays within AWS EC2 boxes using EBS volumes.

* Remeber that the RAID available in AWS is only **software**
* You can have two types of RAID:

  * [RAID 0](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_0) – splits ("stripes") data evenly across two or more disks. When I/O performance is more important than fault tolerance; for example, as in a heavily used database (where data replication is already set up separately). You can use RAID 0 configurations in scenarios where you are using heavy databases with perhaps mirroring and replication.
  * [RAID 1](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_1) – consists of an exact copy (or mirror) of a set of data on two or more disks. When fault tolerance is more important than I/O performance; for example, as in a critical application. With RAID 1 you get more data durability in addition to the replication features of the AWS cloud.
  * RAID 5 and RAID 6 are not recommended for Amazon EBS because the parity write operations of these RAID modes consume some of the IOPS available to your volumes. Depending on the configuration of your RAID array, these RAID modes provide 20-30% fewer usable IOPS than a RAID 0 configuration. Increased cost is a factor with these RAID modes as well; when using identical volume sizes and speeds, a 2-volume RAID 0 array can outperform a 4-volume RAID 6 array that costs twice as much.

Remember also that you can create [snapshots of your RAID arrays](https://aws.amazon.com/premiumsupport/knowledge-center/snapshot-ebs-raid-array/)

## EBS Benefits

* Data Availability
    * EBS volume is automatically replicated in an Availability Zone to prevent data loss due to failure of any single hardware component.
* Data Persistence
    * persists independently of the running life of an EC2 instance
    * persists when an instance is stopped and started or rebooted
    * Root EBS volume is deleted, by default, on Instance termination but can be modified by changing the DeleteOnTermination flag
    * All attached volumes persist, by default, on instance termination
    * If underlying Hyper-V start failing or have issues then we can stop and start the EC2 instance (EBS Backed) and start again. This will launch the instance on a different Hyper-v

* Data Encryption
    * can be encrypted by EBS encryption feature
    * EBS encryption uses 256-bit Advanced Encryption Standard algorithms (AES-256) and an Amazon-managed key infrastructure.
    * Encryption occurs on the server that hosts the EC2 instance, providing encryption of data-in-transit from the EC2 instance to EBS storage
    * Snapshots of encrypted EBS volumes are automatically encrypted.

* Snapshots
    * EBS provides the ability to create snapshots (backups) of any EBS volume and write a copy of the data in the volume to Amazon S3, where it is stored redundantly in multiple Availability Zones
    * Snapshots can be used to create new volumes, increase the size of the volumes or replicate data across Availability Zones or regions
    * Snapshots are incremental backups and store only the data that was changed from the time the last snapshot was taken.
    * Snapshots size can probably be smaller then the volume size as the data is compressed before being saved to S3
    * Even though snapshots are saved incrementally, the snapshot deletion process is designed so that you need to retain only the most recent snapshot in order to restore the volume.

## EBS Volume Creation

* EBS volume can be created either
    * Creating New volumes
        * Completely new from console or command line tools and can then be attached to an EC2 instance in the same Availability Zone
    * Restore volume from Snapshots
        * EBS volumes can also be restored from a previously created snapshots
        * New volumes created from existing EBS snapshots load lazily in the background.
        * There is no need to wait for all of the data to transfer from S3 to the EBS volume before the attached instance can start accessing the volume and all its data.
        * If the instance accesses the data that hasn’t yet been loaded, the volume immediately downloads the requested data from S3, and continues loading the rest of the data in the background.
        * EBS volumes restored from encrypted snapshots are encrypted, by default
    * EBS volumes can be created and attached to a running EC2 instance by specifying a block device mapping

## EBS Volume Detachment

* EBS volumes can be detached from an instance explicitly or by terminating the instance
EBS root volumes can be detached by stopping the instance
* EBS data volumes, attached to a running instance, can be detached by unmounting the volume from the instance first.
* If the volume is detached without being unmounted, it might result the volume being stuck in the busy state and could possibly damaged the file system or the data it contains
* EBS volume can be force detached from an instance, using the Force Detach option, but it might lead to data loss or a corrupted file system as the instance does not get an opportunity to flush file system caches or file system metadata
* Charges are still incurred for the volume after its detachment

## EBS Encryption

* EBS volumes can be created and attached to a supported instance type, and supports following types of data
    * Data at rest
    * All disk I/O i.e All data moving between the volume and the instance
    * All snapshots created from the volume
    * All volumes created from those snapshots
* Encryption occurs on the servers that host EC2 instances, providing encryption of data-in-transit from EC2 instances to EBS storage
* EBS encryption is supported with all EBS volume types (gp2, io1, st1 and sc1), and has the same IOPS performance on encrypted volumes as with unencrypted volumes, with a minimal effect on latency
* EBS encryption is only available on select instance types
* **Snapshots of encrypted volumes and volumes created from encrypted snapshots are automatically encrypted using the same volume encryption key**
* EBS encryption uses AWS Key Management Service (AWS KMS) customer master keys (CMK) when creating encrypted volumes and any snapshots created from the encrypted volumes.
* EBS volumes can be encrypted using either
    * a default CMK is created for you automatically.
    * a CMK that you created separately using AWS KMS, giving you more flexibility, including the ability to create, rotate, disable, define access controls, and audit the encryption keys used to protect your data.
* Public or shared snapshots of encrypted volumes are not supported, because other accounts would be able to decrypt your data and needs to be migrated to an unencrypted status before sharing.
* Existing unencrypted volumes cannot be encrypted directly, but can be migrated by
    * create a unencrypted snapshot from the volume
    * create an encrypted copy of unencrypted snapshot
    * create an encrypted volume from the encrypted snapshot
* Encrypted snapshot can be created from a unencrypted snapshot by create an encrypted copy of the unencrypted snapshot
* Unencrypted volume cannot be created from an encrypted volume directly but needs to be migrated


* There is a limit of 5000 EBS volumes per AWS account

## Multi Attach
* Amazon EBS Multi-Attach enables you to attach a single Provisioned IOPS SSD (io1) volume to up to 16 Nitro-based instances that are in the same Availability Zone
* Each instance to which the volume is attached has full read and write permission to the shared volume
* Multi-Attach is available only in the us-east-1, us-west-2, eu-west-1, and ap-northeast-2 Regions
* Multi-Attach enabled volumes can't be created as boot volumes
* You can't enable or disable Multi-Attach after volume creation
* You can't change the volume type, size, or Provisioned IOPS of a Multi-Attach enabled volume
