# AwsRdsDbCluster<a name="asff-resourcedetails-awsrdsdbcluster"></a>

The `AwsRdsDbCluster` object provides details about an Amazon RDS database cluster\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsRdsDbCluster` object\. To view descriptions of `AwsRdsDbCluster` attributes, see [AwsRdsDbClusterDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsRdsDbClusterDetails.html) in the *AWS Security Hub API Reference*\.

`Example`

```
"AwsRdsDbCluster": {
    "AllocatedStorage": 1,
    "AvailabilityZones": [
        "us-east-1c",
        "us-east-1e",
        "us-east-1a"
    ],
    "BackupRetentionPeriod": 1,
    "DatabaseName": "",
    "Status": "modifying",
    "Endpoint": "database-3.cluster-example.us-east-1.rds.amazonaws.com",
    "ReaderEndpoint": "database-3.cluster-ro-example.us-east-1.rds.amazonaws.com",
    "CustomEndpoints": [],
    "MultiAz": false,
    "Engine": "aurora-mysql",
    "EngineVersion": "5.7.mysql_aurora.2.03.4",
    "Port": 3306,
    "MasterUsername": "admin",
    "PreferredBackupWindow": "04:52-05:22",
    "PreferredMaintenanceWindow": "sun:09:32-sun:10:02",
    "ReadReplicaIdentifiers": [],
    "VpcSecurityGroups": [
        {
            "VpcSecurityGroupId": "sg-example-1",
            "Status": "active"
        }
    ],
    "HostedZoneId": "ZONE1",
    "StorageEncrypted": true,
    "KmsKeyId": "arn:aws:kms:us-east-1:777788889999:key/key1",
    "DbClusterResourceId": "cluster-example",
    "AssociatedRoles": [
        {
        "RoleArn": "arn:aws:iam::777788889999:role/aws-service-role/rds.amazonaws.com/AWSServiceRoleForRDS",
        "Status": "PENDING"
        }
    ],
    "ClusterCreateTime": "2020-06-22T17:40:12.322Z",
    "EnabledCloudwatchLogsExports": [
        "audit",
        "error",
        "general",
        "slowquery"
    ],
    "EngineMode": "provisioned",
    "DeletionProtection": false,
    "HttpEndpointEnabled": false,
    "ActivityStreamStatus": "stopped",
    "CopyTagsToSnapshot": true,
    "CrossAccountClone": false,
    "DomainMemberships": [],
    "DbClusterParameterGroup": "cluster-parameter-group",
    "DbSubnetGroup": "subnet-group",
    "DbClusterOptionGroupMemberships": [],
    "DbClusterIdentifier": "database-3",
    "DbClusterMembers": [
        {
        "IsClusterWriter": true,
        "PromotionTier": 1,
        "DbInstanceIdentifier": "database-3-instance-1",
        "DbClusterParameterGroupStatus": "in-sync"
        }
    ],
    "IamDatabaseAuthenticationEnabled": false
}
```

The following is a list of valid value examples for `AwsRdsDbCluster` attributes:
+ `ActivityStreamStatus`

  Valid values: `stopped` \| `starting` \| `started` \| `stopping`
+ `Engine`

  Valid values: `aurora` \| `aurora-mysql` \| `aurora-postgresql`
+ `EngineMode`

  Valid values: `provisioned` \| `serverless` \| `parallelquery` \| `global` \| `multimaster`
+ `AssociatedRoles Status`

  Valid values: `ACTIVE` \| `PENDING` \| `INVALID`