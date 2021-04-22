# Making the transition to AWS Organizations for account management<a name="accounts-transition-to-orgs"></a>

You might have an existing administrator account with member accounts that accepted a manual invitation\. If you are enrolled in AWS Organizations, use the following steps to use Organizations to enable and manage member accounts instead of using the manual invitation process:

1. [Designate a Security Hub administrator account for your organization\.](#account-transition-delegated-administrator)

1. [Enable organization accounts under the administrator account\. Existing member accounts are enabled automatically\.](#account-transition-enable-members)

The following diagram shows an overview of the administrator and member account structure before the transition, the configuration in Organizations, and the account structure after the transition\.

![\[Diagram that shows an administrator account that has member accounts by invitation. In Organizations, the administrator account becomes the Security Hub administrator account for the organization. The organization accounts are then member accounts by organization.\]](http://docs.aws.amazon.com/securityhub/latest/userguide/images/diagram_account_transition.png)

## Designate a Security Hub administrator account for your organization<a name="account-transition-delegated-administrator"></a>

Your organization management account designates the Security Hub administrator account for your organization\. See [Designating a Security Hub administrator account](designate-orgs-admin-account.md)\.

To make the transition simpler, Security Hub recommends that you choose the current administrator account as the Security Hub administrator account for the organization\. This is because a member account cannot belong to more than one administrator account\. The administrator account for the organization cannot enable any organization accounts that are member accounts under another administrator account\.

## Enable organization accounts as member accounts<a name="account-transition-enable-members"></a>

The administrator account for the organization determines which organization accounts to enable as member accounts\. See [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md)\.

On the **Accounts** page, the administrator account sees all of the accounts in the organization\. Organization accounts have a type of **By organization**, even if they were previously member accounts by invitation\.

If the administrator account for the organization was already a Security Hub administrator account, all of their existing member accounts are enabled automatically\. Existing member accounts that do not belong to the organization have a type of **By invitation**\.

The **Accounts** page also provides an option to automatically enable new accounts as they are added to an organization\. See [Automatically enabling new organization accounts](accounts-orgs-auto-enable.md)\. The option is initially turned off \(**Auto\-enable is off**\)\.

Until you enable that option, the **Accounts** page displays a message that contains an **Enable** button\. When you choose **Enable**, Security Hub performs the following actions:
+ Enables all of the organization accounts, except for accounts that are member accounts under another administrator account\.

  Before the administrator account can enable those accounts, they must be disassociated from the other administrator account\. See [Disassociating member accounts](securityhub-disassociate-members.md)\.
+ Toggles the setting to enable new accounts automatically \(**Auto\-enable is on**\)\.