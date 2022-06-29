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
        "Type": "i3.xlarge",
        "ImageId": "ami-abcd1234",
        "IpV4Addresses": [ "54.194.252.215", "192.168.1.88" ],
        "IpV6Addresses": [ "2001:db8:1234:1a2b::123" ],
        "KeyName": "my_keypair",
        "IamInstanceProfileArn": "arn:aws:iam::111111111111:instance-profile/AdminRole",
        "VpcId": "vpc-11112222",
        "SubnetId": "subnet-56f5f633",
        "LaunchedAt": "2018-05-08T16:46:19.000Z"
      }  
    }
  }
]
```

**Topics**
+ [Resource attributes](asff-resources-attributes.md)
+ [DataClassification](asff-resources-dataclassification.md)
+ [AwsApiGatewayRestApi](asff-resourcedetails-awsapigatewayrestapi.md)
+ [AwsApiGatewayStage](asff-resourcedetails-awsapigatewaystage.md)
+ [AwsApiGatewayV2Api](asff-resourcedetails-awsapigatewayv2api.md)
+ [AwsApiGatewayV2Stage](asff-resourcedetails-awsapigatewayv2stage.md)
+ [AwsAutoScalingAutoScalingGroup](asff-resourcedetails-awsautoscalingautoscalinggroup.md)
+ [AwsAutoScalingLaunchConfiguration](asff-resourcedetails-awsautoscalinglaunchconfiguration.md)
+ [AwsCertificateManagerCertificate](asff-resourcedetails-awscertificatemanagercertificate.md)
+ [AwsCloudFormationStack](asff-resourcedetails-awscloudformationstack.md)
+ [AwsCloudFrontDistribution](asff-resourcedetails-awscloudfrontdistribution.md)
+ [AwsCloudTrailTrail](asff-resourcedetails-awscloudtrailtrail.md)
+ [AwsCloudWatchAlarm](asff-resourcedetails-awscloudwatchalarm.md)
+ [AwsCodeBuildProject](asff-resourcedetails-awscodebuildproject.md)
+ [AwsDynamoDbTable](asff-resourcedetails-awsdynamodbtable.md)
+ [AwsEc2Eip](asff-resourcedetails-awsec2eip.md)
+ [AwsEc2Instance](asff-resourcedetails-awsec2instance.md)
+ [AwsEc2NetworkAcl](asff-resourcedetails-awsec2networkacl.md)
+ [AwsEc2NetworkInterface](asff-resourcedetails-awsec2networkinterface.md)
+ [AwsEc2SecurityGroup](asff-resourcedetails-awsec2securitygroup.md)
+ [AwsEc2Subnet](asff-resourcedetails-awsec2subnet.md)
+ [AwsEc2TransitGateway](asff-resourcedetails-awsec2transitgateway.md)
+ [AwsEc2Volume](asff-resourcedetails-awsec2volume.md)
+ [AwsEc2Vpc](asff-resourcedetails-awsec2vpc.md)
+ [AwsEc2VpcEndpointService](asff-resourcedetails-awsec2vpcendpointservice.md)
+ [AwsEc2VpcPeeringConnection](asff-resourcedetails-awsec2vpcpeeringconnection.md)
+ [AwsEc2VpnConnection](asff-resourcedetails-awsec2vpnconnection.md)
+ [AwsEcrContainerImage](asff-resourcedetails-awsecrcontainerimage.md)
+ [AwsEcrRepository](asff-resourcedetails-awsecrrepository.md)
+ [AwsEcsCluster](asff-resourcedetails-awsecscluster.md)
+ [AwsEcsContainer](asff-resourcedetails-awsecscontainer.md)
+ [AwsEcsService](asff-resourcedetails-awsecsservice.md)
+ [AwsEcsTask](asff-resourcedetails-awsecstask.md)
+ [AwsEcsTaskDefinition](asff-resourcedetails-awsecstaskdefinition.md)
+ [AwsEfsAccessPoint](asff-resourcedetails-awsefsaccesspoint.md)
+ [AwsEksCluster](asff-resourcedetails-awsekscluster.md)
+ [AwsElasticBeanstalkEnvironment](asff-resourcedetails-awselasticbeanstalkenvironment.md)
+ [AwsElasticSearchDomain](asff-resourcedetails-awselasticsearchdomain.md)
+ [AwsElbLoadBalancer](asff-resourcedetails-awselbloadbalancer.md)
+ [AwsElbv2LoadBalancer](asff-resourcedetails-awselbv2loadbalancer.md)
+ [AwsIamAccessKey](asff-resourcedetails-awsiamaccesskey.md)
+ [AwsIamGroup](asff-resourcedetails-awsiamgroup.md)
+ [AwsIamPolicy](asff-resourcedetails-awsiampolicy.md)
+ [AwsIamRole](asff-resourcedetails-awsiamrole.md)
+ [AwsIamUser](asff-resourcedetails-awsiamuser.md)
+ [AwsKinesisStream](asff-resourcedetails-awskinesisstream.md)
+ [AwsKmsKey](asff-resourcedetails-awskmskey.md)
+ [AwsLambdaFunction](asff-resourcedetails-awslambdafunction.md)
+ [AwsLambdaLayerVersion](asff-resourcedetails-awslambdalayerversion.md)
+ [AwsNetworkFirewallFirewall](asff-resourcedetails-awsnetworkfirewallfirewall.md)
+ [AwsNetworkFirewallFirewallPolicy](asff-resourcedetails-awsnetworkfirewallfirewallpolicy.md)
+ [AwsNetworkFirewallRuleGroup](asff-resourcedetails-awsnetworkfirewallrulegroup.md)
+ [AwsOpenSearchServiceDomain](asff-resourcedetails-awsopensearchservicedomain.md)
+ [AwsRdsDbCluster](asff-resourcedetails-awsrdsdbcluster.md)
+ [AwsRdsDbClusterSnapshot](asff-resourcedetails-awsrdsdbclustersnapshot.md)
+ [AwsRdsDbInstance](asff-resourcedetails-awsrdsdbinstance.md)
+ [AwsRdsDbSecurityGroup](asff-resourcedetails-awsrdsdbsecuritygroup.md)
+ [AwsRdsDbSnapshot](asff-resourcedetails-awsrdsdbsnapshot.md)
+ [AwsRdsEventSubscription](asff-resourcedetails-awsrdseventsubscription.md)
+ [AwsRedshiftCluster](asff-resourcedetails-awsredshiftcluster.md)
+ [AwsS3AccountPublicAccessBlock](asff-resourcedetails-awss3accountpublicaccessblock.md)
+ [AwsS3Bucket](asff-resourcedetails-awss3bucket.md)
+ [AwsS3Object](asff-resourcedetails-awss3object.md)
+ [AwsSecretsManagerSecret](asff-resourcedetails-awssecretsmanagersecret.md)
+ [AwsSnsTopic](asff-resourcedetails-awssnstopic.md)
+ [AwsSqsQueue](asff-resourcedetails-awssqsqueue.md)
+ [AwsSsmPatchCompliance](asff-resourcedetails-awsssmpatchcompliance.md)
+ [AwsWafRateBasedRule](asff-resourcedetails-awswafratebasedrule.md)
+ [AwsWafRegionalRateBasedRule](asff-resourcedetails-awswafregionalratebasedrule.md)
+ [AwsWafRegionalRule](asff-resourcedetails-awswafregionalrule.md)
+ [AwsWafRegionalRuleGroup](asff-resourcedetails-awswafregionalrulegroup.md)
+ [AwsWafRegionalWebAcl](asff-resourcedetails-awswafregionalwebacl.md)
+ [AwsWafRule](asff-resourcedetails-awswafrule.md)
+ [AwsWafRuleGroup](asff-resourcedetails-awswafrulegroup.md)
+ [AwsWafWebAcl](asff-resourcedetails-awswafwebacl.md)
+ [AwsXrayEncryptionConfig](asff-resourcedetails-awsxrayencryptionconfig.md)
+ [Container](asff-resourcedetails-container.md)
+ [Other](asff-resourcedetails-other.md)