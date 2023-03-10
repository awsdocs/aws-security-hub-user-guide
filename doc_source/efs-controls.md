# Amazon Elastic File System controls<a name="efs-controls"></a>

These controls are related to Amazon EFS resources\.

## \[EFS\.1\] Elastic File System should be configured to encrypt file data at\-rest using AWS KMS<a name="efs-1"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::EFS::FileSystem`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether Amazon Elastic File System is configured to encrypt the file data using AWS KMS\. The check fails in the following cases\.
+ `Encrypted` is set to `false` in the [https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html](https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html) response\.
+ The `KmsKeyId` key in the [https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html](https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html) response does not match the `KmsKeyId` parameter for [https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html)\.

Note that this control does not use the `KmsKeyId` parameter for [https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html)\. It only checks the value of `Encrypted`\.

For an added layer of security for your sensitive data in Amazon EFS, you should create encrypted file systems\. Amazon EFS supports encryption for file systems at\-rest\. You can enable encryption of data at rest when you create an Amazon EFS file system\. To learn more about Amazon EFS encryption, see[ Data encryption in Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/encryption.html) in the *Amazon Elastic File System User Guide*\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="efs-1-remediation"></a>

For details on how to encrypt a new Amazon EFS file system, see [Encrypting data at rest](https://docs.aws.amazon.com/efs/latest/ug/encryption-at-rest.html) in the *Amazon Elastic File System User Guide*\.

## \[EFS\.2\] Amazon EFS volumes should be in backup plans<a name="efs-2"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6, NIST\.800\-53\.r5 CP\-6\(1\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-12, NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > Backup

**Severity:** Medium

**Resource type:** `AWS::EFS::FileSystem`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-in-backup-plan.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-in-backup-plan.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether Amazon Elastic File System \(Amazon EFS\) file systems are added to the backup plans in AWS Backup\. The control fails if Amazon EFS file systems are not included in the backup plans\. 

Including EFS file systems in the backup plans helps you to protect your data from deletion and data loss\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="efs-2-remediation"></a>

To remediate this issue, update your file system to enable automatic backups\.

**To enable automatic backups for an existing file system**

1. Open the Amazon Elastic File System console at [https://console\.aws\.amazon\.com/efs/](https://console.aws.amazon.com/efs/)\.

1. On the **File systems** page, choose the file system for which to enable automatic backups\.

   The **File system details** page is displayed\.

1. Under **General**, choose **Edit**\.

1. To enable automatic backups, select **Enable automatic backups**\. 

1. Choose **Save changes**\.

To learn more, visit [Using AWS Backup with Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/awsbackup.html) in the *Amazon Elastic File System User Guide*\.

## \[EFS\.3\] EFS access points should enforce a root directory<a name="efs-3"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-6\(10\)

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::EFS::AccessPoint`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-access-point-enforce-root-directory.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-access-point-enforce-root-directory.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon EFS access points are configured to enforce a root directory\. The control fails if the value of `Path` is set to `/` \(the default root directory of the file system\)\.

When you enforce a root directory, the NFS client using the access point uses the root directory configured on the access point instead of the file system's root directory\. Enforcing a root directory for an access point helps restrict data access by ensuring that users of the access point can only reach files of the specified subdirectory\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="efs-3-remediation"></a>

For instructions on how to enforce a root directory for an Amazon EFS access point, see [Enforcing a root directory with an access point](https://docs.aws.amazon.com/efs/latest/ug/efs-access-points.html#enforce-root-directory-access-point) in the *Amazon Elastic File System User Guide*\. 

## \[EFS\.4\] EFS access points should enforce a user identity<a name="efs-4"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-6\(2\)

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::EFS::AccessPoint`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-access-point-enforce-user-identity.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-access-point-enforce-user-identity.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon EFS access points are configured to enforce a user identity\. This control fails if a POSIX user identity is not defined while creating the EFS access point\.

Amazon EFS access points are application\-specific entry points into an EFS file system that make it easier to manage application access to shared datasets\. Access points can enforce a user identity, including the user's POSIX groups, for all file system requests that are made through the access point\. Access points can also enforce a different root directory for the file system so that clients can only access data in the specified directory or its subdirectories\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="efs-4-remediation"></a>

To enforce a user identity for an Amazon EFS access point, see [Enforcing a user identity using an access point](https://docs.aws.amazon.com/efs/latest/ug/efs-access-points.html#enforce-identity-access-points) in the *Amazon Elastic File System User Guide*\. 