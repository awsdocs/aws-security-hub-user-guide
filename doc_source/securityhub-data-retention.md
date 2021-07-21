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

## Account is suspended<a name="securityhub-effects-account-suspended"></a>

When an account is suspended in AWS, the account loses permission to view their findings in Security Hub\. No new findings are generated for that account\. The administrator account for a suspended account can view the existing account findings\.

For an organization account, the member account status can also change to **Account Suspended**\. This happens if the account is suspended at the same time that the administrator account attempts to enable the account\. The administrator account for an **Account Suspended** account cannot view findings for that account\.

Otherwise, the suspended status does not affect the member account status\.

After 90 days, the account is either terminated or reactivated\. When the account is reactivated, its Security Hub permissions are restored\. If the member account status is **Account Suspended**, the administrator account must enable the account manually\.

## Account is closed<a name="securityhub-effects-account-deletion"></a>

When an AWS account is closed, Security Hub responds to the closure as follows\.

 AWS retains the policy data for the account for 90 days from the effective date of the administrator account closure\. At the end of the 90 day period, AWS permanently deletes all policy data for the account\. 
+  To retain findings for more than 90 days, you can archive the policies\. You can also use a custom action with an EventBridge rule to store the findings in an S3 bucket\. 
+  As long as AWS retains the policy data, when you reopen the closed account, AWS reassigns the account as the service administrator and recovers the service policy data for the account\. 
+  For more information, see [Closing an account](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/close-account.html)\. 

**Important**  
 For customers in the AWS GovCloud \(US\) Regions:   
 Before closing your account, back up and then delete your policy data and other account resources\. You will no longer have access to them after you close the account\. 