# Master and member accounts in AWS Security Hub<a name="securityhub-accounts"></a>

You can invite other AWS accounts to enable AWS Security Hub and become associated with your AWS account\. If the owner of the account that you invite enables Security Hub and then accepts the invitation, your account is designated as the *master* Security Hub account\. The invited accounts become associated as *member* accounts\.

When the invited account accepts the invitation, permission is granted to the master account to view the findings from the member account\. The master account can also perform actions on findings in a member account\.

**Topics**
+ [Restrictions and recommendations](securityhub-account-restrictions-recommendations.md)
+ [Adding and inviting member accounts](securityhub-accounts-add-invite.md)
+ [Responding to an invitation to be a member account](securityhub-invitation-respond.md)
+ [Disassociating member accounts](securityhub-disassociate-members.md)
+ [Deleting member accounts](securityhub-delete-member-accounts.md)
+ [Disassociating from your master account](securityhub-disassociate-from-master.md)
+ [Effect of account actions on Security Hub data](securityhub-data-retention.md)