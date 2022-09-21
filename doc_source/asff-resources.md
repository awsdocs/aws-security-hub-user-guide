# Resources<a name="asff-resources"></a>

The `Resources` object provides information about the resources involved in a finding\.

It contains an array of up to 32 resource objects\.

**Example**

```
"Resources": [
  {
    "Type": "AwsEc2Instance",
    "Id": "arn:aws:ec2:us-west-2:111122223333:instance/i-1234567890abcdef0",
    "Partition": "aws",
    "Region": "us-west-2",
    "ResourceRole": "Target",
    "Tags": {
        "billingCode": "Lotus-1-2-3",
        "needsPatching": "true"
    },
    "Details": {
        "AwsEc2Instance": {
            "IamInstanceProfileArn": "string",
            "ImageId": "string",
            "IpV4Addresses": [ "string" ],
            "IpV6Addresses": [ "string" ],
            "KeyName": "string",
            "LaunchedAt": "string",
            "NetworkInterfaces": [
             {
                "NetworkInterfaceId": "string"
             }
            ],
            "SubnetId": "string",
            "Type": "string",
            "VpcId": "string"
        }
    }
  }
]
```

**Topics**
+ [Resource attributes](asff-resources-attributes.md)
+ [AwsApiGateway](asff-resourcedetails-awsapigateway.md)
+ [AwsAutoScaling](asff-resourcedetails-awsautoscaling.md)
+ [AwsBackup](asff-resourcedetails-awsbackup.md)
+ [AwsCertificateManager](asff-resourcedetails-awscertificatemanager.md)
+ [AwsCloudFormation](asff-resourcedetails-awscloudformation.md)
+ [AwsCloudFront](asff-resourcedetails-awscloudfront.md)
+ [AwsCloudTrail](asff-resourcedetails-awscloudtrail.md)
+ [AwsCloudWatch](asff-resourcedetails-awscloudwatch.md)
+ [AwsCodeBuild](asff-resourcedetails-awscodebuild.md)
+ [AwsDynamoDB](asff-resourcedetails-awsdynamodb.md)
+ [AwsEc2](asff-resourcedetails-awsec2.md)
+ [AwsEcr](asff-resourcedetails-awsecr.md)
+ [AwsEcs](asff-resourcedetails-awsecs.md)
+ [AwsEfs](asff-resourcedetails-awsefs.md)
+ [AwsEks](asff-resourcedetails-awseks.md)
+ [AwsElasticBeanstalk](asff-resourcedetails-awselasticbeanstalk.md)
+ [AwsElasticSearch](asff-resourcedetails-awselasticsearch.md)
+ [AwsElb](asff-resourcedetails-awselb.md)
+ [AwsIam](asff-resourcedetails-awsiam.md)
+ [AwsKinesis](asff-resourcedetails-awskinesis.md)
+ [AwsKms](asff-resourcedetails-awskms.md)
+ [AwsLambda](asff-resourcedetails-awslambda.md)
+ [AwsNetworkFirewall](asff-resourcedetails-awsnetworkfirewall.md)
+ [AwsOpenSearchService](asff-resourcedetails-awsopensearchservice.md)
+ [AwsRds](asff-resourcedetails-awsrds.md)
+ [AwsRedshift](asff-resourcedetails-awsredshift.md)
+ [AwsS3](asff-resourcedetails-awss3.md)
+ [AwsSecretsManager](asff-resourcedetails-awssecretsmanager.md)
+ [AwsSns](asff-resourcedetails-awssns.md)
+ [AwsSqs](asff-resourcedetails-awssqs.md)
+ [AwsSsm](asff-resourcedetails-awsssm.md)
+ [AwsWaf](asff-resourcedetails-awswaf.md)
+ [AwsXray](asff-resourcedetails-awsxray.md)
+ [Container](asff-resourcedetails-container.md)
+ [Other](asff-resourcedetails-other.md)