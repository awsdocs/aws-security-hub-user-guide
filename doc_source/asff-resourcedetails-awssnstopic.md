# AwsSnsTopic<a name="asff-resourcedetails-awssnstopic"></a>

The `AwsSnsTopic` object contains details about an Amazon SNS topic\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsSnsTopic` object\. To view descriptions of `AwsSnsTopic` attributes, see [AwsSnsTopicDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsSnsTopicDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsSnsTopic": {
                        "KmsMasterKeyId": "string",
                        "Owner": "string",
                        "Subscription": {
                            "Endpoint": "string",
                            "Protocol": "string"
                        },
                        "TopicName": "string"
                    }
```