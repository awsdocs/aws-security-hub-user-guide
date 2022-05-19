# Resource attributes<a name="asff-resources-attributes"></a>

In the `Resources` object, each resource object can have the following attributes\.

**[`DataClassification`](asff-resources-dataclassification.md)**  
Optional  
Used to provide details about sensitive data that was detected on a resource\.  
**Type:** Object

**`Details`**  
Optional  
This field provides additional details about a single resource using the appropriate objects\.  
Note that if the finding size exceeds the maximum of 240 KB, then the `Details` object is removed from the finding\. For findings for controls that use AWS Config rules, you can view the resource details on the AWS Config console\.  
Each resource must be provided in a separate resource object in the `Resources` object\.  
Security Hub provides a set of available resource details objects for its supported resource types\. These objects correspond to values of the resource `Type`\. Use the provided types and objects whenever possible\.  
For example, if the resource is an S3 bucket, then set the resource `Type` to `AwsS3Bucket` and provide the resource details in the [`AwsS3Bucket`](asff-resourcedetails-awss3bucket.md) object\.  
The [`Other`](asff-resourcedetails-other.md) object allows you to provide custom fields and values\. You use the [`Other`](asff-resourcedetails-other.md) object in the following cases\.  
+ The resource type \(the value of the resource `Type`\) does not have a corresponding details object\. To provide details for the resource, you use the [`Other`](asff-resourcedetails-other.md) details object\.
+ The object for the resource type does not include all of the fields that you want to populate\. In this case, use the details object for the resource type to populate the available fields\. Use the `Other` object to populate the fields that are not in the type\-specific object\.
+ The resource type is not one of the provided types\. In this case, set the resource `Type` to `Other`, and use the [`Other`](asff-resourcedetails-other.md) details object to populate the details\.
**Type:** Object  
**Example**  

```
"Details": {
  "AwsEc2Instance": {
    "Type": "i3.xlarge",
    "ImageId": "ami-abcd1234",
    "IpV4Addresses": [ "54.194.252.215", "192.168.1.88" ],
    "IpV6Addresses": [ "2001:db8:1234:1a2b::123" ],
    "KeyName": "my_keypair",
    "IamInstanceProfileArn": "arn:aws:iam::111111111111:instance-profile/AdminRole",
    "VpcId": "vpc-11112222",
    "SubnetId": "subnet-56f5f633",
    "LaunchedAt": "2018-05-08T16:46:19.000Z"
  },
  "AwsS3Bucket": {
    "OwnerId": "da4d66eac431652a4d44d490a00500bded52c97d235b7b4752f9f688566fe6de",
    "OwnerName": "acmes3bucketowner"
  },
  "Other": { "LightPen": "blinky", "SerialNo": "1234abcd"}  
}
```

**`Id`**  
Required  
The canonical identifier for the given resource type\.  
For AWS resources that are identified by ARNs, this must be the ARN\.  
For all other AWS resource types that lack ARNs, this must be the identifier as defined by the AWS service that created the resource\.  
For non AWS resources, this should be a unique identifier that is associated with the resource\.  
**Type:** String or ARN  
**Maximum length:** 512  
**Example**  

```
"Id": "arn:aws:s3:::example-bucket"
```

**`Partition`**  
Optional  
The canonical AWS partition name that the Region is assigned to\.   
**Type:** Enum  
**Valid values:**      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/asff-resources-attributes.html)
**Example**  

```
"Partition": "aws"
```

**`Region`**  
Optional  
The canonical AWS external Region name where this resource is located\.   
**Type:** String  
**Maximum length:** 16  
**Example**  

```
"Region": "us-west-2"
```

**`ResourceRole`**  
Optional  
Identifies the role of the resource in the finding\. A resource is either the target of the finding activity or the actor that performed the activity\.  
**Type:** String  
**Valid values:** `Actor` \| `Target`

**`Tags`**  
Optional  
A list of AWS tags that are associated with a resource at the time the finding was processed\. Include the `Tags` attribute only for resources that have an associated tag\. If a resource has no associated tag, don't include a `Tags` attribute in the finding\.  
**Type: **Map of tags  
**Maximum number of tags:** 50  
**Maximum length per value:** 256  
The following basic restrictions apply to tags:  
+ You can provide only tags that actually exist on an AWS resource in this field\. To provide data for a resource type that isn't defined in the AWS Security Finding Format, use the `Other` details subfield\.
+ Values are limited to the following characters: A\-Z, a\-z, 0\-9, blank spaces, and \. : \+ = @ \_ / \- \(hyphen\)\.
+ Values are limited to the AWS tag value length of 256 characters max\.
**Example**  

```
"Tags": {
    "billingCode": "Lotus-1-2-3",
    "needsPatching": "true"
}
```

**`Type`**  
Required  
The type of the resource that you are providing details for\.  
Whenever possible, use one of the provided resource types, such as `AwsEc2Instance` or `AwsS3Bucket`\.  
If the resource type does not match any of the provided resource types, then set the resource `Type` to `Other`, and use the `Other` details subfield to populate the details\.  
**Type:** String  
**Maximum length:** 256  
Supported values are as follows\. If a type has a corresponding `Details` object, then to view the details for the `Details` object, choose the type name\.  
+ `AwsAccount`
+ `AwsApiGatewayMethod`
+ [`AwsApiGatewayRestApi`](asff-resourcedetails-awsapigatewayrestapi.md)
+ [`AwsApiGatewayStage`](asff-resourcedetails-awsapigatewaystage.md)
+ [`AwsApiGatewayV2Api`](asff-resourcedetails-awsapigatewayv2api.md)
+ [`AwsApiGatewayV2Stage`](asff-resourcedetails-awsapigatewayv2stage.md)
+ `AwsAppStreamFleet`
+ [`AwsAutoscalingAutoscalingGroup`](asff-resourcedetails-awsautoscalingautoscalinggroup.md)
+ [`AwsAutoscalingLaunchConfiguration`](asff-resourcedetails-awsautoscalinglaunchconfiguration.md)
+ [`AwsCertificateManagerCertificate`](asff-resourcedetails-awscertificatemanagercertificate.md)
+ `AwsCloudFormationStack`
+ [`AwsCloudFrontDistribution`](asff-resourcedetails-awscloudfrontdistribution.md)
+ [`AwsCloudTrailTrail`](asff-resourcedetails-awscloudtrailtrail.md)
+ `AwsCloudWatchAlarm`
+ [`AwsCodeBuildProject`](asff-resourcedetails-awscodebuildproject.md)
+ `AwsCodeCommitRepository`
+ `AwsCodeDeployApplication`
+ `AwsCodeDeployDeploymentGroup`
+ `AwsCodePipelinePipeline`
+ `AwsCognitoIdentityPool`
+ `AwsCognitoUserPool`
+ `AwsDmsReplicationInstance`
+ [`AwsDynamoDbTable`](asff-resourcedetails-awsdynamodbtable.md)
+ [`AwsEc2Eip`](asff-resourcedetails-awsec2eip.md)
+ [`AwsEc2Instance`](asff-resourcedetails-awsec2instance.md)
+ [`AwsEc2NetworkAcl`](asff-resourcedetails-awsec2networkacl.md)
+ [`AwsEc2NetworkInterface`](asff-resourcedetails-awsec2networkinterface.md)
+ [`AwsEc2SecurityGroup`](asff-resourcedetails-awsec2securitygroup.md)
+ `AwsEc2Snapshot`
+ [`AwsEc2Subnet`](asff-resourcedetails-awsec2subnet.md)
+ [`AwsEc2Volume`](asff-resourcedetails-awsec2volume.md)
+ [`AwsEc2Vpc`](asff-resourcedetails-awsec2vpc.md)
+ [`AwsEc2VpnConnection`](asff-resourcedetails-awsec2vpnconnection.md)
+ [`AwsEc2VpcEndPointService`](asff-resourcedetails-awsec2vpcendpointservice.md)
+ [`AwsEcrContainerImage`](asff-resourcedetails-awsecrcontainerimage.md)
+ [`AwsEcrRepository`](asff-resourcedetails-awsecrrepository.md)
+ [`AwsEcsCluster`](asff-resourcedetails-awsecscluster.md)
+ [`AwsEcsService`](asff-resourcedetails-awsecsservice.md)
+ [`AwsEcsTaskDefinition`](asff-resourcedetails-awsecstaskdefinition.md)
+ `AwsEfsFileSystem`
+ [`AwsEksCluster`](asff-resourcedetails-awsekscluster.md)
+ `AwsElastiCacheCacheCluster`
+ [`AwsElasticBeanstalkEnvironment`](asff-resourcedetails-awselasticbeanstalkenvironment.md)
+ [`AwsElasticsearchDomain`](asff-resourcedetails-awselasticsearchdomain.md)
+ [`AwsElbLoadBalancer`](asff-resourcedetails-awselbloadbalancer.md)``
+ [`AwsElbv2LoadBalancer`](asff-resourcedetails-awselbv2loadbalancer.md)
+ AwsEmrCluster
+ [`AwsIamAccessKey`](asff-resourcedetails-awsiamaccesskey.md)
+ [`AwsIamGroup`](asff-resourcedetails-awsiamgroup.md)
+ [`AwsIamPolicy`](asff-resourcedetails-awsiampolicy.md)
+ [`AwsIamRole`](asff-resourcedetails-awsiamrole.md)
+ [`AwsIamUser`](asff-resourcedetails-awsiamuser.md)
+ `AwsKinesisStream`
+ [`AwsKmsKey`](asff-resourcedetails-awskmskey.md)
+ [`AwsLambdaFunction`](asff-resourcedetails-awslambdafunction.md)
+ [`AwsLambdaLayerVersion`](asff-resourcedetails-awslambdalayerversion.md)
+ `AwsLogsLogGroup`
+ [`AwsNetworkFirewallFirewall`](asff-resourcedetails-awsnetworkfirewallfirewall.md)
+ [`AwsNetworkFirewallFirewallPolicy`](asff-resourcedetails-awsnetworkfirewallfirewallpolicy.md)
+ [`AwsNetworkFirewallRuleGroup`](asff-resourcedetails-awsnetworkfirewallrulegroup.md)
+ [`AwsOpenSearchServiceDomain`](asff-resourcedetails-awsopensearchservicedomain.md)
+ [`AwsRdsDbCluster`](asff-resourcedetails-awsrdsdbcluster.md)
+ [`AwsRdsDbClusterSnapshot`](asff-resourcedetails-awsrdsdbclustersnapshot.md)
+ [`AwsRdsDbInstance`](asff-resourcedetails-awsrdsdbinstance.md)
+ [`AwsRdsDbSnapshot`](asff-resourcedetails-awsrdsdbsnapshot.md)
+ [`AwsRdsEventSubscription`](asff-resourcedetails-awsrdseventsubscription.md)
+ [`AwsRedshiftCluster`](asff-resourcedetails-awsredshiftcluster.md)
+ [`AwsS3AccountPublicAccessBlock`](asff-resourcedetails-awss3accountpublicaccessblock.md)
+ [`AwsS3Bucket`](asff-resourcedetails-awss3bucket.md)
+ [`AwsS3Object`](asff-resourcedetails-awss3object.md)
+ `AwsSageMakerNotebookInstance`
+ [`AwsSecretsManagerSecret`](asff-resourcedetails-awssecretsmanagersecret.md)
+ [`AwsSnsTopic`](asff-resourcedetails-awssnstopic.md)
+ [`AwsSqsQueue`](asff-resourcedetails-awssqsqueue.md)
+ `AwsSsmAssociationCompliance`
+ [`AwsSsmPatchCompliance`](asff-resourcedetails-awsssmpatchcompliance.md)
+ [`AwsWafRateBasedRule`](asff-resourcedetails-awswafratebasedrule.md)
+ [`AwsWafRegionalRateBasedRule`](asff-resourcedetails-awswafregionalratebasedrule.md)
+ [`AwsWafWebAcl`](asff-resourcedetails-awswafwebacl.md)
+ [`AwsXrayEncryptionConfig`](asff-resourcedetails-awsxrayencryptionconfig.md)
+ [`Container`](asff-resourcedetails-container.md)
+ [`Other`](asff-resourcedetails-other.md)
**Example**  

```
"Type": "AwsS3Bucket"
```