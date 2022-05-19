# AwsS3Object<a name="asff-resourcedetails-awss3object"></a>

The `AwsS3Object` object provides information about an Amazon S3 object\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsS3Object` object\. To view descriptions of `AwsS3Object` attributes, see [AwsS3ObjectDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsS3ObjectDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsS3Object": {
    "ContentType": "text/html",
    "ETag": "\"30a6ec7e1a9ad79c203d05a589c8b400\"",
    "LastModified": "2012-04-23T18:25:43.511Z",
    "ServerSideEncryption": "aws:kms",
    "SSEKMSKeyId": "arn:aws:kms:us-west-2:123456789012:key/4dff8393-e225-4793-a9a0-608ec069e5a7",
    "VersionId": "ws31OurgOOjH_HHllIxPE35P.MELYaYh"
}
```