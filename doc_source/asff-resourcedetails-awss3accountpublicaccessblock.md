# AwsS3AccountPublicAccessBlock<a name="asff-resourcedetails-awss3accountpublicaccessblock"></a>

`AwsS3AccountPublicAccessBlock` provides information about the Amazon S3 Public Access Block configuration for accounts\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsS3AccountPublicAccessBlock` object\. To view descriptions of `AwsS3AccountPublicAccessBlock` attributes, see [AwsS3AccountPublicAccessBlockDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsS3AccountPublicAccessBlockDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsS3AccountPublicAccessBlock": {
    "BlockPublicAcls": true,
    "BlockPublicPolicy": true,
    "IgnorePublicAcls": false,
    "RestrictPublicBuckets": true
}
```