# AwsEcsCluster<a name="asff-resourcedetails-awsecscluster"></a>

The `AwsEcsCluster` object provides details about an Amazon Elastic Container Service cluster\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcsCluster` object\. To view descriptions of `AwsEcsCluster` attributes, see [AwsEcsClusterDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcsClusterDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
    "AwsEcsCluster": {
        "CapacityProviders": [],
        "ClusterSettings": [
            {
                "Name": "containerInsights",
                "Value": "enabled"
            }
        ],
        "Configuration": {
            "ExecuteCommandConfiguration": {
                "KmsKeyId": "kmsKeyId",
                "LogConfiguration": {
                    "CloudWatchEncryptionEnabled": true,
                    "CloudWatchLogGroupName": "cloudWatchLogGroupName",
                    "S3BucketName": "s3BucketName",
                    "S3EncryptionEnabled": true,
                    "S3KeyPrefix": "s3KeyPrefix"
                },
                "Logging": "DEFAULT"
            }
        }
        "DefaultCapacityProviderStrategy": [
            {
                "Base": 0,
                "CapacityProvider": "capacityProvider",
                "Weight": 1
            }
        ]
    }
```

**Contents**

The following is a list of valid value examples for `AwsCertificateManagerCertificate` attributes:
+ `ClusterSettings Name`

  Valid value: `containerInsights`
+ `ClusterSettings Value`

  Valid values: `enabled` \| `disabled`