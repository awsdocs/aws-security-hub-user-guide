# AwsXray<a name="asff-resourcedetails-awsxray"></a>

The following are examples of the AWS Security Finding Format for `AwsXray` resources\.

## AwsXrayEncryptionConfig<a name="asff-resourcedetails-awsxrayencryptionconfig"></a>

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