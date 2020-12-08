## [Amazon Storage](https://aws.amazon.com/products/storage/)  - Data Transfer

### [Amazon Storage Gateway](https://aws.amazon.com/storagegateway/)

What's an Amazon Storage Gateway: AWS Storage Gateway connects an on-premises software appliance with cloud-based storage to provide seamless integration with data security features between your on-premises IT environment and the AWS storage infrastructure.

* Its a Service that connects an on-prem software application with cloud-based storage to provide seamless and secure integration b/w an organization's on-prem IT environment and AWS storage infrastructure. This service enables you ro securely store data to the AWS cloud for scalable and cost effective storage
* AWS Storage Gateway's s/w applicance is available for download as a VM inage that can be installed on the host in your datacenter. SG supports VMWare ESXi or Microsoft Hyper-V

![Diagram](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2019/11/23/Storage-Gateway-summary-picture.png)

![Storage Gareway](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2019/11/23/Use-case-1-More-on-premises-backups-to-the-cloud.png)


* **File Gateway**: NFS & SMB - 
  * Files are stored as objects in S3 buckets, accessed through a NFS mount point. Once objects are transfered to S3 they can be managed as native S3 objects

![File Gateway](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2019/11/23/File-Gateway-for-on-premises-backups.png)
* **Volume gateway** (iSCSI): 
  * Block-based storage. 
  * Volume Gateway presents cloud-backed iSCSI block storage volumes to your on-premises applications
  * Volume Gateway stores and manages on-premises data in Amazon S3 on your behalf and operates in either cache mode or stored mode
    * **Store volume** 
      * your primary data is stored locally and your entire dataset is available for low latency access on premises while also asynchronously getting backed up to Amazon S3
    * **Cached Volumes**
      * you keep only the most recent data on prem
      * your primary data is stored in Amazon S3 while retaining your frequently accessed data locally in the cache for low latency access

![Volume Gateway](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2019/11/23/volume-gateway-for-on-premises-backups.png)

* Tape Gateway (VTL): Virtual tapes

![Tape Gateway](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2019/11/23/Tape-Gateway-for-on-premises-backups.png)

## Use Cases
* Move backups to the cloud
* Use on-premises file shares backed by cloud storage
* Low latency access for on-premises applications to cloud
* Data protection and disaster recovery