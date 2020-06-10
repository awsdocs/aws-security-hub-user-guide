# Master and member accounts in AWS Security Hub<a name="securityhub-accounts"></a>

You can invite other AWS accounts to enable AWS Security Hub and become associated with your AWS account\. If the owner of the account that you invite enables Security Hub and then accepts the invitation, your account is designated as the *master* Security Hub account, and the invited accounts become associated as *member* accounts\.

When the invited account accepts the invitation, permission is granted to the master account to view the findings from the member account\. The master account can also perform actions on findings in a member account\.

## Restrictions on master and member accounts<a name="securityhub-master-member-restrictions"></a>

Security Hub supports up to 1000 member accounts per master account per Region\.

The master\-member account association is created only in the Region that the invitation was sent from\. You must enable Security Hub in each Region that you want to use it in, and then invite each account to associate as a member account in each Region\.

An account cannot be a Security Hub master account and member account at the same time\.

An account can accept only one Security Hub membership invitation\. Accepting a membership invitation is optional\.

## Coordinating master accounts across services<a name="securityhub-coordinate-masters"></a>

Security Hub aggregates findings from various AWS services, such as Amazon GuardDuty, Amazon Inspector, and Amazon Macie\. Security Hub also allows users to pivot from a GuardDuty finding to start an investigation in Amazon Detective\.

However, the master\-member relationships that you set up in these other services do not automatically apply to Security Hub\. Security Hub recommends that you use the same account as the master account for all of these services\. This master account should be an account that is responsible for security tools\.

For example, a user from GuardDuty master account A can see findings for GuardDuty member accounts B and C on the GuardDuty console\. If account A then enables Security Hub, users from account A do *not* automatically see GuardDuty findings for accounts B and C in Security Hub\. There must also be a Security Hub master\-member relationship for these accounts\. To do this, first enable Security Hub in all three accounts \(A, B, and C\)\. Next, make account A the Security Hub master account and invite accounts B and C to become Security Hub member accounts\.

## Designating master and member accounts on the Security Hub console<a name="securityhub-become-console"></a>

In Security Hub, your account becomes the master account when the account that you invite accepts your invitation\. When you accept an invitation from another account, your account becomes a member account\. If your account is the master account, you cannot accept an invitation to become a member account\.

Use the following procedures to add an account, invite an account, or accept an invitation from another account\.
+ Procedure 1: Adding an account
+ Procedure 2: Inviting an account
+ Procedure 3: Accepting an invitation

**Procedure 1: Adding an account**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the left pane, choose **Settings**\.

1. On the **Settings page** choose **Accounts**, choose **Add accounts**, and then do one of the following:

1. Under **Enter accounts**, enter the **Account ID** of the account to add, then choose **Add**\.

   To add more accounts, enter the account ID and then choose **Add** for each account\.

   You can add multiple accounts at the same time by using a comma\-separated values \(CSV\) file\. Add the account ID and email address for each account to add, and then choose **Upload list \(\.csv\)** to bulk\-add accounts\.
**Important**  
In your \.csv list, accounts must appear one per line\. The first line of the \.csv file must contain the following header, as shown in the following example: **Account ID,Email**\. Each subsequent line must contain a valid account ID and email address for the account to add\. Separate the account ID and email address with a comma\.  

   ```
   Account ID,Email
   111111111111,user@example.com
   ```

1. After you finish adding accounts, choose **Add**\. Then in the **Accounts to be added** section, choose **Next**\.

**Procedure 2: Inviting an account**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, under **Settings**, choose **Accounts**\. 

1. For the account to invite, choose **Invite** in the **Status** column\.

1. In the **Invitation to Security Hub** dialog box, choose **Invite**\.

   The value in the **Status** column for the invited account changes to **Invited**\.

**Procedure 3: Accepting an invitation**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Do one of the following:
   + If Security Hub isn't enabled, on the Security Hub first\-run experience page, in the **AWS Security Hub Setup** section, choose **Enable Security Hub**\. On the **Welcome to AWS Security Hub** page, choose **Enable AWS Security Hub**\. Back on the first\-run experience page, choose **Go to Security Hub**\.

     After Security Hub is enabled, choose **Settings**, then choose **Accounts**\. Locate the invitation to accept\. Use the **Accept** widget and the **Accept invitation** button to accept the membership invitation\.
**Important**  
You must enable Security Hub before you can accept a membership invitation\.
   + If Security Hub is already enabled, use the **Accept** widget and the **Accept invitation** button to accept the membership invitation\.

   After you accept the invitation, your account becomes a Security Hub member account\. The account used to send the invitation becomes the Security Hub master account\.  The master account user can now view Security Hub aggregated findings for your member account\.

## Designating master and member accounts through Security Hub API operations<a name="securityhub-become-api"></a>

You can also designate Security Hub master and member accounts with operations in the Security Hub API\. Use the following Security Hub API operations in the order listed to create master and member accounts\.

**To designate a master account and send invitations to become a member account**

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateMembers.html) using the credentials of the account that has Security Hub enabled\. This is the account that you want to be the master Security Hub account\.

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_InviteMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_InviteMembers.html) using the master account\.

Use these operations to enable Security Hub and then accept an invitation\. Use the credentials for the account you invited to become the member account\.

**To enable Security Hub for the member accounts and accept the invitation**

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableSecurityHub.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableSecurityHub.html) for each account that you invited\. Security Hub must be enabled in the account before the account owner can accept the invitation\.

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AcceptInvitation.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AcceptInvitation.html) for each account you invited to accept your invitation\.

## Accounts and data retention in Security Hub<a name="securityhub-data-retention"></a>

When you perform these actions on accounts, it has the following effects on the Security Hub data\.

### Security Hub disabled<a name="securityhub-effects-disable-securityhub"></a>

When you disable Security Hub for an account, either master or member, it is disabled only for that account in the AWS Region that is selected when you disable it\.

You must disable Security Hub separately in each Region where you enabled it\.

### Security Hub disabled for master account<a name="securityhub-effect-disable-master"></a>

When you disable Security Hub for a master account, the default company and product settings are removed\.

Integrations with Macie, GuardDuty, and Amazon Inspector are removed\.

Enabled security standards are disabled\.

No new findings are generated for the master account while Security Hub is disabled\. Existing findings are deleted after 90 days\.

Other Security Hub data and settings, including member account associations, custom actions, insights, and subscriptions to third\-party products are not removed\.

If you enable Security Hub again later, the default company and product settings, security standards that you had enabled, and integrations with AWS services are restored\. This allows you to use Security Hub as you did before you disabled it without having to reconfigure it\.

### Security Hub disabled for member account<a name="securityhub-effects-disable-member"></a>

When you disable Security Hub for a member account, no new findings are generated for the member account in the Region, but the master account can still view existing findings in the member account\.

Findings are deleted 90 days after the last update\. If there are no updates, then findings are deleted 90 days after they are created\.

The relationship of master and member account is maintained\. You can enable Security Hub in the member account and use it as you did before you disabled it, except that there are no findings for the period of time when Security Hub was not enabled\.

### Member account disassociated from master account<a name="securityhub-effects-member-disassociation"></a>

When a member account is disassociated from the master account, the master account loses permission to view findings in the member account\.

Security Hub continues to run in both accounts\.

Custom settings or integrations defined for the master account are not applied to findings from the former member account\. For example, after the accounts are disassociated, a custom action in the master account used as the event pattern in a CloudWatch Events rule cannot be used in the member account\.

### AWS account deleted or suspended<a name="securityhub-effects-account-deletion"></a>

When your AWS account is deleted or suspended, all Security Hub–related data for that account is deleted after 90 days\. The data cannot be retrieved after it is deleted\.

To retain findings for more than 90 days, you can archive them or use a custom action with a CloudWatch Events rule to store findings in your Amazon S3 bucket\.