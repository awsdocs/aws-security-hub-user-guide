# Managing administrator and member accounts<a name="securityhub-accounts"></a>

An administrator account can view data from and manage configuration for its member accounts\. The administrator\-member relationship is established differently based on whether the accounts belong to an organization in AWS Organizations\.

If you are integrated with Organizations, the organization management account designates the Security Hub administrator account\. See [Designating a Security Hub administrator account](designate-orgs-admin-account.md)\. The Security Hub administrator account automatically has access to all of the accounts in the organization\. The Security Hub administrator account determines which organization accounts to enable as member accounts\. See [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md)\. These member accounts cannot disassociate themselves from the administrator account\.

If you are not integrated with Organizations, member accounts accept an invitation from an administrator account\. The Security Hub administrator account for an organization can also invite member accounts that are not part of the organization\. See [Managing member accounts by invitation](account-management-manual.md)\. Accounts that are added by invitation can disassociate themselves from their administrator account\.

**Topics**
+ [Effects of an administrator\-member relationship](accounts-admin-member-relationship.md)
+ [Restrictions and recommendations](securityhub-account-restrictions-recommendations.md)
+ [Making the transition to AWS Organizations for account management](accounts-transition-to-orgs.md)
+ [Allowed actions for accounts](securityhub-accounts-allowed-actions.md)
+ [Designating a Security Hub administrator account](designate-orgs-admin-account.md)
+ [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md)
+ [Managing member accounts by invitation](account-management-manual.md)
+ [Effect of account actions on Security Hub data](securityhub-data-retention.md)