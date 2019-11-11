# Standards Supported in AWS Security Hub: CIS AWS Foundations<a name="securityhub-standards"></a>

AWS Security Hub consumes, aggregates, and analyzes security findings from various supported AWS and third\-party products\. Security Hub also generates its own findings as the result of running automated and continuous checks against the compliance rules in the supported security standards\. These checks provide a compliance score and identify specific accounts and resources that require attention\.

In this release, Security Hub supports the CIS AWS Foundations standard\. For more information, see [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/) on the CIS website\.

AWS Security Hub has satisfied the requirements of CIS Security Software Certification and is hereby awarded CIS Security Software Certification for the following CIS Benchmarks:
+ CIS Benchmark for CIS Amazon Web Services Foundations Benchmark, v1\.2\.0, Level 1
+ CIS Benchmark for CIS Amazon Web Services Foundations Benchmark, v1\.2\.0, Level 2

## Enabling the CIS AWS Foundations Standard in Security Hub<a name="securityhub-standards-enabling"></a>

After you enable Security Hub in a particular AWS account and Region, the CIS AWS Foundations standard in that account and Region is automatically enabled\.

After the CIS AWS Foundations standard is enabled in Security Hub in a particular account and Region, it begins running checks on your environment's resources in that account and Region against the compliance rules in the standard\. Then Security Hub generates findings based on the results of these checks\.

**Important**  
Cross\-Region processing isn't supported for the CIS AWS Foundations standard in Security Hub\. In other words, if you enable Security Hub \(and consequently this standard in Security Hub\) in one Region and a resource that it checks is located in another Region, the return value for such check is Failed\. For example, if you're storing your AWS CloudTrail logs in an Amazon S3 bucket in the us\-east\-2 Region and the CIS AWS Foundations standard is running in Security Hub enabled in us\-west\-2, checks 2\.3 \(Ensure the S3 bucket CloudTrail logs to is not publicly accessible\) and 2\.6 \(Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket\) are returned as Failed\.  
You must enable Security Hub in all Regions to be fully compliant with CIS AWS Foundations Benchmark checks\.

## How the CIS AWS Foundations Standard in Security Hub Uses AWS Config<a name="securityhub-standards-config"></a>

To run the CIS AWS Foundations standard's compliance checks on your environment's resources, Security Hub either runs through the exact audit steps prescribed for the checks in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/) or uses specific AWS Config managed rules\. Therefore, for the CIS AWS Foundations standard to be functional in Security Hub, when you enable it in a particular account, you must also enable AWS Config in that account\.

Security Hub doesn't manage AWS Config for you\. If you already have AWS Config enabled, you can continue configuring its settings through the AWS Config console or APIs\. If you don't have AWS Config enabled, you can enable it manually or by using the AWS CloudFormation "Enable AWS Config" template in AWS CloudFormation StackSets Sample Templates\.

When you enable Security Hub in a particular account, you also, by default, enable the supported CIS AWS Foundations standard in that account\. In other words, after you enable Security Hub, it immediately begins running checks on your environment's resources against the compliance rules in the now\-enabled CIS AWS Foundations standard\. Then Security Hub generates findings based on the results of these checks\.

To run CIS AWS Foundations standard's compliance checks on your environment's resources, Security Hub uses AWS Config rules to evaluate the configuration settings of your AWS resources\. AWS Config rules represent your ideal resource configuration settings\. Therefore, when you enable Security Hub in a particular account, you must also enable AWS Config in that account\. After Security Hub and AWS Config are enabled, Security Hub automatically creates the requisite infrastructure of AWS Config rules that it needs to run the CIS AWS Foundations standard's compliance checks\.

**Note**  
If you're working with a Security Hub master account, enable AWS Config in each of this master account's Security Hub member accounts\.

**Important**  
When you turn on the AWS Config recorder as part of enabling AWS Config, choose to record all resources supported in a given Region, including global resources\.

For more information, see [Getting Started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.

**Important**  
If you enable AWS Config in your Security Hub master account, this doesn't automatically enable AWS Config in the Security Hub member accounts for this master account\. If you want Security Hub to generate findings against the compliance rules in the CIS AWS Foundations standard for the resources in a Security Hub member account, you must enable AWS Config in that member account\.

After the CIS AWS Foundations standard is enabled, Security Hub automatically creates the requisite infrastructure of AWS Config rules that it needs to run the standard's compliance checks\. For every check that uses a specific AWS Config managed rule or rules, Security Hub creates an instance of that rule or rules specific to Security Hub \(even if another instance of this rule already exists\) in your AWS environment\. For information about which specific AWS Config managed rules the CIS AWS Foundations standard in Security Hub uses, see [CIS AWS Foundations Standard Checks Supported in Security Hub](#securityhub-standards-checks)\.

The limit for the AWS Config managed rules is 150 rules per account per Region\. If you have already reached this limit, you can still enable the CIS AWS Foundations standard in Security Hub\. This in turn automatically creates the requisite infrastructure of AWS Config rules that this standard needs to be functional\. If you're below the maximum allowed limit of AWS Config rules and you enable the CIS AWS Foundations standard in Security Hub, the rules that are automatically created for this standard do count toward the maximum allowed limit of AWS Config rules\. After you reach this limit, you can't manually create any more rules in AWS Config\.

### AWS Config Resources Required for CIS Checks<a name="securityhub-config-resources"></a>

If you don't enable all resources in AWS Config, a finding is generated for the check [2\.5 – Ensure AWS Config is enabled in all Regions](#securityhub-standards-checks-2.5)\. For other checks, you must enable the following resources in AWS Config for Security Hub to accurately report findings based on the CIS AWS Foundation standard checks:
+ AwsEc2Instance
+ AwsS3Bucket
+ Container
+ AwsIamAccessKey
+ AwsIamUser
+ AwsAccount
+ AwsIamPolicy
+ AwsCloudTrailTrail
+ AwsKmsKey
+ AwsEc2Vpc
+ AwsEc2SecurityGroup

When you view the details of a compliance standards rule that is based on an AWS Config rule, you can choose **Compliance rules** to open the AWS Config rule associated with the compliance check\. Only compliance checks that are based on AWS Config rules provide links to the AWS Config rule\.

## Results of Standards Checks in Security Hub<a name="securityhub-standards-checks-results"></a>

Security Hub uses the [AWS Security Finding Format](securityhub-findings-format.md) format for the findings that it generates as the result of running checks against the compliance rules included in the enabled standards\. For these findings, the AWS Security Finding format includes a special **Compliance** field that contains the standard's compliance\-related findings details, including the results of the checks that Security Hub ran\. The possible return values for a standard check are Passed, Failed, Warning \(if Security Hub or AWS Config can't complete the check\), and Not available \(if the service whose resources are being checked isn't available\)\. If all resources in the Security Hub master account and across all member accounts passed a given check, the rule that this check used is considered **Compliant**\. If one or more resources in the Security Hub master account, across member accounts, or both failed a given check or received a warning about it, the rule that this check used is considered **Noncompliant**\.

The **Compliance** field displays the result of the most recent check that Security Hub ran against a given rule\. The results of the previous checks are kept in an archived state for 90 days\. If a subsequent check against a given rule generates a new result \(for example, the status of "Avoid the use of the root account" changed from Failed to Passed\), a new finding that contains the most recent result is generated\. If a subsequent check against a given rule generates a result that is identical to the current result, the existing finding is updated, and no new finding is generated\.

Security Hub starts running the standards checks within 2 hours after the CIS AWS Foundations standard is enabled\. The checks run again automatically within 12 hours from the latest check\.

Security Hub supports both periodic and change\-triggered compliance checks\. Periodic checks are automatically run again within 12 hours after the latest run\. Change\-triggered checks are run when the resource associated with the check has any state changes\. For any Security Hub compliance check based on a managed AWS Config rule, you can click through to that rule to see whether it is change triggered or periodic\. In general, Security Hub leverages change triggered rules whenever possible, but there must be Config Configuration Item support for the resource to use a change triggered rule\. Security Hub's compliance checks that leverage Security Hub's own custom lambda functions are always periodic\. Periodicity cannot currently be changed\.

## CIS AWS Foundations Standard Checks Supported in Security Hub<a name="securityhub-standards-checks"></a>

The following are the CIS AWS Foundations standard's compliance checks that are supported in this release of Security Hub\.

**Important**  
You can disable the entire CIS AWS Foundations standard and thus stop Security Hub from running checks against its rules and generating findings based on those checks\. You *can't* disable individual rules in the CIS AWS Foundations standard\.

## 1\.1 – Avoid the use of the "root" account<a name="securityhub-standards-checks-1.1"></a>

The root account has unrestricted access to all resources in the AWS account\. We highly recommend that you avoid using this account\. The root account is the most privileged account\. Minimizing the use of this account and adopting the principle of least privilege for access management reduces the risk of accidental changes and unintended disclosure of highly privileged credentials\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="1.1-remediation"></a>

Use the root credentials for your AWS account only to create the first IAM user and add the user to a group\. Then use the IAM user account to perform common admin tasks\. Store your root credentials in a secure location that only authorized users can access\. Use your root credentials only when required to [ perform account and service management tasks](https://docs.aws.amazon.com/general/latest/gr/aws_tasks-that-require-root.html)\. As a best practice, apply IAM policies directly to groups and roles but not users\. For a tutorial on how to set up an administrator for daily use, see [ Creating Your First IAM Admin User and Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

## 1\.2 – Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password<a name="securityhub-standards-checks-1.2"></a>

Multi\-factor authentication \(MFA\) adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they're prompted for their user name and password as well as for an authentication code from their AWS MFA device\. We recommend enabling MFA for all accounts that have a console password\. Enabling MFA provides increased security for console access because it requires the authenticating principal to possess a device that emits a time\-sensitive key and have knowledge of a credential\.

To run this check, Security Hub uses the [mfa\-enabled\-for\-iam\-console\-access](https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

**Important**  
The AWS Config rule used for this check may take up to 4 hours to accurately report results for MFA\. Any findings that are generated within the first 4 hours after enabling CIS Standards checks may not be accurate\. It may also take up to 4 hours after remediating this issue for the check to report compliance\.

### Remediation<a name="1.2-remediation"></a>

**To configure MFA for a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the **User name** of the user to configure MFA for\.

1. Choose **Security credentials** and then choose **Manage** next to **Assigned MFA device**\.

1. Follow the **Manage MFA Device** wizard to assign the type of device appropriate for your environment\.

To learn how to delegate MFA setup to users, see [How to Delegate Management of Multi\-Factor Authentication to AWS IAM Users](http://aws.amazon.com/blogs/security/how-to-delegate-management-of-multi-factor-authentication-to-aws-iam-users/) on the AWS Security Blog\.

## 1\.3 – Ensure credentials unused for 90 days or greater are disabled<a name="securityhub-standards-checks-1.3"></a>

IAM users can access AWS resources using different types of credentials, such as passwords or access keys\. We recommend that you remove or deactivate all credentials that have been unused in 90 days or more\. Disabling or removing unnecessary credentials reduces the window of opportunity for credentials associated with a compromised or abandoned account to be used\. 

To run this check, Security Hub uses the [iam\-user\-unused\-credentials\-check](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.3-remediation"></a>

To get some of the information that you need to monitor accounts for dated credentials, use the IAM console\. For example, when you view users in your account, there is a column for **Access key age**, **Password age**, and **Last activity**\. If the value in any of these columns is greater than 90 days, make the credentials for those users inactive\.

You can also use credential reports to monitor user accounts and identify those with no activity for 90 or more days\. You can download credential reports in \.csv format from the IAM console\. For more information about credential reports, see [ Getting Credential Reports for Your AWS Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html#getting-credential-reports-console)\. 

After you identify the inactive accounts or unused credentials, use the following steps to disable them\.

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the name of the user with credentials over 90 days old\.

1. Choose **Security credentials** and then choose **Make inactive** for all sign\-in credentials and access keys that haven't been used in 90 days or more\.

## 1\.4 – Ensure access keys are rotated every 90 days or less<a name="securityhub-standards-checks-1.4"></a>

Access keys consist of an access key ID and secret access key, which are used to sign programmatic requests that you make to AWS\. AWS users need their own access keys to make programmatic calls to AWS from the AWS Command Line Interface \(AWS CLI\), Tools for Windows PowerShell, the AWS SDKs, or direct HTTP calls using the APIs for individual AWS services\. We recommend that you regularly rotate all access keys\. Rotating access keys reduces the chance for an access key that is associated with a compromised or terminated account to be used\. Rotate access keys to ensure that data can't be accessed with an old key that might have been lost, cracked, or stolen\. 

To run this check, Security Hub uses the [access\-keys\-rotated](https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.4-remediation"></a>

**To ensure that access keys aren't more than 90 days old**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. For each user that shows an **Access key age** that is greater than 90 days, choose the **User name** to open the settings for that user\.

1. Choose **Security credentials**\.

1. To create a new key for the user, choose **Create access key**\. Then either download the secret access key or choose **Show** and then copy it from the page\. Store it in a secure location to provide to the user and then choose **Close**\.

1. Update all applications that were using the previous key to use the new key\.

1. For the previous key, choose **Make inactive** to make the access key inactive\. Now the user can't make requests using that key\.

1. Confirm that all applications work as expected with the new key\.

1. After confirming that all applications work with the new key, delete the previous key\. To delete it, choose the **X** at the end of the row and then choose **Delete**\. After you delete the access key, you can't recover it\.

## 1\.5 – Ensure IAM password policy requires at least one uppercase letter<a name="securityhub-standards-checks-1.5"></a>

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\. We recommend that the password policy require at least one uppercase letter\. Setting a password complexity policy increases account resiliency against brute force login attempts\. 

To run this check, Security Hub uses the [iam\-password\-policy](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.5-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Requires at least one uppercase letter** and then choose **Apply password policy**\.

## 1\.6 – Ensure IAM password policy requires at least one lowercase letter<a name="securityhub-standards-checks-1.6"></a>

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\. We recommend that the password policy require at least one lowercase letter\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

To run this check, Security Hub uses the [iam\-password\-policy](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.6-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Requires at least one lowercase letter** and then choose **Apply password policy**\.

## 1\.7 – Ensure IAM password policy requires at least one symbol<a name="securityhub-standards-checks-1.7"></a>

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\. We recommend that the password policy require at least one symbol\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

To run this check, Security Hub uses the [iam\-password\-policy](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.7-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Require at least one non\-alphanumeric character** and then choose **Apply password policy**\.

## 1\.8 – Ensure IAM password policy requires at least one number<a name="securityhub-standards-checks-1.8"></a>

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\. We recommend that the password policy require at least one number\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

To run this check, Security Hub uses the [iam\-password\-policy](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.8-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Requires at least one number** and then choose **Apply password policy**\.

## 1\.9 – Ensure IAM password policy requires a minimum length of 14 or greater<a name="securityhub-standards-checks-1.9"></a>

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords are at least a given length\. We recommend that the password policy require a minimum password length of 14 characters\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

To run this check, Security Hub uses the [iam\-password\-policy](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.9-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. In the **Minimum password length** field, enter **14**, then choose **Apply password policy**\.

## 1\.10 – Ensure IAM password policy prevents password reuse<a name="securityhub-standards-checks-1.10"></a>

IAM password policies can prevent the reuse of a given password by the same user\. We recommend that the password policy prevent the reuse of passwords\. Preventing password reuse increases account resiliency against brute force login attempts\.

To run this check, Security Hub uses the [iam\-password\-policy](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.10-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Prevent password reuse** and then enter **24** for **Number of passwords to remember**\.

1. Choose **Apply password policy**\.

## 1\.11 – Ensure IAM password policy expires passwords within 90 days or less<a name="securityhub-standards-checks-1.11"></a>

IAM password policies can require passwords to be rotated or expired after a given number of days\. We recommend that the password policy expire passwords after 90 days or less\. Reducing the password lifetime increases account resiliency against brute force login attempts\. Additionally, requiring regular password changes helps in the following scenarios:
+ Passwords can be stolen or compromised without your knowledge\. This can happen via a system compromise, software vulnerability, or internal threat\.
+ Certain corporate and government web filters or proxy servers can intercept and record traffic even if it's encrypted\.
+ Many people use the same password for many systems such as work, email, and personal\.
+ Compromised end\-user workstations might have a keystroke logger\.

To run this check, Security Hub uses the [iam\-password\-policy](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.11-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Enable password expiration** and then enter **90** for **Password expiration period \(in days\)**\.

1. Choose **Apply password policy**\.

## 1\.12 – Ensure no root account access key exists<a name="securityhub-standards-checks-1.12"></a>

The root account is the most privileged user in an AWS account\. AWS Access Keys provide programmatic access to a given account\. We recommend that all access keys be associated with the root account be removed\. Removing access keys associated with the root account limits vectors that the account can be compromised by\. Additionally, removing the root access keys encourages the creation and use of role\-based accounts that are least privileged\.

To run this check, Security Hub uses the [iam\-root\-access\-key\-check](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.12-remediation"></a>

**To deactivate or delete access keys**

1. Log in to your account using the root credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Access keys \(access key ID and secret access key\)**\.

1. For any existing keys, do one of the following:
   + Choose **Make Inactive** to prevent the key from being used to authenticate the account\.
   + Choose **Delete** and then choose **Yes** to permanently delete the key\. You can't recover deleted keys\.

## 1\.13 – Ensure MFA is enabled for the "root" account<a name="securityhub-standards-checks-1.13"></a>

The root account is the most privileged user in an account\. MFA adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they're prompted for their user name and password and for an authentication code from their AWS MFA device\. When you use virtual MFA for root accounts, we recommend that the device used is *not* a personal device\. Instead, use a dedicated mobile device \(tablet or phone\) that you manage to keep charged and secured independent of any individual personal devices\. This lessens the risks of losing access to the MFA due to device loss, device trade\-in, or if the individual owning the device is no longer employed at the company\.

To run this check, Security Hub uses the [root\-account\-mfa\-enabled](https://docs.aws.amazon.com/config/latest/developerguide/root-account-mfa-enabled.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.13-remediation"></a>

**To enable MFA for the root account**

1. Log in to your account using the root credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Multi\-factor authentication \(MFA\)**\.

1. Choose **Activate MFA**\.

1. Choose the type of device to use for MFA and then choose **Continue**\.

1. Complete the steps to configure the device type appropriate to your selection\.

   Choose a hardware\-based authentication mechanism for best results in passing the check [1\.14 – Ensure hardware MFA is enabled for the "root" account ](#securityhub-standards-checks-1.14)\.

## 1\.14 – Ensure hardware MFA is enabled for the "root" account<a name="securityhub-standards-checks-1.14"></a>

The root account is the most privileged user in an account\. MFA adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they're prompted for their user name and password and for an authentication code from their AWS MFA device\. For Level 2, we recommend that you protect the root account with a hardware MFA\. A hardware MFA has a smaller attack surface than a virtual MFA\. For example, a hardware MFA doesn't suffer the attack surface introduced by the mobile smartphone that a virtual MFA resides on\.

**Note**  
Using hardware MFA for many, many accounts might create a logistical device management issue\. If this is the case, consider implementing this Level 2 recommendation selectively to the highest security accounts and the Level 1 recommendation applied to the remaining accounts\.

To run this check, Security Hub uses the [root\-account\-hardware\-mfa\-enabled](https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.14-remediation"></a>

**To enable hardware\-based MFA for the root account**

1. Log in to your account using the root credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Multi\-factor authentication \(MFA\)**\.

1. Choose **Activate MFA**\.

1. Choose a hardware\-based \(not virtual\) device to use for MFA and then choose **Continue**\.

1. Complete the steps to configure the device type appropriate to your selection\.

## 1\.16 – Ensure IAM policies are attached only to groups or roles<a name="securityhub-standards-checks-1.16"></a>

By default, IAM users, groups, and roles have no access to AWS resources\. IAM policies are how privileges are granted to users, groups, or roles\. We recommend that you apply IAM policies directly to groups and roles but not users\. Assigning privileges at the group or role level reduces the complexity of access management as the number of users grow\. Reducing access management complexity might in turn reduce opportunity for a principal to inadvertently receive or retain excessive privileges\.

To run this check, Security Hub uses the [iam\-user\-no\-policies\-check](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.16-remediation"></a>

To resolve this issue, create an IAM group, assign the policy to the group, and then add the users to the group\. The policy is applied to each user in the group\.

**To create an IAM group**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Groups** and then choose **Create New Group**\.

1. Enter a name for the group to create and then choose **Next Step**\.

1. Select each policy to assign to the group and then choose **Next Step**\.

   The policies that you choose should include any policies currently attached directly to a user account\. The next step to resolve a failed check is to add users to a group and then assign the policies to that group\. Each user in the group gets assigned the policies assigned to the group\.

1. Confirm the details on the **Review** page and then choose **Create Group**\.

For more information about creating groups, see [Creating IAM Groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_create.html) in the *IAM User Guide*\.

**To add users to an IAM group**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Groups**\.

1. Choose **Group Actions** and then choose **Add Users to Group**\.

1. Select the users to add to the group and then choose **Add Users**\.

For more information about adding users to groups, see [Adding and Removing Users in an IAM Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_manage_add-remove-users.html)\.

**To remove a policy attached directly to a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. For the user to detach a policy from, choose the name in the **User name** column\.

1. For each policy listed under **Attached directly**, choose the **X** on the right side of the page to remove the policy from the user and then choose **Remove**\.

1. Confirm that the user can still use AWS services as expected\.

## 1\.22 – Ensure IAM policies that allow full "\*:\*" administrative privileges are not created<a name="securityhub-standards-checks-1.22"></a>

IAM policies define a set of privileges granted to users, groups, or roles\. It's recommended and considered a standard security advice to grant least privilege—that is, granting only the permissions required to perform a task\. Determine what users need to do and then craft policies that let the users perform only those tasks, instead of allowing full administrative privileges\.

It's more secure to start with a minimum set of permissions and grant additional permissions as necessary, rather than starting with permissions that are too lenient and then trying to tighten them later\. Providing full administrative privileges instead of restricting to the minimum set of permissions that the user is required to do exposes the resources to potentially unwanted actions\.

You should remove IAM policies that have a statement with "Effect": "Allow" with "Action": "\*" over "Resource": "\*"\.

To run this check, Security Hub uses the [iam\-policy\-no\-statements\-with\-admin\-access](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="1.22-remediation"></a>

**To modify an IAM policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Policies**\.

1. Select the radio button next to the policy to remove\.

1. From the **Policy actions** drop\-down menu, choose **Detach**\.

1. On the **Detach policy** page, select the radio button next to each user to detach the policy from and then choose **Detach policy**\.

Confirm that the user that you detached the policy from can still access AWS services and resources as expected\.

## 2\.1 – Ensure CloudTrail is enabled in all Regions<a name="securityhub-standards-checks-2.1"></a>

CloudTrail is a service that records AWS API calls for your account and delivers log files to you\. The recorded information includes the identity of the API caller, the time of the API call, the source IP address of the API caller, the request parameters, and the response elements returned by the AWS service\. CloudTrail provides a history of AWS API calls for an account, including API calls made via the AWS Management Console, AWS SDKs, command\-line tools, and higher\-level AWS services \(such as AWS CloudFormation\)\.

The AWS API call history produced by CloudTrail enables security analysis, resource change tracking, and compliance auditing\. Additionally:
+ Ensuring that a multi\-Region trail exists ensures that unexpected activity occurring in otherwise unused Regions is detected
+ Ensuring that a multi\-Region trail exists ensures that Global Service Logging is enabled for a trail by default to capture recording of events generated on AWS global services
+ For a multi\-Region trail, ensuring that management events configured for all type of Read/Writes ensures recording of management operations that are performed on all resources in an AWS account

To run this check, Security Hub uses the [multi\-region\-cloud\-trail\-enabled](https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloud-trail-enabled.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="2.1-remediation"></a>

**To create a new trail in CloudTrail**

1. Sign in to the AWS Management Console and open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. If you haven't used CloudTrail before, choose **Get Started Now**\.

1. Choose **Trails** and then choose **Create trail**\.

1. Enter a name for the trail\.

1. For **Apply trail to all regions**, choose **Yes**\.

1. Under **Storage location**, do one of the following:
   + To create a new S3 bucket for CloudTrail logs, choose **Yes** next to **Create a new S3 bucket** and then enter a name for the bucket\.
   + Choose **No** next to **Create a new S3 bucket** and then select the bucket to use\.

1. Choose **Advanced** and, for **Enable log file validation**, choose **Yes** to pass [2\.2\. – Ensure CloudTrail log file validation is enabled ](#securityhub-standards-checks-2.2) \.

1. Choose **Create**\.

**To update an existing trail in CloudTrail**

1. Sign in to the AWS Management Console and open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the name of the trail in the **Name** column\.

1. Choose the pencil icon for the **Trail settings**\.

1. For **Apply trail to all regions**, choose **Yes** and then choose **Save**\.

1. Choose the pencil icon for the **Management events**\.

1. Select **All** for **Read/Write events**, then choose **Save**\.

1. Choose the pencil icon for the **Storage location**\.

1. Choose **Yes** for **Enable log file validation** to pass check 2\.2, then choose **Save**\.

## 2\.2\. – Ensure CloudTrail log file validation is enabled<a name="securityhub-standards-checks-2.2"></a>

CloudTrail log file validation creates a digitally signed digest file containing a hash of each log that CloudTrail writes to S3\. You can use these digest files to determine whether a log file was changed, deleted, or unchanged after CloudTrail delivered the log\. We recommend that you enable file validation on all trails\. Enabling log file validation provides additional integrity checking of CloudTrail logs\.

To run this check, Security Hub uses the [cloud\-trail\-log\-file\-validation\-enabled](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="2.2-remediation"></a>

**To enable CloudTrail log file validation**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the name of a trail to edit in the **Name** column\.

1. Choose the pencil icon for the **Storage location**\.

1. For **Enable log file validation**, choose **Yes** and then choose **Save**\.

## 2\.3 – Ensure the S3 bucket CloudTrail logs to is not publicly accessible<a name="securityhub-standards-checks-2.3"></a>

CloudTrail logs a record of every API call made in your account\. These log files are stored in an S3 bucket\. We recommend that the bucket policy, or access control list \(ACL\), applied to the S3 bucket that CloudTrail logs to prevents public access to the CloudTrail logs\. Allowing public access to CloudTrail log content might aid an adversary in identifying weaknesses in the affected account's use or configuration\.

**Important**  
Cross\-Region processing isn't supported for the CIS AWS Foundations standard in Security Hub\. In other words, if you enable this standard in Security Hub in one Region and a resource that it checks is located in another Region, the return value for such check is Failed\. For example, if you're storing your CloudTrail logs in an S3 bucket in the us\-east\-2 Region and the CIS AWS Foundations standard is running in Security Hub enabled in us\-west\-2, this check returns as Failed\.

To run this check, Security Hub uses the [s3\-bucket\-public\-read\-prohibited](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited.html) and [s3\-bucket\-public\-write\-prohibited](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html) AWS Config managed rules\. After the CIS AWS Foundations standard is enabled, an instance of each of these rules, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="2.3-remediation"></a>

**To remove public access for an Amazon S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the name of the bucket where your CloudTrail are stored\.

1. Choose **Permissions** and then choose **Public access settings**\.

1. Choose **Edit**, select all four options, and then choose **Save**\.

1. If prompted, enter **confirm** and then choose **Confirm**\.

## 2\.4 – Ensure CloudTrail trails are integrated with Amazon CloudWatch Logs<a name="securityhub-standards-checks-2.4"></a>

CloudTrail is a web service that records AWS API calls made in a given account\. The recorded information includes the identity of the API caller, the time of the API call, the source IP address of the API caller, the request parameters, and the response elements returned by the AWS service\. CloudTrail uses Amazon S3 for log file storage and delivery, so log files are stored durably\. In addition to capturing CloudTrail logs in a specified Amazon S3 bucket for long\-term analysis, you can perform real\-time analysis by configuring CloudTrail to send logs to CloudWatch Logs\. For a trail that is enabled in all Regions in an account, CloudTrail sends log files from all those Regions to a CloudWatch Logs log group\. We recommend that you send CloudTrail logs to CloudWatch Logs\.

**Note**  
 The intent of this recommendation is to ensure that account activity is being captured, monitored, and appropriately alarmed on\. CloudWatch Logs is a native way to accomplish this using AWS services but doesn't preclude the use of an alternate solution\.

Sending CloudTrail logs to CloudWatch Logs facilitates real\-time and historic activity logging based on user, API, resource, and IP address\. It provides the opportunity to establish alarms and notifications for anomalous or sensitivity account activity\.

To run this check, Security Hub uses the [cloud\-trail\-cloud\-watch\-logs\-enabled](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-cloud-watch-logs-enabled.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="2.4-remediation"></a>

**To ensure that CloudTrail trails are integrated with CloudWatch Logs**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose a trail that there is no value for in the **CloudWatch Logs Log group** column\.

1. Scroll down to the **CloudWatch Logs** section and then choose **Configure**\.

1. In the **New or existing log group** field, do one of the following:
   + To use the default log group, keep the name as is\.
   + To use an existing log group, enter the name of the log group to use\.
   + To create a new log group, enter a name for the log group to create\.

1. Choose **Continue**\.

1. Do one of the following:
   + To use the default IAM role, go to the next step\.
   + To specify the role to use, choose **View Details**\.

     1. For **IAM role**, do one of the following:
       + Choose the **CloudTrail\_CloudWatchLogs\_role** and then select the policy to use in the **Policy Name** drop\-down list\.
       + Choose **Create a new IAM Role** and then enter a name for the role to create\.

         A role is created and assigned a policy that grants the necessary permissions\.

1. Choose **Allow**\.

For more information, see [Configuring CloudWatch Logs Monitoring with the Console](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/send-cloudtrail-events-to-cloudwatch-logs.html#send-cloudtrail-events-to-cloudwatch-logs-console) in the *AWS CloudTrail User Guide*\.

## 2\.5 – Ensure AWS Config is enabled in all Regions<a name="securityhub-standards-checks-2.5"></a>

AWS Config is a web service that performs configuration management of supported AWS resources in your account and delivers log files to you\. The recorded information includes the configuration item \(AWS resource\), relationships between configuration items \(AWS resources\), and any configuration changes between resources\. We recommend that you enable AWS Config in all Regions\. The AWS configuration item history that AWS Config captures enables security analysis, resource change tracking, and compliance auditing\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="2.5-remediation"></a>

**To configure AWS Config settings**

1. Open the AWS Config console at [https://console\.aws\.amazon\.com/config/](https://console.aws.amazon.com/config/)\.

1. Select the Region to configure AWS Config in\.

1. If you haven't used AWS Config before, choose **Get started**\.

1. On the Settings page, do the following:
   + Under **Resource types to record**, select **Record all resources supported in this region** and **Include global resources \(e\.g\., AWS IAM resources\)**\.
   + Under **Amazon S3 bucket**, specify the bucket to use or create a bucket and optionally include a prefix\.
   + Under **Amazon SNS topic**, select an Amazon SNS topic from your account or create one\. For more information about Amazon SNS, see the [Amazon Simple Notification Service Getting Started Guide](https://docs.aws.amazon.com/sns/latest/gsg/)\.
   + Under **AWS Config role**, either choose **Create AWS Config service\-linked role** or choose **Choose a role from your account** and then select the role to use\.

1. Choose **Next**\.

1. On the **AWS Config** rules page, choose **Skip**\.

1. Choose **Confirm**\.

For more information about using AWS Config from the AWS Command Line Interface, see [Turning on AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/gs-cli-subscribe.html) in the *AWS Config Developer Guide*\.

You can also use an AWS CloudFormation template to automate this process\. For more information, see the [AWS CloudFormation StackSets Sample Template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html) in the *AWS CloudFormation User Guide*\.

## 2\.6 – Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket<a name="securityhub-standards-checks-2.6"></a>

Amazon S3 bucket access logging generates a log that contains access records for each request made to your S3 bucket\. An access log record contains details about the request, such as the request type, the resources specified in the request worked, and the time and date the request was processed\. We recommend that you enable bucket access logging on the CloudTrail S3 bucket\.

 By enabling S3 bucket logging on target S3 buckets, you can capture all events that might affect objects in a target bucket\. Configuring logs to be placed in a separate bucket enables access to log information, which can be useful in security and incident response workflows\.

**Important**  
Cross\-Region processing isn't supported for the CIS AWS Foundations standard in Security Hub\. In other words, if you enable this standard in Security Hub in one Region and a resource that it checks is located in another Region, the return value for such check is Failed\. For example, if you're storing your CloudTrail logs in an S3 bucket in the us\-east\-2 Region and the CIS AWS Foundations standard is running in Security Hub enabled in us\-west\-2, this check returns as Failed\.

To run this check, Security Hub uses the [s3\-bucket\-logging\-enabled](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-logging-enabled.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="2.6-remediation"></a>

**To enable S3 bucket access logging**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the bucket used for CloudTrail\.

1. Choose **Properties**\.

1. Choose **Server access logging**, then choose **Enable logging**\.

1. Select a bucket from the **Target bucket** list, and optionally enter a prefix\.

1. Choose **Save**\.

## 2\.7 – Ensure CloudTrail logs are encrypted at rest using AWS KMS CMKs<a name="securityhub-standards-checks-2.7"></a>

CloudTrail is a web service that records AWS API calls for an account and makes those logs available to users and resources in accordance with IAM policies\. AWS Key Management Service \(AWS KMS\) is a managed service that helps create and control the encryption keys used to encrypt account data, and uses hardware security modules \(HSMs\) to protect the security of encryption keys\. You can configure CloudTrail logs to leverage server\-side encryption \(SSE\) and AWS KMS customer\-created master keys \(CMKs\) to further protect CloudTrail logs\. We recommend that you configure CloudTrail to use SSE\-KMS\.

Configuring CloudTrail to use SSE\-KMS provides additional confidentiality controls on log data because a given user must have S3 read permission on the corresponding log bucket and must be granted decrypt permission by the CMK policy\.

To run this check, Security Hub uses the [cloud\-trail\-encryption\-enabled](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="2.7-remediation"></a>

**To enable encryption for CloudTrail logs**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the trail to update\.

1. Under **Storage location**, choose the pencil icon to edit the settings\.

1. For **Encrypt log files with SSE\-KMS**, choose **Yes**\.

1. For **Create a new KMS key**, do one of the following:
   + To create a key, choose **Yes** and then enter an alias for the key in the **KMS key** field\. The key is created in the same Region as the bucket\.
   + To use an existing key, choose **No** and then select the key from the **KMS key** list\.
**Note**  
The AWS KMS key and S3 bucket must be in the same Region\.

1. Choose **Save**\.

You might need to modify the policy for CloudTrail to successfully interact with your CMK\. For more information, see [Encrypting CloudTrail Log Files with AWS KMS–Managed Keys \(SSE\-KMS\)](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html?icmpid=docs_cloudtrail_console) in the *AWS CloudTrail User Guide*\.

## 2\.8 – Ensure rotation for customer created CMKs is enabled<a name="securityhub-standards-checks-2.8"></a>

AWS KMS enables customers to rotate the backing key, which is key material stored in AWS KMS and is tied to the key ID of the CMK\. It's the backing key that is used to perform cryptographic operations such as encryption and decryption\. Automated key rotation currently retains all previous backing keys so that decryption of encrypted data can take place transparently\. We recommend that you enable CMK key rotation\. Rotating encryption keys helps reduce the potential impact of a compromised key because data encrypted with a new key can't be accessed with a previous key that might have been exposed\.

To run this check, Security Hub uses the [cmk\-backing\-key\-rotation\-enabled](https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="2.8-remediation"></a>

**To enable CMK rotation**

1. Open the AWS KMS console at [https://console\.aws\.amazon\.com/kms](https://console.aws.amazon.com/kms)\.

1. To change the AWS Region, use the Region selector in the upper\-right corner of the page\.

1. Choose **Customer managed keys**\.

1. Choose the alias of the key to update in the **Alias** column\.

1. Choose **Key rotation**\.

1. Select **Automatically rotate this CMK every year** and then choose **Save**\.

## 2\.9 – Ensure VPC flow logging is enabled in all VPCs<a name="securityhub-standards-checks-2.9"></a>

VPC flow logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC\. After you have created a flow log, you can view and retrieve its data in CloudWatch Logs\. We recommend that you enable flow logging for packet rejects for VPCs\. Flow logs provide visibility into network traffic that traverses the VPC and can detect anomalous traffic or insight during security workflows\. 

To run this check, Security Hub uses the [vpc\-flow\-logs\-enabled](https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="2.9-remediation"></a>

**To enable VPC flow logging**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Choose **Your VPCs**\.

1. Select a VPC to update\.

1. Choose the **Flow Logs** tab in the bottom section of the page\.

1. Choose **Create flow log**\.

1. For **Filter**, choose **Reject**\.

1. For **Destination log group**, select the log group to use\.

1. For **IAM role**, select the IAM role to use\.

1. Choose **Create**\.

## 3\.1 – Ensure a log metric filter and alarm exist for unauthorized API calls<a name="securityhub-standards-checks-3.1"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. We recommend that you create a metric filter and alarm unauthorized API calls\. Monitoring unauthorized API calls helps reveal application errors and might reduce time to detect malicious activity\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.1-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.errorCode="*UnauthorizedOperation") || ($.errorCode="AccessDenied*")}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.1\-UnauthorizedAPICalls**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.2 – Ensure a log metric filter and alarm exist for AWS Management Console sign\-in without MFA<a name="securityhub-standards-checks-3.2"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. We recommend that you create a metric filter and alarm console logins that aren't protected by MFA\. Monitoring for single\-factor console logins increases visibility into accounts that aren't protected by MFA\. 

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.2-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventName="ConsoleLogin") && ($.additionalEventData.MFAUsed !="Yes")}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.2\-ConsoleSigninWithoutMFA**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.3 – Ensure a log metric filter and alarm exist for usage of "root" account<a name="securityhub-standards-checks-3.3"></a>

You can do real\-time monitoring of API calls directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. We recommend that you create a metric filter and alarm root login attempts\. Monitoring for root account logins provides visibility into the use of a fully privileged account and an opportunity to reduce the use of it\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.3-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {$.userIdentity.type="Root" && $.userIdentity.invokedBy NOT EXISTS && $.eventType !="AwsServiceEvent"}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.3\-RootAccountUsage**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.4 – Ensure a log metric filter and alarm exist for IAM policy changes<a name="securityhub-standards-checks-3.4"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. We recommend that you create a metric filter and alarm for changes made to IAM policies\. Monitoring these changes helps ensure that authentication and authorization controls remain intact\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.4-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventName=DeleteGroupPolicy) || ($.eventName=DeleteRolePolicy) || ($.eventName=DeleteUserPolicy) || ($.eventName=PutGroupPolicy) || ($.eventName=PutRolePolicy) || ($.eventName=PutUserPolicy) || ($.eventName=CreatePolicy) || ($.eventName=DeletePolicy) || ($.eventName=CreatePolicyVersion) || ($.eventName=DeletePolicyVersion) || ($.eventName=AttachRolePolicy) || ($.eventName=DetachRolePolicy) || ($.eventName=AttachUserPolicy) || ($.eventName=DetachUserPolicy) || ($.eventName=AttachGroupPolicy) || ($.eventName=DetachGroupPolicy)}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.4\-IAMPolicyChanges**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.5 – Ensure a log metric filter and alarm exist for CloudTrail configuration changes<a name="securityhub-standards-checks-3.5"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. We recommend that you create a metric filter and alarm for changes to CloudTrail configuration settings\. Monitoring these changes helps ensure sustained visibility to activities in the account\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.5-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventName=CreateTrail) || ($.eventName=UpdateTrail) || ($.eventName=DeleteTrail) || ($.eventName=StartLogging) || ($.eventName=StopLogging)}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.5\-CloudTrailChanges**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.6 – Ensure a log metric filter and alarm exist for AWS Management Console authentication failures<a name="securityhub-standards-checks-3.6"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. We recommend that you create a metric filter and alarm for failed console authentication attempts\. Monitoring failed console logins might decrease lead time to detect an attempt to brute\-force a credential, which might provide an indicator, such as source IP, that you can use in other event correlations\. 

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.6-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventName=ConsoleLogin) && ($.errorMessage="Failed authentication")}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.6\-ConsoleAuthenticationFailure**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.7 – Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs<a name="securityhub-standards-checks-3.7"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. We recommend that you create a metric filter and alarm for customer\-created CMKs that have changed state to disabled or scheduled deletion\. Data encrypted with disabled or deleted keys is no longer accessible\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.7-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventSource=kms.amazonaws.com) && (($.eventName=DisableKey) || ($.eventName=ScheduleKeyDeletion))}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.7\-DisableOrDeleteCMK**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.8 – Ensure a log metric filter and alarm exist for S3 bucket policy changes<a name="securityhub-standards-checks-3.8"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. We recommend that you create a metric filter and alarm for changes to S3 bucket policies\. Monitoring these changes might reduce time to detect and correct permissive policies on sensitive S3 buckets\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.8-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventSource=s3.amazonaws.com) && (($.eventName=PutBucketAcl) || ($.eventName=PutBucketPolicy) || ($.eventName=PutBucketCors) || ($.eventName=PutBucketLifecycle) || ($.eventName=PutBucketReplication) || ($.eventName=DeleteBucketPolicy) || ($.eventName=DeleteBucketCors) || ($.eventName=DeleteBucketLifecycle) || ($.eventName=DeleteBucketReplication))}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.8\-S3BucketPolicyChanges**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.9 – Ensure a log metric filter and alarm exist for AWS Config configuration changes<a name="securityhub-standards-checks-3.9"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. We recommend that you create a metric filter and alarm for changes to AWS Config configuration settings\. Monitoring these changes helps ensure sustained visibility of configuration items in the account\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.9-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventSource=config.amazonaws.com) && (($.eventName=StopConfigurationRecorder) || ($.eventName=DeleteDeliveryChannel) || ($.eventName=PutDeliveryChannel) || ($.eventName=PutConfigurationRecorder))}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.9\-AWSConfigChanges**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.10 – Ensure a log metric filter and alarm exist for security group changes<a name="securityhub-standards-checks-3.10"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Security groups are a stateful packet filter that controls ingress and egress traffic in a VPC\. We recommend that you create a metric filter and alarm for changes to security groups\. Monitoring these changes helps ensure that resources and services aren't unintentionally exposed\. 

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.10-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventName=AuthorizeSecurityGroupIngress) || ($.eventName=AuthorizeSecurityGroupEgress) || ($.eventName=RevokeSecurityGroupIngress) || ($.eventName=RevokeSecurityGroupEgress) || ($.eventName=CreateSecurityGroup) || ($.eventName=DeleteSecurityGroup)}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.10\-SecurityGroupChanges**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.11 – Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)<a name="securityhub-standards-checks-3.11"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. NACLs are used as a stateless packet filter to control ingress and egress traffic for subnets in a VPC\. We recommend that you create a metric filter and alarm for changes to NACLs\. Monitoring these changes helps ensure that AWS resources and services aren't unintentionally exposed\. 

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.11-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventName=CreateNetworkAcl) || ($.eventName=CreateNetworkAclEntry) || ($.eventName=DeleteNetworkAcl) || ($.eventName=DeleteNetworkAclEntry) || ($.eventName=ReplaceNetworkAclEntry) || ($.eventName=ReplaceNetworkAclAssociation)}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.11\-NetworkACLChanges**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.12 – Ensure a log metric filter and alarm exist for changes to network gateways<a name="securityhub-standards-checks-3.12"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Network gateways are required to send and receive traffic to a destination outside a VPC\. We recommend that you create a metric filter and alarm for changes to network gateways\. Monitoring these changes helps ensure that all ingress and egress traffic traverses the VPC border via a controlled path\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.12-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventName=CreateCustomerGateway) || ($.eventName=DeleteCustomerGateway) || ($.eventName=AttachInternetGateway) || ($.eventName=CreateInternetGateway) || ($.eventName=DeleteInternetGateway) || ($.eventName=DetachInternetGateway)}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.12\-NetworkGatewayChanges**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.13 – Ensure a log metric filter and alarm exist for route table changes<a name="securityhub-standards-checks-3.13"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Routing tables route network traffic between subnets and to network gateways\. We recommend that you create a metric filter and alarm for changes to route tables\. Monitoring these changes helps ensure that all VPC traffic flows through an expected path\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.13-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventName=CreateRoute) || ($.eventName=CreateRouteTable) || ($.eventName=ReplaceRoute) || ($.eventName=ReplaceRouteTableAssociation) || ($.eventName=DeleteRouteTable) || ($.eventName=DeleteRoute) || ($.eventName=DisassociateRouteTable)}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.13\-RouteTableChanges**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 3\.14 – Ensure a log metric filter and alarm exist for VPC changes<a name="securityhub-standards-checks-3.14"></a>

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. You can have more than one VPC in an account, and you can create a peer connection between two VPCs, enabling network traffic to route between VPCs\. We recommend that you create a metric filter and alarm for changes to VPCs\. Monitoring these changes helps ensure that authentication and authorization controls remain intact\.

To run this check, Security Hub runs through the exact audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

### Remediation<a name="3.14-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**Create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-standards-checks-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\.

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\.

1. Choose **Add Metric Filter**\.

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {($.eventName=CreateVpc) || ($.eventName=DeleteVpc) || ($.eventName=ModifyVpcAttribute) || ($.eventName=AcceptVpcPeeringConnection) || ($.eventName=CreateVpcPeeringConnection) || ($.eventName=DeleteVpcPeeringConnection) || ($.eventName=RejectVpcPeeringConnection) || ($.eventName=AttachClassicLinkVpc) || ($.eventName=DetachClassicLinkVpc) || ($.eventName=DisableVpcClassicLink) || ($.eventName=EnableVpcClassicLink)}
   ```

1. Choose **Assign Metric**\.

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is **LogMetrics**\.

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\.

   The filter is created, and its details appear\.

1. Choose **Create Alarm**\.

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-3\.14\-VPCChanges**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 4\.1 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 22<a name="securityhub-standards-checks-4.1"></a>

Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\. We recommend that no security group allow unrestricted ingress access to port 22\. Removing unfettered connectivity to remote console services, such as SSH, reduces a server's exposure to risk\.

To run this check, Security Hub uses the [restricted\-ssh](https://docs.aws.amazon.com/config/latest/developerguide/restricted-ssh.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\. 

### Remediation<a name="4.1-remediation"></a>

Perform the following steps for each security group associated with a VPC\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the left pane, choose **Security groups**\.

1. Select a security group\.

1. In the bottom section of the page, choose the **Inbound Rules** tab\.

1. Choose **Edit rules**\.

1. Identify the rule that allows access through port 22 and then choose the **X** to remove it\.

1. Choose **Save rules**\.

## 4\.2 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389<a name="securityhub-standards-checks-4.2"></a>

Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\. We recommend that no security group allow unrestricted ingress access to port 3389\. Removing unfettered connectivity to remote console services, such as RDP, reduces a server's exposure to risk\.

To run this check, Security Hub uses the [restricted\-common\-ports](https://docs.aws.amazon.com/config/latest/developerguide/restricted-common-ports.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="4.2-remediation"></a>

Perform the following steps for each security group associated with a VPC\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the left pane, choose **Security groups**\.

1. Select a security group\.

1. In the bottom section of the page, choose the **Inbound Rules** tab\.

1. Choose **Edit rules**\.

1. Identify the rule that allows access through port 3389 and then choose the **X** to remove it\.

1. Choose **Save rules**\.

## 4\.3 – Ensure the default security group of every VPC restricts all traffic<a name="securityhub-standards-checks-4.3"></a>

A VPC comes with a default security group with initial settings that deny all inbound traffic, allow all outbound traffic, and allow all traffic between instances assigned to the security group\. If you don't specify a security group when you launch an instance, the instance is automatically assigned to this default security group\. Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\. We recommend that the default security group restrict all traffic\.

Update the default security group for the default VPC in every Region to comply\. Any new VPCs automatically contain a default security group that you need to remediate to comply with this recommendation\.

**Note**  
When implementing this recommendation, you can use VPC flow logging, enabled for check 2\.9, to determine the least\-privilege port access required by systems to work properly because it can log all packet acceptances and rejections occurring under the current security groups\.

Configuring all VPC default security groups to restrict all traffic encourages least\-privilege security group development and mindful placement of AWS resources into security groups, which in turn reduces the exposure of those resources\.

To run this check, Security Hub uses the [vpc\-default\-security\-group\-closed](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html) AWS Config managed rule\. After the CIS AWS Foundations standard is enabled, an instance of this rule, specific to Security Hub, is created in your AWS environment\.

### Remediation<a name="4.3-remediation"></a>

**To update the default security group to restrict all access**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. View the default security groups details to see the resources that are assigned to them\.

1. Create a set of least\-privilege security groups for the resources\.

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the Amazon EC2 console, change the security group for the resources that use the default security groups to the least\-privilege security group you created\.

1. For each default security group, choose the **Inbound** tab and delete all inbound rules\.

1. For each default security group, choose the **Outbound** tab and delete all outbound rules\.

For more information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the *Amazon VPC User Guide*\.

## CIS AWS Foundations Standard Checks That Aren't Supported in Security Hub<a name="securityhub-standards-checks-not-supported"></a>

The following are the compliance rules that are *not* supported in the CIS AWS Foundations standard in Security Hub:
+ 1\.15 – Ensure security questions are registered in the AWS account 
+ 1\.17 – Maintain current contact details 
+ 1\.18 – Ensure security contact information is registered 
+ 1\.19 – Ensure IAM instance roles are used for AWS resource access from instances
+ 1\.20 – Ensure a support role has been created to manage incidents with AWS Support
+ 1\.21 – Do not set up access keys during initial user setup for all IAM users that have a console password
+ 4\.4 – Ensure routing tables for VPC peering are "least access"
