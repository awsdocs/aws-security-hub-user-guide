# Amazon DynamoDB controls<a name="dynamodb-controls"></a>

These controls are related to DynamoDB resources\.

## \[DynamoDB\.1\] DynamoDB tables should automatically scale capacity with demand<a name="dynamodb-1"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-2\(2\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::DynamoDB::Table`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-autoscaling-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-autoscaling-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether an Amazon DynamoDB table can scale its read and write capacity as needed\. This control passes if the table uses either on\-demand capacity mode or provisioned mode with auto scaling configured\. Scaling capacity with demand avoids throttling exceptions, which helps to maintain availability of your applications\.

DynamoDB tables in on\-demand capacity mode are only limited by the DynamoDB throughput default table quotas\. To raise these quotas, you can file a support ticket through [AWS Support](http://aws.amazon.com/support)\.

DynamoDB tables in provisioned mode with auto scaling adjust the provisioned throughput capacity dynamically in response to traffic patterns\. For additional information on DynamoDB request throttling, see [Request throttling and burst capacity](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/ProvisionedThroughput.html#ProvisionedThroughput.Throttling) in the *Amazon DynamoDB Developer Guide*\.

**Note**  
This control is not supported in AWS GovCloud \(US\-East\) or AWS GovCloud \(US\-West\)\.

### Remediation<a name="dynamodb-1-remediation"></a>

For detailed instructions on enabling DynamoDB automatic scaling on existing tables in capacity mode, see [Enabling DynamoDB auto scaling on existing tables](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/AutoScaling.Console.html#AutoScaling.Console.ExistingTable) in the*Amazon DynamoDB Developer Guide*\.

## \[DynamoDB\.2\] DynamoDB tables should have point\-in\-time recovery enabled<a name="dynamodb-2"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-12, NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > Backups enabled

**Severity:** Medium

**Resource type:** `AWS::DynamoDB::Table`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-pitr-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-pitr-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether point\-in\-time recovery \(PITR\) is enabled for an Amazon DynamoDB table\.

Backups help you to recover more quickly from a security incident\. They also strengthen the resilience of your systems\. DynamoDB point\-in\-time recovery automates backups for DynamoDB tables\. It reduces the time to recover from accidental delete or write operations\. DynamoDB tables that have PITR enabled can be restored to any point in time in the last 35 days\.

### Remediation<a name="dynamodb-2-remediation"></a>

To remediate this issue, add point\-in\-time recovery to your DynamoDB table\.

**To enable DynamoDB point\-in\-time recovery for an existing table**

1. Open the DynamoDB console at [https://console\.aws\.amazon\.com/dynamodb/](https://console.aws.amazon.com/dynamodb/)\.

1. Choose the table that you want to work with, and then choose **Backups**\. 

1. In the **Point\-in\-time Recovery** section, under **Status**, choose **Enable**\.

1. Choose **Enable** again to confirm the change\.

## \[DynamoDB\.3\] DynamoDB Accelerator \(DAX\) clusters should be encrypted at rest<a name="dynamodb-3"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest 

**Severity:** Medium

**Resource type:** `AWS::DAX::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dax-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/dax-encryption-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether a DAX cluster is encrypted at rest\. 

Encrypting data at rest reduces the risk of data stored on disk being accessed by a user not authenticated to AWS\. The encryption adds another set of access controls to limit the ability of unauthorized users to access to the data\. For example, API permissions are required to decrypt the data before it can be read\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="dynamodb-3-remediation"></a>

You cannot enable or disable encryption at rest after a cluster is created\. You must recreate the cluster in order to enable encryption at rest\. For detailed instructions on how to create a DAX cluster with encryption at rest enabled, see[ Enabling encryption at rest using the AWS Management Console](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DAXEncryptionAtRest.html#dax.encryption.tutorial-console) in the *Amazon DynamoDB Developer Guide*\.

## \[DynamoDB\.4\] DynamoDB tables should be covered by a backup plan<a name="dynamodb-4"></a>

**Category:** Recover > Resilience > Backups enabled

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6, NIST\.800\-53\.r5 CP\-6\(1\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-12, NIST\.800\-53\.r5 SI\-13\(5\)

**Severity:** Medium

**Resource type:** `AWS::DynamoDB::Table`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-resources-protected-by-backup-plan.html](https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-resources-protected-by-backup-plan.html) ``

**Schedule type:** Periodic

**Parameters:** None

This control evaluates whether a DynamoDB table is covered by a backup plan\. The control fails if a DynamoDB table isn't covered by a backup plan\. This control only evaluates DynamoDB tables that are in ACTIVE state\.

Backups help you recover more quickly from a security incident\. They also strengthen the resilience of your systems\. Including DynamoDB tables in a backup plan helps you protect your data from unintended loss or deletion\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="dynamodb-4-remediation"></a>

To add a DynamoDB table to an AWS Backup backup plan, see [Assigning resources to a backup plan](https://docs.aws.amazon.com/aws-backup/latest/devguide/assigning-resources.html) in the *AWS Backup Developer Guide*\.