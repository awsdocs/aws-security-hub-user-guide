# Amazon Simple Queue Service controls<a name="sqs-controls"></a>

These controls are related to Amazon SQS resources\.

## \[SQS\.1\] Amazon SQS queues should be encrypted at rest<a name="sqs-1"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::SQS::Queue`

**AWS Config rule:** `sqs-queue-encrypted` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon SQS queues are encrypted at rest\. The control passes if you use an Amazon SQS managed key \(SSE\-SQS\) or an AWS Key Management Service \(AWS KMS\) key \(SSE\-KMS\)\.

Server\-side encryption \(SSE\) allows you to transmit sensitive data in encrypted queues\. To protect the content of messages in queues, SSE uses KMS keys\. For more information, see [Encryption at rest](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html) in the *Amazon Simple Queue Service Developer Guide*\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="sqs-1-remediation"></a>

For information about managing SSE using the AWS Management Console, see[ Configuring server\-side encryption \(SSE\) for a queue \(console\)](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-configure-sse-existing-queue.html) in the *Amazon Simple Queue Service Developer Guide*\.