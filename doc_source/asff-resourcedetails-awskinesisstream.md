# AwsKinesisStream<a name="asff-resourcedetails-awskinesisstream"></a>

The `AwsKinesisStream` object provides details about Amazon Kinesis Data Streams\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsKinesisStream` object\. To view descriptions of `AwsKinesisStream` attributes, see [AwsKinesisStreamDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsKinesisStreamDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsKinesisStream": { 
	"Name": "test-vir-kinesis-stream",
	"Arn": "arn:aws:kinesis:us-east-1:293279581038:stream/test-vir-kinesis-stream",
	"RetentionPeriodHours": 24,
	"ShardCount": 2,
	"StreamEncryption": {
		"EncryptionType": "KMS",
		"KeyId": "arn:aws:kms:us-east-1:293279581038:key/849cf029-4143-4c59-91f8-ea76007247eb"
	}
}
```