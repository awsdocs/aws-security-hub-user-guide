# Setting up AWS Security Hub<a name="securityhub-settingup"></a>

If you are integrated with AWS Organizations, accounts that belong to the organization do not need to enable Security Hub manually\.

The organization management account designates the Security Hub administrator account\. The Security Hub administrator account then has Security Hub enabled automatically\. The organization management account does not need to enable Security Hub\. See [Designating a Security Hub administrator account](designate-orgs-admin-account.md)\.

The Security Hub administrator account chooses the organization accounts to enable as member accounts\. Those accounts also have Security Hub enabled automatically\. See [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md)\. The exception to this is the organization management account\. The organization management account must enable Security Hub before the Security Hub administrator account enables the organization management account as a member account\.

An account that is not part of an organization must enable Security Hub manually\. The Security Hub administrator\-member relationship is then established through manual invitations that the administrator account sends to the member accounts\. See [Managing member accounts that are not in an organization](account-management-manual.md)\.

For both types of enablement, you need to enable AWS Config, which is needed for the security checks against security controls\. See [Enabling and configuring AWS Config](securityhub-prereq-config.md)\.

**Contents**
+ [Enabling Security Hub manually](securityhub-enable.md)
  + [Attaching the required IAM policy to the IAM identity](securityhub-enable.md#securityhub-enable-attach-policy)
  + [Enabling Security Hub \(console\)](securityhub-enable.md#securityhub-enable-console)
  + [Enabling Security Hub \(Security Hub API, AWS CLI\)](securityhub-enable.md#securityhub-enable-api)
  + [Enabling Security Hub \(Multi\-account script\)](securityhub-enable.md#securityhub-enable-multiaccount-script)
+ [Service\-linked role assigned to Security Hub](security-hub-enable-slr.md)