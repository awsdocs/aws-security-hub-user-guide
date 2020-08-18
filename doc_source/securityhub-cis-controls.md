# CIS AWS Foundations Benchmark controls<a name="securityhub-cis-controls"></a>

For the CIS AWS Foundations standard, Security Hub supports the following controls\. For each control, the information includes the required AWS Config rule and the remediation steps\.

## 1\.1 – Avoid the use of the "root" account<a name="securityhub-standards-cis-controls-1.1"></a>

**Severity:** Critical

**AWS Config** rule: None

The root account has unrestricted access to all resources in the AWS account\. We highly recommend that you avoid using this account\. The root account is the most privileged account\. Minimizing the use of this account and adopting the principle of least privilege for access management reduces the risk of accidental changes and unintended disclosure of highly privileged credentials\.

As a best practice, use your root credentials only when required to [ perform account and service management tasks](https://docs.aws.amazon.com/general/latest/gr/aws_tasks-that-require-root.html)\. Apply IAM policies directly to groups and roles but not users\. For a tutorial on how to set up an administrator for daily use, see [ Creating your first IAM admin user and group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.3 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

### Remediation<a name="cis-1.1-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\. These are the same steps to remediate findings for [3\.3 – Ensure a log metric filter and alarm exist for usage of "root" account ](#securityhub-cis-controls-3.3)\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-1\.1\-RootAccountUsage**\.

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\.

## 1\.2 – Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password<a name="securityhub-cis-controls-1.2"></a>

**Severity:** Medium

**AWS Config rule: **[https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html](https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html)

Multi\-factor authentication \(MFA\) adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they're prompted for their user name and password as well as for an authentication code from their AWS MFA device\.

Security Hub recommends enabling MFA for all accounts that have a console password\. Enabling MFA provides increased security for console access because it requires the authenticating principal to possess a device that emits a time\-sensitive key and have knowledge of a credential\.

**Important**  
The AWS Config rule used for this check may take up to 4 hours to accurately report results for MFA\. Any findings that are generated within the first 4 hours after enabling the CIS security checks may not be accurate\. It may also take up to 4 hours after remediating this issue for the check to pass\.

### Remediation<a name="cis-1.2-remediation"></a>

**To configure MFA for a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the **User name** of the user to configure MFA for\.

1. Choose **Security credentials** and then choose **Manage** next to **Assigned MFA device**\.

1. Follow the **Manage MFA Device** wizard to assign the type of device appropriate for your environment\.

To learn how to delegate MFA setup to users, see [How to Delegate Management of Multi\-Factor Authentication to AWS IAM Users](http://aws.amazon.com/blogs/security/how-to-delegate-management-of-multi-factor-authentication-to-aws-iam-users/) on the AWS Security Blog\.

## 1\.3 – Ensure credentials unused for 90 days or greater are disabled<a name="securityhub-cis-controls-1.3"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html)

IAM users can access AWS resources using different types of credentials, such as passwords or access keys\.

Security Hub recommends that you remove or deactivate all credentials that have been unused in 90 days or more\. Disabling or removing unnecessary credentials reduces the window of opportunity for credentials associated with a compromised or abandoned account to be used\. 

The AWS Config rule for this control uses the [https://docs.aws.amazon.com/IAM/latest/APIReference/API_GetCredentialReport.html](https://docs.aws.amazon.com/IAM/latest/APIReference/API_GetCredentialReport.html) and [https://docs.aws.amazon.com/IAM/latest/APIReference/API_GenerateCredentialReport.html](https://docs.aws.amazon.com/IAM/latest/APIReference/API_GenerateCredentialReport.html) API operations, which are only updated every four hours\. Changes to IAM users can take up to four hours to be visible to this control\.

### Remediation<a name="cis-1.3-remediation"></a>

To get some of the information that you need to monitor accounts for dated credentials, use the IAM console\. For example, when you view users in your account, there is a column for **Access key age**, **Password age**, and **Last activity**\. If the value in any of these columns is greater than 90 days, make the credentials for those users inactive\.

You can also use credential reports to monitor user accounts and identify those with no activity for 90 or more days\. You can download credential reports in \.csv format from the IAM console\. For more information about credential reports, see [ Getting credential reports for your AWS Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html#getting-credential-reports-console)\. 

After you identify the inactive accounts or unused credentials, use the following steps to disable them\.

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the name of the user with credentials over 90 days old\.

1. Choose **Security credentials** and then choose **Make inactive** for all sign\-in credentials and access keys that haven't been used in 90 days or more\.

## 1\.4 – Ensure access keys are rotated every 90 days or less<a name="securityhub-cis-controls-1.4"></a>

**Severity:** Medium

**AWS Config managed rule:** [https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html](https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html)

Access keys consist of an access key ID and secret access key, which are used to sign programmatic requests that you make to AWS\. AWS users need their own access keys to make programmatic calls to AWS from the AWS Command Line Interface \(AWS CLI\), Tools for Windows PowerShell, the AWS SDKs, or direct HTTP calls using the APIs for individual AWS services\.

Security Hub recommends that you regularly rotate all access keys\. Rotating access keys reduces the chance for an access key that is associated with a compromised or terminated account to be used\. Rotate access keys to ensure that data can't be accessed with an old key that might have been lost, cracked, or stolen\. 

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="cis-1.4-remediation"></a>

**To ensure that access keys aren't more than 90 days old**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. For each user that shows an **Access key age** that is greater than 90 days, choose the **User name** to open the settings for that user\.

1. Choose **Security credentials**\.

1. To create a new key for the user:

   1. Choose **Create access key**\.

   1. To save the key content, either download the secret access key, or choose **Show** and then copy it from the page\.

   1. Store the key in a secure location to provide to the user\.

   1. Choose **Close**\.

1. Update all applications that were using the previous key to use the new key\.

1. For the previous key, choose **Make inactive** to make the access key inactive\. Now the user can't make requests using that key\.

1. Confirm that all applications work as expected with the new key\.

1. After confirming that all applications work with the new key, delete the previous key\. After you delete the access key, you can't recover it\.

   To delete the previous key, choose the **X** at the end of the row and then choose **Delete**\.

## 1\.5 – Ensure IAM password policy requires at least one uppercase letter<a name="securityhub-cis-controls-1.5"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\.

Security Hub recommends that the password policy require at least one uppercase letter\. Setting a password complexity policy increases account resiliency against brute force login attempts\. 

### Remediation<a name="cis-1.5-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Requires at least one uppercase letter** and then choose **Apply password policy**\.

## 1\.6 – Ensure IAM password policy requires at least one lowercase letter<a name="securityhub-cis-controls-1.6"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\. Security Hub recommends that the password policy require at least one lowercase letter\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

### Remediation<a name="cis-1.6-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Requires at least one lowercase letter** and then choose **Apply password policy**\.

## 1\.7 – Ensure IAM password policy requires at least one symbol<a name="securityhub-cis-controls-1.7"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\.

Security Hub recommends that the password policy require at least one symbol\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

### Remediation<a name="cis-1.7-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Require at least one non\-alphanumeric character** and then choose **Apply password policy**\.

## 1\.8 – Ensure IAM password policy requires at least one number<a name="securityhub-cis-controls-1.8"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\.

Security Hub recommends that the password policy require at least one number\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

### Remediation<a name="cis-1.8-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Requires at least one number** and then choose **Apply password policy**\.

## 1\.9 – Ensure IAM password policy requires a minimum length of 14 or greater<a name="securityhub-cis-controls-1.9"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords are at least a given length\.

Security Hub recommends that the password policy require a minimum password length of 14 characters\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

### Remediation<a name="cis-1.9-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. In the **Minimum password length** field, enter **14**, then choose **Apply password policy**\.

## 1\.10 – Ensure IAM password policy prevents password reuse<a name="securityhub-cis-controls-1.10"></a>

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

This control checks whether the number of passwords to remember is set to 24\. The control fails if the value is not 24\.

IAM password policies can prevent the reuse of a given password by the same user\.

Security Hub recommends that the password policy prevent the reuse of passwords\. Preventing password reuse increases account resiliency against brute force login attempts\.

### Remediation<a name="cis-1.10-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Prevent password reuse** and then enter **24** for **Number of passwords to remember**\.

1. Choose **Apply password policy**\.

## 1\.11 – Ensure IAM password policy expires passwords within 90 days or less<a name="securityhub-cis-controls-1.11"></a>

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

IAM password policies can require passwords to be rotated or expired after a given number of days\.

Security Hub recommends that the password policy expire passwords after 90 days or less\. Reducing the password lifetime increases account resiliency against brute force login attempts\. Requiring regular password changes also helps in the following scenarios:
+ Passwords can be stolen or compromised without your knowledge\. This can happen via a system compromise, software vulnerability, or internal threat\.
+ Certain corporate and government web filters or proxy servers can intercept and record traffic even if it's encrypted\.
+ Many people use the same password for many systems such as work, email, and personal\.
+ Compromised end\-user workstations might have a keystroke logger\.

### Remediation<a name="cis-1.11-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Enable password expiration** and then enter **90** for **Password expiration period \(in days\)**\.

1. Choose **Apply password policy**\.

## 1\.12 – Ensure no root account access key exists<a name="securityhub-cis-controls-1.12"></a>

**Severity:** Critical

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html)

The root account is the most privileged user in an AWS account\. AWS Access Keys provide programmatic access to a given account\.

Security Hub recommends that all access keys be associated with the root account be removed\. Removing access keys associated with the root account limits vectors that the account can be compromised by\. Removing the root access keys also encourages the creation and use of role\-based accounts that are least privileged\.

**Note**  
This control is not supported in Africa \(Cape Town\)\.

### Remediation<a name="cis-1.12-remediation"></a>

**To deactivate or delete access keys**

1. Log in to your account using the root credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Access keys \(access key ID and secret access key\)**\.

1. For any existing keys, do one of the following:
   + Choose **Make Inactive** to prevent the key from being used to authenticate the account\.
   + Choose **Delete** and then choose **Yes** to permanently delete the key\. You can't recover deleted keys\.

## 1\.13 – Ensure MFA is enabled for the "root" account<a name="securityhub-cis-controls-1.13"></a>

**Severity:** Critical

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-mfa-enabled.html)

The root account is the most privileged user in an account\. MFA adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they're prompted for their user name and password and for an authentication code from their AWS MFA device\.

When you use virtual MFA for root accounts, Security Hub recommends that the device used is *not* a personal device\. Instead, use a dedicated mobile device \(tablet or phone\) that you manage to keep charged and secured independent of any individual personal devices\. This lessens the risks of losing access to the MFA due to device loss, device trade\-in, or if the individual owning the device is no longer employed at the company\.

**Note**  
This control is not supported in AWS GovCloud \(US\-East\) or AWS GovCloud \(US\-West\)\.

### Remediation<a name="cis-1.13-remediation"></a>

**To enable MFA for the root account**

1. Log in to your account using the root credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Multi\-factor authentication \(MFA\)**\.

1. Choose **Activate MFA**\.

1. Choose the type of device to use for MFA and then choose **Continue**\.

1. Complete the steps to configure the device type appropriate to your selection\.

   Choose a hardware\-based authentication mechanism for best results in passing the check [1\.14 – Ensure hardware MFA is enabled for the "root" account ](#securityhub-cis-controls-1.14)\.

## 1\.14 – Ensure hardware MFA is enabled for the "root" account<a name="securityhub-cis-controls-1.14"></a>

**Severity:** Critical

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html)

The root account is the most privileged user in an account\. MFA adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they're prompted for their user name and password and for an authentication code from their AWS MFA device\.

For Level 2, Security Hub recommends that you protect the root account with a hardware MFA\. A hardware MFA has a smaller attack surface than a virtual MFA\. For example, a hardware MFA doesn't suffer the attack surface introduced by the mobile smartphone that a virtual MFA resides on\.

Using hardware MFA for many, many accounts might create a logistical device management issue\. If this occurs, consider implementing this Level 2 recommendation selectively to the highest security accounts\. You can then apply the Level 1 recommendation to the remaining accounts\.

**Note**  
This control is not supported in AWS GovCloud \(US\-East\) or AWS GovCloud \(US\-West\)\.

### Remediation<a name="cis-1.14-remediation"></a>

**To enable hardware\-based MFA for the root account**

1. Log in to your account using the root credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Multi\-factor authentication \(MFA\)**\.

1. Choose **Activate MFA**\.

1. Choose a hardware\-based \(not virtual\) device to use for MFA and then choose **Continue**\.

1. Complete the steps to configure the device type appropriate to your selection\.

## 1\.16 – Ensure IAM policies are attached only to groups or roles<a name="securityhub-cis-controls-1.16"></a>

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html)

By default, IAM users, groups, and roles have no access to AWS resources\. IAM policies are how privileges are granted to users, groups, or roles\.

Security Hub recommends that you apply IAM policies directly to groups and roles but not users\. Assigning privileges at the group or role level reduces the complexity of access management as the number of users grow\. Reducing access management complexity might in turn reduce opportunity for a principal to inadvertently receive or retain excessive privileges\.

### Remediation<a name="cis-1.16-remediation"></a>

To resolve this issue, create an IAM group, assign the policy to the group, and then add the users to the group\. The policy is applied to each user in the group\.

**To create an IAM group**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Groups** and then choose **Create New Group**\.

1. Enter a name for the group to create and then choose **Next Step**\.

1. Select each policy to assign to the group and then choose **Next Step**\.

   The policies that you choose should include any policies currently attached directly to a user account\. The next step to resolve a failed check is to add users to a group and then assign the policies to that group\. Each user in the group gets assigned the policies assigned to the group\.

1. Confirm the details on the **Review** page and then choose **Create Group**\.

For more information about creating groups, see [Creating IAM groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_create.html) in the *IAM User Guide*\.

**To add users to an IAM group**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Groups**\.

1. Choose **Group Actions** and then choose **Add Users to Group**\.

1. Select the users to add to the group and then choose **Add Users**\.

For more information about adding users to groups, see [Adding and removing users in an IAM group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_manage_add-remove-users.html)\.

**To remove a policy attached directly to a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. For the user to detach a policy from, choose the name in the **User name** column\.

1. For each policy listed under **Attached directly**, choose the **X** on the right side of the page to remove the policy from the user and then choose **Remove**\.

1. Confirm that the user can still use AWS services as expected\.

## 1\.20 \- Ensure a support role has been created to manage incidents with AWS Support<a name="securityhub-cis-controls-1.20"></a>

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-in-use.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-in-use.html)

AWS provides a support center that can be used for incident notification and response, as well as technical support and customer services\.

Create an IAM role to allow authorized users to manage incidents with AWS Support\. By implementing least privilege for access control, an IAM role will require an appropriate IAM policy to allow support center access in order to manage incidents with AWS Support\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="cis-1.20-remediation"></a>

To remediate this issue, create a role to allow authorized users to manage AWS Support incidents\.

**To create the role to use for AWS Support access**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the IAM navigation pane, choose **Roles**, then choose **Create role**\.

1. For **Role type**, choose the **Another AWS account**\.

1. For **Account ID**, enter the AWS account ID of the AWS account to which you want to grant access to your resources\.

   If the users or groups that will assume this role are in the same account, then enter the local account number\.
**Note**  
The administrator of the specified account can grant permission to assume this role to any IAM user in that account\. To do this, the administrator attaches a policy to the user or a group that grants permission for the `sts:AssumeRole` action\. In that policy, the resource must be the role ARN\.

1. Choose **Next: Permissions**\.

1. Search for the managed policy `AWSSupportAccess`\.

1. Select the check box for the `AWSSupportAccess` managed policy\.

1. Choose **Next: Tags**\.

1. \(Optional\) To add metadata to the role, attach tags as key–value pairs\.

   For more information about using tags in IAM, see [Tagging IAM users and roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html) in the *IAM User Guide*\.

1. Choose **Next: Review**\.

1. For **Role name**, enter a name for your role\.

   Role names must be unique within your AWS account\. They are not case sensitive\.

1. \(Optional\) For **Role description**, enter a description for the new role\.

1. Review the role, then choose **Create role**\.

## 1\.22 – Ensure IAM policies that allow full "\*:\*" administrative privileges are not created<a name="securityhub-cis-controls-1.22"></a>

**Severity:** Critical

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html)

IAM policies define a set of privileges granted to users, groups, or roles\. It's recommended and considered a standard security advice to grant least privilege—that is, granting only the permissions required to perform a task\. Determine what users need to do and then craft policies that let the users perform only those tasks, instead of allowing full administrative privileges\.

It's more secure to start with a minimum set of permissions and grant additional permissions as necessary, rather than starting with permissions that are too lenient and then trying to tighten them later\. Providing full administrative privileges instead of restricting to the minimum set of permissions that the user is required to do exposes the resources to potentially unwanted actions\.

You should remove IAM policies that have a statement with `"Effect": "Allow"` with `"Action": "*" `over `"Resource": "*"`\.

### Remediation<a name="cis-1.22-remediation"></a>

**To modify an IAM policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Policies**\.

1. Select the radio button next to the policy to remove\.

1. From the **Policy actions** drop\-down menu, choose **Detach**\.

1. On the **Detach policy** page, select the radio button next to each user to detach the policy from and then choose **Detach policy**\.

Confirm that the user that you detached the policy from can still access AWS services and resources as expected\.

## 2\.1 – Ensure CloudTrail is enabled in all Regions<a name="securityhub-cis-controls-2.1"></a>

**Severity:** Critical

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloudtrail-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloudtrail-enabled.html)

CloudTrail is a service that records AWS API calls for your account and delivers log files to you\. The recorded information includes the identity of the API caller, the time of the API call, the source IP address of the API caller, the request parameters, and the response elements returned by the AWS service\. CloudTrail provides a history of AWS API calls for an account, including API calls made via the AWS Management Console, AWS SDKs, command\-line tools, and higher\-level AWS services \(such as AWS CloudFormation\)\.

The AWS API call history produced by CloudTrail enables security analysis, resource change tracking, and compliance auditing\. Additionally:
+ Ensuring that a multi\-Region trail exists ensures that unexpected activity occurring in otherwise unused Regions is detected
+ Ensuring that a multi\-Region trail exists ensures that Global Service Logging is enabled for a trail by default to capture recording of events generated on AWS global services
+ For a multi\-Region trail, ensuring that management events configured for all type of Read/Writes ensures recording of management operations that are performed on all resources in an AWS account

### Remediation<a name="cis-2.1-remediation"></a>

**To create a new trail in CloudTrail**

1. Sign in to the AWS Management Console and open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. If you haven't used CloudTrail before, choose **Get Started Now**\.

1. Choose **Trails** and then choose **Create trail**\.

1. Enter a name for the trail\.

1. For **Apply trail to all regions**, choose **Yes**\.

1. Under **Storage location**, do one of the following:
   + To create a new S3 bucket for CloudTrail logs, choose **Yes** next to **Create a new S3 bucket** and then enter a name for the bucket\.
   + Choose **No** next to **Create a new S3 bucket** and then select the bucket to use\.

1. Choose **Additional settings** and, for **Enable log file validation**, choose **Yes** to pass [2\.2\. – Ensure CloudTrail log file validation is enabled ](#securityhub-cis-controls-2.2) \.

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

## 2\.2\. – Ensure CloudTrail log file validation is enabled<a name="securityhub-cis-controls-2.2"></a>

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html)

CloudTrail log file validation creates a digitally signed digest file containing a hash of each log that CloudTrail writes to S3\. You can use these digest files to determine whether a log file was changed, deleted, or unchanged after CloudTrail delivered the log\.

Security Hub recommends that you enable file validation on all trails\. Enabling log file validation provides additional integrity checking of CloudTrail logs\.

### Remediation<a name="cis-2.2-remediation"></a>

**To enable CloudTrail log file validation**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the name of a trail to edit in the **Name** column\.

1. Choose the pencil icon for the **Storage location**\.

1. For **Enable log file validation**, choose **Yes** and then choose **Save**\.

## 2\.3 – Ensure the S3 bucket CloudTrail logs to is not publicly accessible<a name="securityhub-cis-controls-2.3"></a>

**Severity:** Critical

**AWS Config rules:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited.html), [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html)

CloudTrail logs a record of every API call made in your account\. These log files are stored in an S3 bucket\. Security Hub recommends that the bucket policy, or access control list \(ACL\), applied to the S3 bucket that CloudTrail logs to prevents public access to the CloudTrail logs\. Allowing public access to CloudTrail log content might aid an adversary in identifying weaknesses in the affected account's use or configuration\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you are using Security Hub in the US East \(N\. Virginia\) Region, and you are storing AWS CloudTrail logs in a bucket in the US West \(N\. California\) Region, Security Hub cannot find the bucket in the US West \(N\. California\) Region\. When this happens, the check returns a warning that the resource cannot be located\.  
Similarly, if you are aggregating logs from multiple accounts into a single bucket, the CIS check returns a warning finding for all accounts except the account that owns the bucket\. Failed findings are returned when the bucket is located in the account and region where the check is being performed and that bucket is publicly accessible\.

To run this check, Security Hub first uses custom logic to look for the bucket where your CloudTrail logs are stored\. It then uses the AWS Config managed rules to check that bucket is publicly accessible\.

If Security Hub cannot discover the bucket because it is in a different account or region, a warning finding is generated\.

If the bucket is discovered and is publicly accessible, the check generates a failed finding\.

### Remediation<a name="cis-2.3-remediation"></a>

**To remove public access for an Amazon S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the name of the bucket where your CloudTrail are stored\.

1. Choose **Permissions** and then choose **Public access settings**\.

1. Choose **Edit**, select all four options, and then choose **Save**\.

1. If prompted, enter **confirm** and then choose **Confirm**\.

## 2\.4 – Ensure CloudTrail trails are integrated with Amazon CloudWatch Logs<a name="securityhub-cis-controls-2.4"></a>

**Severity:** Low

**AWS Config rule: **[https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-cloud-watch-logs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-cloud-watch-logs-enabled.html)

CloudTrail is a web service that records AWS API calls made in a given account\. The recorded information includes the identity of the API caller, the time of the API call, the source IP address of the API caller, the request parameters, and the response elements returned by the AWS service\.

CloudTrail uses Amazon S3 for log file storage and delivery, so log files are stored durably\. In addition to capturing CloudTrail logs in a specified Amazon S3 bucket for long\-term analysis, you can perform real\-time analysis by configuring CloudTrail to send logs to CloudWatch Logs\.

For a trail that is enabled in all Regions in an account, CloudTrail sends log files from all those Regions to a CloudWatch Logs log group\.

Security Hub recommends that you send CloudTrail logs to CloudWatch Logs\.

**Note**  
 The intent of this recommendation is to ensure that account activity is being captured, monitored, and appropriately alarmed on\. CloudWatch Logs is a native way to accomplish this using AWS services but doesn't preclude the use of an alternate solution\.

Sending CloudTrail logs to CloudWatch Logs facilitates real\-time and historic activity logging based on user, API, resource, and IP address\. It provides the opportunity to establish alarms and notifications for anomalous or sensitivity account activity\.

### Remediation<a name="cis-2.4-remediation"></a>

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

For more information, see [Configuring CloudWatch Logs monitoring with the console](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/send-cloudtrail-events-to-cloudwatch-logs.html#send-cloudtrail-events-to-cloudwatch-logs-console) in the *AWS CloudTrail User Guide*\.

## 2\.5 – Ensure AWS Config is enabled<a name="securityhub-cis-controls-2.5"></a>

**Severity:** Medium

**AWS Config** rule: None

AWS Config is a web service that performs configuration management of supported AWS resources in your account and delivers log files to you\. The recorded information includes the configuration item \(AWS resource\), relationships between configuration items \(AWS resources\), and any configuration changes between resources\.

Security Hub recommends that you enable AWS Config in all Regions\. The AWS configuration item history that AWS Config captures enables security analysis, resource change tracking, and compliance auditing\.

**Note**  
CIS 2\.5 requires that AWS Config is enabled in all Regions in which you use Security Hub\.  
Because Security Hub is a regional service, the check performed for this control checks only the current Region for the account\. It does not check all Regions\.  
You also must record global resources so that security checks against global resources can be checked in each Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

To run this check, Security Hub performs custom logic to perform the audit steps prescribed for it in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. Security Hub also requires that global resources are recorded in each Region, because Security Hub is a regional service and performs its security checks on a Region\-by\-Region basis\.

### Remediation<a name="cis-2.5-remediation"></a>

**To configure AWS Config settings**

1. Open the AWS Config console at [https://console\.aws\.amazon\.com/config/](https://console.aws.amazon.com/config/)\.

1. Select the Region to configure AWS Config in\.

1. If you haven't used AWS Config before, choose **Get started**\.

1. On the Settings page, do the following:
   + Under **Resource types to record**, select **Record all resources supported in this region** and **Include global resources \(e\.g\., AWS IAM resources\)**\.
   + Under **Amazon S3 bucket**, specify the bucket to use or create a bucket and optionally include a prefix\.
   + Under **Amazon SNS topic**, select an Amazon SNS topic from your account or create one\. For more information about Amazon SNS, see the [https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html)\.
   + Under **AWS Config role**, either choose **Create AWS Config service\-linked role** or choose **Choose a role from your account** and then select the role to use\.

1. Choose **Next**\.

1. On the **AWS Config** rules page, choose **Skip**\.

1. Choose **Confirm**\.

For more information about using AWS Config from the AWS Command Line Interface, see [Turning on AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/gs-cli-subscribe.html) in the *AWS Config Developer Guide*\.

You can also use an AWS CloudFormation template to automate this process\. For more information, see the [AWS CloudFormation StackSets sample template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html) in the *AWS CloudFormation User Guide*\.

## 2\.6 – Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket<a name="securityhub-cis-controls-2.6"></a>

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-logging-enabled.html)

Amazon S3 bucket access logging generates a log that contains access records for each request made to your S3 bucket\. An access log record contains details about the request, such as the request type, the resources specified in the request worked, and the time and date the request was processed\.

Security Hub recommends that you enable bucket access logging on the CloudTrail S3 bucket\.

By enabling S3 bucket logging on target S3 buckets, you can capture all events that might affect objects in a target bucket\. Configuring logs to be placed in a separate bucket enables access to log information, which can be useful in security and incident response workflows\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you are using Security Hub in the US East \(N\. Virginia\) Region, and you are storing AWS CloudTrail logs in a bucket in the US West \(N\. California\) Region, Security Hub cannot find the bucket in the US West \(N\. California\) Region\. When this happens, the check returns a warning that the resource cannot be located\.  
Similarly, if you are aggregating logs from multiple accounts into a single bucket, the CIS check returns a warning finding for all accounts except the account that owns the bucket\.  
Failed findings are returned when the bucket is located in the account and region where the check is being performed and that bucket is publicly accessible\.

To run this check, Security Hub first uses custom logic to look for the bucket where your CloudTrail logs are stored and then uses the AWS Config managed rule to check if logging is enabled\.

If the bucket cannot be discovered because it is in a different account or region, a warning finding is generated\. If the bucket is discovered and is publicly accessible, the check generates a failed finding\.

### Remediation<a name="cis-2.6-remediation"></a>

**To enable S3 bucket access logging**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the bucket used for CloudTrail\.

1. Choose **Properties**\.

1. Choose **Server access logging**, then choose **Enable logging**\.

1. Select a bucket from the **Target bucket** list, and optionally enter a prefix\.

1. Choose **Save**\.

## 2\.7 – Ensure CloudTrail logs are encrypted at rest using AWS KMS CMKs<a name="securityhub-cis-controls-2.7"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html)

CloudTrail is a web service that records AWS API calls for an account and makes those logs available to users and resources in accordance with IAM policies\. AWS Key Management Service \(AWS KMS\) is a managed service that helps create and control the encryption keys used to encrypt account data, and uses hardware security modules \(HSMs\) to protect the security of encryption keys\.

You can configure CloudTrail logs to leverage server\-side encryption \(SSE\) and AWS KMS customer\-created master keys \(CMKs\) to further protect CloudTrail logs\.

Security Hub recommends that you configure CloudTrail to use SSE\-KMS\.

Configuring CloudTrail to use SSE\-KMS provides additional confidentiality controls on log data because a given user must have S3 read permission on the corresponding log bucket and must be granted decrypt permission by the CMK policy\.

### Remediation<a name="cis-2.7-remediation"></a>

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

You might need to modify the policy for CloudTrail to successfully interact with your CMK\. For more information, see [Encrypting CloudTrail log files with AWS KMS–Managed Keys \(SSE\-KMS\)](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html?icmpid=docs_cloudtrail_console) in the *AWS CloudTrail User Guide*\.

## 2\.8 – Ensure rotation for customer\-created CMKs is enabled<a name="securityhub-cis-controls-2.8"></a>

**Severity:** High

**AWS Config rule: **[https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html)

AWS KMS enables customers to rotate the backing key, which is key material stored in AWS KMS and is tied to the key ID of the CMK\. It's the backing key that is used to perform cryptographic operations such as encryption and decryption\. Automated key rotation currently retains all previous backing keys so that decryption of encrypted data can take place transparently\.

Security Hub recommends that you enable CMK key rotation\. Rotating encryption keys helps reduce the potential impact of a compromised key because data encrypted with a new key can't be accessed with a previous key that might have been exposed\.

### Remediation<a name="cis-2.8-remediation"></a>

**To enable CMK rotation**

1. Open the AWS KMS console at [https://console\.aws\.amazon\.com/kms](https://console.aws.amazon.com/kms)\.

1. To change the AWS Region, use the Region selector in the upper\-right corner of the page\.

1. Choose **Customer managed keys**\.

1. Choose the alias of the key to update in the **Alias** column\.

1. Choose **Key rotation**\.

1. Select **Automatically rotate this CMK every year** and then choose **Save**\.

## 2\.9 – Ensure VPC flow logging is enabled in all VPCs<a name="securityhub-cis-controls-2.9"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html)

VPC flow logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC\. After you have created a flow log, you can view and retrieve its data in CloudWatch Logs\.

Security Hub recommends that you enable flow logging for packet rejects for VPCs\. Flow logs provide visibility into network traffic that traverses the VPC and can detect anomalous traffic or insight during security workflows\. 

### Remediation<a name="cis-2.9-remediation"></a>

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

## 3\.1 – Ensure a log metric filter and alarm exist for unauthorized API calls<a name="securityhub-cis-controls-3.1"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

Security Hub recommends that you create a metric filter and alarm unauthorized API calls\. Monitoring unauthorized API calls helps reveal application errors and might reduce time to detect malicious activity\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.1 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.1-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.2 – Ensure a log metric filter and alarm exist for AWS Management Console sign\-in without MFA<a name="securityhub-cis-controls-3.2"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

Security Hub recommends that you create a metric filter and alarm console logins that aren't protected by MFA\. Monitoring for single\-factor console logins increases visibility into accounts that aren't protected by MFA\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.2 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.2-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.3 – Ensure a log metric filter and alarm exist for usage of "root" account<a name="securityhub-cis-controls-3.3"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

Security Hub recommends that you create a metric filter and alarm for root login attempts\. Monitoring for root account logins provides visibility into the use of a fully privileged account and an opportunity to reduce the use of it\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.3 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.3-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**, then choose **Log groups**\. 

1. Choose the log group where CloudTrail is logging\.

1. On the log group details page, choose ** Metric filters**\.

1. Choose **Create metric filter**\. 

1. Copy the following pattern and then paste it into **Filter pattern**\.

   ```
   {$.userIdentity.type="Root" && $.userIdentity.invokedBy NOT EXISTS && $.eventType !="AwsServiceEvent"}
   ```

1. Choose **Next**\.

1. Enter the name of the new filter\. For example, **RootAccountUsage**\.

1. Confirm that the value for **Metric namespace** is `LogMetrics`\. 

   This ensures that all CIS Benchmark metrics are grouped together\.

1. In **Metric name**, enter the name of the metric\.

1. In **Metric value**, enter **1**, and then choose **Next**\.

1. Choose **Create metric filter**\. 

1. Next, set up the notification\. Select the select the metric filter you just created, then choose **Create alarm**\.

1. Enter the threshold for the alarm \(for example, **1**\), then choose **Next**\.

1. Under **Select an SNS topic**, for **Send notification to**, choose an email list, then choose **Next**\.

1. Enter a **Name** and **Description** for the alarm, such as **RootAccountUsageAlarm**, then choose **Next**\. 

1. Choose **Create Alarm**\. 

## 3\.4 – Ensure a log metric filter and alarm exist for IAM policy changes<a name="securityhub-cis-controls-3.4"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

Security Hub recommends that you create a metric filter and alarm for changes made to IAM policies\. Monitoring these changes helps ensure that authentication and authorization controls remain intact\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.4 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.4-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.5 – Ensure a log metric filter and alarm exist for CloudTrail configuration changes<a name="securityhub-cis-controls-3.5"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

Security Hub recommends that you create a metric filter and alarm for changes to CloudTrail configuration settings\. Monitoring these changes helps ensure sustained visibility to activities in the account\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.5 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.5-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.6 – Ensure a log metric filter and alarm exist for AWS Management Console authentication failures<a name="securityhub-cis-controls-3.6"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

Security Hub recommends that you create a metric filter and alarm for failed console authentication attempts\. Monitoring failed console logins might decrease lead time to detect an attempt to brute\-force a credential, which might provide an indicator, such as source IP, that you can use in other event correlations\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.6 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.6-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.7 – Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs<a name="securityhub-cis-controls-3.7"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

Security Hub recommends that you create a metric filter and alarm for customer\-created CMKs that have changed state to disabled or scheduled deletion\. Data encrypted with disabled or deleted keys is no longer accessible\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.7 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.7-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.8 – Ensure a log metric filter and alarm exist for S3 bucket policy changes<a name="securityhub-cis-controls-3.8"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

Security Hub recommends that you create a metric filter and alarm for changes to S3 bucket policies\. Monitoring these changes might reduce time to detect and correct permissive policies on sensitive S3 buckets\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.8 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.8-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.9 – Ensure a log metric filter and alarm exist for AWS Config configuration changes<a name="securityhub-cis-controls-3.9"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

Security Hub recommends that you create a metric filter and alarm for changes to AWS Config configuration settings\. Monitoring these changes helps ensure sustained visibility of configuration items in the account\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.9 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.9-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.10 – Ensure a log metric filter and alarm exist for security group changes<a name="securityhub-cis-controls-3.10"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Security groups are a stateful packet filter that controls ingress and egress traffic in a VPC\.

Security Hub recommends that you create a metric filter and alarm for changes to security groups\. Monitoring these changes helps ensure that resources and services aren't unintentionally exposed\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.10 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.10-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting Started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.11 – Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)<a name="securityhub-cis-controls-3.11"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. NACLs are used as a stateless packet filter to control ingress and egress traffic for subnets in a VPC\.

Security Hub recommends that you create a metric filter and alarm for changes to NACLs\. Monitoring these changes helps ensure that AWS resources and services aren't unintentionally exposed\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.11 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.11-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.12 – Ensure a log metric filter and alarm exist for changes to network gateways<a name="securityhub-cis-controls-3.12"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Network gateways are required to send and receive traffic to a destination outside a VPC\.

Security Hub recommends that you create a metric filter and alarm for changes to network gateways\. Monitoring these changes helps ensure that all ingress and egress traffic traverses the VPC border via a controlled path\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.12 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.12-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.13 – Ensure a log metric filter and alarm exist for route table changes<a name="securityhub-cis-controls-3.13"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Routing tables route network traffic between subnets and to network gateways\.

Security Hub recommends that you create a metric filter and alarm for changes to route tables\. Monitoring these changes helps ensure that all VPC traffic flows through an expected path\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.13 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.13-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 3\.14 – Ensure a log metric filter and alarm exist for VPC changes<a name="securityhub-cis-controls-3.14"></a>

**Severity:** Medium

**AWS Config** rule: None

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. You can have more than one VPC in an account, and you can create a peer connection between two VPCs, enabling network traffic to route between VPCs\.

Security Hub recommends that you create a metric filter and alarm for changes to VPCs\. Monitoring these changes helps ensure that authentication and authorization controls remain intact\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.14 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Important**  
Security Hub supports CIS AWS Foundations checks only on resources in the same Region and owned by the same account as the one in which Security Hub is enabled\.  
For example, if you enable Security Hub in the US East \(N\. Virginia\) Region, but you create CloudWatch alarms or SNS topics in the US West \(N\. California\) Region, Security Hub running in the US East \(N\. Virginia\) Region can’t locate the CloudWatch alarms or SNS topics in the US West \(N\. California\) Region\.  
When this happens, the check returns a warning that the resource can’t be located\. A Failed finding is generated only when a resource is successfully located but is not compliant with CIS requirements for the control\.

### Remediation<a name="cis-3.14-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

**Create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

1. Set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis-controls-2.1)\.

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

## 4\.1 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 22<a name="securityhub-cis-controls-4.1"></a>

**Severity:** High

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/restricted-ssh.html](https://docs.aws.amazon.com/config/latest/developerguide/restricted-ssh.html)

Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\.

Security Hub recommends that no security group allow unrestricted ingress access to port 22\. Removing unfettered connectivity to remote console services, such as SSH, reduces a server's exposure to risk\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="cis-4.1-remediation"></a>

Perform the following steps for each security group associated with a VPC\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the left pane, choose **Security groups**\.

1. Select a security group\.

1. In the bottom section of the page, choose the **Inbound Rules** tab\.

1. Choose **Edit rules**\.

1. Identify the rule that allows access through port 22 and then choose the **X** to remove it\.

1. Choose **Save rules**\.

## 4\.2 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389<a name="securityhub-cis-controls-4.2"></a>

**Severity:** High

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/restricted-common-ports.html](https://docs.aws.amazon.com/config/latest/developerguide/restricted-common-ports.html)

Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\.

Security Hub recommends that no security group allow unrestricted ingress access to port 3389\. Removing unfettered connectivity to remote console services, such as RDP, reduces a server's exposure to risk\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="cis-4.2-remediation"></a>

Perform the following steps for each security group associated with a VPC\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the left pane, choose **Security groups**\.

1. Select a security group\.

1. In the bottom section of the page, choose the **Inbound Rules** tab\.

1. Choose **Edit rules**\.

1. Identify the rule that allows access through port 3389 and then choose the **X** to remove it\.

1. Choose **Save rules**\.

## 4\.3 – Ensure the default security group of every VPC restricts all traffic<a name="securityhub-cis-controls-4.3"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html)

A VPC comes with a default security group with initial settings that deny all inbound traffic, allow all outbound traffic, and allow all traffic between instances assigned to the security group\. If you don't specify a security group when you launch an instance, the instance is automatically assigned to this default security group\. Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\.

Security Hub recommends that the default security group restrict all traffic\.

Update the default security group for the default VPC in every Region to comply\. Any new VPCs automatically contain a default security group that you need to remediate to comply with this recommendation\.

**Note**  
When implementing this recommendation, you can use VPC flow logging, enabled for [2\.9 – Ensure VPC flow logging is enabled in all VPCs ](#securityhub-cis-controls-2.9), to determine the least\-privilege port access required by systems to work properly because it can log all packet acceptances and rejections occurring under the current security groups\.

Configuring all VPC default security groups to restrict all traffic encourages least\-privilege security group development and mindful placement of AWS resources into security groups, which in turn reduces the exposure of those resources\.

### Remediation<a name="cis-4.3-remediation"></a>

**To update the default security group to restrict all access**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. View the default security groups details to see the resources that are assigned to them\.

1. Create a set of least\-privilege security groups for the resources\.

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the Amazon EC2 console, change the security group for the resources that use the default security groups to the least\-privilege security group you created\.

1. For each default security group, choose the **Inbound** tab and delete all inbound rules\.

1. For each default security group, choose the **Outbound** tab and delete all outbound rules\.

For more information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the *Amazon VPC User Guide*\.