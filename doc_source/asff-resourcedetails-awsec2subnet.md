# AwsEc2Subnet<a name="asff-resourcedetails-awsec2subnet"></a>

The `AwsEc2Subnet` object provides information about a subnet in Amazon EC2\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Subnet` object\. To view descriptions of `AwsEc2Subnet` attributes, see [AwsEc2SubnetDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2SubnetDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
AwsEc2Subnet: {
    "AssignIpv6AddressOnCreation": false,
    "AvailabilityZone": "us-west-2c",
    "AvailabilityZoneId": "usw2-az3",
    "AvailableIpAddressCount": 8185,
    "CidrBlock": "10.0.0.0/24",
    "DefaultForAz": false,
    "MapPublicIpOnLaunch": false,
    "OwnerId": "123456789012",
    "State": "available",
    "SubnetArn": "arn:aws:ec2:us-west-2:123456789012:subnet/subnet-d5436c93",
    "SubnetId": "subnet-d5436c93",
    "VpcId": "vpc-153ade70",
    "Ipv6CidrBlockAssociationSet": [{
        "AssociationId": "subnet-cidr-assoc-EXAMPLE",
        "Ipv6CidrBlock": "2001:DB8::/32",
        "CidrBlockState": "associated"
   }]
}
```

The following is a list of valid value examples for `AwsEc2Subnet` attributes:
+ `State`

  Valid values: `pending` \| `available`
+ `CidrBlockState`

  Valid values: `associating` \| `associated` \| `disassociating` \| `disassociated` \| `failing` \| `failed`