# AwsEfsAccessPoint<a name="asff-resourcedetails-awsefsaccesspoint"></a>

The `AwsEfsAccessPoint` object provides details about files stored in Amazon EFS\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEfsAccessPoint` object\. To view descriptions of `AwsEfsAccessPoint` attributes, see [AwsEfsAccessPointDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEfsAccessPointDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEfsAccessPoint": { 
	"AccessPointId": "fsap-05c4c0e79ba0b118a",
	"Arn": "arn:aws:elasticfilesystem:us-east-1:863155670886:access-point/fsap-05c4c0e79ba0b118a",
	"ClientToken": "AccessPointCompliant-ASk06ZZSXsEp",
	"FileSystemId": "fs-0f8137f731cb32146",
	"PosixUser": {
		"Gid": "1000",
		"SecondaryGids": ["0", "4294967295"],
		"Uid": "1234"
	},
	"RootDirectory": {
		"CreationInfo": {
			"OwnerGid": "1000",
			"OwnerUid": "1234",
			"Permissions": "777"
		},
		"Path": "/tmp/example"
	}
}
```