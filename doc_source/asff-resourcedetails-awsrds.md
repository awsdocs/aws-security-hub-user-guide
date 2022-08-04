# AwsRds<a name="asff-resourcedetails-awsrds"></a>

The following are examples of the AWS Security Finding Format for `AwsRds` resources\.

## AwsRdsDbCluster<a name="asff-resourcedetails-awsrdsdbcluster"></a>

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

## AwsRdsDbClusterSnapshot<a name="asff-resourcedetails-awsrdsdbclustersnapshot"></a>

The `AwsRdsDbClusterSnapshot` object contains information about an Amazon RDS DB cluster snapshot\.

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

## AwsRdsDbInstance<a name="asff-resourcedetails-awsrdsdbinstance"></a>

The `AwsRdsDbInstance` object provides details about an Amazon RDS DB instance\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsRdsDbInstance` object\. To view descriptions of `AwsRdsDbInstance` attributes, see [AwsRdsDbInstanceDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsRdsDbInstanceDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsRdsDbInstance": {
    "AllocatedStorage": 20,
    "AssociatedRoles": [],
    "AutoMinorVersionUpgrade": true,
    "AvailabilityZone": "us-east-1d",
    "BackupRetentionPeriod": 7,
    "CaCertificateIdentifier": "certificate1",
    "CharacterSetName": "",
    "CopyTagsToSnapshot": true,
    "DbClusterIdentifier": "",
    "DbInstanceArn": "arn:aws:rds:us-east-1:111122223333:db:database-1",
    "DbInstanceClass": "db.t2.micro",
    "DbInstanceIdentifier": "database-1",
    "DbInstancePort": 0,
    "DbInstanceStatus": "available",
    "DbiResourceId": "db-EXAMPLE123",
    "DbName": "",
    "DbParameterGroups": [
        {
            "DbParameterGroupName": "default.mysql5.7",
            "ParameterApplyStatus": "in-sync"
        }
    ],
    "DbSecurityGroups": [],                                                                                                                                                                                                 
    "DbSubnetGroup": {
        "DbSubnetGroupName": "my-group-123abc",
        "DbSubnetGroupDescription": "My subnet group",
        "VpcId": "vpc-example1",
        "SubnetGroupStatus": "Complete",
        "Subnets": [
            {
                "SubnetIdentifier": "subnet-123abc",
                "SubnetAvailabilityZone": {
                    "Name": "us-east-1d"
                },
                "SubnetStatus": "Active"
            },
            {
                "SubnetIdentifier": "subnet-456def",
                "SubnetAvailabilityZone": {
                    "Name": "us-east-1c"
                },
                "SubnetStatus": "Active"
            }
      ],
        "DbSubnetGroupArn": ""
    },
    "DeletionProtection": false,
    "DomainMemberships": [],
    "EnabledCloudWatchLogsExports": [],
    "Endpoint": {
        "address": "database-1.example.us-east-1.rds.amazonaws.com",
        "port": 3306,
        "hostedZoneId": "ZONEID1"
    },
    "Engine": "mysql",
    "EngineVersion": "5.7.22",
    "EnhancedMonitoringResourceArn": "arn:aws:logs:us-east-1:111122223333:log-group:Example:log-stream:db-EXAMPLE1",
    "IamDatabaseAuthenticationEnabled": false,
    "InstanceCreateTime": "2020-06-22T17:40:12.322Z",
    "Iops": "",
    "KmsKeyId": "",
    "LatestRestorableTime": "2020-06-24T05:50:00.000Z",
    "LicenseModel": "general-public-license",
    "ListenerEndpoint": "",
    "MasterUsername": "admin",
    "MaxAllocatedStorage": 1000,
    "MonitoringInterval": 60,
    "MonitoringRoleArn": "arn:aws:iam::111122223333:role/rds-monitoring-role",
    "MultiAz": false,
    "OptionGroupMemberships": [
        {
            "OptionGroupName": "default:mysql-5-7",
            "Status": "in-sync"
        }
    ],
    "PreferredBackupWindow": "03:57-04:27",
    "PreferredMaintenanceWindow": "thu:10:13-thu:10:43",
    "PendingModifiedValues": {
        "DbInstanceClass": "",
        "AllocatedStorage": "",
        "MasterUserPassword": "",
        "Port": "",
        "BackupRetentionPeriod": "",
        "MultiAZ": "",
        "EngineVersion": "",
        "LicenseModel": "",
        "Iops": "",
        "DbInstanceIdentifier": "",
        "StorageType": "",
        "CaCertificateIdentifier": "",
        "DbSubnetGroupName": "",
        "PendingCloudWatchLogsExports": "",
        "ProcessorFeatures": []
    },
    "PerformanceInsightsEnabled": false,
    "PerformanceInsightsKmsKeyId": "",
    "PerformanceInsightsRetentionPeriod": "",
    "ProcessorFeatures": [],
    "PromotionTier": "",
    "PubliclyAccessible": false,
    "ReadReplicaDBClusterIdentifiers": [],
    "ReadReplicaDBInstanceIdentifiers": [],
    "ReadReplicaSourceDBInstanceIdentifier": "",
    "SecondaryAvailabilityZone": "",
    "StatusInfos": [],
    "StorageEncrypted": false,
    "StorageType": "gp2",
    "TdeCredentialArn": "",
    "Timezone": "",
    "VpcSecurityGroups": [
        {
            "VpcSecurityGroupId": "sg-example1",
            "Status": "active"
        }
    ]
}
```

## AwsRdsDbSecurityGroup<a name="asff-resourcedetails-awsrdsdbsecuritygroup"></a>

The `AwsRdsDbSecurityGroup` object contains information about an Amazon Relational Database Service

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsRdsDbSecurityGroup` object\. To view descriptions of `AwsRdsDbSecurityGroup` attributes, see [AwsRdsDbSecurityGroupDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsRdsDbSecurityGroupDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsRdsDbSecurityGroup": {
    "DbSecurityGroupArn": "arn:aws:rds:us-west-1:111122223333:secgrp:default",
    "DbSecurityGroupDescription": "default",
    "DbSecurityGroupName": "mysecgroup",
    "Ec2SecurityGroups": [
        {
          "Ec2SecurityGroupuId": "myec2group",
          "Ec2SecurityGroupName": "default",
          "Ec2SecurityGroupOwnerId": "987654321021",
          "Status": "authorizing"
        }
    ],
    "IpRanges": [
        {
          "Cidrip": "0.0.0.0/0",
          "Status": "authorizing"
        }
    ],
    "OwnerId": "123456789012",
    "VpcId": "vpc-1234567f"
}
```

## AwsRdsDbSnapshot<a name="asff-resourcedetails-awsrdsdbsnapshot"></a>

The `AwsRdsDbSnapshot` object contains details about an Amazon RDS DB cluster snapshot\.

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

## AwsRdsEventSubscription<a name="asff-resourcedetails-awsrdseventsubscription"></a>

The `AwsRdsEventSubscription` contains details about an RDS event notification subscription\. The subscription allows RDS to post events to an SNS topic\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsRdsEventSubscription` object\. To view descriptions of `AwsRdsEventSubscription` attributes, see [AwsRdsEventSubscriptionDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsRdsEventSubscriptionDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsRdsEventSubscription": {
    "CustSubscriptionId": "myawsuser-secgrp",
    "CustomerAwsId": "111111111111",
    "Enabled": true,
    "EventCategoriesList": [
        "configuration change",
        "failure"
    ],
    "EventSubscriptionArn": "arn:aws:rds:us-east-1:111111111111:es:my-instance-events",
    "SnsTopicArn": "arn:aws:sns:us-east-1:111111111111:myawsuser-RDS",
    "SourceIdsList": [
        "si-sample",
        "mysqldb-rr"
    ],
    "SourceType": "db-security-group",
    "Status": "creating",
    "SubscriptionCreationTime": "2021-06-27T01:38:01.090Z"
}
```