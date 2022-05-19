# AwsEc2NetworkAcl<a name="asff-resourcedetails-awsec2networkacl"></a>

The `AwsEc2NetworkAcl` object contains details about an Amazon EC2 network access control list \(ACL\)\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2NetworkAcl` object\. To view descriptions of `AwsEc2NetworkAcl` attributes, see [AwsEc2NetworkAclDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2NetworkAclDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
AwsEc2NetworkAcl: {
    "IsDefault": false,
    "NetworkAclId": "acl-1234567890abcdef0",
    "OwnerId": "123456789012",
    "VpcId": "vpc-1234abcd",
    "Associations": [{
        "NetworkAclAssociationId": "aclassoc-abcd1234",
        "NetworkAclId": "acl-021345abcdef6789",
        "SubnetId": "subnet-abcd1234"
   }],
   "Entries": [{
        "CidrBlock": "10.24.34.0/23",
        "Egress": true,
        "IcmpTypeCode": {
            "Code": 10,
            "Type": 30
        },
        "Ipv6CidrBlock": "2001:DB8::/32",
        "PortRange": {
            "From": 20,
            "To": 40
        },
        "Protocol": "tcp",
        "RuleAction": "allow",
        "RuleNumber": 100
   }]
}
```