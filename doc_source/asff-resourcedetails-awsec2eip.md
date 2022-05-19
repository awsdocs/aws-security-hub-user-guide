# AwsEc2Eip<a name="asff-resourcedetails-awsec2eip"></a>

The `AwsEc2Eip` object provides information about an Elastic IP address\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Eip` object\. To view descriptions of `AwsEc2Eip` attributes, see [AwsEc2EipDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2EipDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2Eip": {
    "InstanceId": "instance1",
    "PublicIp": "192.0.2.04",
    "AllocationId": "eipalloc-example-id-1",
    "AssociationId": "eipassoc-example-id-1",
    "Domain": "vpc",
    "PublicIpv4Pool": "anycompany",
    "NetworkBorderGroup": "eu-central-1",
    "NetworkInterfaceId": "eni-example-id-1",
    "NetworkInterfaceOwnerId": "777788889999",
    "PrivateIpAddress": "192.0.2.03"
}
```