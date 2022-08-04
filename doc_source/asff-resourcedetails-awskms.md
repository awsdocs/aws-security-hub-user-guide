# AwsKms<a name="asff-resourcedetails-awskms"></a>

The following are examples of the AWS Security Finding Format for `AwsKms` resources\.

## AwsKmsKey<a name="asff-resourcedetails-awskmskey"></a>

The `AwsKmsKey` object provides details about an AWS KMS key\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsKmsKey` object\. To view descriptions of `AwsKmsKey` attributes, see [AwsKmsKeyDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsKmsKeyDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsKmsKey": {
                        "AWSAccountId": "string",
                        "CreationDate": "string",
                        "Description": "string",
                        "KeyId": "string",
                        "KeyManager": "string",
                        "KeyRotationStatus": boolean,
                        "KeyState": "string",
                        "Origin": "string"
                    }
```