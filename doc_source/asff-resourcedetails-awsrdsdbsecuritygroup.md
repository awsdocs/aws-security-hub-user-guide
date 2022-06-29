# AwsRdsDbSecurityGroup<a name="asff-resourcedetails-awsrdsdbsecuritygroup"></a>

The `AwsRdsDbSecurityGroup` object contains information about an Amazon Relational Database Service security group\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsRdsDbSecurityGroup` object\. To view descriptions of `AwsRdsDbSecurityGroup` attributes, see [AwsRdsDbSecurityGroupDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsRdsDbSecurityGroupDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsRdsDbSecurityGroup": {
    "DbSecurityGroupArn": "arn:aws:rds:us-west-1:111122223333:secgrp:default",
    "DbSecurityGroupDescription": "default",
    "DbSecurityGroupName": "mysecgroup",
    "Ec2SecurityGroups": [
        {
          "Ec2SecurityGroupuId": "myec2group",
          "Ec2SecurityGroupName": "default",
          "Ec2SecurityGroupOwnerId": "987654321021",
          "Status": "authorizing"
        }
    ],
    "IpRanges": [
        {
          "Cidrip": "0.0.0.0/0",
          "Status": "authorizing"
        }
    ],
    "OwnerId": "123456789012",
    "VpcId": "vpc-1234567f"
}
```