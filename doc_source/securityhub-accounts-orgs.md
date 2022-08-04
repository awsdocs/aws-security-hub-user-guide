# Managing member accounts that belong to an organization<a name="securityhub-accounts-orgs"></a>

For organization accounts, the Security Hub administrator account can perform the following actions\.
+ Automatically treat *new* organization accounts as Security Hub member accounts as they are added to the organization\.
+ Treat *existing* organization accounts as Security Hub member accounts\.
+ Disassociate and delete member accounts that belong to the organization\.

To ensure that the Security Hub administrator account has the required permissions to manage the organization accounts, attach the following managed policies to the associated IAM principal\.
+ [`AWSSecurityHubFullAccess`](security-iam-awsmanpol.md#security-iam-awsmanpol-awssecurityhubfullaccess)
+ [`AWSSecurityHubOrganizationsAccess`](security-iam-awsmanpol.md#security-iam-awsmanpol-awssecurityhuborganizationsaccess)

If the Security Hub administrator account has not turned on the option to automatically enable new organization accounts, then the **Accounts** page displays a message at the top of the page\. The message contains an **Enable** option\.

**Note**  
Choosing **Enable** from this message impacts newly added and existing organization accounts\. Turning on **Auto\-enable accounts** only impacts newly added organization accounts\. For more information, see [Automatically enabling new organization accounts](accounts-orgs-auto-enable.md)\.

When you choose **Enable**, Security Hub treats all of the existing organization accounts as member accounts, and automatically treats new accounts as member accounts as they are added to the organization\.

For organization accounts that do not have Security Hub enabled, enables Security Hub, and enables the CIS AWS Foundations Benchmark standard and the AWS Foundational Best Practices standard\. For organization accounts that already have Security Hub enabled, Security Hub does not make any other changes to those accounts\. It does not change their enabled standards or controls\.

**Topics**
+ [Automatically enabling new organization accounts](accounts-orgs-auto-enable.md)
+ [Enabling member accounts from your organization](orgs-accounts-enable.md)
+ [Disassociating member accounts from your organization](accounts-orgs-disassociate.md)