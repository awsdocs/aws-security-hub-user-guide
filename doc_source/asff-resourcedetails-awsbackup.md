# AwsBackup<a name="asff-resourcedetails-awsbackup"></a>

The following are examples of the AWS Security Finding Format for `AwsBackup` resources\.

## AwsBackupBackupPlan<a name="asff-resourcedetails-awsbackupbackupplan"></a>

The `AwsBackupBackupPlan` object provides information about an AWS Backup backup plan\. An AWS Backup backup plan is a policy expression that defines when and how you want to back up your AWS resources\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsBackupBackupPlan` object\. To view descriptions of `AwsBackupBackupPlan` attributes, see [AwsBackupBackupPlan](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsBackupBackupPlanDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsBackupBackupPlan": {
    "BackupPlan": {
    	"AdvancedBackupSettings": [{
    		"BackupOptions": {
    			"WindowsVSS":"enabled"
    		},
    		"ResourceType":"EC2"
    	}],
    	"BackupPlanName": "test",
    	"BackupPlanRule": [{
    		"CompletionWindowMinutes": 10080,
    		"CopyActions": [{
    			"DestinationBackupVaultArn": "arn:aws:backup:us-east-1:858726136373:backup-vault:aws/efs/automatic-backup-vault",
    			"Lifecycle": {
    				"DeleteAfterDays": 365,
    				"MoveToColdStorageAfterDays": 30
    			}
    		}],
    		"Lifecycle": {
    			"DeleteAfterDays": 35
    		},
    		"RuleName": "DailyBackups",
    		"ScheduleExpression": "cron(0 5 ? * * *)",
    		"StartWindowMinutes": 480,
    		"TargetBackupVault": "Default"
    		},
    		{
    		"CompletionWindowMinutes": 10080,
    		"CopyActions": [{
    			"DestinationBackupVaultArn": "arn:aws:backup:us-east-1:858726136373:backup-vault:aws/efs/automatic-backup-vault",
    			"Lifecycle": {
    				"DeleteAfterDays": 365,
    				"MoveToColdStorageAfterDays": 30
    			}
    		}],
    		"Lifecycle": {
    			"DeleteAfterDays": 35
    		},
    		"RuleName": "Monthly",
    		"ScheduleExpression": "cron(0 5 1 * ? *)",
    		"StartWindowMinutes": 480,
    		"TargetBackupVault": "Default"
    	}]
    },
    "BackupPlanArn": "arn:aws:backup:us-east-1:858726136373:backup-plan:b6d6b896-590d-4ee1-bf29-c5ccae63f4e7",
    "BackupPlanId": "b6d6b896-590d-4ee1-bf29-c5ccae63f4e7",
    "VersionId": "ZDVjNDIzMjItYTZiNS00NzczLTg4YzctNmExMWM2NjZhY2E1"
}
```

## AwsBackupBackupVault<a name="asff-resourcedetails-awsbackupbackupvault"></a>

The `AwsBackupBackupVault` object provides information about an AWS Backup backup vault\. A AWS Backup backup vault is a container that stores and organizes your backups\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsBackupBackupVault` object\. To view descriptions of `AwsBackupBackupVault` attributes, see [AwsBackupBackupVault](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsBackupBackupVaultDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsBackupBackupVault": {
    "AccessPolicy": {
    	"Statement": [{
    		"Action": [
    			"backup:DeleteBackupVault",
    			"backup:DeleteBackupVaultAccessPolicy",
    			"backup:DeleteRecoveryPoint",
    			"backup:StartCopyJob",
    			"backup:StartRestoreJob",
    			"backup:UpdateRecoveryPointLifecycle"
    		],
    		"Effect": "Deny",
    		"Principal": {
    			"AWS": "*"
    		},
    		"Resource": "*"
    	}],
    	"Version": "2012-10-17"
    },
    "BackupVaultArn": "arn:aws:backup:us-east-1:123456789012:backup-vault:aws/efs/automatic-backup-vault",
    "BackupVaultName": "aws/efs/automatic-backup-vault",
    "EncrytionKeyArn": "arn:aws:kms:us-east-1:444455556666:key/72ba68d4-5e43-40b0-ba38-838bf8d06ca0",
    "Notifications": {
    	"BackupVaultEvents": ["BACKUP_JOB_STARTED", "BACKUP_JOB_COMPLETED", "COPY_JOB_STARTED"],
    	"SNSTopicArn": "arn:aws:sns:us-west-2:111122223333:MyVaultTopic"
    }
}
```

## AwsBackupRecoveryPoint<a name="asff-resourcedetails-awsbackuprecoverypoint"></a>

The `AwsBackupRecoveryPoint` object provides information about an AWS Backup backup, also referred to as a recovery point\. An AWS Backup recovery point represents the content of a resource at a specified time\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsBackupRecoveryPoint` object\. To view descriptions of `AwsBackupBackupVault` attributes, see [AwsBackupRecoveryPoint](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsBackupRecoveryPointDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsBackupRecoveryPoint": {
    "BackupSizeInBytes": 0,
    "BackupVaultName": "aws/efs/automatic-backup-vault",
    "BackupVaultArn": "arn:aws:backup:us-east-1:111122223333:backup-vault:aws/efs/automatic-backup-vault",
    "CalculatedLifecycle": {
    	"DeleteAt": "2021-08-30T06:51:58.271Z",
    	"MoveToColdStorageAt": "2020-08-10T06:51:58.271Z"
    },
    "CompletionDate": "2021-07-26T07:21:40.361Z",
    "CreatedBy": {
    	"BackupPlanArn": "arn:aws:backup:us-east-1:111122223333:backup-plan:aws/efs/73d922fb-9312-3a70-99c3-e69367f9fdad",
    	"BackupPlanId": "aws/efs/73d922fb-9312-3a70-99c3-e69367f9fdad",
    	"BackupPlanVersion": "ZGM4YzY5YjktMWYxNC00ZTBmLWE5MjYtZmU5OWNiZmM5ZjIz",
    	"BackupRuleId": "2a600c2-42ad-4196-808e-084923ebfd25"
    },
    "CreationDate": "2021-07-26T06:51:58.271Z",
    "EncryptionKeyArn": "arn:aws:kms:us-east-1:111122223333:key/72ba68d4-5e43-40b0-ba38-838bf8d06ca0",
    "IamRoleArn": "arn:aws:iam::111122223333:role/aws-service-role/backup.amazonaws.com/AWSServiceRoleForBackup",
    "IsEncrypted": true,
    "LastRestoreTime": "2021-07-26T06:51:58.271Z",
    "Lifecycle": {
    	"DeleteAfterDays": 35,
    	"MoveToColdStorageAfterDays": 15
    },
    "RecoveryPointArn": "arn:aws:backup:us-east-1:111122223333:recovery-point:151a59e4-f1d5-4587-a7fd-0774c6e91268",
    "ResourceArn": "arn:aws:elasticfilesystem:us-east-1:858726136373:file-system/fs-15bd31a1",
    "ResourceType": "EFS",
    "SourceBackupVaultArn": "arn:aws:backup:us-east-1:111122223333:backup-vault:aws/efs/automatic-backup-vault",
    "Status": "COMPLETED",
    "StatusMessage": "Failure message",
    "StorageClass": "WARM"
}
```