# AWS SNS
* Amazon Simple Notification Service (Amazon SNS) is a web service that makes it easy to set up, operate, and send notifications from the cloud
* It provides developers with a highly scalable, flexible, and cost-effective capability to publish messages from an application and immediately deliver them to subscribers or other applications
* Amazon SNS follows the “publish-subscribe” (pub-sub) messaging paradigm, with notifications being delivered to clients using a “push” mechanism that eliminates the need to periodically check or “poll” for new information and updates
* Amazon SNS offers several benefits making it a versatile option for building and integrating loosely-coupled, distributed applications:
    * Instantaneous, push-based delivery (no polling)
    * Simple APIs and easy integration with applications
    * Flexible message delivery over multiple transport protocols
    * Inexpensive, pay-as-you-go model with no up-front costs
    * Web-based AWS Management Console offers the simplicity of a point-and-click interface
* Amazon SNS service can support a wide variety of needs including 
    * event notification
    * monitoring applications
    * workflow systems
    * time-sensitive information updates
    * mobile applications
    * any other application that generates or consumes notifications
    * A common pattern is to use SNS to publish messages to Amazon SQS message queues to reliably send messages to one or many system components asynchronously
    * Another example use for Amazon SNS is to relay time-critical events to mobile applications and devices

## How it works?
* Developers must first create a “topic” which is an “access point” – identifying a specific subject or event type – for publishing messages and allowing clients to subscribe for notifications. 
* Once a topic is created, the topic owner can set policies for it such as limiting who can publish messages or subscribe to notifications, or specifying which notification protocols will be supported (i.e. HTTP/HTTPS, email, SMS)
* Subscribers are clients interested in receiving notifications from topics of interest; they can subscribe to a topic or be subscribed by the topic owner
* Subscribers specify the protocol and end-point (URL, email address, etc.) for notifications to be delivered
* When publishers have information or updates to notify their subscribers about, they can publish a message to the topic – which immediately triggers Amazon SNS to deliver the message to all applicable subscribers.

## Billing
* there is no minimum fee and you pay only for what you use


## Features and functionality
* Topic names are limited to 256 characters
* Topic names must be unique within an AWS account
* When a topic is created, Amazon SNS will assign a unique ARN (Amazon Resource Name) to the topic, which will include the service name (SNS), region, AWS ID of the user and the topic name
* Different delivery formats/transports for receiving notification
    * “HTTP”, “HTTPS” – Subscribers specify a URL as part of the subscription registration; notifications will be delivered through an HTTP POST to the specified URL.
    * ”Email”, “Email-JSON” – Messages are sent to registered addresses as email. Email-JSON sends notifications as a JSON object, while Email sends text-based email.
    * “SQS” – Users can specify an SQS standard queue as the endpoint; Amazon SNS will enqueue a notification message to the specified queue (which subscribers can then process using SQS APIs such as ReceiveMessage, DeleteMessage, etc.).
    * “SMS” – Messages are sent to registered phone numbers as SMS text messages
* **Message Filtering** 
    * Use message filtering on Amazon Simple Notification Service (SNS) to build simpler and more streamlined pub/sub architectures
    * Message filtering enables Amazon SNS topic subscribers to selectively receive only a subset of the messages they are interested in, as opposed to receiving all messages published to a topic
* Message filtering enables Amazon SNS topic subscribers to selectively receive only a subset of the messages they are interested in, as opposed to receiving all messages published to a topic
* users should create the SQS queue prior to subscribing it to a Topic
* Multiple users can publish to same topic if the owner has explicitly set permission to allow more that one users (with a valid AWS ID) to publish a message to the topic


## Reliability
* SNS provides durable storage of all messages that it receives. Upon receiving a publish request, SNS stores multiple copies (to disk) of the message across multiple Availability Zones before acknowledging receipt of the request to the sender
* all notification messages will contain a single published message
* Although most of the time each message will be delivered to your application exactly once, the distributed nature of Amazon SNS and transient network conditions could result in occasional, duplicate messages at the subscriber end. Developers should design their applications such that processing a message more than once does not create any errors or inconsistencies.
* The Amazon SNS service will attempt to deliver messages from the publisher in the order they were published into the topic. However, network issues could potentially result in out-of-order messages at the subscriber end.
* The Amazon SNS service will attempt to deliver messages from the publisher in the order they were published into the topic. However, network issues could potentially result in out-of-order messages at the subscriber end.
* once a message has been successfully published to a topic, it cannot be recalled.
* In case a subscriber is not available then Amazon SNS will retry connecting until the connection is successful or it exceeds the number of retries it will then discards the message — unless a dead-letter queue is attached to the subscription

## Quotas & Restrictions
* By default, SNS offers 10 million subscriptions per topic, and 100,000 topics per account
* Amazon SNS messages can contain up to 256 KB of text data, including XML, JSON and unformatted text
* Each 64KB chunk of published data is billed as 1 request. For example, a single API call with a 256KB payload will be billed as four requests.
* By default, 200 filter policies per account per region can be applied to a topic
* SNS uses a default Time to Live (TTL) of 4 weeks for all mobile platforms
