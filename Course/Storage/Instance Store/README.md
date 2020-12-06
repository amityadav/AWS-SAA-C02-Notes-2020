# Instance Store
* Provides temporary block-level storage for the EC2 instances
* Located on the disks that are physically attached to the host computer
* Ideal for temporary storage of info that changes frequently (buffer, cache, scratch data)
* Size of the instance store as well as the number of devices available varies by instance type
* Virtual devices for instance store volume are ephermal[0-23]

![Instance Store](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/instance_storage.png)

* Can specify instance store for an instance only while launching the instance
* Instance store can't be detached from an instance and attached to another instance
* Data in instance store persists only during the lifetime of its associated instance
* Data persists during reboots (intentionally or unintentionally)
* Data is lost under following circumstances
    * underlying disk drive fails
    * Instance stops
    * instance hibernates
    * instance terminates
* AMI's from an instance - data from instance store isn't preserved
* If an instance type is changed then the instance store will not be attached to the new instance
* The root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3
* If underlying hosts fails, we will lose our data