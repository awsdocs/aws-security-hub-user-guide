# AwsEcrRepository<a name="asff-resourcedetails-awsecrrepository"></a>

The `AwsEcrRepository` object provides information about an Amazon Elastic Container Registry repository\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcrRepository` object\. To view descriptions of `AwsEcrRepository` attributes, see [AwsEcrRepositoryDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcrRepositoryDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEcrRepository": {
    "LifecyclePolicy": {
        "RegistryId": "123456789012",
    },  
    "RepositoryName": "sample-repo",
    "Arn": "arn:aws:ecr:us-west-2:111122223333:repository/sample-repo",
    "ImageScanningConfiguration": {
        "ScanOnPush": true
    },
    "ImageTagMutability": "IMMUTABLE"
}
```

The following is a list of valid value examples for `AwsEcrRepository` attributes:
+ `ImageTagMutability`

  Valid values: `MUTABLE` \| `IMMUTABLE`