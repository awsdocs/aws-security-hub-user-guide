# Amazon Redshift controls<a name="redshift-controls"></a>

These controls are related to Amazon Redshift resources\.

## \[Redshift\.1\] Amazon Redshift clusters should prohibit public access<a name="redshift-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.2, PCI DSS v3\.2\.1/1\.3\.4, PCI DSS v3\.2\.1/1\.3\.6, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration > Resources not publicly accessible

**Severity:** Critical

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-public-access-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-public-access-check.html)

**Schedule type:** Change triggered

**Parameters:** None 

This control checks whether Amazon Redshift clusters are publicly accessible\. It evaluates the `PubliclyAccessible` field in the cluster configuration item\. 

The `PubliclyAccessible` attribute of the Amazon Redshift cluster configuration indicates whether the cluster is publicly accessible\. When the cluster is configured with `PubliclyAccessible` set to `true`, it is an Internet\-facing instance that has a publicly resolvable DNS name, which resolves to a public IP address\.

When the cluster is not publicly accessible, it is an internal instance with a DNS name that resolves to a private IP address\. Unless you intend for your cluster to be publicly accessible, the cluster should not be configured with `PubliclyAccessible` set to `true`\.

### Remediation<a name="redshift-1-remediation"></a>

To remediate this issue, update your Amazon Redshift cluster to disable public access\.

**To disable public access to an Amazon Redshift cluster**

1. Open the Amazon Redshift console at [https://console\.aws\.amazon\.com/redshift/](https://console.aws.amazon.com/redshift/)\.

1. In the navigation menu, choose **Clusters**, then choose the name of the cluster with the security group to modify\.

1. Choose **Actions**, then choose **Modify publicly accessible setting**\.

1. Under **Allow instances and devices outside the VPC to connect to your database through the cluster endpoint**, choose **No**\.

1. Choose **Confirm**\.

## \[Redshift\.2\] Connections to Amazon Redshift clusters should be encrypted in transit<a name="redshift-2"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\)

**Category:** Protect > Data protection > Encryption of data in transit 

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`, `AWS::Redshift::ClusterParameterGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-require-tls-ssl.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-require-tls-ssl.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether connections to Amazon Redshift clusters are required to use encryption in transit\. The check fails if the Amazon Redshift cluster parameter `require_SSL` isn't set to `True`\.

TLS can be used to help prevent potential attackers from using person\-in\-the\-middle or similar attacks to eavesdrop on or manipulate network traffic\. Only encrypted connections over TLS should be allowed\. Encrypting data in transit can affect performance\. You should test your application with this feature to understand the performance profile and the impact of TLS\. 

**Note**  
This control is not supported in Europe \(Milan\)\.

### Remediation<a name="redshift-2-remediation"></a>

To remediate this issue, update the parameter group to require encryption\.

**To modify a parameter group**

1. Open the Amazon Redshift console at [https://console\.aws\.amazon\.com/redshift/](https://console.aws.amazon.com/redshift/)\.

1. In the navigation menu, choose **Config**, then choose **Workload management** to display the **Workload management** page\. 

1. Choose the parameter group that you want to modify\. 

1. Choose **Parameters**\.

1. Choose **Edit parameters**, and then set `require_ssl` to **True**\.

1. Enter your changes and then choose **Save**\.

## \[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled<a name="redshift-3"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6, NIST\.800\-53\.r5 CP\-6\(1\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > Backups enabled 

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-backup-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-backup-enabled.html)

**Schedule type:** Change triggered

**Parameters:**
+ `MinRetentionPeriod = 7`

This control checks whether Amazon Redshift clusters have automated snapshots enabled\. It also checks whether the snapshot retention period is greater than or equal to seven\.

Backups help you to recover more quickly from a security incident\. They strengthen the resilience of your systems\. Amazon Redshift takes periodic snapshots by default\. This control checks whether automatic snapshots are enabled and retained for at least seven days\. For more details on Amazon Redshift automated snapshots, see [Automated snapshots](https://docs.aws.amazon.com/redshift/latest/mgmt/working-with-snapshots.html#about-automated-snapshots) in the *Amazon Redshift Management Guide*\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
Asia Pacific \(Sydney\)
China \(Ningxia\)
Europe \(Milan\)

### Remediation<a name="redshift-3-remediation"></a>

To remediate this issue, update the snapshot retention period to at least 7\.

**To modify the snapshot retention period**

1. Open the Amazon Redshift console at [https://console\.aws\.amazon\.com/redshift/](https://console.aws.amazon.com/redshift/)\.

1. In the navigation menu, choose **Clusters**, then choose the name of the cluster to modify\.

1. Choose **Edit**\.

1. Under **Backup**, set **Snapshot retention** to a value of 7 or greater\.

1. Choose **Modify Cluster**\.

## \[Redshift\.4\] Amazon Redshift clusters should have audit logging enabled<a name="redshift-4"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(4\), NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AC\-6\(9\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4\(20\), NIST\.800\-53\.r5 SI\-7\(8\)

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** `redshift-cluster-audit-logging-enabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:**
+ `loggingEnabled = true`

This control checks whether an Amazon Redshift cluster has audit logging enabled\.

Amazon Redshift audit logging provides additional information about connections and user activities in your cluster\. This data can be stored and secured in Amazon S3 and can be helpful in security audits and investigations\. For more information, see [Database audit logging](https://docs.aws.amazon.com/redshift/latest/mgmt/db-auditing.html) in the *Amazon Redshift Management Guide*\.

### Remediation<a name="redshift-4-remediation"></a>

**To enable cluster audit logging**

1. Open the Amazon Redshift console at [https://console\.aws\.amazon\.com/redshift/](https://console.aws.amazon.com/redshift/)\.

1. In the navigation menu, choose **Clusters**, then choose the name of the cluster to modify\.

1. Choose **Maintenance and monitoring**\.

1. Under **Audit logging**, choose **Edit**\.

1. Set **Enable audit logging** to **yes**, then enter the log destination bucket details\.

1. Choose **Confirm**\.

## \[Redshift\.6\] Amazon Redshift should have automatic upgrades to major versions enabled<a name="redshift-6"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-2, NIST\.800\-53\.r5 SI\-2\(2\), NIST\.800\-53\.r5 SI\-2\(4\), NIST\.800\-53\.r5 SI\-2\(5\)

**Category:** Detect > Vulnerability and patch management

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-maintenancesettings-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-maintenancesettings-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `allowVersionUpgrade = true`

This control checks whether automatic major version upgrades are enabled for the Amazon Redshift cluster\.

Enabling automatic major version upgrades ensures that the latest major version updates to Amazon Redshift clusters are installed during the maintenance window\. These updates might include security patches and bug fixes\. Keeping up to date with patch installation is an important step in securing systems\.

**Note**  
This control is not supported in Middle East \(Bahrain\)\.

### Remediation<a name="redshift-6-remediation"></a>

To remediate this issue from the AWS CLI, use the Amazon Redshift `modify-cluster` command to set the `--allow-version-upgrade` attribute\.

```
aws redshift modify-cluster --cluster-identifier clustername --allow-version-upgrade
```

Where `clustername` is the name of your Amazon Redshift cluster\.

## \[Redshift\.7\] Redshift clusters should use enhanced VPC routing<a name="redshift-7"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration > API private access

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-enhanced-vpc-routing-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-enhanced-vpc-routing-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon Redshift cluster has `EnhancedVpcRouting` enabled\.

Enhanced VPC routing forces all `COPY` and `UNLOAD` traffic between the cluster and data repositories to go through your VPC\. You can then use VPC features such as security groups and network access control lists to secure network traffic\. You can also use VPC Flow Logs to monitor network traffic\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="redshift-7-remediation"></a>

For detailed remediation instructions, see [Enabling enhanced VPC routing](https://docs.aws.amazon.com/redshift/latest/mgmt/enhanced-vpc-enabling-cluster.html) in the *Amazon Redshift Management Guide*\.

## \[Redshift\.8\] Amazon Redshift clusters should not use the default Admin username<a name="redshift-8"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Identify > Resource Configuration

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-default-admin-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-default-admin-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon Redshift cluster has changed the admin username from its default value\. This control will fail if the admin username for a Redshift cluster is set to `awsuser`\.

When creating a Redshift cluster, you should change the default admin username to a unique value\. Default usernames are public knowledge and should be changed upon configuration\. Changing the default usernames reduces the risk of unintended access\.

### Remediation<a name="redshift-8-remediation"></a>

You can't change the admin username for your Amazon Redshift cluster after it is created\. To create a new cluster, follow the instructions [here](https://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-prereq.html)\.

## \[Redshift\.9\] Redshift clusters should not use the default database name<a name="redshift-9"></a>

**Category:** Identify > Resource Configuration

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-default-db-name-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-default-db-name-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon Redshift cluster has changed the database name from its default value\. The control will fail if the database name for a Redshift cluster is set to `dev`\.

When creating a Redshift cluster, you should change the default database name to a unique value\. Default names are public knowledge and should be changed upon configuration\. As an example, a well\-known name could lead to inadvertent access if it was used in IAM policy conditions\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="redshift-9-remediation"></a>

You can't change the database name for your Amazon Redshift cluster after it is created\. For instructions on creating a new cluster, see [Getting started with Amazon Redshift](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html) in the * Amazon Redshift Getting Started Guide*\.