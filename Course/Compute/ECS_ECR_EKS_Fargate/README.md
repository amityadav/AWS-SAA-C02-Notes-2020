# ECS (Elastic Container Service)
* A container is a package that contains an application, libraries, runtime & tools required to run it
* Managed container orchestration service
* Create clusters to manage fleets of container deployments
* ECS manage EC2 or Fargate instances
* Schedules container for optimal placement
* Defines rules for CPU & memory requirement
* Monitors resource utilizations
* Deploy, update, roll back
* Free
* Intergrates with VPC, SG & EBS volumes
* ELB
* Cloudtrail & CloudWatch

![](https://d1.awsstatic.com/reInvent/re20-pdp-tier1/Mithril/product-page-diagram_Amazon-ECS@2x.0d872eb6fb782ddc733a27d2bb9db795fed71185.png)
## ECS Components
### Cluster
* Logical collection of ECS resources - either ECS EC2 instances or Fargate Instances

### Task Definition
* Defines your application. Similar to DockerFile but for running containers in ECS. Can contain multiple containers

### Container Definition
* Inside a task definition, it defines the individual containers a task uses. Controls CPU & memory allocations and port mappints

### Task
* Single running copy of any containers defined by a task definition. One working copy of an application (e.g. DB, Web Component)

### Service
* Allows task definition to be scaled by adding tasks. Defines minimum & maximum values

### Registry
* Storage for container images (e.g. Elastic Container Registery - ECR or Docker Hub). Used to download images to create containers

## Fargate
* Serverless container engine
* Eliminates needs to provision and manage servers
* Specify and pay for resources per application
* Works with both ECS & EKS
* Each workload run in its own kernel
* Isolation & security
* Choose EC2 instead if
    * Compliance requirements
    * Require broader customization
    * Application requires GPU


## EKS (Elastic Kuberneties Service)
* k8s is open-source software that lets you deploy & manage containerized applications at scale
* Same toolset on-prem & in cloud
* Containers are grouped in pods
* Like ECS, it supports EC2 and Fargate instances
* Why use EKS
    * Already using K8s
    * Want to migrate to AWS

## ECR (Elastic Container Registry)
* Amazon Elastic Container Registry (ECR) is a fully-managed container registry that makes it easy for developers to share and deploy container images and artifacts
* Amazon ECR is integrated with Amazon Elastic Container Service (ECS),  Amazon Elastic Kubernetes Service (EKS), and AWS Lambda
* Amazon ECR eliminates the need to operate your own container repositories or worry about scaling the underlying infrastructure
* Amazon ECR hosts your images in a highly available and scalable architecture
* Integration with AWS Identity and Access Management (IAM) provides resource-level control of each repository 
* Amazon ECR transfers your container images over HTTPS and automatically encrypts your images at rest
* there are no upfront fees or commitments. You pay only for the amount of data you store in your public or private repositories, and data transferred to the Internet
* Amazon ECR is a regional service and is designed to give you flexibility in how images are deployed
* Pulling images between regions or out to the internet will have additional latency and data transfer costs
* Amazon ECR can host public container images
* Integrates with CloudTrail
* Amazon ECR work with AWS Elastic Beanstalk
Amazon ECR currently supports Docker Engine 1.7.0 and up