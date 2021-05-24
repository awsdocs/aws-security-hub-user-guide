# Effect of account actions on Security Hub data<a name="securityhub-data-retention"></a>

These account actions have the following effects on AWS Security Hub data\.

## Security Hub disabled<a name="securityhub-effects-disable-securityhub"></a>

When you disable Security Hub for an account, it is disabled only for that account in the AWS Region that is selected when you disable it\.

You must disable Security Hub separately in each Region where you enabled it\.

No new findings are generated for the administrator account while Security Hub is disabled\. Existing findings are deleted after 90 days\.

Integrations with Amazon Macie, Amazon GuardDuty, and Amazon Inspector are removed\.

Other Security Hub data and settings, including custom actions, insights, and subscriptions to third\-party products are not removed\.

Enabled security standards are disabled\.

## Member account disassociated from administrator account<a name="securityhub-effects-member-disassociation"></a>

When a member account is disassociated from the administrator account, the administrator account loses permission to view findings in the member account\.

Security Hub continues to run in both accounts\.

Custom settings or integrations that are defined for the administrator account are not applied to findings from the former member account\. For example, after the accounts are disassociated, you might have a custom action in the administrator account used as the event pattern in an Amazon EventBridge rule\. However, this custom action cannot be used in the member account\.

## Member account is removed from an organization<a name="securityhub-effects-member-leaves-org"></a>

When a member account is removed from an organization, the administrator account loses permission to view findings in the member account\.

Security Hub continues to run in both accounts\.

In the **Accounts** list for the administrator account, the account has a status of **Disassociated**\.

## AWS account deleted or suspended<a name="securityhub-effects-account-deletion"></a>

When an AWS account is deleted or suspended, all Security Hub related data for that account is deleted after 90 days\. The data cannot be retrieved after it is deleted\.

To retain findings for more than 90 days, you can archive them\. You can also use a custom action with an EventBridge rule to store findings in an Amazon S3 bucket\.