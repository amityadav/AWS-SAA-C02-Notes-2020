# AWS MQ
* Amazon MQ is a managed message broker service for [Apache ActiveMQ](http://activemq.apache.org/components/classic/) and [RabbitMQ](https://www.rabbitmq.com/) that makes it easy to set up and operate message brokers on AWS
* Amazon MQ reduces your operational responsibilities by managing the provisioning, setup, and maintenance of message brokers
* Amazon manages ongoing software upgrades, security updates, and fault detection and recovery
* Amazon MQ stores messages redundantly across multiple Availability Zones (AZs) for message durability
* With active/standby brokers, Amazon MQ automatically fails over to a standby instance in the event of a failure
* Follows formats such as JMS, NMS, AMQP 1.0 and 0.9.1, STOMP, MQTT, and WebSocket
* Its ntegrated with the following AWS services:
    * [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) - monitor metrics and generate alarms
    * [Amazon CloudWatch Logs](https://aws.amazon.com/cloudwatch/features/) - publish logs from your Amazon MQ brokers to Amazon CloudWatch Logs
    * [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) - log, continously monitor, and retain Amazon MQ API calls
    * [AWS CloudFormation](https://aws.amazon.com/cloudformation/) - automate the process of creating, updating, and deleting message brokers
    * [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) - authentication and authorization of the service API
    * [AWS Key Management Service (KMS)](https://aws.amazon.com/kms/) - create and control the keys used to encrypt your data
* You are charged for broker instance and storage usage, and standard data transfer fees
* Amazon MQ is HIPAA eligible, and meets standards for PCI, SOC, and ISO compliance
* Amazon MQ supports the AWS Key Management Service (AWS KMS) to create and manage keys for at-rest encryption of your data in Amazon MQ
* Amazon MQ for ActiveMQ supports two types of broker storage – durability optimized using Amazon Elastic File System (Amazon EFS) and throughput optimized using Amazon Elastic Block Store (EBS)

## When should I use Amazon MQ vs. Amazon SQS and SNS?
    Amazon MQ, Amazon SQS, and Amazon SNS are messaging services that are suitable for anyone from startups to enterprises
    
    If you're using messaging with existing applications, and want to move your messaging to the cloud quickly and easily, we recommend you consider Amazon MQ. It supports industry-standard APIs and protocols so you can switch from any standards-based message broker to Amazon MQ without rewriting the messaging code in your applications
    
    If you are building brand new applications in the cloud, we recommend you consider Amazon SQS and Amazon SNS. Amazon SQS and SNS are lightweight, fully managed message queue and topic services that scale almost infinitely and provide simple, easy-to-use APIs


## Message Broker
    Message brokers are an inter-application communication technology to help build a common integration mechanism to support cloud native, microservices-based, serverless and hybrid cloud architectures

