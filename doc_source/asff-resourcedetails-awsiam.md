# AwsIam<a name="asff-resourcedetails-awsiam"></a>

The following are examples of the AWS Security Finding Format for `AwsIam` resources\.

## AwsIamAccessKey<a name="asff-resourcedetails-awsiamaccesskey"></a>

The `AwsIamAccessKey` object contains details about an IAM access key that is related to a finding\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsIamAccessKey` object\. To view descriptions of `AwsIamAccessKey` attributes, see [AwsIamAccessKeyDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsIamAccessKeyDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsIamAccessKey": { 
                        "AccessKeyId": "string",
                        "AccountId": "string",
                        "CreatedAt": "string",
                        "PrincipalId": "string",
                        "PrincipalName": "string",
                        "PrincipalType": "string",
                        "SessionContext": {
                            "Attributes": {
                                "CreationDate": "string",
                                "MfaAuthenticated": boolean
                            },
                            "SessionIssuer": {
                                "AccountId": "string",
                                "Arn": "string",
                                "PrincipalId": "string",
                                "Type": "string",
                                "UserName": "string"
                            }
                        },
                        "Status": "string"
                    }
```

## AwsIamGroup<a name="asff-resourcedetails-awsiamgroup"></a>

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

## AwsIamPolicy<a name="asff-resourcedetails-awsiampolicy"></a>

The `AwsIamPolicy` object represents an IAM permissions policy\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsIamPolicy` object\. To view descriptions of `AwsIamPolicy` attributes, see [AwsIamPolicyDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsIamPolicyDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsIamPolicy": {
    "AttachmentCount": 1,
    "CreateDate": "2017-09-14T08:17:29.000Z",
    "DefaultVersionId": "v1",
    "Description": "Example IAM policy",
    "IsAttachable": true,
    "Path": "/",
    "PermissionsBoundaryUsageCount": 5,
    "PolicyId": "ANPAJ2UCCR6DPCEXAMPLE",
    "PolicyName": "EXAMPLE-MANAGED-POLICY",
    "PolicyVersionList": [
        {
            "VersionId": "v1",
            "IsDefaultVersion": true,
            "CreateDate": "2017-09-14T08:17:29.000Z"
        }
    ],
    "UpdateDate": "2017-09-14T08:17:29.000Z"
}
```

## AwsIamRole<a name="asff-resourcedetails-awsiamrole"></a>

The `AwsIamRole` object contains information about an IAM role, including all of the role's policies\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsIamRole` object\. To view descriptions of `AwsIamRole` attributes, see [AwsIamRoleDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsIamRoleDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsIamRole": {
    "AssumeRolePolicyDocument": "{'Version': '2012-10-17','Statement': [{'Effect': 'Allow','Action': 'sts:AssumeRole'}]}",
    "AttachedManagedPolicies": [
        {
            "PolicyArn": "arn:aws:iam::aws:policy/ExamplePolicy1",
            "PolicyName": "Example policy 1"
        },
        {
            "PolicyArn": "arn:aws:iam::444455556666:policy/ExamplePolicy2",
            "PolicyName": "Example policy 2"
        }
        ],
        "CreateDate": "2020-03-14T07:19:14.000Z",
        "InstanceProfileList": [
            {
                "Arn": "arn:aws:iam::333333333333:ExampleProfile",
                "CreateDate": "2020-03-11T00:02:27Z",
                "InstanceProfileId": "AIPAIXEU4NUHUPEXAMPLE",
                "InstanceProfileName": "ExampleInstanceProfile",
                "Path": "/",
                "Roles": [
                    {
                       "Arn": "arn:aws:iam::444455556666:role/example-role",
                        "AssumeRolePolicyDocument": "",
                        "CreateDate": "2020-03-11T00:02:27Z",
                        "Path": "/",
                        "RoleId": "AROAJ52OTH4H7LEXAMPLE",
                        "RoleName": "example-role",
                    }
                ]
            }
        ],
        "MaxSessionDuration": 3600,
        "Path": "/",
        "PermissionsBoundary": {
            "PermissionsBoundaryArn": "arn:aws:iam::aws:policy/AdministratorAccess",
            "PermissionsBoundaryType": "PermissionsBoundaryPolicy"
        },
        "RoleId": "AROA4TPS3VLEXAMPLE",
        "RoleName": "BONESBootstrapHydra-OverbridgeOpsFunctionsLambda",
        "RolePolicyList": [
            {
                "PolicyName": "Example role policy"
            }
        ]
    }
```

## AwsIamUser<a name="asff-resourcedetails-awsiamuser"></a>

The `AwsIamUser` object provides information about a user\.

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