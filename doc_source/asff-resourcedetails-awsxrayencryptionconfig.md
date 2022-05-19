# AwsXrayEncryptionConfig<a name="asff-resourcedetails-awsxrayencryptionconfig"></a>

The `AwsXrayEncryptionConfig` object contains information about the encryption configuration for AWS X\-Ray\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsXrayEncryptionConfig` object\. To view descriptions of `AwsXrayEncryptionConfig` attributes, see [AwsXrayEncryptionConfigDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsXrayEncryptionConfigDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsXRayEncryptionConfig":{
    "KeyId": "arn:aws:kms:us-east-2:222222222222:key/example-key",
    "Status": "UPDATING",
    "Type":"KMS"
}
```

The following is a list of valid value examples for `AwsXRayEncryptionConfig` attributes:
+ `Status`

  Valid values: `UPDATING` \| `ACTIVE`
+ `Type`

  Valid values: `NONE` \| `KMS`