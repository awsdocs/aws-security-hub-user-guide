# Security Hub controls that you might want to disable<a name="controls-to-disable"></a>

We recommend disabling some Security Hub controls to reduce finding noise\.

## Controls that deal with global resources<a name="controls-to-disable-global-resources"></a>

To save on the cost of AWS Config, you can disable recording of global resources in all but one AWS Region\. After you do this, AWS Security Hub will still run security checks in all Regions where controls are enabled and will charge you based on the number of checks per account per Region\. Accordingly, to save on the cost of Security Hub, disable the following controls that deal with global resources in all Regions except the Region that records global resources\.

If you disable these controls and disable recording of global resources in particular Regions, you should also disable [\[Config\.1\] AWS Config should be enabled](config-controls.md#config-1) in those Regions\. This is because Config\.1 requires recording of global resources in order to pass\.
+ [\[IAM\.1\] IAM policies should not allow full "\*" administrative privileges](iam-controls.md#iam-1)
+ [\[IAM\.2\] IAM users should not have IAM policies attached](iam-controls.md#iam-2)
+ [\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](iam-controls.md#iam-3)
+ [\[IAM\.4\] IAM root user access key should not exist](iam-controls.md#iam-4)
+ [\[IAM\.5\] MFA should be enabled for all IAM users that have a console password](iam-controls.md#iam-5)
+ [\[IAM\.6\] Hardware MFA should be enabled for the root user](iam-controls.md#iam-6)
+ [\[IAM\.7\] Password policies for IAM users should have strong AWS Configurations](iam-controls.md#iam-7)
+ [\[IAM\.8\] Unused IAM user credentials should be removed](iam-controls.md#iam-8)
+ [\[IAM\.9\] Virtual MFA should be enabled for the root user](iam-controls.md#iam-9)
+ [\[IAM\.10\] Password policies for IAM users should have strong AWS Configurations](iam-controls.md#iam-10)
+ [\[IAM\.11\] Ensure IAM password policy requires at least one uppercase letter](iam-controls.md#iam-11)
+ [\[IAM\.12\] Ensure IAM password policy requires at least one lowercase letter](iam-controls.md#iam-12)
+ [\[IAM\.13\] Ensure IAM password policy requires at least one symbol](iam-controls.md#iam-13)
+ [\[IAM\.14\] Ensure IAM password policy requires at least one number](iam-controls.md#iam-14)
+ [\[IAM\.15\] Ensure IAM password policy requires minimum password length of 14 or greater](iam-controls.md#iam-15)
+ [\[IAM\.16\] Ensure IAM password policy prevents password reuse](iam-controls.md#iam-16)
+ [\[IAM\.17\] Ensure IAM password policy expires passwords within 90 days or less](iam-controls.md#iam-17)
+ [\[IAM\.18\] Ensure a support role has been created to manage incidents with AWS Support](iam-controls.md#iam-18)
+ [\[IAM\.19\] MFA should be enabled for all IAM users](iam-controls.md#iam-19)
+ [\[IAM\.20\] Avoid the use of the root user](iam-controls.md#iam-20)
+ [\[IAM\.21\] IAM customer managed policies that you create should not allow wildcard actions for services](iam-controls.md#iam-21)
+ [\[IAM\.22\] IAM user credentials unused for 45 days should be removed](iam-controls.md#iam-22)
+ [\[KMS\.1\] IAM customer managed policies should not allow decryption actions on all KMS keys](kms-controls.md#kms-1)
+ [\[KMS\.2\] IAM principals should not have IAM inline policies that allow decryption actions on all KMS keys](kms-controls.md#kms-2)

## Controls that deal with CloudTrail logging<a name="controls-to-disable-cloudtrail-logging"></a>

This control deals with using AWS Key Management Service \(AWS KMS\) to encrypt AWS CloudTrail trail logs\. If you log these trails in a centralized logging account, you only need to enable this control in the account and Region where centralized logging takes place\.
+ [\[CloudTrail\.2\] CloudTrail should have encryption at\-rest enabled](cloudtrail-controls.md#cloudtrail-2)

## Controls that deal with CloudWatch alarms<a name="controls-to-disable-cloudwatch-alarms"></a>

If you prefer to use Amazon GuardDuty for anomaly detection instead of Amazon CloudWatch alarms, you can disable these controls, which focus on CloudWatch alarms\.
+ [\[CloudWatch\.1\] A log metric filter and alarm should exist for usage of the "root" user](cloudwatch-controls.md#cloudwatch-1)
+ [\[CloudWatch\.2\] Ensure a log metric filter and alarm exist for unauthorized API calls](cloudwatch-controls.md#cloudwatch-2)
+ [\[CloudWatch\.3\] Ensure a log metric filter and alarm exist for Management Console sign\-in without MFA](cloudwatch-controls.md#cloudwatch-3)
+ [\[CloudWatch\.4\] Ensure a log metric filter and alarm exist for IAM policy changes](cloudwatch-controls.md#cloudwatch-4)
+ [\[CloudWatch\.5\] Ensure a log metric filter and alarm exist for CloudTrail AWS Configuration changes](cloudwatch-controls.md#cloudwatch-5)
+ [\[CloudWatch\.6\] Ensure a log metric filter and alarm exist for AWS Management Console authentication failures](cloudwatch-controls.md#cloudwatch-6)
+ [\[CloudWatch\.7\] Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer managed keys](cloudwatch-controls.md#cloudwatch-7)
+ [\[CloudWatch\.8\] Ensure a log metric filter and alarm exist for S3 bucket policy changes](cloudwatch-controls.md#cloudwatch-8)
+ [\[CloudWatch\.9\] Ensure a log metric filter and alarm exist for AWS Config configuration changes](cloudwatch-controls.md#cloudwatch-9)
+ [\[CloudWatch\.10\] Ensure a log metric filter and alarm exist for security group changes](cloudwatch-controls.md#cloudwatch-10)
+ [\[CloudWatch\.11\] Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)](cloudwatch-controls.md#cloudwatch-11)
+ [\[CloudWatch\.12\] Ensure a log metric filter and alarm exist for changes to network gateways](cloudwatch-controls.md#cloudwatch-12)
+ [\[CloudWatch\.13\] Ensure a log metric filter and alarm exist for route table changes](cloudwatch-controls.md#cloudwatch-13)
+ [\[CloudWatch\.14\] Ensure a log metric filter and alarm exist for VPC changes](cloudwatch-controls.md#cloudwatch-14)