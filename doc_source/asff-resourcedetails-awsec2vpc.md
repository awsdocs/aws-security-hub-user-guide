# AwsEc2Vpc<a name="asff-resourcedetails-awsec2vpc"></a>

The `AwsEc2Vpc` object provides details about an Amazon Elastic Compute Cloud virtual private cloud \(VPC\)\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Vpc` object\. To view descriptions of `AwsEc2Vpc` attributes, see [AwsEc2VpcDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2VpcDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2Vpc": {
    "CidrBlockAssociationSet": [
        {
            "AssociationId": "vpc-cidr-assoc-0dc4c852f52abda97",
            "CidrBlock": "192.0.2.0/24",
            "CidrBlockState": "associated"
        }
    ],
    "DhcpOptionsId": "dopt-4e42ce28",
    "Ipv6CidrBlockAssociationSet": [
        {
            "AssociationId": "vpc-cidr-assoc-0dc4c852f52abda97",
            "CidrBlockState": "associated",
            "Ipv6CidrBlock": "192.0.2.0/24"
       }

    ],
    "State": "available"
}
```

The following is a list of valid value examples for `AwsEc2Vpc` attributes:
+ `State`

  Valid values: `pending` \| `available`