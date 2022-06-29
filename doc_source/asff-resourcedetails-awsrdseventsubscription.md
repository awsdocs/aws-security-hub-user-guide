# AwsRdsEventSubscription<a name="asff-resourcedetails-awsrdseventsubscription"></a>

The `AwsRdsEventSubscription` contains details about an Amazon Relational Database Service event notification subscription\. The subscription allows Amazon RDS to post events to an Amazon Simple Notification Service topic\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsRdsEventSubscription` object\. To view descriptions of `AwsRdsEventSubscription` attributes, see [AwsRdsEventSubscriptionDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsRdsEventSubscriptionDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsRdsEventSubscription": {
    "CustSubscriptionId": "myawsuser-secgrp",
    "CustomerAwsId": "111111111111",
    "Enabled": true,
    "EventCategoriesList": [
        "configuration change",
        "failure"
    ],
    "EventSubscriptionArn": "arn:aws:rds:us-east-1:111111111111:es:my-instance-events",
    "SnsTopicArn": "arn:aws:sns:us-east-1:111111111111:myawsuser-RDS",
    "SourceIdsList": [
        "si-sample",
        "mysqldb-rr"
    ],
    "SourceType": "db-security-group",
    "Status": "creating",
    "SubscriptionCreationTime": "2021-06-27T01:38:01.090Z"
}
```