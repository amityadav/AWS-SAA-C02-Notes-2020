# Amazon FSx for Lustre - File Storage
* Fully managed service that provides cost-effective, high-performance, scalable storage for compute workloads
* workloads as machine learning, high performance computing (HPC), video rendering & financial simulations
* Amazon FSx provides multiple deployment options to optimize cost
    * Scratch file systems
        * designed for temporary storage and short-term processing of data.
        * data is not replicated and does not persist if a file server fails.
    * Persistent file systems
        * designed for long-term storage and workloads.
        * is highly available, and data is automatically replicated within the AZ that is associated with the file system.
        * data volumes attached to the file servers are replicated independently from the file servers to which they are attached.
* FSx for Lustre is compatible with most popular Linux-based AMIs, including Amazon Linux, Amazon Linix2, Red hat Enterprise Linux (RHEL), CentOS, SUSE Linux & Ubuntu
* FSx for Lustre can be accessed from a Linux instance, by installing the open-source Lustre client and mounting the file system using standard Linux commands

## FSx for Lustre with S3
* amazon FSx also integrates seamlessly with S3, making it easy to process cloud data sets with Lustre high performance system
* transparently presents S3 objects as files and allows writing changed data back to S3
* Can be linked with a specified S3 bucket, making the data in S3 accessible to the file system
* S3 objects name and prefixes will be visible as files and directories
* S3 Objects are lazy loaded by default
    * Objects are only loaded into the file system only when first accessed by the application
    * Amazon FSx for Lustre automatically loads the corresponding objects from S3 when accessed
    * Subsequent reads of these files are served directly out of the file system with low, consistent latencies
    * Amazon FSx for Lustre file system can optionally batch hydrated
* Uses parallel data transfer techniques to transfer data from S3 at up to hundreds of GB/s
* Files from the file system can be exported back to S3 bucket

## FSx for Lustre Security
* FSx for Lustre provides encryption at rest for the file system and the backups, by default, using KMS
* FSx encrypts data-in-transit when accessed from supported EC2 instances only

## FSx for Lustre Scalability
* Scales to hundreds of GB/s of throughput and millions of IOPs
* Supports concurrent access to the same file or directory from thousands of compute instances
* Provides consistent, sub-millisecond latencies for file operations

## FSx for Lustre Availability & Durability
* On a scratch file system, file servers are not replaced if they fail and data is not replicated.
* On a persistent file system, if a file server becomes unavailable it is replaced automatically and within minutes.
* Amazon FSx for Lustre provides a parallel file system, where data is stored across multiple network file servers to maximize performance and reduce bottlenecks, and each server has multiple disks.
* Amazon FSx takes daily automatic incremental backups of the file systems, and allows manual backups at any point.
* Backups are highly durable and file-system-consistent