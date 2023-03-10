# AWS Identity and Access Management controls<a name="iam-controls"></a>

These controls are related to IAM resources\.

## \[IAM\.1\] IAM policies should not allow full "\*" administrative privileges<a name="iam-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/7\.2\.1, CIS AWS Foundations Benchmark v1\.2\.0/1\.22, CIS AWS Foundations Benchmark v1\.4\.0/1\.16, NIST\.800\-53\.r5 AC\-2, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-5, NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 AC\-6\(10\), NIST\.800\-53\.r5 AC\-6\(2\), NIST\.800\-53\.r5 AC\-6\(3\)

**Category:** Protect > Secure access management

**Severity:** High

**Resource type:** `AWS::IAM::Policy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html)

**Schedule type:** Change triggered

**Parameters:**
+ `excludePermissionBoundaryPolicy: true`

This control checks whether the default version of IAM policies \(also known as customer managed policies\) has administrator access by including a statement with `"Effect": "Allow"` with `"Action": "*"` over `"Resource": "*"`\. The control fails if you have IAM policies with such a statement\.

The control only checks the customer managed policies that you create\. It does not check inline and AWS managed policies\.

IAM policies define a set of privileges that are granted to users, groups, or roles\. Following standard security advice, AWS recommends that you grant least privilege, which means to grant only the permissions that are required to perform a task\. When you provide full administrative privileges instead of the minimum set of permissions that the user needs, you expose the resources to potentially unwanted actions\.

Instead of allowing full administrative privileges, determine what users need to do and then craft policies that let the users perform only those tasks\. It is more secure to start with a minimum set of permissions and grant additional permissions as necessary\. Do not start with permissions that are too lenient and then try to tighten them later\.

You should remove IAM policies that have a statement with `"Effect": "Allow" `with `"Action": "*"` over `"Resource": "*"`\.

**Note**  
This control is not supported in Middle East \(UAE\)\.  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-1-remediation"></a>

To modify your IAM policies so that they do not allow full "\*" administrative privileges, see [Editing IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-edit.html) in the *IAM User Guide*\.

## \[IAM\.2\] IAM users should not have IAM policies attached<a name="iam-2"></a>

**Related requirements:** PCI DSS v3\.2\.1/7\.2\.1, CIS AWS Foundations Benchmark v1\.2\.0/1\.16, NIST\.800\-53\.r5 AC\-2, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 AC\-6\(3\)

**Category:** Protect > Secure access management

**Severity:** Low

**Resource type:** `AWS::IAM::User`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks that none of your IAM users have policies attached\. Instead, IAM users must inherit permissions from IAM groups or roles\.

By default, IAM users, groups, and roles have no access to AWS resources\. IAM policies grant privileges to users, groups, or roles\. We recommend that you apply IAM policies directly to groups and roles but not to users\. Assigning privileges at the group or role level reduces the complexity of access management as the number of users grows\. Reducing access management complexity might in turn reduce the opportunity for a principal to inadvertently receive or retain excessive privileges\. 

**Note**  
This control is not supported in Middle East \(UAE\)\.  
IAM users created by Amazon Simple Email Service are automatically created using inline policies\. Security Hub automatically exempts these users from this control\.  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-2-remediation"></a>

To resolve this issue, [create an IAM group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_create.html), and attach the policy to the group\. Then, [add the users to the group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_manage_add-remove-users.html)\. The policy is applied to each user in the group\. To remove a policy attached directly to a user, see [Adding and removing IAM identity permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html) in the *IAM User Guide*\.

## \[IAM\.3\] IAM users' access keys should be rotated every 90 days or less<a name="iam-3"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.4, CIS AWS Foundations Benchmark v1\.4\.0/1\.14, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-2\(3\), NIST\.800\-53\.r5 AC\-3\(15\)

**Category:** Protect > Secure access management

**Severity:** Medium 

**Resource type:** `AWS::IAM::User`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html](https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html)

**Schedule type:** Periodic

**Parameters:**
+ `maxAccessKeyAge`: 90

This control checks whether the active access keys are rotated within 90 days\.

We highly recommend that you do not generate and remove all access keys in your account\. Instead, the recommended best practice is to either create one or more IAM roles or to use [federation](http://aws.amazon.com/identity/federation/) through AWS IAM Identity Center \(successor to AWS Single Sign\-On\)\. You can use these methods to allow your users to access the AWS Management Console and AWS CLI\.

Each approach has its use cases\. Federation is generally better for enterprises that have an existing central directory or plan to need more than the current limit on IAM users\. Applications that run outside of an AWS environment need access keys for programmatic access to AWS resources\.

However, if the resources that need programmatic access run inside AWS, the best practice is to use IAM roles\. Roles allow you to grant a resource access without hardcoding an access key ID and secret access key into the configuration\.

To learn more about protecting your access keys and account, see [Best practices for managing AWS access keys](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html) in the *AWS General Reference*\. Also see the blog post [Guidelines for protecting your AWS account while using programmatic access](http://aws.amazon.com/blogs/security/guidelines-for-protecting-your-aws-account-while-using-programmatic-access/)\.

If you already have an access key, Security Hub recommends that you rotate the access keys every 90 days\. Rotating access keys reduces the chance that an access key that is associated with a compromised or terminated account is used\. It also ensures that data cannot be accessed with an old key that might have been lost, cracked, or stolen\. Always update your applications after you rotate access keys\. 

Access keys consist of an access key ID and a secret access key\. They are used to sign programmatic requests that you make to AWS\. Users need their own access keys to make programmatic calls to AWS from the AWS CLI, Tools for Windows PowerShell, the AWS SDKs, or direct HTTP calls using the API operations for individual AWS services\.

If your organization uses AWS IAM Identity Center \(successor to AWS Single Sign\-On\) \(IAM Identity Center\), your users can sign in to Active Directory, a built\-in IAM Identity Center directory, or [another identity provider \(IdP\) connected to IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-idp.html)\. They can then be mapped to an IAM role that enables them to run AWS CLI commands or call AWS API operations without the need for access keys\. To learn more, see [Configuring the AWS CLI to use AWS IAM Identity Center \(successor to AWS Single Sign\-On\)](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html) in the *AWS Command Line Interface User Guide*\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-3-remediation"></a>

To remediate this issue, replace any keys that are older than 90 days\.

**To ensure that access keys aren't more than 90 days old**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. For each user that shows an **Access key age** that is greater than 90 days, choose the **User name** to open the settings for that user\.

1. Choose **Security credentials**\.

1. Create a new key for the user:

   1. Choose **Create access key**\.

   1. To save the key content, either download the secret access key, or choose **Show** and then copy it from the page\.

   1. Store the key in a secure location to provide to the user\.

   1. Choose **Close**\.

1. Update all applications that were using the previous key to use the new key\.

1. For the previous key, choose **Make inactive** to make the access key inactive\. The user now cannot use that key to make requests\.

1. Confirm that all applications work as expected with the new key\.

1. After confirming that all applications work with the new key, delete the previous key\. After you delete the access key, you cannot recover it\.

   To delete the previous key, choose the **X** at the end of the row and then choose **Delete**\.

## \[IAM\.4\] IAM root user access key should not exist<a name="iam-4"></a>

**Related requirements:** PCI DSS v3\.2\.1/2\.1, PCI DSS v3\.2\.1/2\.2, PCI DSS v3\.2\.1/7\.2\.1, CIS AWS Foundations Benchmark v1\.2\.0/1\.12, CIS AWS Foundations Benchmark v1\.4\.0/1\.4, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 AC\-6\(10\), NIST\.800\-53\.r5 AC\-6\(2\)

**Category:** Protect > Secure access management

**Severity:** Critical 

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether the root user access key is present\. 

The root user is the most privileged user in an AWS account\. AWS access keys provide programmatic access to a given account\.

Security Hub recommends that you remove all access keys that are associated with the root user\. This limits that vectors that can be used to compromise your account\. It also encourages the creation and use of role\-based accounts that are least privileged\. 

**Note**  
This control is not supported in the following Regions\.  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
Middle East \(UAE\)

### Remediation<a name="iam-4-remediation"></a>

To delete the root user access key, see [Deleting access keys for the root user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_delete-key) in the *IAM User Guide*\.

## \[IAM\.5\] MFA should be enabled for all IAM users that have a console password<a name="iam-5"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.2, CIS AWS Foundations Benchmark v1\.4\.0/1\.10, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 IA\-2\(1\), NIST\.800\-53\.r5 IA\-2\(2\), NIST\.800\-53\.r5 IA\-2\(6\), NIST\.800\-53\.r5 IA\-2\(8\)

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::IAM::User`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html](https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether AWS multi\-factor authentication \(MFA\) is enabled for all IAM users that use a console password\.

Multi\-factor authentication \(MFA\) adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they are prompted for their user name and password\. In addition, they are prompted for an authentication code from their AWS MFA device\.

We recommend that you enable MFA for all accounts that have a console password\. MFA is designed to provide increased security for console access\. The authenticating principal must possess a device that emits a time\-sensitive key and must have knowledge of a credential\.

**Note**  
This control is not supported in Middle East \(UAE\)\.  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-5-remediation"></a>

To add MFA for IAM users, see [Using multi\-factor authentication \(MFA\) in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) in the *IAM User Guide*\.

We are offering a free MFA security key to eligible customers\. [See if you quality, and order your free key](https://console.aws.amazon.com/securityhub/home/?region=us-east-1#/free-mfa-security-key/)\.

## \[IAM\.6\] Hardware MFA should be enabled for the root user<a name="iam-6"></a>

**Related requirements:** PCI DSS v3\.2\.1/8\.3\.1, CIS AWS Foundations Benchmark v1\.2\.0/1\.14, CIS AWS Foundations Benchmark v1\.4\.0/1\.6, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 IA\-2\(1\), NIST\.800\-53\.r5 IA\-2\(2\), NIST\.800\-53\.r5 IA\-2\(6\), NIST\.800\-53\.r5 IA\-2\(8\)

**Category:** Protect > Secure access management

**Severity:** Critical

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether your AWS account is enabled to use a hardware multi\-factor authentication \(MFA\) device to sign in with root user credentials\.

Virtual MFA might not provide the same level of security as hardware MFA devices\. We recommend that you use only a virtual MFA device while you wait for hardware purchase approval or for your hardware to arrive\. To learn more, see[ Enabling a virtual multi\-factor authentication \(MFA\) device \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html) in the *IAM User Guide*\.

Both time\-based one\-time password \(TOTP\) and Universal 2nd Factor \(U2F\) tokens are viable as hardware MFA options\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)\.

### Remediation<a name="iam-6-remediation"></a>

To add a hardware MFA device for the root user, see [Enable a hardware MFA device for the AWS account root user \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_physical.html#enable-hw-mfa-for-root) in the *IAM User Guide*\.

We are offering a free MFA security key to eligible customers\. [See if you quality, and order your free key](https://console.aws.amazon.com/securityhub/home/?region=us-east-1#/free-mfa-security-key/)\.

## \[IAM\.7\] Password policies for IAM users should have strong AWS Configurations<a name="iam-7"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-2\(3\), NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 IA\-5\(1\)

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

**Parameters:**
+ `RequireUppercaseCharacters`: `true`
+ `RequireLowercaseCharacters`: `true`
+ `RequireSymbols`: `true`
+ `RequireNumbers`: `true`
+ `MinimumPasswordLength`: `8`

This control checks whether the account password policy for IAM users uses the recommended configurations\.

To access the AWS Management Console, IAM users need passwords\. As a best practice, Security Hub highly recommends that instead of creating IAM users, you use federation\. Federation allows users to use their existing corporate credentials to log into the AWS Management Console\. Use AWS IAM Identity Center \(successor to AWS Single Sign\-On\) \(IAM Identity Center\) to create or federate the user, and then assume an IAM role into an account\.

To learn more about identity providers and federation, see [Identity providers and federation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html) in the *IAM User Guide*\. To learn more about IAM Identity Center, see the [https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)\.

 If you need to use IAM users, Security Hub recommends that you enforce the creation of strong user passwords\. You can set a password policy on your AWS account to specify complexity requirements and mandatory rotation periods for passwords\. When you create or change a password policy, most of the password policy settings are enforced the next time users change their passwords\. Some of the settings are enforced immediately\.

### Remediation<a name="iam-7-remediation"></a>

To update your password policy to use the recommended configuration, see [Setting an account password policy for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html) in the *IAM User Guide*\.

## \[IAM\.8\] Unused IAM user credentials should be removed<a name="iam-8"></a>

**Related requirements:** PCI DSS v3\.2\.1/8\.1\.4, CIS AWS Foundations Benchmark v1\.2\.0/1\.3, NIST\.800\-53\.r5 AC\-2, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-2\(3\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-6

**Category:** Protect > Secure access management 

**Severity:** Medium 

**Resource type:** `AWS::IAM::User`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html)

**Schedule type:** Periodic

**Parameters:**
+ `maxCredentialUsageAge`: 90 

This control checks whether your IAM users have passwords or active access keys that have not been used for 90 days\.

IAM users can access AWS resources using different types of credentials, such as passwords or access keys\. 

Security Hub recommends that you remove or deactivate all credentials that were unused for 90 days or more\. Disabling or removing unnecessary credentials reduces the window of opportunity for credentials associated with a compromised or abandoned account to be used\.

**Note**  
This control is not supported in Middle East \(UAE\)\.  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-8-remediation"></a>

To get some of the information that you need to monitor accounts for dated credentials, use the IAM console\. For example, when you view users in your account, there is a column for **Access key age**, **Password age**, and **Last activity**\. If the value in any of these columns is greater than 90 days, make the credentials for those users inactive\.

You can also use credential reports to monitor users and identify those with no activity for 90 or more days\. You can download credential reports in `.csv` format from the IAM console\. For more information about credential reports, see [Getting credential reports for your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html#getting-credential-reports-console) in the *IAM User Guide*\.

After you identify the inactive accounts or unused credentials, use the following steps to disable them\.

**To disable credentials for inactive accounts**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the name of the user that has credentials over 90 days old\.

1. Choose** Security credentials**\.

1. For each sign\-in credential and access key that hasn't been used in at least 90 days, choose **Make inactive**\.

## \[IAM\.9\] Virtual MFA should be enabled for the root user<a name="iam-9"></a>

**Related requirements:** PCI DSS v3\.2\.1/8\.3\.1, CIS AWS Foundations Benchmark v1\.2\.0/1\.13, CIS AWS Foundations Benchmark v1\.4\.0/1\.5, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 IA\-2\(1\), NIST\.800\-53\.r5 IA\-2\(2\), NIST\.800\-53\.r5 IA\-2\(6\), NIST\.800\-53\.r5 IA\-2\(8\)

**Category:** Protect > Secure access management 

**Severity:** Critical

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-mfa-enabled.html)

**Schedule type:** Periodic

The root user has complete access to all the services and resources in an AWS account\. MFA adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to the AWS Management Console, they're prompted for their user name and password and for an authentication code from their AWS MFA device\.

When you use virtual MFA for the root user, CIS recommends that the device used is *not* a personal device\. Instead, use a dedicated mobile device \(tablet or phone\) that you manage to keep charged and secured independent of any individual personal devices\. This lessens the risks of losing access to the MFA due to device loss, device trade\-in, or if the individual owning the device is no longer employed at the company\.

**Note**  
This control is not supported in the following Regions\.  
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
 AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="iam-9-remediation"></a>

**To enable MFA for the root user**

1. Log in to your account using the root user credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Multi\-factor authentication \(MFA\)**\.

1. Choose **Activate MFA**\.

1. Choose the type of device to use for MFA and then choose **Continue**\.

1. Complete the steps to configure the device type appropriate to your selection\.

   Choose a hardware\-based authentication mechanism for best results in passing the check [\[IAM\.6\] Hardware MFA should be enabled for the root user](#iam-6)\.

## \[IAM\.10\] Password policies for IAM users should have strong AWS Configurations<a name="iam-10"></a>

**Related requirements:** PCI DSS v3\.2\.1/8\.1\.4, PCI DSS v3\.2\.1/8\.2\.3, PCI DSS v3\.2\.1/8\.2\.4, PCI DSS v3\.2\.1/8\.2\.5

**Category:** Protect > Secure access management 

**Severity:** Medium

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether the account password policy for IAM users uses the following minimum PCI DSS configurations\.
+ `RequireUppercaseCharacters` – Require at least one uppercase character in password\. \(Default = `true`\)
+ `RequireLowercaseCharacters` – Require at least one lowercase character in password\. \(Default = `true`\)
+ `RequireNumbers` – Require at least one number in password\. \(Default = `true`\)
+ `MinimumPasswordLength` – Password minimum length\. \(Default = 7 or longer\)
+ `PasswordReusePrevention` – Number of passwords before allowing reuse\. \(Default = 4\)
+ MaxPasswordAge – Number of days before password expiration\. \(Default = 90\)

### Remediation<a name="iam-10-remediation"></a>

To update your password policy to use the recommended configuration, see [Setting an account password policy for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html) in the *IAM User Guide*\.

## \[IAM\.11\] Ensure IAM password policy requires at least one uppercase letter<a name="iam-11"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.5

**Category:** Protect > Secure access management 

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\.

CIS recommends that the password policy require at least one uppercase letter\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

### Remediation<a name="iam-11-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Requires at least one uppercase letter** and then choose **Apply password policy**\.

## \[IAM\.12\] Ensure IAM password policy requires at least one lowercase letter<a name="iam-12"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.6

**Category:** Protect > Secure access management 

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\. CIS recommends that the password policy require at least one lowercase letter\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

### Remediation<a name="iam-12-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Requires at least one lowercase letter** and then choose **Apply password policy**\.

## \[IAM\.13\] Ensure IAM password policy requires at least one symbol<a name="iam-13"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.7

**Category:** Protect > Secure access management

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\.

CIS recommends that the password policy require at least one symbol\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

### Remediation<a name="iam-13-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Require at least one non\-alphanumeric character** and then choose **Apply password policy**\.

## \[IAM\.14\] Ensure IAM password policy requires at least one number<a name="iam-14"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.8

**Category:** Protect > Secure access management

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords use different character sets\.

CIS recommends that the password policy require at least one number\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

### Remediation<a name="iam-14-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Requires at least one number** and then choose **Apply password policy**\.

## \[IAM\.15\] Ensure IAM password policy requires minimum password length of 14 or greater<a name="iam-15"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.9, CIS AWS Foundations Benchmark v1\.4\.0/1\.8

**Category:** Protect > Secure access management

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords are at least a given length\.

CIS recommends that the password policy require a minimum password length of 14 characters\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

### Remediation<a name="iam-15-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. In the **Minimum password length** field, enter **14**, then choose **Apply password policy**\.

## \[IAM\.16\] Ensure IAM password policy prevents password reuse<a name="iam-16"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.10, CIS AWS Foundations Benchmark v1\.4\.0/1\.9

**Category:** Protect > Secure access management

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

This control checks whether the number of passwords to remember is set to 24\. The control fails if the value is not 24\.

IAM password policies can prevent the reuse of a given password by the same user\.

CIS recommends that the password policy prevent the reuse of passwords\. Preventing password reuse increases account resiliency against brute force login attempts\.

### Remediation<a name="iam-16-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Prevent password reuse** and then enter **24** for **Number of passwords to remember**\.

1. Choose **Apply password policy**\.

## \[IAM\.17\] Ensure IAM password policy expires passwords within 90 days or less<a name="iam-17"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.11

**Category:** Protect > Secure access management

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

IAM password policies can require passwords to be rotated or expired after a given number of days\.

CIS recommends that the password policy expire passwords after 90 days or less\. Reducing the password lifetime increases account resiliency against brute force login attempts\. Requiring regular password changes also helps in the following scenarios:
+ Passwords can be stolen or compromised without your knowledge\. This can happen via a system compromise, software vulnerability, or internal threat\.
+ Certain corporate and government web filters or proxy servers can intercept and record traffic even if it's encrypted\.
+ Many people use the same password for many systems such as work, email, and personal\.
+ Compromised end\-user workstations might have a keystroke logger\.

### Remediation<a name="iam-17-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Enable password expiration** and then enter **90** for **Password expiration period \(in days\)**\.

1. Choose **Apply password policy**\.

## \[IAM\.18\] Ensure a support role has been created to manage incidents with AWS Support<a name="iam-18"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.20, CIS AWS Foundations Benchmark v1\.4\.0/1\.17

**Category:** Protect > Secure access management

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-in-use.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-in-use.html)

**Schedule type:** Periodic

AWS provides a support center that can be used for incident notification and response, as well as technical support and customer services\.

Create an IAM role to allow authorized users to manage incidents with AWS Support\. By implementing least privilege for access control, an IAM role will require an appropriate IAM policy to allow support center access in order to manage incidents with AWS Support\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
 Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="iam-18-remediation"></a>

To remediate this issue, create a role to allow authorized users to manage AWS Support incidents\.

**To create the role to use for AWS Support access**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the IAM navigation pane, choose **Roles**, then choose **Create role**\.

1. For **Role type**, choose the **Another AWS account**\.

1. For **Account ID**, enter the AWS account ID of the AWS account to which you want to grant access to your resources\.

   If the users or groups that will assume this role are in the same account, then enter the local account number\.
**Note**  
The administrator of the specified account can grant permission to assume this role to any user in that account\. To do this, the administrator attaches a policy to the user or a group that grants permission for the `sts:AssumeRole` action\. In that policy, the resource must be the role ARN\.

1. Choose **Next: Permissions**\.

1. Search for the managed policy `AWSSupportAccess`\.

1. Select the check box for the `AWSSupportAccess` managed policy\.

1. Choose **Next: Tags**\.

1. \(Optional\) To add metadata to the role, attach tags as key\-value pairs\.

   For more information about using tags in IAM, see [Tagging IAM users and roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html) in the *IAM User Guide*\.

1. Choose **Next: Review**\.

1. For **Role name**, enter a name for your role\.

   Role names must be unique within your AWS account\. They are not case sensitive\.

1. \(Optional\) For **Role description**, enter a description for the new role\.

1. Review the role, then choose **Create role**\.

## \[IAM\.19\] MFA should be enabled for all IAM users<a name="iam-19"></a>

**Related requirements:** PCI DSS v3\.2\.1/8\.3\.1, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 IA\-2\(1\), NIST\.800\-53\.r5 IA\-2\(2\), NIST\.800\-53\.r5 IA\-2\(6\), NIST\.800\-53\.r5 IA\-2\(8\)

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::IAM::User`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-mfa-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether the IAM users have multi\-factor authentication \(MFA\) enabled\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="iam-19-remediation"></a>

To add MFA for IAM users, see [Using multi\-factor authentication \(MFA\) in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) in the *IAM User Guide*\.

## \[IAM\.20\] Avoid the use of the root user<a name="iam-20"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/1\.1

**Category:** Protect > Secure access management

**Severity:** Low

**AWS Config rule:** None \(custom Security Hub rule\)

**Schedule type:** Periodic

The root user has unrestricted access to all services and resources in an AWS account\. We highly recommend that you avoid using the root user for daily tasks\. Minimizing the use of the root user and adopting the principle of least privilege for access management reduce the risk of accidental changes and unintended disclosure of highly privileged credentials\.

As a best practice, use your root user credentials only when required to [ perform account and service management tasks](https://docs.aws.amazon.com/general/latest/gr/aws_tasks-that-require-root.html)\. Apply IAM policies directly to groups and roles but not users\. For a tutorial on how to set up an administrator for daily use, see [ Creating your first IAM admin user and group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.3 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="iam-20-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {$.userIdentity.type="Root" && $.userIdentity.invokedBy NOT EXISTS && $.eventType !="AwsServiceEvent"}
      ```

   1. Choose **Next**\.

1. Under **Assign Metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric Namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric Name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then, choose **Create metric filter**\.

1. In the navigation pane, choose **Log groups**, and then choose the filter you created under **Metric filters**\.

1. Select the check box for the filter\. Choose **Create alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm, such as **CIS\-1\.1\-RootAccountUsage**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[IAM\.21\] IAM customer managed policies that you create should not allow wildcard actions for services<a name="iam-21"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-5, NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 AC\-6\(10\), NIST\.800\-53\.r5 AC\-6\(2\), NIST\.800\-53\.r5 AC\-6\(3\)

**Category:** Detect > Secure access management 

**Severity:** Low

**Resource type:** `AWS::IAM::Policy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-full-access.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-full-access.html)

**Schedule type:** Change triggered

**Parameters:**
+ `excludePermissionBoundaryPolicy`: `True`

This control checks whether the IAM identity\-based policies that you create have Allow statements that use the \* wildcard to grant permissions for all actions on any service\. The control fails if any policy statement includes `"Effect": "Allow"` with `"Action": "Service:*"`\. 

For example, the following statement in a policy results in a failed finding\.

```
"Statement": [
{
  "Sid": "EC2-Wildcard",
  "Effect": "Allow",
  "Action": "ec2:*",
  "Resource": "*"
}
```

The control also fails if you use `"Effect": "Allow"` with `"NotAction": "service:*"`\. In that case, the `NotAction` element provides access to all of the actions in an AWS service, except for the actions specified in `NotAction`\.

This control only applies to customer managed IAM policies\. It does not apply to IAM policies that are managed by AWS\.

When you assign permissions to AWS services, it is important to scope the allowed IAM actions in your IAM policies\. You should restrict IAM actions to only those actions that are needed\. This helps you to provision least privilege permissions\. Overly permissive policies might lead to privilege escalation if the policies are attached to an IAM principal that might not require the permission\.

In some cases, you might want to allow IAM actions that have a similar prefix, such as `DescribeFlowLogs` and `DescribeAvailabilityZones`\. In these authorized cases, you can add a suffixed wildcard to the common prefix\. For example, `ec2:Describe*`\.

This control passes if you use a prefixed IAM action with a suffixed wildcard\. For example, the following statement in a policy results in a passed finding\.

```
"Statement": [
{
  "Sid": "EC2-Wildcard",
  "Effect": "Allow",
  "Action": "ec2:Describe*",
  "Resource": "*"
}
```

When you group related IAM actions in this way, you can also avoid exceeding the IAM policy size limits\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-21-remediation"></a>

To remediate this issue, update your IAM policies so that they do not allow full "\*" administrative privileges\. For details about how to edit an IAM policy, see [Editing IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-edit.html) in the *IAM User Guide*\.

## \[IAM\.22\] IAM user credentials unused for 45 days should be removed<a name="iam-22"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.4\.0/1\.12

**Category:** Protect > Secure access management

**Severity:** Medium

**AWS Config rule: **[https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html)

**Schedule type:** Periodic

This control checks whether your IAM users have passwords or active access keys that have not been used for 45 days or more\. To do so, it checks whether the `maxCredentialUsageAge` parameter of the AWS Config rule is equal to 45 or more\.

Users can access AWS resources using different types of credentials, such as passwords or access keys\.

CIS recommends that you remove or deactivate all credentials that have been unused for 45 days or more\. Disabling or removing unnecessary credentials reduces the window of opportunity for credentials associated with a compromised or abandoned account to be used\.

The AWS Config rule for this control uses the [https://docs.aws.amazon.com/IAM/latest/APIReference/API_GetCredentialReport.html](https://docs.aws.amazon.com/IAM/latest/APIReference/API_GetCredentialReport.html) and [https://docs.aws.amazon.com/IAM/latest/APIReference/API_GenerateCredentialReport.html](https://docs.aws.amazon.com/IAM/latest/APIReference/API_GenerateCredentialReport.html) API operations, which are only updated every four hours\. Changes to IAM users can take up to four hours to be visible to this control\.

**Note**  
This control is not supported in Middle East \(UAE\)\.  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, you can enable recording of global resources in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\. 

### Remediation<a name="iam-22-remediation"></a>

To get some of the information that you need to monitor accounts for dated credentials, use the IAM console\. For example, when you view users in your account, there is a column for **Access key age**, **Password age**, and **Last activity**\. If the value in any of these columns is greater than 45 days, make the credentials for those users inactive\.

You can also use credential reports to monitor user accounts and identify those with no activity for 45 or more days\. You can download credential reports in \.csv format from the IAM console\. For more information about credential reports, see [Getting credential reports for your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html#getting-credential-reports-console) in the *IAM User Guide*\.

After you identify the inactive accounts or unused credentials, use the following steps to disable them\.

**To disable credentials for inactive accounts**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the name of the user that has credentials over 45 days old\.

1. Choose **Security credentials**\.

1. For each sign\-in credential and access key that hasn't been used in at least 45 days, choose **Make inactive**\.