# Disabling AWS Security Hub<a name="securityhub-disable"></a>

To disable AWS Security Hub, you can use the Security Hub console or the Security Hub API\.

When you disable Security Hub for an account, it is disabled only in the current Region\. No new findings are processed for the account in that Region\.

The following also occurs\.
+ After 90 days, your existing findings and insights and any Security Hub configuration settings are deleted and cannot be recovered\.

  If you want to save your existing findings, you must export them before you disable Security Hub\. For more information, see [Effect of account actions on Security Hub data](securityhub-data-retention.md)\.
+ Any enabled standards are disabled\.

## Disabling Security Hub \(console\)<a name="securityhub-disable-console"></a>

You can disable Security Hub from the AWS Management Console\.

**To disable Security Hub \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**\.

1. On the **Settings** page, choose **General**\.

1. Under **Disable AWS Security Hub**, choose **Disable AWS Security Hub**\. Then choose **Disable AWS Security Hub** again\.

## Disabling Security Hub \(Security Hub API, AWS CLI\)<a name="securityhub-disable-api"></a>

To disable Security Hub, you can use an API call or the AWS Command Line Interface\.

**To disable Security Hub \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableSecurityHub.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableSecurityHub.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/disable-security-hub.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/disable-security-hub.html) command\.

  ```
  aws securityhub disable-security-hub
  ```