# Amazon EC2 Auto Scalling
* Fully managed service designed to launch or terminate Amazon EC2 instances automatically to handle the load for the application
* helps maintain application availability through fleet management for EC2 instances
* detects unhealthy instances and scalling EC2 capacity up or down automatically according to the condifitons defined


Q. When should I use Amazon EC2 Auto Scaling vs. AWS Auto Scaling?
---
You should use AWS Auto Scaling to manage scaling for multiple resources across multiple services. AWS Auto Scaling lets you define dynamic scaling policies for multiple EC2 Auto Scaling groups or other resources using predefined scaling strategies. Using AWS Auto Scaling to configure scaling policies for all of the scalable resources in your application is faster than managing scaling policies for each resource via its individual service console. 
You should use EC2 Auto Scaling if you only need to scale Amazon EC2 Auto Scaling groups, or if you are only interested in maintaining the health of your EC2 fleet.

Q: What is an EC2 Auto Scaling group (ASG)?
---
An Amazon EC2 Auto Scaling group (ASG) contains a collection of EC2 instances that share similar characteristics and are treated as a logical grouping for the purposes of fleet management and dynamic scaling.

Q: What happens to my Amazon EC2 instances if I delete my ASG?
---
If you have an EC2 Auto Scaling group (ASG) with running instances and you choose to delete the ASG, the instances will be terminated and the ASG will be deleted.

Q: What is a launch configuration?
---
* A launch configuration is a template that an EC2 Auto Scaling group uses to launch EC2 instances. 
* When you create a launch configuration, you specify information for the instances such as the ID of the Amazon Machine Image (AMI), the instance type, a key pair, one or more security groups, and a block device mapping.
* You can specify your launch configuration with multiple EC2 Auto Scaling groups. 
* However, you can only specify one launch configuration for an EC2 Auto Scaling group at a time, and you can't modify a launch configuration after you've created it.
* Therefore, if you want to change the launch configuration for your EC2 Auto Scaling group, you must create a launch configuration and then update your EC2 Auto Scaling group with the new launch configuration. 
* When you change the launch configuration for your EC2 Auto Scaling group, any new instances are launched using the new configuration parameters, but existing instances are not affected.

Q: How do I control access to Amazon EC2 Auto Scaling resources?
---
Amazon EC2 Auto Scaling integrates with AWS Identity and Access Management (IAM), a service that enables you to do the following:

* Create users and groups under your organization's AWS account
* Assign unique security credentials to each user under your AWS account
* Control each user's permissions to perform tasks using AWS resources
* Allow the users in another AWS account to share your AWS resources
* Create roles for your AWS account and define the users or services that can assume them
* Use existing identities for your enterprise to grant permissions to perform tasks using AWS resources

Q: Can I create a single ASG to scale instances across different purchase options?
---
Yes. You can provision and automatically scale EC2 capacity across different EC2 instance types, Availability Zones, and On-Demand, RIs and Spot purchase options in a single Auto Scaling Group. You have the option to define the desired split between On-Demand and Spot capacity, select which instance types work for your application, and specify preference for how EC2 Auto Scaling should distribute the ASG capacity within each purchasing model. 

Q: What are the costs for using Amazon EC2 Auto Scaling?
---
Amazon EC2 Auto Scaling fleet managment for EC2 instances carries no additional fees. The dynamic scaling capabilities of Amazon EC2 Auto Scaling are enabled by Amazon CloudWatch and also carry no additional fees. Amazon EC2 and Amazon CloudWatch service fees apply and are billed separately.