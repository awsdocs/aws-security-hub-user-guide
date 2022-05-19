# AwsIamAccessKey<a name="asff-resourcedetails-awsiamaccesskey"></a>

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