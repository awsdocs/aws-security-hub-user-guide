# AwsEc2SecurityGroup<a name="asff-resourcedetails-awsec2securitygroup"></a>

The `AwsEc2SecurityGroup` object describes an Amazon EC2 security group\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2SecurityGroup` object\. To view descriptions of `AwsEc2SecurityGroup` attributes, see [AwsEc2SecurityGroupDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2SecurityGroupDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2SecurityGroup": {
    "GroupName": "MySecurityGroup",
    "GroupId": "sg-903004f8",
    "OwnerId": "123456789012",
    "VpcId": "vpc-1a2b3c4d",
    "IpPermissions": [
        {
            "IpProtocol": "-1",
            "IpRanges": [],
            "UserIdGroupPairs": [
                {
                    "UserId": "123456789012",
                    "GroupId": "sg-903004f8"
                }
            ],
            "PrefixListIds": [
                {"PrefixListId": "pl-63a5400a"}
            ]
        },
        {
            "PrefixListIds": [],
            "FromPort": 22,
            "IpRanges": [
                {
                    "CidrIp": "203.0.113.0/24"
                }
            ],
            "ToPort": 22,
            "IpProtocol": "tcp",
            "UserIdGroupPairs": []
        }
    ]
}
```