# AwsEcsTask<a name="asff-resourcedetails-awsecstask"></a>

Provides details about an Amazon Elastic Container Service task\. 

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcsTask` object\. To view descriptions of `AwsEcsTask` attributes, see [AwsEcsTask](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcsTaskDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEcsTask": {
	"ClusterArn": "arn:aws:ecs:us-west-2:123456789012:task/MyCluster/1234567890123456789",
	"CreatedAt": "1557134011644",
	"Group": "service:fargate-service",
	"StartedAt": "1557134011644",
	"StartedBy": "ecs-svc/1234567890123456789",
	"TaskDefinitionArn": "arn:aws:ecs:us-west-2:123456789012:task-definition/sample-fargate:2",
	"Version": 3,
	"Volumes": [{
		"Name": "string",
		"Host": {
			"SourcePath": "string"
		}
	}],
	"Containers": {
		"Image": "1111111/knotejs@sha256:356131c9fef111111111111115f4ed8de5f9dce4dc3bd34bg21846588a3",
		"MountPoints": [{
			"ContainerPath": "/mnt/etc",
			"SourceVolume": "vol-03909e9"
		}],
		"Name": "knote",
		"Privileged": true
	}
}
```