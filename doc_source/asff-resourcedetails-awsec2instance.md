# AwsEc2Instance<a name="asff-resourcedetails-awsec2instance"></a>

The `AwsEc2Instance` object provides details about an Amazon EC2 instance\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Instance` object\. To view descriptions of `AwsEc2Instance` attributes, see [AwsEc2InstanceDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2InstanceDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2Instance": { 
     "IamInstanceProfileArn": "arn:aws:iam::123456789012:role/IamInstanceProfileArn",
     "ImageId": "ami-79fd7eee",
     "IpV4Addresses": ["1.1.1.1"],
     "IpV6Addresses": ["2001:db8:1234:1a2b::123"],
     "KeyName": "testkey",
     "LaunchedAt": "2018-09-29T01:25:54Z",
     "MetadataOptions": {
          "HttpEndpoint": "enabled",
          "HttpProtocolIpv6": "enabled",
          "HttpPutResponseHopLimit": 1,
          "HttpTokens": "optional",
          "InstanceMetadataTags": "disabled"
     },
     "NetworkInterfaces": [
       {
          "NetworkInterfaceId": "eni-e5aa89a3"
       }
     ],
     "SubnetId": "PublicSubnet",
     "Type": "i3.xlarge",
     "VirtualizationType": "hvm",
     "VpcId": "TestVPCIpv6"
}
```