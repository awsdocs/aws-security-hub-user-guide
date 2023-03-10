# Amazon ElastiCache controls<a name="elasticache-controls"></a>

These controls are related to ElastiCache resources\.

## \[ElastiCache\.1\] ElastiCache for Redis clusters should have automatic backups scheduled<a name="elasticache-1"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6, NIST\.800\-53\.r5 CP\-6\(1\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-12, NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > Backups enabled

**Severity:** High

**Resource type:** `AWS::ElastiCache::CacheCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticache-redis-cluster-automatic-backup-check.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticache-redis-cluster-automatic-backup-check.html) ``

**Schedule type:** Periodic

**Parameters:**
+ `snapshotRetentionPeriod: 1`

This control evaluates if Amazon ElastiCache for Redis clusters have automatic backup scheduled\. The control fails if the `SnapshotRetentionLimit` for the Redis cluster is less than `1`\.

Amazon ElastiCache for Redis clusters can back up their data\. You can use the backup to restore a cluster or seed a new cluster\. The backup consists of the cluster's metadata, along with all of the data in the cluster\. All backups are written to Amazon Simple Storage Service \(Amazon S3\), which provides durable storage\. You can restore your data by creating a new Redis cluster and populating it with data from a backup\. You can manage backups using the AWS Management Console, the AWS Command Line Interface \(AWS CLI\), and the ElastiCache API\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
US East \(N\. Virginia\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Jakarta\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Osaka\)
Asia Pacific \(Seoul\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticache-1-remediation"></a>

For information about scheduling automatic backups, see [Scheduling Automatic Backups](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/backups-automatic.html) in the *Amazon ElastiCache User Guide*\.

## \[ElastiCache\.2\] Minor version upgrades should be automatically applied to ElastiCache for Redis cache clusters<a name="elasticache-2"></a>

**Related requirements:** NIST\.800\-53\.r5 SI\-2, NIST\.800\-53\.r5 SI\-2\(2\), NIST\.800\-53\.r5 SI\-2\(4\), NIST\.800\-53\.r5 SI\-2\(5\)

**Category:** Identify > Vulnerability, patch, and version management

**Severity:** High

**Resource type:** `AWS::ElastiCache::CacheCluster`

**AWS Config rule:** `elasticache-auto-minor-version-upgrade-check`

**Schedule type:** Periodic

**Parameters:** None

This control evaluates whether ElastiCache for Redis automatically applies minor version upgrades to cache clusters\. This control fails if ElastiCache for Redis cache clusters do not have minor version upgrades automatically applied\.

`AutoMinorVersionUpgrade` is a feature that you can turn on in ElastiCache for Redis to have your cache clusters automatically upgraded when a new minor cache engine version is available\. These upgrades might include security patches and bug fixes\. Staying up\-to\-date with patch installation is an important step in securing systems\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
US East \(N\. Virginia\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Seoul\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticache-2-remediation"></a>

For instructions on turning on automatic minor version upgrades for an existing ElastiCache for Redis cache cluster, see [Upgrading engine versions](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/VersionManagement.html) in the *Amazon ElastiCache User Guide*\.

## \[ElastiCache\.3\] ElastiCache for Redis replication groups should have automatic failover enabled<a name="elasticache-3"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::ElastiCache::ReplicationGroup`

**AWS Config rule:** `elasticache-repl-grp-auto-failover-enabled`

**Schedule type:** Periodic

**Parameters:** None

This control checks if ElastiCache for Redis replication groups have automatic failover enabled\. This control fails if automatic failover isn't enabled for a Redis replication group\.

When automatic failover is enabled for a replication group, the role of primary node will automatically fail over to one of the read replicas\. This failover and replica promotion ensure that you can resume writing to the new primary after promotion is complete, which reduces overall downtime in case of failure\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
US East \(N\. Virginia\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Seoul\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticache-3-remediation"></a>

To enable automatic failover for an existing ElastiCache for Redis replication group,, see [Modifying an ElastiCache cluster](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Clusters.Modify.html#Clusters.Modify.CON) in the *Amazon ElastiCache User Guide*\. If you use the ElastiCache console, set **Auto failover** to enabled\.

## \[ElastiCache\.4\] ElastiCache for Redis replication groups should be encrypted at rest<a name="elasticache-4"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data Protection > Encryption of data\-at\-rest

**Severity:** Medium

**Resource type:** `AWS::ElastiCache::ReplicationGroup`

**AWS Config rule:** `elasticache-repl-grp-encrypted-at-rest`

**Schedule type:** Periodic

**Parameters:** None

This control checks if ElastiCache for Redis replication groups are encrypted at rest\. This control fails if an ElastiCache for Redis replication group isn't encrypted at rest\.

Encrypting data at rest reduces the risk that an unauthenticated user gets access to data that is stored on disk\. ElastiCache for Redis replication groups should be encrypted at rest for an added layer of security\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
US East \(N\. Virginia\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Seoul\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticache-4-remediation"></a>

To configure at\-rest encryption on an ElastiCache for Redis replication group, see [Enabling at\-rest encryption](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/at-rest-encryption.html#at-rest-encryption-enable) in the *Amazon ElastiCache User Guide*\.

## \[ElastiCache\.5\] ElastiCache for Redis replication groups should be encrypted in transit<a name="elasticache-5"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data Protection > Encryption of data\-in\-transit

**Severity:** Medium

**Resource type:** `AWS::ElastiCache::ReplicationGroup`

**AWS Config rule:** `elasticache-repl-grp-encrypted-in-transit`

**Schedule type:** Periodic

**Parameters:** None

This control checks if ElastiCache for Redis replication groups are encrypted in transit\. This control fails if an ElastiCache for Redis replication group isn't encrypted in transit\.

Encrypting data in transit reduces the risk that an unauthorized user can eavesdrop on network traffic\. Enabling encryption in transit on an ElastiCache for Redis replication group encrypts your data whenever it's moving from one place to another, such as between nodes in your cluster or between your cluster and your application\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
US East \(N\. Virginia\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Seoul\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticache-5-remediation"></a>

To configure in\-transit encryption on an ElastiCache for Redis replication group, see [Enabling in\-transit encryption](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/in-transit-encryption.html) in the *Amazon ElastiCache User Guide*\.

## \[ElastiCache\.6\] ElastiCache for Redis replication groups before version 6\.0 should use Redis AUTH<a name="elasticache-6"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-6

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::ElastiCache::ReplicationGroup`

**AWS Config rule:** `elasticache-repl-grp-redis-auth-enabled`

**Schedule type:** Periodic

**Parameters:** None

This control checks if ElastiCache for Redis replication groups have Redis AUTH enabled\. The control fails for an ElastiCache for Redis replication group if the Redis version of its nodes is below 6\.0 and `AuthToken` isn't in use\.

When you use Redis authentication tokens, or passwords, Redis requires a password before allowing clients to run commands, which improves data security\. For Redis 6\.0 and later versions, we recommend using Role\-Based Access Control \(RBAC\)\. Since RBAC is not supported for Redis versions earlier than 6\.0, this control only evaluates versions which can't use the RBAC feature\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
US East \(N\. Virginia\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Jakarta\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Seoul\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticache-6-remediation"></a>

To use Redis AUTH on an ElastiCache for Redis replication group, see [Modifying the AUTH token on an existing ElastiCache for Redis cluster](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/auth.html#auth-modifyng-token) in the *Amazon ElastiCache User Guide*\.

## \[ElastiCache\.7\] ElastiCache clusters should not use the default subnet group<a name="elasticache-7"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(5\)

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::ElastiCache::CacheCluster`

**AWS Config rule:** `elasticache-subnet-group-check`

**Schedule type:** Periodic

**Parameters:** None

This control checks if ElastiCache clusters are configured with a custom subnet group\. The control fails for an ElastiCache cluster if `CacheSubnetGroupName` has the value `default`\.

When launching an ElastiCache cluster, a default subnet group is created if one doesn't exist already\. The default group uses subnets from the default Virtual Private Cloud \(VPC\)\. We recommend using custom subnet groups that are more restrictive of the subnets that the cluster resides in, and the networking that the cluster inherits from the subnets\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
US East \(N\. Virginia\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Jakarta\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Osaka\)
Asia Pacific \(Seoul\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticache-7-remediation"></a>

To create a new subnet group for an ElastiCache cluster, see [Creating a subnet group](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/SubnetGroups.Creating.html) in the *Amazon ElastiCache User Guide*\.