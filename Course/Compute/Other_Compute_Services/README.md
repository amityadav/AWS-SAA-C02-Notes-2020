# Amazon Lightsail
* Amazon Lightsail is the easiest way to get started with AWS for developers, small businesses, students, and other users who need a solution to build and host their applications on cloud. Lightsail provides developers compute, storage, and networking capacity and capabilities to deploy and manage websites and web applications in the cloud. Lightsail includes everything you need to launch your project quickly – virtual machines, containers, databases, CDN, load balancers, DNS management etc. – for a low, predictable monthly price
* You can get preconfigured virtual private server plans that include everything to easily deploy and manage your application
* Application templates include WordPress, Drupal, Joomla!, Ghost, Magento, Redmine, LAMP, Nginx (LEMP), MEAN, Node.js, Django, and more
* Lightsail current supports tagging for the following resources:
    * Instances (Linux and Windows)
    * Container services
    * Block storage disks
    * Load balancers
    * Databases
    * DNS zones
    * Instance, disk, and database snapshots
* You can change to a Static IP after creating your app. They're free in Lightsail
* DNS management is free within Lightsail


# AWS Elastic Beanstalk
* AWS Elastic Beanstalk is detailed as "Quickly deploy and manage applications in the AWS cloud
* AWS Elastic Beanstalk provides an environment where you can easily deploy and run applications in the cloud
* Elastic Beanstalk is intended to make developers' lives easier
* Elastic Beanstalk is a PaaS-like layer ontop of AWS's IaaS services which abstracts away the underlying EC2 instances, Elastic Load Balancers, auto scaling groups, etc
* It is integrated with developer tools and provides a one-stop experience for managing application lifecycle

# AWS CloudFormation
* AWS CloudFormation is a service that gives developers and businesses an easy way to create a collection of related AWS and third-party resources, and provision and manage them in an orderly and predictable fashion
* AWS CloudFormation is a convenient provisioning mechanism for a broad range of AWS and third-party resources
* It supports the infrastructure needs of many different types of applications such as existing enterprise applications, legacy applications, applications built using a variety of AWS resources, and container-based solutions (including those built using AWS Elastic Beanstalk)
* Elements of an AWS CloudFormation template
    * An optional list of template parameters (input values supplied at stack creation time)
    * An optional list of output values (e.g., the complete URL to a web application)
    * An optional list of data tables used to look up static configuration values (e.g., AMI names)
    * The list of AWS resources and their configuration values
    * A template file format version number
* “automatic rollback on error” feature is enabled
* AWS CloudFormation Registry
    * The AWS CloudFormation Registry is a managed service that lets you register, use, and discover AWS and third-party resource types
* There are no limits to the number of templates. Each AWS CloudFormation account is limited to a maximum of 200 stacks
* You can include up to 60 parameters and 60 outputs in a template
* Currently, you can create up to 200 resources per stack




| AWS Elastic Beanstalk | AWS Lighsail | AWS OpsWorks | AWS CloudFormation | On Demand |
|---|---|---|---| --- |
|* AWS Elastic Beanstalk is detailed as "Quickly deploy and manage applications in the AWS cloud <br/> * Elastic Beanstalk is intended to make developers' lives easier <br/> * Elastic Beanstalk is a PaaS-like layer ontop of AWS's IaaS services which abstracts away the underlying EC2 instances, Elastic Load Balancers, auto scaling groups, etc| Developers describe Amazon LightSail as "Simple Virtual Private Servers on AWS". Everything you need to jumpstart your project on AWS—compute, storage, and networking—for a low, predictable price|AWS OpsWorks is a configuration management service that provides managed instances of Chef and Puppet|CloudFormation is intended to make systems engineers' lives easier| EC2, S3, VPC etc |
||||||

