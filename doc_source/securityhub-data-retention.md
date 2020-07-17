# Effect of account actions on Security Hub data<a name="securityhub-data-retention"></a>

When you perform these actions on accounts, it has the following effects on the AWS Security Hub data\.

## Security Hub disabled<a name="securityhub-effects-disable-securityhub"></a>

When you disable Security Hub for an account, either master or member, it is disabled only for that account in the AWS Region that is selected when you disable it\.

You must disable Security Hub separately in each Region where you enabled it\.

## Security Hub disabled for master account<a name="securityhub-effect-disable-master"></a>

When you disable Security Hub for a master account, the default company and product settings are removed\.

Integrations with Macie, GuardDuty, and Amazon Inspector are removed\.

Enabled security standards are disabled\.

No new findings are generated for the master account while Security Hub is disabled\. Existing findings are deleted after 90 days\.

Other Security Hub data and settings, including member account associations, custom actions, insights, and subscriptions to third\-party products are not removed\.

If you enable Security Hub again later, the default company and product settings, security standards that you had enabled, and integrations with AWS services are restored\. This allows you to use Security Hub as you did before you disabled it without having to reconfigure it\.

## Security Hub disabled for member account<a name="securityhub-effects-disable-member"></a>

When you disable Security Hub for a member account, no new findings are generated for the member account in the Region\. But the master account can still view existing findings in the member account\.

Findings are deleted 90 days after the last update\. If there are no updates, then findings are deleted 90 days after they are created\.

The relationship of master and member account is maintained\. You can enable Security Hub in the member account and use it as you did before you disabled it\. The only difference is that no findings are available for the period of time when Security Hub was not enabled\.

## Member account disassociated from master account<a name="securityhub-effects-member-disassociation"></a>

When a member account is disassociated from the master account, the master account loses permission to view findings in the member account\.

Security Hub continues to run in both accounts\.

Custom settings or integrations that are defined for the master account are not applied to findings from the former member account\. For example, after the accounts are disassociated, you might have a custom action in the master account used as the event pattern in a CloudWatch Events rule\. However, this custom action cannot be used in the member account\.

## AWS account deleted or suspended<a name="securityhub-effects-account-deletion"></a>

When your AWS account is deleted or suspended, all Security Hub–related data for that account is deleted after 90 days\. The data cannot be retrieved after it is deleted\.

To retain findings for more than 90 days, you can archive them\. You can also use a custom action with a CloudWatch Events rule to store findings in your Amazon S3 bucket\.