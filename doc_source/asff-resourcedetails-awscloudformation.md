# AwsCloudFormation<a name="asff-resourcedetails-awscloudformation"></a>

The following are examples of the AWS Security Finding Format for `AwsCloudFormation` resources\.

## AwsCloudFormationStack<a name="asff-resourcedetails-awscloudformationstack"></a>

The `AwsCloudFormationStack` object provides details about an AWS CloudFormation stack that is nested as a resource in a top\-level template\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsCloudFormationStack` object\. To view descriptions of `AwsCloudFormationStack` attributes, see [AwsCloudFormationStackDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsCloudFormationStackDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsCloudFormationStack": { 
	"Capabilities": [
		"CAPABILITY_IAM",
		"CAPABILITY_NAMED_IAM"
	],
	"CreationTime": "2022-02-18T15:31:53.161Z",
	"Description": "AWS CloudFormation Sample",
	"DisableRollback": true,
	"DriftInformation": {
		"StackDriftStatus": "DRIFTED"
	},
	"EnableTerminationProtection": false,
	"LastUpdatedTime": "2022-02-18T15:31:53.161Z",
	"NotificationArns": [
		"arn:aws:sns:us-east-1:978084797471:sample-sns-cfn"
	],
	"Outputs": [{
		"Description": "URL for newly created LAMP stack",
		"OutputKey": "WebsiteUrl",
		"OutputValue": "http://ec2-44-193-18-241.compute-1.amazonaws.com"
	}],
	"RoleArn": "arn:aws:iam::012345678910:role/exampleRole",
	"StackId": "arn:aws:cloudformation:us-east-1:978084797471:stack/sample-stack/e5d9f7e0-90cf-11ec-88c6-12ac1f91724b",
	"StackName": "sample-stack",
	"StackStatus": "CREATE_COMPLETE",
	"StackStatusReason": "Success",
	"TimeoutInMinutes": 1
}
```