# Managing member accounts by invitation<a name="account-management-manual"></a>

AWS Security Hub also supports a manual invitation process\. You use the manual process if you do not use AWS Organizations\.

You also use this process for accounts that do not belong to your organization\. For example, you might not include a test account in your organization\. Or you might want to consolidate accounts from multiple organizations under a single Security Hub administrator account\. The Security Hub administrator account must send invitations to accounts that belong to other organizations\.

On the **Accounts** tab of the **Settings** page, accounts that were added by invitation have **Type** set to **By invitation**\.

If you do not use Organizations at all, then an account becomes an administrator account when a member account accepts an invitation\.

**Topics**
+ [Adding and inviting member accounts](securityhub-accounts-add-invite.md)
+ [Responding to an invitation to be a member account](securityhub-invitation-respond.md)
+ [Disassociating member accounts](securityhub-disassociate-members.md)
+ [Deleting member accounts](securityhub-delete-member-accounts.md)
+ [Disassociating from your administrator account](securityhub-disassociate-from-admin.md)