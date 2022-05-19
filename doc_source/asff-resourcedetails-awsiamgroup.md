# AwsIamGroup<a name="asff-resourcedetails-awsiamgroup"></a>

The `AwsIamGroup` object contains details about an IAM group\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsIamGroup` object\. To view descriptions of `AwsIamGroup` attributes, see [AwsIamGroupDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsIamGroupDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsIamGroup": {
    "AttachedManagedPolicies": [
        {
            "PolicyArn": "arn:aws:iam::aws:policy/ExampleManagedAccess",
            "PolicyName": "ExampleManagedAccess",
        }
    ],
    "CreateDate": "2020-04-28T14:08:37.000Z",
    "GroupId": "AGPA4TPS3VLP7QEXAMPLE",
    "GroupName": "Example_User_Group",
    "GroupPolicyList": [
        {
            "PolicyName": "ExampleGroupPolicy"
        }
    ],
    "Path": "/"
}
```