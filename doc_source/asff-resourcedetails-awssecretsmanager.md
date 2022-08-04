# AwsSecretsManager<a name="asff-resourcedetails-awssecretsmanager"></a>

The following are examples of the AWS Security Finding Format for `AwsSecretsManager` resources\.

## AwsSecretsManagerSecret<a name="asff-resourcedetails-awssecretsmanagersecret"></a>

The `AwsSecretsManagerSecret` object provides details about a Secrets Manager secret\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsSecretsManagerSecret` object\. To view descriptions of `AwsSecretsManagerSecret` attributes, see [AwsSecretsManagerSecretDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsSecretsManagerSecretDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsSecretsManagerSecret": {
    "RotationRules": {
        "AutomaticallyAfterDays": 30
    },
    "RotationOccurredWithinFrequency": true,
    "KmsKeyId": "kmsKeyId",
    "RotationEnabled": true,
    "RotationLambdaArn": "arn:aws:lambda:us-west-2:777788889999:function:MyTestRotationLambda",
    "Deleted": false,
    "Name": "MyTestDatabaseSecret",
    "Description": "My test database secret"
}
```