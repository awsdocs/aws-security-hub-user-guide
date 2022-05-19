# AwsIamPolicy<a name="asff-resourcedetails-awsiampolicy"></a>

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