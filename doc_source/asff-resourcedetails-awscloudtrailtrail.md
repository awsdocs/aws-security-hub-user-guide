# AwsCloudTrailTrail<a name="asff-resourcedetails-awscloudtrailtrail"></a>

The `AwsCloudTrailTrail` object provides details about a AWS CloudTrail trail\.

The following is an example `AwsCloudTrailTrail` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsCloudTrailTrail` attributes, see [AwsCloudTrailTrailDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsCloudTrailTrailDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsCloudTrailTrail": {
    "CloudWatchLogsLogGroupArn": "arn:aws:logs:us-west-2:123456789012:log-group:CloudTrail/regression:*",
    "CloudWatchLogsRoleArn": "arn:aws:iam::866482105055:role/CloudTrail_CloudWatchLogs",
    "HasCustomEventSelectors": true,
    "HomeRegion": "us-west-2",
    "IncludeGlobalServiceEvents": true,
    "IsMultiRegionTrail": true,
    "IsOrganizationTrail": false,
    "KmsKeyId": "kmsKeyId",
    "LogFileValidationEnabled": true,
    "Name": "regression-trail",
    "S3BucketName": "cloudtrail-bucket",
    "S3KeyPrefix": "s3KeyPrefix",
    "SnsTopicArn": "arn:aws:sns:us-east-2:123456789012:MyTopic",
    "SnsTopicName": "snsTopicName",
    "TrailArn": "arn:aws:cloudtrail:us-west-2:123456789012:trail"
}
```