# AWS SQS
* Amazon SQS is a message queue service used by distributed applications to exchange messages through a polling model, and can be used to decouple sending and receiving components
* Amazon SQS provides flexibility for distributed components of applications to send and receive messages without requiring each component to be concurrently available.
* “SQS” – Users can specify an SQS standard or FIFO queue as the endpoint; Amazon SNS will enqueue a notification message to the specified queue (which subscribers can then process using SQS APIs such as ReceiveMessage, DeleteMessage, etc.)

## Queue types
Amazon SQS offers two queue types for different application requirements:

    You can't convert an existing standard queue into a FIFO queue. To make the move, you must either create a new FIFO queue for your application or delete your existing standard queue and recreate it as a FIFO queue.

### Standard Queues
* **Unlimited Throughput:** Standard queues support a nearly unlimited number of transactions per second (TPS) per API action.
* **At-Least-Once Delivery:** A message is delivered at least once, but occasionally more than one copy of a message is delivered.
* **Best-Effort Ordering:** Occasionally, messages might be delivered in an order different from which they were sent.

![](https://d1.awsstatic.com/AmazonSQS/sqs-what-is-sqs-standard-queue-diagram.29963b2823bc048492c7af2757535d500aa2c159.png)

You can use standard message queues in many scenarios, as long as your application can process messages that arrive more than once and out of order, for example:
* Decouple live user requests from intensive background work: Let users upload media while resizing or encoding it.
* Allocate tasks to multiple worker nodes: Process a high number of credit card validation requests.
* Batch messages for future processing: Schedule multiple entries to be added to a database.

### FIFO Queues
* **High Throughput:** By default, FIFO queues support up to 300 messages per second (300 send, receive, or delete operations per second). When you batch 10 messages per operation (maximum), FIFO queues can support up to 3,000 messages per second. To request a quota increase, file a support request.
* **Exactly-Once Processing:** A message is delivered once and remains available until a consumer processes and deletes it. Duplicates aren't introduced into the queue.
* **First-In-First-Out Delivery:** The order in which messages are sent and received is strictly preserved (i.e. First-In-First-Out).

![](https://d1.awsstatic.com/AmazonSQS/sqs-what-is-sqs-fifo-queue-diagram.8f1c8d366f58845ce03bb2983c16349102cf1524.png)

FIFO queues are designed to enhance messaging between applications when the order of operations and events is critical, or where duplicates can't be tolerated, for example:
* Ensure that user-entered commands are executed in the right order.
* Display the correct product price by sending price modifications in the right order.
* Prevent a student from enrolling in a course before registering for an account.


## Functionality

* **Unlimited queues and messages:** Create unlimited Amazon SQS queues with an unlimited number of message in any region
* **Payload Size:** Message payloads can contain up to 256KB of text in any format. Each 64KB ‘chunk’ of payload is billed as 1 request. For example, a single API call with a 256KB payload will be billed as four requests. To send messages larger than 256KB, you can use the Amazon SQS Extended Client Library for Java, which uses Amazon S3 to store the message payload. A reference to the message payload is sent using SQS.
* **Batches:* Send, receive, or delete messages in batches of up to 10 messages or 256KB. Batches cost the same amount as single messages, meaning SQS can be even more cost effective for customers that use batching.
* **Long polling:** Reduce extraneous polling to minimize cost while receiving new messages as quickly as possible. When your queue is empty, long-poll requests wait up to 20 seconds for the next message to arrive. Long poll requests cost the same amount as regular requests.
* **Retain messages in queues for up to 14 days.**
* **Send and read messages simultaneously.**
* **Message locking:** When a message is received, it becomes “locked” while being processed. This keeps other computers from processing the message simultaneously. If the message processing fails, the lock will expire and the message will be available again.
* **Queue sharing:** Securely share Amazon SQS queues anonymously or with specific AWS accounts. Queue sharing can also be restricted by IP address and time-of-day.
* **Server-side encryption (SSE):** Protect the contents of messages in Amazon SQS queues using keys managed in the AWS Key Management Service (AWS KMS). SSE encrypts messages as soon as Amazon SQS receives them. The messages are stored in encrypted form and Amazon SQS decrypts messages only when they are sent to an authorized consumer.
* **Dead Letter Queues (DLQ):** Handle messages that have not been successfully processed by a consumer with Dead Letter Queues. When the maximum receive count is exceeded for a message it will be moved to the DLQ associated with the original queue. Set up separate consumer processes for DLQs which can help analyze and understand why messages are getting stuck. DLQs must be of the same type as the source queue (standard or FIFO).


### Using Amazon SQS with other AWS infrastructure web services
Amazon SQS message queuing can be used with other AWS Services such as Redshift, DynamoDB, RDS, EC2, ECS, Lambda, and S3, to make distributed applications more scalable and reliable. Below are some common design patterns:

* Work Queues: Decouple components of a distributed application that may not all process the same amount of work simultaneously.
* Buffer and Batch Operations: Add scalability and reliability to your architecture, and smooth out temporary volume spikes without losing messages or increasing latency.
* Request Offloading: Move slow operations off of interactive request paths by enqueing the request.
* Fanout: Combine SQS with Simple Notification Service (SNS) to send identical copies of a message to multiple queues in parallel.
* Priority: Use separate queues to provide prioritization of work.
* Scalability: Because message queues decouple your processes, it’s easy to scale up the send or receive rate of messages - simply add another process.
* Resiliency: When part of your system fails, it doesn’t need to take the entire system down. Message queues decouple components of your system, so if a process that is reading messages from the queue fails, messages can still be added to the queue to be processed when the system recovers.