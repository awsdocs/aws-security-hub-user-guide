# AwsSqs<a name="asff-resourcedetails-awssqs"></a>

The following are examples of the AWS Security Finding Format for `AwsSqs` resources\.

## AwsSqsQueue<a name="asff-resourcedetails-awssqsqueue"></a>

The `AwsSqsQueue` object contains information about an Amazon Simple Queue Service queue\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsSqsQueue` object\. To view descriptions of `AwsSqsQueue` attributes, see [AwsSqsQueueDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsSqsQueueDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsSqsQueue": {
    "DeadLetterTargetArn": "arn:aws:sqs:us-west-2:123456789012:queue/target",
    "KmsDataKeyReusePeriodSeconds": 60,,
    "KmsMasterKeyId": "1234abcd-12ab-34cd-56ef-1234567890ab",
    "QueueName": "sample-queue"
}
```