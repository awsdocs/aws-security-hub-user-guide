# AwsS3<a name="asff-resourcedetails-awss3"></a>

The following are examples of the AWS Security Finding Format for `AwsS3` resources\.

## AwsS3AccountPublicAccessBlock<a name="asff-resourcedetails-awss3accountpublicaccessblock"></a>

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

## AwsS3Bucket<a name="asff-resourcedetails-awss3bucket"></a>

The `AwsS3Bucket` object provides details about an Amazon S3 bucket\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsS3Bucket` object\. To view descriptions of `AwsS3Bucket` attributes, see [AwsS3BucketDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsS3BucketDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsS3Bucket": {
    "OwnerId": "AIDACKCEVSQ6C2EXAMPLE",
    "OwnerName": "s3bucketowner",
    "CreatedAt": "2007-11-30T01:46:56.000Z",
    "ServerSideEncryptionConfiguration": {
        "Rules": [
            {
                "ApplyServerSideEncryptionByDefault": {
                    "SSEAlgorithm": "AES256",
                    "KMSMasterKeyID": "12345678-abcd-abcd-abcd-123456789012"
                }
            }
        ]
     },
    "BucketLifecycleConfiguration": {
       "Rules": [
           {
               "AbortIncompleteMultipartUpload": {
                   "DaysAfterInitiation": 5
               },
               "ExpirationDate": "2021-11-10T00:00:00.000Z",
               "ExpirationInDays": 365,
               "ExpiredObjectDeleteMarker": false,
               "Filter: {
                   "Predicate": {
                       "Operands": [
                           {
                               "Prefix": "tmp/",
                               "Type": "LifecyclePrefixPredicate"
                           },
                           {
                               "Tag": {
                                   "Key": "ArchiveAge",
                                   "Value": "9m"
                               },
                               "Type": "LifecycleTagPredicate"
                           }
                       ],
                       "Type": "LifecycleAndOperator"
                   }
               },
               "ID": "Move rotated logs to Glacier",
               "NoncurrentVersionExpirationInDays": -1,
               "NoncurrentVersionTransitions": [
                   {
                       "Days": 2,
                       "StorageClass": "GLACIER"
                   }
               ],
               "Prefix": "rotated/",
               "Status": "Enabled",
               "Transitions": [
                   {
                       "Date": "2020-11-10T00:00:00.000Z",
                       "Days": 100,
                       "StorageClass": "GLACIER"
                   }
               ]
           }
       ]
    },
    "PublicAccessBlockConfiguration": {
        "BlockPublicAcls": true,
        "BlockPublicPolicy": true,
        "IgnorePublicAcls": true,
        "RestrictPublicBuckets": true,
    }
}
```

## AwsS3Object<a name="asff-resourcedetails-awss3object"></a>

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