# Making the transition to AWS Organizations for account management<a name="accounts-transition-to-orgs"></a>

You might have an existing master account with member accounts that accepted a manual invitation\. If you are enrolled in AWS Organizations, use the following steps to use Organizations to enable and manage member accounts instead of using the manual invitation process:

1. [Designate a delegated administrator for your organization\.](#account-transition-delegated-administrator)

1. [Enable organization accounts under the delegated administrator\. Existing member accounts are enabled automatically\.](#account-transition-enable-members)

The following diagram shows an overview of the master and member account structure before the transition, the configuration in Organizations, and the account structure after the transition\.

![\[Diagram that shows a master account that has member accounts by invitation. In Organizations, the master account becomes the delegated administrator for AWS Security Hub. The organization accounts are then member accounts by organization.\]](http://docs.aws.amazon.com/securityhub/latest/userguide/images/diagram_account_transition.png)

## Designate a delegated administrator<a name="account-transition-delegated-administrator"></a>

Your organization management account designates the delegated administrator account for Security Hub\. See [Designating a Security Hub administrator account](designate-orgs-admin-account.md)\.

To make the transition simpler, Security Hub recommends that you choose the current master account as the Security Hub delegated administrator account\. This is because a member account cannot belong to more than one master account\. The delegated administrator cannot enable any organization accounts that are member accounts under another master account\.

## Enable organization accounts as member accounts<a name="account-transition-enable-members"></a>

The delegated administrator account determines which organization accounts to enable as member accounts\. See [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md)\.

On the **Accounts** page, the delegated administrator account sees all of the accounts in the organization\. Organization accounts have a type of **By organization**, even if they were previously member accounts by invitation\.

If the delegated administrator account was already a Security Hub master account, all of their existing member accounts are enabled automatically\. Existing member accounts that do not belong to the organization have a type of **By invitation**\.

The **Accounts** page also provides an option to automatically enable new accounts as they are added to an organization\. See [Automatically enabling new organization accounts](accounts-orgs-auto-enable.md)\. The option is initially turned off \(**Auto\-enable is off**\)\.

Until you enable that option, the **Accounts** page displays a message that contains an **Enable** button\. When you choose **Enable**, Security Hub performs the following actions:
+ Enables all of the organization accounts, except for accounts that are member accounts under another master account\.

  Before the administrator account can enable those accounts, they must be disassociated from the other master account\. See [Disassociating member accounts](securityhub-disassociate-members.md)\.
+ Toggles the setting to enable new accounts automatically \(**Auto\-enable is on**\)\.