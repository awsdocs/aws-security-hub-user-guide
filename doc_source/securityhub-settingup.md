# Setting up AWS Security Hub<a name="securityhub-settingup"></a>

Whether an account needs to enable AWS Security Hub manually depends on how the accounts are managed\.

You can use the integration with AWS Organizations, or you can manage accounts manually\.

In both cases, you set up Security Hub and manage accounts separately in each Region\. All accounts also must enable AWS Config, which is needed for the security checks against security controls\. See [Enabling and configuring AWS Config](securityhub-prereq-config.md)\.

**Organizations integration**  
If you use the integration with AWS Organizations, then most organization accounts have Security Hub enabled automatically\.  
The organization management account chooses a Security Hub administrator account\. Security Hub is enabled automatically for the chosen account\. See [Designating a Security Hub administrator account](designate-orgs-admin-account.md)\.  
The Security Hub administrator account enables organization accounts as member accounts\. Those organization accounts also have Security Hub enabled automatically\. See [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md)\.  
The only organization account for which Security Hub is not enabled automatically is the organization management account\. The organization management account does not need to enable Security Hub before it designates the Security Hub administrator account\. The organization management account must enable Security Hub before it is enabled as a member account\.

**Manual account management**  
Accounts that are not managed using the Organizations integration must enable Security Hub manually\.  
The Security Hub administrator\-member relationship is established when the member account accepts an invitation from the administrator account\. See [Managing member accounts by invitation](account-management-manual.md)\.

**Contents**
+ [Enabling Security Hub manually](securityhub-enable.md)
  + [Attaching the required IAM policy to the IAM identity](securityhub-enable.md#securityhub-enable-attach-policy)
  + [Enabling Security Hub \(console\)](securityhub-enable.md#securityhub-enable-console)
  + [Enabling Security Hub \(Security Hub API, AWS CLI\)](securityhub-enable.md#securityhub-enable-api)
  + [Enabling Security Hub \(Multi\-account script\)](securityhub-enable.md#securityhub-enable-multiaccount-script)
+ [Service\-linked role assigned to Security Hub](security-hub-enable-slr.md)