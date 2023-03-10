# Amazon Relational Database Service controls<a name="rds-controls"></a>

These controls are related to Amazon RDS resources\.

## \[RDS\.1\] RDS snapshot should be private<a name="rds-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.4, PCI DSS v3\.2\.1/1\.3\.6, PCI DSS v3\.2\.1/7\.2\.1, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::RDS::DBSnapshot`, `AWS::RDS::DBClusterSnapshot`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon RDS snapshots are public\. The control fails if RDS snapshots are public\. This control evaluates RDS instances, Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters\.

RDS snapshots are used to back up the data on your RDS instances at a specific point in time\. They can be used to restore previous states of RDS instances\.

An RDS snapshot must not be public unless intended\. If you share an unencrypted manual snapshot as public, this makes the snapshot available to all AWS accounts\. This may result in unintended data exposure of your RDS instance\.

Note that if the configuration is changed to allow public access, the AWS Config rule may not be able to detect the change for up to 12 hours\. Until the AWS Config rule detects the change, the check passes even though the configuration violates the rule\.

To learn more about sharing a DB snapshot, see [Sharing a DB snapshot](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html) in the *Amazon RDS User Guide*\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="rds-1-remediation"></a>

To remediate this issue, update your RDS snapshots to remove public access\.

**To remove public access for RDS snapshots**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Navigate to **Snapshots** and then choose the public snapshot you want to modify\.

1. From **Actions**, choose **Share Snapshots**\.

1. From **DB snapshot visibility**, choose **Private**\.

1. Under **DB snapshot visibility**, choose **all**\.

1. Choose **Save**\.

## \[RDS\.2\] RDS DB Instances should prohibit public access, as determined by the PubliclyAccessible AWS Configuration<a name="rds-2"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.2, PCI DSS v3\.2\.1/1\.3\.4, PCI DSS v3\.2\.1/1\.3\.6, PCI DSS v3\.2\.1/7\.2\.1, NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(5\)

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon RDS instances are publicly accessible by evaluating the `PubliclyAccessible` field in the instance configuration item\.

Neptune DB instances and Amazon DocumentDB clusters do not have the `PubliclyAccessible` flag and cannot be evaluated\. However, this control can still generate findings for these resources\. You can suppress these findings\.

The `PubliclyAccessible` value in the RDS instance configuration indicates whether the DB instance is publicly accessible\. When the DB instance is configured with `PubliclyAccessible`, it is an Internet\-facing instance with a publicly resolvable DNS name, which resolves to a public IP address\. When the DB instance isn't publicly accessible, it is an internal instance with a DNS name that resolves to a private IP address\.

Unless you intend for your RDS instance to be publicly accessible, the RDS instance should not be configured with `PubliclyAccessible` value\. Doing so might allow unnecessary traffic to your database instance\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="rds-2-remediation"></a>

To remediate this issue, update your RDS DB instances to remove public access\.

**To remove public access from RDS DB instances**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Navigate to **Databases** and then choose your public database\.

1. Choose **Modify**\.

1. Under **Connectivity**, expand **Additional connectivity configuration**\.

1. Under **Public access**, choose **Not publicly accessible**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose **Apply immediately**\.

1. Choose **Modify DB Instance**\.

For more information, see [Working with a DB instance in a VPC](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html) in the *Amazon RDS User Guide*\.

## \[RDS\.3\] RDS DB instances should have encryption at\-rest enabled<a name="rds-3"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.4\.0/2\.3\.1, NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether storage encryption is enabled for your Amazon RDS DB instances\.

This control is intended for RDS DB instances\. However, it can also generate findings for Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters\. If these findings are not useful, then you can suppress them\.

For an added layer of security for your sensitive data in RDS DB instances, you should configure your RDS DB instances to be encrypted at rest\. To encrypt your RDS DB instances and snapshots at rest, enable the encryption option for your RDS DB instances\. Data that is encrypted at rest includes the underlying storage for DB instances, its automated backups, read replicas, and snapshots\. 

RDS encrypted DB instances use the open standard AES\-256 encryption algorithm to encrypt your data on the server that hosts your RDS DB instances\. After your data is encrypted, Amazon RDS handles authentication of access and decryption of your data transparently with a minimal impact on performance\. You do not need to modify your database client applications to use encryption\. 

Amazon RDS encryption is currently available for all database engines and storage types\. Amazon RDS encryption is available for most DB instance classes\. To learn about DB instance classes that do not support Amazon RDS encryption, see [Encrypting Amazon RDS resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html) in the *Amazon RDS User Guide*\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="rds-3-remediation"></a>

For information about encrypting DB instances in Amazon RDS, see [Encrypting Amazon RDS resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html) in the *Amazon RDS User Guide*\.

## \[RDS\.4\] RDS cluster snapshots and database snapshots should be encrypted at rest<a name="rds-4"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::RDS::DBClusterSnapshot`,` AWS::RDS::DBSnapshot`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshot-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshot-encrypted.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether RDS DB snapshots are encrypted\.

This control is intended for RDS DB instances\. However, it can also generate findings for snapshots of Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters\. If these findings are not useful, then you can suppress them\.

Encrypting data at rest reduces the risk that an unauthenticated user gets access to data that is stored on disk\. Data in RDS snapshots should be encrypted at rest for an added layer of security\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="rds-4-remediation"></a>

You can use the Amazon RDS console to remediate this issue\.

**To encrypt an unencrypted RDS snapshot**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Snapshots**\.

1. Find the snapshot to encrypt under **Manual** or **System**\.

1. Select the check box next to the snapshot to encrypt\.

1. Choose **Actions**, then choose **Copy Snapshot**\.

1. Under **New DB Snapshot Identifier**, type a name for the new snapshot\.

1. Under **Encryption**, select **Enable Encryption**\.

1. Choose the KMS key to use to encrypt the snapshot\.

1. Choose **Copy Snapshot**\.

1. After the new snapshot is created, delete the original snapshot\.

1. For **Backup Retention Period**, choose a positive nonzero value\. For example, 30 days\.

## \[RDS\.5\] RDS DB instances should be configured with multiple Availability Zones<a name="rds-5"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-multi-az-support.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-multi-az-support.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether high availability is enabled for your RDS DB instances\.

RDS DB instances should be configured for multiple Availability Zones \(AZs\)\. This ensures the availability of the data stored\. Multi\-AZ deployments allow for automated failover if there is an issue with Availability Zone availability and during regular RDS maintenance\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="rds-5-remediation"></a>

To remediate this issue, update your DB instances to enable multiple Availability Zones\.

**To enable multiple Availability Zones for a DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**, and then choose the DB instance that you want to modify\. 

1. Choose **Modify**\. The **Modify DB Instance** page appears\. 

1. Under **Instance Specifications**, set **Multi\-AZ deployment** to **Yes**\.

1. Choose **Continue** and then check the summary of modifications\. 

1. \(Optional\) Choose **Apply immediately** to apply the changes immediately\. Choosing this option can cause an outage in some cases\. For more information, see [Using the Apply Immediately setting](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.DBInstance.Modifying.html#USER_ModifyInstance.ApplyImmediately) in the *Amazon RDS User Guide*\.

1. On the confirmation page, review your changes\. If they are correct, choose **Modify DB Instance** to save your changes\.

## \[RDS\.6\] Enhanced monitoring should be configured for RDS DB instances<a name="rds-6"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SI\-2

**Category:** Detect > Detection services

**Severity:** Low

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-enhanced-monitoring-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-enhanced-monitoring-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether enhanced monitoring is enabled for your RDS DB instances\.

In Amazon RDS, Enhanced Monitoring enables a more rapid response to performance changes in underlying infrastructure\. These performance changes could result in a lack of availability of the data\. Enhanced Monitoring provides real\-time metrics of the operating system that your RDS DB instance runs on\. An agent is installed on the instance\. The agent can obtain metrics more accurately than is possible from the hypervisor layer\.

Enhanced Monitoring metrics are useful when you want to see how different processes or threads on a DB instance use the CPU\. For more information, see [Enhanced Monitoring](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.html) in the *Amazon RDS User Guide*\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="rds-6-remediation"></a>

For detailed instructions on how to enable Enhanced Monitoring for your DB instance, see [Setting up for and enabling Enhanced Monitoring](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.html#USER_Monitoring.OS.Enabling) in the *Amazon RDS User Guide*\.

## \[RDS\.7\] RDS clusters should have deletion protection enabled<a name="rds-7"></a>

**Related requirements:** NIST\.800\-53\.r5 CM\-3, NIST\.800\-53\.r5 SC\-5\(2\)

**Category:** Protect > Data protection > Data deletion protection

**Severity:** Low

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-deletion-protection-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-deletion-protection-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether RDS clusters have deletion protection enabled\. 

This control is intended for RDS DB instances\. However, it can also generate findings for Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters\. If these findings are not useful, then you can suppress them\.

Enabling cluster deletion protection is an additional layer of protection against accidental database deletion or deletion by an unauthorized entity\.

When deletion protection is enabled, an RDS cluster cannot be deleted\. Before a deletion request can succeed, deletion protection must be disabled\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)
Middle East \(UAE\)
South America \(São Paulo\)\.

### Remediation<a name="rds-7-remediation"></a>

To remediate this issue, update your RDS DB cluster to enable delete protection\.

**To enable deletion protection for an RDS DB cluster**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**, then choose the DB cluster that you want to modify\. 

1. Choose **Modify**\.

1. Under **Deletion protection**, choose **Enable deletion protection**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. The options are **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. Choose **Modify Cluster**\.

## \[RDS\.8\] RDS DB instances should have deletion protection enabled<a name="rds-8"></a>

**Related requirements:** NIST\.800\-53\.r5 CM\-3, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category: **Protect > Data protection > Data deletion protection

**Severity:** Low

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-deletion-protection-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-deletion-protection-enabled.html)

**Schedule type:** Change triggered

**Parameters:**
+ `databaseEngines`: `mariadb,mysql,oracle-ee,oracle-se2,oracle-se1,oracle-se,postgres,sqlserver-ee,sqlserver-se,sqlserver-ex,sqlserver-web`

This control checks whether your RDS DB instances that use one of the listed database engines have deletion protection enabled\.

Enabling instance deletion protection is an additional layer of protection against accidental database deletion or deletion by an unauthorized entity\.

While deletion protection is enabled, an RDS DB instance cannot be deleted\. Before a deletion request can succeed, deletion protection must be disabled\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="rds-8-remediation"></a>

To remediate this issue, update your RDS DB instance to enable deletion protection\.

**To enable deletion protection for an RDS DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**, then choose the DB instance that you want to modify\. 

1. Choose **Modify**\.

1. Under **Deletion protection**, choose **Enable deletion protection**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. The options are **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. Choose **Modify DB Instance**\.

## \[RDS\.9\] Database logging should be enabled<a name="rds-9"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(4\), NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AC\-6\(9\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4\(20\), NIST\.800\-53\.r5 SI\-7\(8\)

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-logging-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the following logs of Amazon RDS are enabled and sent to CloudWatch Logs:
+ Oracle: \(Alert, Audit, Trace, Listener\)
+ PostgreSQL: \(Postgresql, Upgrade\)
+ MySQL: \(Audit, Error, General, SlowQuery\)
+ MariaDB: \(Audit, Error, General, SlowQuery\)
+ SQL Server: \(Error, Agent\)
+ Aurora: \(Audit, Error, General, SlowQuery\)
+ Aurora\-MySQL: \(Audit, Error, General, SlowQuery\)
+ Aurora\-PostgreSQL: \(Postgresql, Upgrade\)\.

RDS databases should have relevant logs enabled\. Database logging provides detailed records of requests made to RDS\. Database logs can assist with security and access audits and can help to diagnose availability issues\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
China \(Ningxia\)
Europe \(Milan\)

### Remediation<a name="rds-9-remediation"></a>

Logging options are contained in the DB parameter group associated with the RDS DB cluster or instance\. To enable logging when the default parameter group for the database engine is used, you must create a new DB parameter group that has the required parameter values\. You must then associate the customer DB parameter group with the DB cluster or instance\.

To enable and publish MariaDB, MySQL, or PostgreSQL logs to CloudWatch Logs from the AWS Management Console, set the following parameters in a custom DB Parameter Group:


|  Database engine  |  Parameters  | 
| --- | --- | 
|  MariaDB  |  `general_log=1` `slow_query_log=1` `log_output = FILE` MariaDB also requires a custom options group, explained below\.  | 
|  MySQL  |  `general_log=1` `slow_query_log=1` `log_output = FILE`  | 
|  PostgreSQL  |  `log_statement=all` `log_min_duration_statement=minimum query duration (ms) to log`  | 

**To create a custom DB parameter group**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Parameter groups**\.

1. Choose **Create parameter group**\. The **Create parameter group** window appears\. 

1. In the **Parameter group** family list, choose a DB parameter group family\. 

1. In the **Type** list, choose **DB Parameter Group**\.

1. In **Group name**, enter the name of the new DB parameter group\.

1. In **Description**, enter a description for the new DB parameter group\. 

1. Choose **Create**\.

**To create a new option group for MariaDB logging by using the console**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Option groups**\. 

1. Choose **Create group**\. 

1. In the **Create option group** window, do the following: 

   1. For **Name**, type a name for the option group that is unique within your AWS account\. The name can contain only letters, digits, and hyphens\.

   1. For **Description**, type a brief description of the option group\. The description is used for display purposes\.

   1. For **Engine**, choose the DB engine that you want\. 

   1. For **Major engine version**, choose the major version of the DB engine that you want\.

1. To continue, choose **Create**\. 

1. Choose the name of the option group you just created\.

1. Choose **Add option**\.

1. Choose **MARIADB\_AUDIT\_PLUGIN** from the** Option name** list\.

1. Set `SERVER_AUDIT_EVENTS` to `CONNECT,QUERY,TABLE,QUERY_DDL,QUERY_DML,QUERY_DCL`\.

1. Choose **Add option**\.

**To publish SQL Server DB, Oracle DB, or PostgreSQL logs to CloudWatch Logs from the AWS Management Console**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**\.

1. Choose the DB instance that you want to modify\. 

1. Choose **Modify**\.

1. Under **Log exports**, choose all of the log files to start publishing to CloudWatch Logs\.

   **Log exports** is available only for database engine versions that support publishing to CloudWatch Logs\.

1. Choose **Continue**\. Then on the summary page, choose** Modify DB Instance**\.

**To apply a new DB parameter group or DB options group to an RDS DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**\.

1. Choose the DB instance that you want to modify\. 

1. Choose **Modify**\. The **Modify DB Instance** page appears\. 

1. Under **Database options**, change the DB parameter group and DB options group as needed\.

1. When you finish you changes, choose **Continue**\. Check the summary of modifications\. 

1. \(Optional\) Choose **Apply immediately** to apply the changes immediately\. Choosing this option can cause an outage in some cases\. For more information, see [Using the Apply Immediately setting](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.DBInstance.Modifying.html#USER_ModifyInstance.ApplyImmediately) in the *Amazon RDS User Guide*\. 

1. Choose **Modify DB Instance** to save your changes\. 

## \[RDS\.10\] IAM authentication should be configured for RDS instances<a name="rds-10"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-6

**Category:** Protect > Secure access management > Passwordless authentication

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-iam-authentication-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-iam-authentication-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an RDS DB instance has IAM database authentication enabled\. The control fails if IAM authentication is not configured for RDS DB instances\. This control only evaluates RDS instances with the following engine types: `mysql`, `postgres`, `aurora`, `aurora-mysql`, `aurora-postgresql`, and `mariadb`\. An RDS instance must also be in one of the following states for a finding to be generated: `available`, `backing-up`, `storage-optimization`, or `storage-full`\.

IAM database authentication allows authentication to database instances with an authentication token instead of a password\. Network traffic to and from the database is encrypted using SSL\. For more information, see [IAM database authentication](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/UsingWithRDS.IAMDBAuth.html) in the *Amazon Aurora User Guide*\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)

### Remediation<a name="rds-10-remediation"></a>

To remediate this issue, update your DB instance to enable IAM authentication\.

**To enable IAM authentication for an existing DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Select the DB instance to modify\.

1. Choose **Modify**\. 

1. Under **Database authentication**, choose **Password and IAM database authentication**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. The options are **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. For clusters, choose **Modify DB Instance**\.

## \[RDS\.11\] RDS instances should have automatic backups enabled<a name="rds-11"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6, NIST\.800\-53\.r5 CP\-6\(1\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-12, NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > Backups enabled 

**Severity:** Medium

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/db-instance-backup-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/db-instance-backup-enabled.html)

**Schedule type:** Change triggered

**Parameters:** 
+ `backupRetentionMinimum:` 7

This control checks whether Amazon Relational Database Service instances have automated backups enabled and the backup retention period is greater than or equal to seven days\. The control fails if backups are not enabled, and if the retention period is less than 7 days\.

Backups help you more quickly recover from a security incident and strengthens the resilience of your systems\. Amazon RDS provides an easy way to configure daily full instance volume snapshots\. For more details on Amazon RDS automated backups, see [Working with Backups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html) in the Amazon RDS User Guide\.

**Note**  
This control is not supported in Asia Pacific \(Osaka\) or Middle East \(UAE\)\.

### Remediation<a name="rds-11-remediation"></a>

**To enable automated backups immediately**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**, and then choose the DB instance that you want to modify\. 

1. Choose **Modify** to open the **Modify DB Instance** page\. 

1. Under **Backup Retention Period**, choose a positive nonzero value, for example 30 days, then choose **Continue**\. 

1. Select the **Scheduling of modifications** section and choose when to apply modifications: you can choose to **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. Then, on the confirmation page, choose **Modify DB Instance** to save your changes and enable automated backups\.

## \[RDS\.12\] IAM authentication should be configured for RDS clusters<a name="rds-12"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-6

**Category:** Protect > Secure access management > Passwordless authentication

**Severity:** Medium

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-iam-authentication-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-iam-authentication-enabled.html)

**Schedule type:** Change triggered

**Parameters:**None

This control checks whether an Amazon RDS DB cluster has IAM database authentication enabled\.

IAM database authentication allows for password\-free authentication to database instances\. The authentication uses an authentication token\. Network traffic to and from the database is encrypted using SSL\. For more information, see [IAM database authentication](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/UsingWithRDS.IAMDBAuth.html) in the *Amazon Aurora User Guide*\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)
Middle East \(UAE\)
South America \(São Paulo\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="rds-12-remediation"></a>

You can enable IAM authentication for a DB cluster from the Amazon RDS console\.

**To enable IAM authentication for an existing DB cluster**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Choose the DB cluster to modify\.

1. Choose **Modify**\.

1. Under **Database options**, select **Enable IAM DB authentication**\.

1. Choose **Continue**\. 

1. Under **Scheduling of modifications**, choose when to apply modifications: **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. Choose **Modify cluster**\.

## \[RDS\.13\] RDS automatic minor version upgrades should be enabled<a name="rds-13"></a>

**Related requirements:** NIST\.800\-53\.r5 SI\-2, NIST\.800\-53\.r5 SI\-2\(2\), NIST\.800\-53\.r5 SI\-2\(4\), NIST\.800\-53\.r5 SI\-2\(5\)

**Category:** Detect > Vulnerability and patch management 

**Severity:** High

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-automatic-minor-version-upgrade-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-automatic-minor-version-upgrade-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether automatic minor version upgrades are enabled for the RDS database instance\.

Enabling automatic minor version upgrades ensures that the latest minor version updates to the relational database management system \(RDBMS\) are installed\. These upgrades might include security patches and bug fixes\. Keeping up to date with patch installation is an important step in securing systems\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="rds-13-remediation"></a>

You can enable minor version upgrades for a DB instance from the Amazon RDS console\.

**To enable automatic minor version upgrades for an existing DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Choose the DB instance to modify\.

1. Choose **Modify**\. 

1. Under **Maintenance**, select **Yes** for **Auto minor version upgrade**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications: **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. Choose **Modify DB Instance**\.

## \[RDS\.14\] Amazon Aurora clusters should have backtracking enabled<a name="rds-14"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6, NIST\.800\-53\.r5 CP\-6\(1\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > Backups enabled 

**Severity:** Medium

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/aurora-mysql-backtracking-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/aurora-mysql-backtracking-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon Aurora clusters have backtracking enabled\.

Backups help you to recover more quickly from a security incident\. They also strengthens the resilience of your systems\. Aurora backtracking reduces the time to recover a database to a point in time\. It does not require a database restore to do so\.

For more information about backtracking in Aurora, see [Backtracking an Aurora DB cluster](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Managing.Backtrack.html) in the *Amazon Aurora User Guide*\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
South America \(São Paulo\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="rds-14-remediation"></a>

For detailed instructions on how to enable Aurora backtracking, see [Configuring backtracking](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Managing.Backtrack.html#AuroraMySQL.Managing.Backtrack.Configuring) in the *Amazon Aurora User Guide*\.

Note that you cannot enable backtracking on an existing cluster\. Instead, you can create a clone that has backtracking enabled\. For more information about the limitations of Aurora backtracking, see the list of limitations in [Overview of backtracking](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Managing.Backtrack.html)\.

For information about pricing for backtracking, see the [Aurora pricing page](http://aws.amazon.com/rds/aurora/pricing/)\.

## \[RDS\.15\] RDS DB clusters should be configured for multiple Availability Zones<a name="rds-15"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-multi-az-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-multi-az-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether high availability is enabled for your RDS DB clusters\.

RDS DB clusters should be configured for multiple Availability Zones to ensure availability of the data that is stored\. Deployment to multiple Availability Zones allows for automated failover in the event of an Availability Zone availability issue and during regular RDS maintenance events\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)
Middle East \(UAE\)
South America \(São Paulo\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="rds-15-remediation"></a>

To remediate this control, configure your DB cluster for multiple Availability Zones\.

**To enable multi\-AZ for a DB cluster**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**, and then choose the DB instance to modify\. 

1. Choose **Modify**\. The **Modify DB Instance** page appears\.

1. Under **Instance Specifications**, set **Multi\-AZ deployment** to **Yes**\.

1. Choose **Continue** and check the summary of modifications\.

1. \(Optional\) Choose **Apply immediately** to apply the changes immediately\. Choosing this option can cause an outage in some cases\. For more information, see [Using the Apply Immediately setting](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.DBInstance.Modifying.html#USER_ModifyInstance.ApplyImmediately) in the *Amazon RDS User Guide*\.

   On the confirmation page, review your changes\. If they are correct, choose **Modify DB Instance**\.

**Note**  
Remediation steps differ for Aurora global databases\. To configure multiple Availability Zones for an Aurora global database, select your DB cluster\. Then, choose **Actions** and **Add reader**\. For more information, see [Adding Aurora Replicas to a DB cluster](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-replicas-adding.html) in the *Amazon Aurora User Guide*\.

## \[RDS\.16\] RDS DB clusters should be configured to copy tags to snapshots<a name="rds-16"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\)

**Category:** Identify > Inventory

**Severity:** Low

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** `rds-cluster-copy-tags-to-snapshots-enabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether RDS DB clusters are configured to copy all tags to snapshots when the snapshots are created\.

Identification and inventory of your IT assets is a crucial aspect of governance and security\. You need to have visibility of all your RDS DB clusters so that you can assess their security posture and take action on potential areas of weakness\. Snapshots should be tagged in the same way as their parent RDS database clusters\. Enabling this setting ensures that snapshots inherit the tags of their parent database clusters\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
Middle East \(Bahrain\)
Middle East \(UAE\)
South America \(São Paulo\)

### Remediation<a name="rds-16-remediation"></a>

**To enable automatic tag copying to snapshots for a DB cluster**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Select the DB cluster to modify\.

1. Choose **Modify**\.

1. Under **Backup**, select **Copy tags to snapshots**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. You can choose either **Apply during the next scheduled maintenance window** or **Apply immediately**\.

## \[RDS\.17\] RDS DB instances should be configured to copy tags to snapshots<a name="rds-17"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\)

**Category:** Identify > Inventory

**Severity:** Low

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** `rds-instance-copy-tags-to-snapshots-enabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether RDS DB instances are configured to copy all tags to snapshots when the snapshots are created\.

Identification and inventory of your IT assets is a crucial aspect of governance and security\. You need to have visibility of all your RDS DB instances so that you can assess their security posture and take action on potential areas of weakness\. Snapshots should be tagged in the same way as their parent RDS database instances\. Enabling this setting ensures that snapshots inherit the tags of their parent database instances\.

### Remediation<a name="rds-17-remediation"></a>

**To enable automatic tag copying to snapshots for a DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Select the DB instance to modify\.

1. Choose **Modify**\.

1. Under **Backup**, select **Copy tags to snapshots**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. You can choose either** Apply during the next scheduled maintenance window** or **Apply immediately**\.

## \[RDS\.18\] RDS instances should be deployed in a VPC<a name="rds-18"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration > Resources within VPC 

**Severity:** High

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** `rds-deployed-in-vpc` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS instance is deployed on EC2\-VPC\.

VPCs provide a number of network controls to secure access to RDS resources\. These controls include VPC Endpoints, network ACLs, and security groups\. To take advantage of these controls, we recommend that you create your RDS instances on EC2\-VPC\.

### Remediation<a name="rds-18-remediation"></a>

For detailed instructions on how to move RDS instances to VPC, see [Updating the VPC for a DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.html#USER_VPC.VPC2VPC) in the *Amazon RDS User Guide*\.

## \[RDS\.19\] An RDS event notifications subscription should be configured for critical cluster events<a name="rds-19"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SI\-2

**Category:** Detect > Detection services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::RDS::EventSubscription`

**AWS Config rule:** `rds-cluster-event-notifications-configured` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS event subscription exists that has notifications enabled for the following source type, event category key\-value pairs\.

```
DBCluster: ["maintenance","failure"]
```

RDS event notifications uses Amazon SNS to make you aware of changes in the availability or configuration of your RDS resources\. These notifications allow for rapid response\. For additional information about RDS event notifications, see [Using Amazon RDS event notification](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-19-remediation"></a>

**To subscribe to RDS cluster event notifications**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Event subscriptions**\.

1. Under **Event subscriptions**, choose **Create event subscription**\.

1. In the **Create event subscription** dialog, do the following: 

   1. For **Name**, enter a name for the event notification subscription\. 

   1. For **Send notifications to**, choose an existing Amazon SNS ARN for an SNS topic\. To use a new topic, choose **create topic** to enter the name of a topic and a list of recipients\. 

   1. For **Source type**, choose **Clusters**\.

   1. Under **Instances to include**, select **All clusters**\.

   1. Under **Event categories to include**, select **Specific event categories**\. The control also passes if you select **All event categories**\.

   1. Select **maintenance** and **failure**\.

   1. Choose **Create**\.

## \[RDS\.20\] An RDS event notifications subscription should be configured for critical database instance events<a name="rds-20"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SI\-2

**Category:** Detect > Detection services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::RDS::EventSubscription`

**AWS Config rule:** `rds-instance-event-notifications-configured` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS event subscription exists with notifications enabled for the following source type, event category key\-value pairs\.

```
DBInstance: ["maintenance","configuration change","failure"]
```

RDS event notifications use Amazon SNS to make you aware of changes in the availability or configuration of your RDS resources\. These notifications allow for rapid response\. For additional information about RDS event notifications, see [Using Amazon RDS event notification](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-20-remediation"></a>

**To subscribe to RDS instance event notifications**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Event subscriptions**\. 

1. Under **Event subscriptions**, choose **Create event subscription**\.

1. In the **Create event subscription** dialog, do the following: 

   1. For **Name**, enter a name for the event notification subscription\. 

   1. For **Send notifications to**, choose an existing Amazon SNS ARN for an SNS topic\. To use a new topic, choose **create topic** to enter the name of a topic and a list of recipients\. 

   1. For **Source type**, choose **Instances**\.

   1. Under **Instances to include**, select **All instances**\.

   1. Under **Event categories to include**, select **Specific event categories**\. The control also passes if you select **All event categories**\.

   1. Select **maintenance**, **configuration change**, and **failure**\.

   1. Choose **Create**\.

## \[RDS\.21\] An RDS event notifications subscription should be configured for critical database parameter group events<a name="rds-21"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SI\-2

**Category:** Detect > Detection services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::RDS::EventSubscription`

**AWS Config rule:** `rds-pg-event-notifications-configured` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS event subscription exists with notifications enabled for the following source type, event category key\-value pairs\.

```
DBParameterGroup: ["configuration change"]
```

RDS event notifications use Amazon SNS to make you aware of changes in the availability or configuration of your RDS resources\. These notifications allow for rapid response\. For additional information about RDS event notifications, see [Using Amazon RDS event notification](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-21-remediation"></a>

**To subscribe to RDS database parameter group event notifications**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Event subscriptions**\. 

1. Under **Event subscriptions**, choose **Create event subscription**\.

1. In the **Create event subscription** dialog, do the following: 

   1. For **Name**, enter a name for the event notification subscription\. 

   1. For **Send notifications to**, choose an existing Amazon SNS ARN for an SNS topic\. To use a new topic, choose **create topic** to enter the name of a topic and a list of recipients\. 

   1. For **Source type**, choose **Parameter groups**\.

   1. Under **Instances to include**, select **All parameter groups**\.

   1. Under **Event categories to include**, select **Specific event categories**\. The control also passes if you select **All event categories**\.

   1. Select **configuration change**\.

   1. Choose **Create**\.

## \[RDS\.22\] An RDS event notifications subscription should be configured for critical database security group events<a name="rds-22"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SI\-2

**Category:** Detect > Detection Services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::RDS::EventSubscription`

**AWS Config rule:** `rds-sg-event-notifications-configured` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS event subscription exists with notifications enabled for the following source type, event category key\-value pairs\.

```
DBSecurityGroup: ["configuration change","failure"]
```

RDS event notifications use Amazon SNS to make you aware of changes in the availability or configuration of your RDS resources\. These notifications allow for a rapid response\. For additional information about RDS event notifications, see [Using Amazon RDS event notification](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-22-remediation"></a>

**To subscribe to RDS database security group event notifications**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Event subscriptions**\. 

1. Under **Event subscriptions**, choose **Create event subscription**\.

1. In the **Create event subscription** dialog, do the following: 

   1. For **Name**, enter a name for the event notification subscription\. 

   1. For **Send notifications to**, choose an existing Amazon SNS ARN for an SNS topic\. To use a new topic, choose** create topic** to enter the name of a topic and a list of recipients\. 

   1. For **Source type**, choose **Security groups**\.

   1. Under **Instances to include**, select **All security groups**\.

   1. Under **Event categories to include**, select **Specific event categories**\. The control also passes if you select **All event categories**\.

   1. Select **configuration change** and **failure**\.

   1. Choose **Create**\.

## \[RDS\.23\] RDS instances should not use a database engine default port<a name="rds-23"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(5\)

**Category:** Protect > Secure network configuration

**Severity:** Low

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** `rds-no-default-ports` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the RDS cluster or instance uses a port other than the default port of the database engine\.

If you use a known port to deploy an RDS cluster or instance, an attacker can guess information about the cluster or instance\. The attacker can use this information in conjunction with other information to connect to an RDS cluster or instance or gain additional information about your application\.

When you change the port, you must also update the existing connection strings that were used to connect to the old port\. You should also check the security group of the DB instance to ensure that it includes an ingress rule that allows connectivity on the new port\.

### Remediation<a name="rds-23-remediation"></a>

**To modify the default port of an existing DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Select the DB instance to modify

1. Choose **Modify**\.

1. Under **Database options**, change **Database port** to a non\-default value\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. You can choose either **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. For clusters, choose **Modify cluster**\. For instances, choose **Modify DB Instance**\.

## \[RDS\.24\] RDS Database clusters should use a custom administrator username<a name="rds-24"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Identify > Resource Configuration

**Severity:** Medium

**Resource type:** `AWS::RDS:DBCluster`

**AWS Config rule:** `[rds\-cluster\-default\-admin\-check](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-default-admin-check.html)`

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS database cluster has changed the admin username from its default value\. The control does not apply to engines of the type neptune \(Neptune DB\) or docdb \(DocumentDB\)\. This rule will fail if the admin username is set to the default value\.

When creating an Amazon RDS database, you should change the default admin username to a unique value\. Default usernames are public knowledge and should be changed during RDS database creation\. Changing the default usernames reduces the risk of unintended access\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="rds-24-remediation"></a>

For changing the admin username associated with the Amazon RDS database cluster, [create a new RDS database cluster](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.CreateInstance.html) and change the default admin username while creating the database\.

## \[RDS\.25\] RDS database instances should use a custom administrator username<a name="rds-25"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Identify > Resource Configuration

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** `[rds\-instance\-default\-admin\-check](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-default-admin-check.html)`

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether you've changed the administrative username for Amazon Relational Database Service \(Amazon RDS\) database instances from the default value\. The control does not apply to engines of the type neptune \(Neptune DB\) or docdb \(DocumentDB\)\. The control fails if the administrative username is set to the default value\.

Default administrative usernames on Amazon RDS databases are public knowledge\. When creating an Amazon RDS database, you should change the default administrative username to a unique value to reduce the risk of unintended access\.

### Remediation<a name="rds-25-remediation"></a>

To change the administrative username associated with an RDS database instance, first [create a new RDS database instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateDBInstance.html)\. Change the default administrative username while creating the database\.

## \[RDS\.26\] RDS DB instances should be covered by a backup plan<a name="rds-26"></a>

**Category:** Recover > Resilience > Backups enabled

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6, NIST\.800\-53\.r5 CP\-6\(1\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-12, NIST\.800\-53\.r5 SI\-13\(5\)

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-resources-protected-by-backup-plan.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-resources-protected-by-backup-plan.html) ``

**Schedule type:** Periodic

**Parameters:** None

This control evaluates if Amazon RDS DB instances are covered by a backup plan\. This control fails if an RDS DB instance isn't covered by a backup plan\.

AWS Backup is a fully managed backup service that centralizes and automates the backing up of data across AWS services\. With AWS Backup, you can create backup policies called backup plans\. You can use these plans to define your backup requirements, such as how frequently to back up your data and how long to retain those backups\. Including RDS DB instances in a backup plan helps you protect your data from unintended loss or deletion\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="rds-26-remediation"></a>

To add an RDS DB instance to an AWS Backup backup plan, see [Assigning resources to a backup plan](https://docs.aws.amazon.com/aws-backup/latest/devguide/assigning-resources.html) in the *AWS Backup Developer Guide*\.