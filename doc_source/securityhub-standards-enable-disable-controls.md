# Disabling and Enabling Individual Controls<a name="securityhub-standards-enable-disable-controls"></a>

When you enable a standard, all of the controls for that standard are enabled by default\. You can then disable and enable specific controls within an enabled standard\.

When you disable a control, the following occurs\.
+ The check for the control is no longer performed\.
+ No additional findings are generated for that control\.
+ The related AWS Config rules that Security Hub created are removed\.

It can be useful to turn off standards checks for controls that are not relevant to your environment\. For example, if you use a single S3 bucket to log your CloudTrail logs, you can turn off controls related to CloudTrail logging in all accounts and Regions except for the account and Region where the centralized S3 bucket is located\. Disabling irrelevant controls reduces the number of irrelevant findings\. It also removes the failed check from the readiness score for the associated standard\.

Remember that Security Hub is regional\. When you disable or enable a control, it is disabled only in the current Region, or in the Region that you specify in an API request\.

Also, when you disable an entire standard \(See [Disabling or Enabling a Security Standard](securityhub-standards-enable-disable.md)\), Security Hub does not track which controls were disabled\. If you subsequently enable the standard again, all of the controls are enabled\.

## Disabling a Control \(Console\)<a name="securityhub-standard-control-disable-console"></a>

On the Security Hub console, each enabled control provides an option to disable that control\.

**To disable a control**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to disable the control\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard that you want to disable controls for, choose **View results**\.

1. Identify the control that you want to disable, then choose **Disable**\.

1. Enter a reason why you are disabling the control\. This can help others in your organization understand why the control is disabled\.

1. Choose **Disable**\.

## Enabling a Control \(Console\)<a name="securityhub-standard-control-enable-console"></a>

For a disabled control, **Disabled** is displayed next to the control title\.

To enable the control at any time, choose **Enable**\.

## Disabling or Enabling a Control \(API\)<a name="securityhub-standard-control-enable-disable-api"></a>

To enable or disable a control programmatically, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html) operation of the Security Hub API\.