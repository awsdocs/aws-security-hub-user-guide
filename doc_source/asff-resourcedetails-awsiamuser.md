# AwsIamUser<a name="asff-resourcedetails-awsiamuser"></a>

The `AwsIamUser` object provides information about an IAM user\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsIamUser` object\. To view descriptions of `AwsIamUser` attributes, see [AwsIamUserDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsIamUserDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsIamUser": {
    "AttachedManagedPolicies": [
        {
            "PolicyName": "ExamplePolicy",
            "PolicyArn": "arn:aws:iam::aws:policy/ExampleAccess"
        }
    ],
    "CreateDate": "2018-01-26T23:50:05.000Z",
    "GroupList": [],
    "Path": "/",
    "PermissionsBoundary" : {
        "PermissionsBoundaryArn" : "arn:aws:iam::aws:policy/AdministratorAccess",
        "PermissionsBoundaryType" : "PermissionsBoundaryPolicy"
    },
    "UserId": "AIDACKCEVSQ6C2EXAMPLE",
    "UserName": "ExampleUser",
    "UserPolicyList": [
        {
            "PolicyName": "InstancePolicy"
        }
    ]
}
```