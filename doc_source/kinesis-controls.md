# Amazon Kinesis controls<a name="kinesis-controls"></a>

These controls are related to Kinesis resources\.

## \[Kinesis\.1\] Kinesis streams should be encrypted at rest<a name="kinesis-1"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::Kinesis::Stream`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/kinesis-stream-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/kinesis-stream-encrypted.html)

**Schedule type:** Change triggered

**Parameters:** None 

This control checks if Kinesis Data Streams are encrypted at rest with server\-side encryption\. This control fails if a Kinesis stream is not encrypted at rest with server\-side encryption\.

Server\-side encryption is a feature in Amazon Kinesis Data Streams that automatically encrypts data before it's at rest by using an AWS KMS key\. Data is encrypted before it's written to the Kinesis stream storage layer, and decrypted after it's retrieved from storage\. As a result, your data is encrypted at rest within the Amazon Kinesis Data Streams service\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="kinesis-1-remediation"></a>

For information about enabling server\-side encryption for Kinesis streams, see [How do I get started with server\-side encryption?](https://docs.aws.amazon.com/streams/latest/dev/getting-started-with-sse.html) in the *Amazon Kinesis Developer Guide*\.