# Using AWS Organizations to manage accounts<a name="securityhub-prereq-orgs"></a>

To help automate and streamline management of accounts, Security Hub strongly recommends that you enable AWS Organizations\.

If you have Organizations enabled, then Security Hub automatically detects new accounts as they are added to your organization\.

For information on setting up Organizations, see [Creating and managing an organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org.html) in the *AWS Organizations User Guide*\.

After you set up your organization, your organization management account designates the Security Hub administrator account\. See [Designating a Security Hub administrator account](designate-orgs-admin-account.md)\. The Security Hub administrator account then enables and manages other organization accounts as Security Hub member accounts\. See [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md)\.