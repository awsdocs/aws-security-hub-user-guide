# Disabling AWS Security Hub<a name="securityhub-disable"></a>

You can use the AWS Security Hub console or the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableSecurityHub.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableSecurityHub.html) operation of the Security Hub API to disable Security Hub\. If you disable Security Hub, your existing findings and insights and any Security Hub configuration settings are deleted after 90 days and can't be recovered\. Any enabled standards are disabled, and your master and member account relationships are removed\. If you want to save your existing findings, you must export them before you disable Security Hub\. For more information, see [Accounts and Data Retention in Security Hub](securityhub-accounts.md#securityhub-data-retention)\.

**To disable Security Hub \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, under **Settings**, choose **General**\.

1. Choose **Disable AWS Security Hub**, then choose **Disable AWS Security Hub** again\.

   When you disable Security Hub for an account, it is disabled only in the current Region\. No new findings are processed for the account in that Region\.