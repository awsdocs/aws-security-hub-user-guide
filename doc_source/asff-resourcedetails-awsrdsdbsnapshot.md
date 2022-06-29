# AwsRdsDbSnapshot<a name="asff-resourcedetails-awsrdsdbsnapshot"></a>

The `AwsRdsDbSnapshot` object contains details about an Amazon RDS database cluster snapshot\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsRdsDbSnapshot` object\. To view descriptions of `AwsRdsDbSnapshot` attributes, see [AwsRdsDbSnapshotDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsRdsDbSnapshotDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsRdsDbSnapshot": {
    "DbSnapshotIdentifier": "rds:database-1-2020-06-22-17-41",
    "DbInstanceIdentifier": "database-1",
    "SnapshotCreateTime": "2020-06-22T17:41:29.967Z",
    "Engine": "mysql",
    "AllocatedStorage": 20,
    "Status": "available",
    "Port": 3306,
    "AvailabilityZone": "us-east-1d",
    "VpcId": "vpc-example1",
    "InstanceCreateTime": "2020-06-22T17:40:12.322Z",
    "MasterUsername": "admin",
    "EngineVersion": "5.7.22",
    "LicenseModel": "general-public-license",
    "SnapshotType": "automated",
    "Iops": null,
    "OptionGroupName": "default:mysql-5-7",
    "PercentProgress": 100,
    "SourceRegion": null,
    "SourceDbSnapshotIdentifier": "",
    "StorageType": "gp2",
    "TdeCredentialArn": "",
    "Encrypted": false,
    "KmsKeyId": "",
    "Timezone": "",
    "IamDatabaseAuthenticationEnabled": false,
    "ProcessorFeatures": [],
    "DbiResourceId": "db-resourceexample1"
}
```

The following is a list of valid value examples for `AwsRdsDbSnapshot` attributes:
+ `Engine`

  Valid values: `aurora` \| `aurora-mysql` \| `aurora-postgresql` \| `mariadb` \| `mysql` \| `oracle-ee` \| `oracle-se2` \| `oracle-se1` \| `oracle-se` \| c`` \| `sqlserver-ee` \| `sqlserver-se` \| `sqlserver-ex` \| `sqlserver-web`
+ `ProcessorFeatures Name`

  Valid values: `coreCount` \| `threadsPerCore`
+ `StorageType`

  Valid values: `standard` \| `gp2` \| `io1`