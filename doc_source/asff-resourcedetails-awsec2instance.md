# AwsEc2Instance<a name="asff-resourcedetails-awsec2instance"></a>

The `AwsEc2Instance` object provides details about an Amazon EC2 instance\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Instance` object\. To view descriptions of `AwsEc2Instance` attributes, see [AwsEc2InstanceDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2InstanceDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
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
```