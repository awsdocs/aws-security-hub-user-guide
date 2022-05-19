# AwsSqsQueue<a name="asff-resourcedetails-awssqsqueue"></a>

The `AwsSqsQueue` object contains information about an Amazon SQS queue\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsSqsQueue` object\. To view descriptions of `AwsSqsQueue` attributes, see [AwsSqsQueueDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsSqsQueueDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsSqsQueue": {
                        "DeadLetterTargetArn": "string",
                        "KmsDataKeyReusePeriodSeconds": number,
                        "KmsMasterKeyId": "string",
                        "QueueName": "string"
                    }
```