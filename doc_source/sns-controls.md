# Amazon Simple Notification Service controls<a name="sns-controls"></a>

These controls are related to Amazon SNS resources\.

## \[SNS\.1\] SNS topics should be encrypted at\-rest using AWS KMS<a name="sns-1"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest 

**Severity:** Medium

**Resource type:** `AWS::SNS::Topic`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/sns-encrypted-kms.html](https://docs.aws.amazon.com/config/latest/developerguide/sns-encrypted-kms.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an SNS topic is encrypted at rest using AWS KMS\. The controls fails if an SNS topic doesn't use a KMS key for server\-side encryption \(SSE\)\.

Encrypting data at rest reduces the risk of data stored on disk being accessed by a user not authenticated to AWS\. It also adds another set of access controls to limit the ability of unauthorized users to access the data\. For example, API permissions are required to decrypt the data before it can be read\. SNS topics should be encrypted at\-rest for an added layer of security\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="sns-1-remediation"></a>

To turn on SSE for an SNS topic, see [Enabling server\-side encryption \(SSE\) for an Amazon SNS topic](https://docs.aws.amazon.com/sns/latest/dg/sns-enable-encryption-for-topic.html) in the *Amazon Simple Notification Service Developer Guide*\. Before you can use SSE, you must also configure AWS KMS key policies to allow encryption of topics and encryption and decryption of messages\. For more information, see [Configuring AWS KMS permissions](https://docs.aws.amazon.com/sns/latest/dg/sns-key-management.html#sns-what-permissions-for-sse) in the *Amazon Simple Notification Service Developer Guide*\.

## \[SNS\.2\] Logging of delivery status should be enabled for notification messages sent to a topic<a name="sns-2"></a>

**Related requirements:** NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::SNS::Topic`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/sns-topic-message-delivery-notification-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/sns-topic-message-delivery-notification-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether logging is enabled for the delivery status of notification messages sent to an Amazon SNS topic for the endpoints\. This control fails if the delivery status notification for messages is not enabled\.

Logging is an important part of maintaining the reliability, availability, and performance of services\. Logging message delivery status helps provide operational insights, such as the following:
+ Knowing whether a message was delivered to the Amazon SNS endpoint\.
+ Identifying the response sent from the Amazon SNS endpoint to Amazon SNS\.
+ Determining the message dwell time \(the time between the publish timestamp and the hand off to an Amazon SNS endpoint\)\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="sns-2-remediation"></a>

To configure delivery status logging for a topic, see [Amazon SNS message delivery status](https://docs.aws.amazon.com/sns/latest/dg/sns-topic-attributes.html) in the *Amazon Simple Notification Service Developer Guide*\.