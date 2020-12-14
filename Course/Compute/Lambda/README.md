# Lambda
* AWS Lambda offers Serverless computing
* Serverless computing allows applications and services to be built and run without thinking about servers. With serverless computing, application still runs on servers, but all the server management is done by AWS.
* Lambda lets you run code without provisioning or managing servers, where you pay only for the compute time when the code is running.
* Lambda is priced on a pay per use basis and there are no charges when the code is not running
* Lambda allows running of code for any type of application or backend service with zero administration
* Lambda performs all the operational and administrative activities on your behalf, including capacity provisioning, monitoring fleet health, applying security patches to the underlying compute resources, deploying code, running a web service front end, and monitoring and logging the code.
* Lambda does not provide access to the underlying compute infrastructure
* AWS Lambda functions can be configured to run up to 15 minutes per execution. You can set the timeout to any value between 1 second and 15 minutes
* You can automate your serverless application’s release process using AWS CodePipeline and AWS CodeDeploy. CodePipeline is a continuous delivery service that enables you to model, visualize and automate the steps required to release your serverless application. CodeDeploy provides a deployment automation engine for your Lambda-based applications
* You can use AWS Step Functions to coordinate a series of AWS Lambda functions in a specific order

## Scalability and availability
* Lambda provides easy scaling and high availability to thcode without additional effort on your part.
* Lambda is designed to process events within milliseconds.
* Latency will be higher immediately after a Lambda functiois created, updated, or if it has not been used recently.
* Lambda is designed to run many instances of the functionin parallel
* Lambda is designed to use replication and redundancy tprovide high availability for both the service and thLambda functions it operates.
* There are no maintenance windows or scheduled downtimefor either
* For any Lambda function updates, there is a brief windoof time, less then a minute, when requests would be serveby both the versions
* Lambda has a default safety throttle for number of concurrent executions per account per region

## Security
* Lambda stores code in S3 and encrypts it at rest and performs additional integrity checks while the code is in use.
* Each AWS Lambda function runs in its own isolated environment, with its own resources and file system view

* All calls made to AWS Lambda must complete execution within 300 900 seconds. Default timeout is 3 seconds. Timeout can be set the timeout to any value between 1 and 300 900 seconds.
* AWS Step Functions can help coordinate a series of Lambda functions in a specific order. Multiple Lambda functions can be invoked sequentially, passing the output of one to the other, and/or in parallel, while the state is being maintain by Step Functions.
* AWS X-Ray helps tracing for Lambda functions, which provides insights such as Lambda service overhead, function init time, and function execution time

## Lambda Functions & Event Sources
* Core components of Lambda are Lambda functions and event sources.
    * Event source is an AWS service or custom application that publishes events
    * Lambda function is the custom code that processes the events

## Lambda Functions
* Each Lambda function has associated configuration information, such as its name, description, entry point, and resource requirements
* Lambda may choose to retain an instance of the function and reuse it to serve a subsequent request, rather than creating a new copy
* Each Lambda function receives 500MB of non-persistent disk space in its own /tmp directory.
* Design Lambda function as stateless
    * Lambda functions should be stateless, to allow AWS Lambda launch as many copies of the function as needed as per the demand
    * Local file system access, child processes, and similar artifacts may not extend beyond the lifetime of the request
    * State can be maintained externally in DynamoDB or S3
* Lambda function can be granted permissions to access other resources using an IAM role
* Lambda functions have the following restrictions
    * Inbound network connections are blocked by AWS Lambda
    * For outbound connections only TCP/IP and UDP/IP sockets are supported and ptrace (debugging) system calls are blocked
    * TCP port 25 traffic is also blocked as an anti-spam measure.
* Lambda automatically monitors functions, reporting real-time metrics through CloudWatch, including total requests, account-level and function-level concurrency usage, latency, error rates, and throttled requests
* Lambda automatically integrates with CloudWatch logs, creating a log group for each function and providing basic application lifecycle event log entries, including logging the resources consumed for each use of that function
* Lambda functions supports code written in
    * Java
    * Go
    * PowerShell
    * Node.js
    * C#
    * Python
    * Ruby

## Security
* For sensitive information, for e.g. passwords, AWS recommends using client-side encryption using AWS Key Management Service and store the resulting values as ciphertext in your environment variable.
* Lambda function code should include the logic to decrypt these values

## Versioning
* Each AWS Lambda function has a single, current version of the code and there is no versioning of the same function.
* Each Lambda function version has a unique ARN and after it is published it is immutable
* Versioning can be implemented using Aliases.
* Lambda supports creating aliases, which are mutable, for each Lambda function versions
* Alias is a pointer to a specific function version, with unique ARN
* Each alias maintains an ARN for a function version to which it points
* An alias can only point to a function version, not to another alias
* Alias helps in rolling out new changes or rolling back to old versions

## Failure Handling
* For S3 bucket notifications and custom events, Lambda will attempt execution of the function three times in the event of an error condition in the code or if a service or resource limit is exceeded
* For ordered event sources, for e.g. DynamoDB Streams and Kinesis streams, that Lambda polls, it will continue attempting execution in the event of a developer code error until the data expires.
* Kinesis and DynamoDB Streams retain data for a minimum of 24 hours
* Dead Letter Queues can be configured for events to be placed, once the retry policy for asynchronous invocations is exceeded

## Lambda Execution Model
* When AWS Lambda executes the Lambda function, it takes care of provisioning and managing resources needed to run the Lambda function.
* When a Lambda function is invoked for the first time or after it has been updated there is a latency for bootstrapping as Lambda tries to reuse the Execution Context for subsequent invocations of the Lambda function
* When a Lambda function is invoked, Lambda launches an Execution Context based on the provided configuration settings i.e. memory and execution time
* After a Lambda function is executed, Lambda maintains the Execution Context for some time in anticipation subsequent function invocation
* Execution Context is a temporary runtime environment that initializes any external dependencies of the Lambda function code, for e.g. database connections or HTTP endpoints.
* Subsequent invocations perform better performance as there is no need to “cold-start” or initialize those external dependencies
* Lambda manages Execution Context creations and deletion, there is no AWS Lambda API to manage Execution Context.

## Provisioned Concurrency
* When enabled, Provisioned Concurrency keeps functions initialized and hyper-ready to respond in double-digit milliseconds
* Provisioned Concurrency adds a pricing dimension, of ‘Provisioned Concurrency’, for keeping functions initialized
* Provisioned Concurrency is ideal for building latency-sensitive applications, such as web or mobile backends, synchronously invoked APIs, and interactive microservices


## Lambda in VPC
* Lambda function can be configured to connect to private subnets in a virtual private cloud (VPC) in the AWS account.
* Lambda runs the function code securely within a VPC by default.
* Lambda function connected to VPC can access private resources databases, cache instances, or internal services during execution
* To enable the Lambda function to access resources inside the private VPC, additional VPC-specific configuration information that includes private subnet IDs and security group IDs must be provided.
* AWS Lambda uses this information to set up elastic network interfaces (ENIs) that enable the function to connect securely to other resources within your private VPC.
* Lambda functions connected to VPC need a NAT Gateway to access any external resources outside of AWS.
* Lambda functions cannot connect directly to a VPC with dedicated instance tenancy, instead peer it to a second VPC with default tenancy.

## Lambda@Edge
* Lambda@Edge allows running of code across AWS locations globally without provisioning or managing servers, responding to end users at the lowest network latency
* Lambda function can be configured to be triggered in response to CloudFront requests, which includes
    * Viewer Request – event occurs when an end user or a device on the Internet makes an HTTP(S) request to CloudFront, and the request arrives at the edge location closest to that user.
    * Viewer Response – event occurs when the CloudFront server at the edge is ready to respond to the end user or the device that made the request
    * Origin Request – event occurs when the CloudFront edge server does not already have the requested object cached, and the viewer request is ready to be sent to backend origin webserver
    * Origin Response – event occurs when the CloudFront server at the edge receives a response from your backend origin webserver.
* Lambda function executes across AWS locations globally when a request for content is received, and scales with the volume of CloudFront requests globally
* Lambda@Edge only supports Node.js for global invocation by CloudFront events at this time

* Lambda Best Practices
* Lambda function code should be stateless, and ensure there is no affinity between the code and the underlying compute infrastructure.
* Instantiate AWS clients outside the scope of the handler to take advantage of connection re-use.
* Make sure you have set +rx permissions on your files in the uploaded ZIP to ensure Lambda can execute code on your behalf.
* Lower costs and improve performance by minimizing the use of startup code not directly related to processing the current event.
* Use the built-in CloudWatch monitoring of your Lambda functions to view and optimize request latencies.
* Delete old Lambda functions that you are no longer using
* You can enable your Lambda function for tracing with AWS X-Ray by adding X-Ray permissions to your Lambda function’s execution role and changing your function’s “tracing mode” to “active"
* Code Signing for AWS Lambda offers trust and integrity controls which enable you to verify that only unaltered code from approved developers is deployed in your Lambda functions
* AWS Lambda support Advanced Vector Extensions 2 (AVX2)

![How it works](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-HowItWorks.68a0bcacfcf46fccf04b97f16b686ea44494303f.png)
![Real-time file processing](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-RealTimeFileProcessing.a59577de4b6471674a540b878b0b684e0249a18c.png)
![Real-time stream processing](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-RealTimeStreamProcessing.d79d55b5f3a5d6b58142a6c0fc8a29eadc81c02b.png)
![Web applications](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-WebApplications%202.c7f8cf38e12cb1daae9965ca048e10d676094dc1.png)
![IoT backends](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-IoTBackends.3440c7f50a9b73e6a084a242d44009dc0fbe5fab.png)
![Mobile backends](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-MobileBackends_option2.00f6421e67e8d6bdbc59f3a2db6fa7d7f8508073.png)