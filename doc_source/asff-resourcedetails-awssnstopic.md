# AwsSnsTopic<a name="asff-resourcedetails-awssnstopic"></a>

The `AwsSnsTopic` object contains details about an Amazon Simple Notification Service topic\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsSnsTopic` object\. To view descriptions of `AwsSnsTopic` attributes, see [AwsSnsTopicDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsSnsTopicDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsSnsTopic": {
                        "ApplicationSuccessFeedbackRoleArn": "arn:aws:iam::123456789012:role/ApplicationSuccessFeedbackRoleArn",                        
                        "FirehoseFailureFeedbackRoleArn": "arn:aws:iam::123456789012:role/FirehoseFailureFeedbackRoleArn",
                        "FirehoseSuccessFeedbackRoleArn": "arn:aws:iam::123456789012:role/FirehoseSuccessFeedbackRoleArn",
                        "HttpFailureFeedbackRoleArn": "arn:aws:iam::123456789012:role/HttpFailureFeedbackRoleArn",
                        "HttpSuccessFeedbackRoleArn": "arn:aws:iam::123456789012:role/HttpSuccessFeedbackRoleArn",                         
                        "KmsMasterKeyId": "alias/ExampleAlias",
                        "Owner": "123456789012",
                        "SqsFailureFeedbackRoleArn": "arn:aws:iam::123456789012:role/SqsFailureFeedbackRoleArn",
                        "SqsSuccessFeedbackRoleArn": "arn:aws:iam::123456789012:role/SqsSuccessFeedbackRoleArn",                         
                        "Subscription": {
                            "Endpoint": "http://sampleendpoint.com",
                            "Protocol": "http"
                        },
                        "TopicName": "SampleTopic"   
               }
```