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


## [Amazon Storage](https://aws.amazon.com/products/storage/)

### [Amazon Storage Gateway](https://aws.amazon.com/storagegateway/)

What's an Amazon Storage Gateway: AWS Storage Gateway connects an on-premises software appliance with cloud-based storage to provide seamless integration with data security features between your on-premises IT environment and the AWS storage infrastructure.

* File Gateway: For flat files, stored directly in S3. You can NFS Mount points
* VOlume gateway (iSCSI): Block-based storage
  * Store volume (you keep all your data on prem)
  * Cached Volumes (you keep only the most recent data on prem)
Tape Gateway (VTL): Virtual tapes