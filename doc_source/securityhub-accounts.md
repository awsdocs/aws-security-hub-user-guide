# Managing master and member accounts<a name="securityhub-accounts"></a>

An AWS Security Hub master account can view data from and manage configuration for its member accounts\. The Security Hub master\-member relationship is established differently based on whether the accounts belong to an organization in AWS Organizations\.

**Note**  
The China \(Beijing\) and China \(Ningxia\) Regions do not support the integration with Organizations\.

If you are integrated with Organizations, the organization management account designates the Security Hub administrator account, which becomes the master account\. See [Designating a Security Hub administrator account](designate-orgs-admin-account.md)\. The Security Hub administrator account automatically has access to all of the accounts in the organization\. The Security Hub administrator account determines which accounts in the organization to enable as member accounts\. See [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md)\. These member accounts cannot disassociate themselves from the Security Hub administrator account\.

If you are not integrated with Organizations, member accounts accept an invitation from a master account\. A Security Hub administrator account for an organization can also invite member accounts that are not part of the organization\. See [Managing member accounts that are not in an organization](account-management-manual.md)\. Accounts that are added by invitation can disassociate themselves from their master account\.

**Topics**
+ [Restrictions and recommendations](securityhub-account-restrictions-recommendations.md)
+ [Allowed actions for accounts](securityhub-accounts-allowed-actions.md)
+ [Designating a Security Hub administrator account](designate-orgs-admin-account.md)
+ [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md)
+ [Managing member accounts that are not in an organization](account-management-manual.md)
+ [Effect of account actions on Security Hub data](securityhub-data-retention.md)