# AwsRdsDbClusterSnapshot<a name="asff-resourcedetails-awsrdsdbclustersnapshot"></a>

The `AwsRdsDbClusterSnapshot` object contains information about an Amazon RDS database cluster snapshot\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsRdsDbClusterSnapshot` object\. To view descriptions of `AwsRdsDbClusterSnapshot` attributes, see [AwsRdsDbClusterSnapshotDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsRdsDbClusterSnapshotDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsRdsDbClusterSnaphot": {
    "AvailabilityZones": [
        "us-east-1a",
        "us-east-1d",
        "us-east-1e"
    ],
    "SnapshotCreateTime": "2020-06-22T17:40:12.322Z",
    "Engine": "aurora",
    "AllocatedStorage": 0,
    "Status": "available",
    "Port": 0,
    "VpcId": "vpc-faf7e380",
    "ClusterCreateTime": "2020-06-12T13:23:15.577Z",
    "MasterUsername": "admin",
    "EngineVersion": "5.6.10a",
    "LicenseModel": "aurora",
    "SnapshotType": "automated",
    "PercentProgress": 100,
    "StorageEncrypted": true,
    "KmsKeyId": "arn:aws:kms:us-east-1:777788889999:key/key1",
    "DbClusterIdentifier": "database-2",
    "DbClusterSnapshotIdentifier": "rds:database-2-2020-06-23-03-52",
    "IamDatabaseAuthenticationEnabled": false
}
```