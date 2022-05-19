# AwsS3Bucket<a name="asff-resourcedetails-awss3bucket"></a>

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
                   "DaysAfterInitiation: 5
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

The following is a list of valid value examples for `AwsS3Bucket` attributes:
+ `Filter Type`

  Valid values: `LifecycleAndOperator` \| `LifecycleOrOperator`
+ `Filter Operands Type`

  Valid values: `LifecyclePrefixPredicate` \| `LifecycleTagPredicate`
+ `StorageClass`

  Valid values: `GLACIER` \| `STANDARD_IA` \|` ONEZONE_IA` \| `INTELLIGENT_TIERING` \| `DEEP_ARCHIVE`
+ `BucketNotificationConfiguration Type`

  Valid values: `LambdaConfiguration` \| `QueueConfiguration` \| `TopicConfiguration`
+ `Filter Name`

  Valid values: `prefix` \| `suffix`
+ `BucketVersioningConfiguration Status`

  Valid values: `Enabled` \| `Suspended`
+ `Protocol`

  Valid values: `http` \| `https`
+ `SSEAAlgorithm`

  Valid values: `AES256` \| `aws:kms`