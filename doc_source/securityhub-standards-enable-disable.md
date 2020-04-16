# Disabling or enabling a security standard<a name="securityhub-standards-enable-disable"></a>

You can disable or enable each security standard\.

Remember that Security Hub is regional\. When you enable or disable a security standard, it is enabled or disabled only in the current Region, or in the Region that you specify in an API request\.

When you disable a security standard, the following occurs\.
+ The checks for its controls are no longer performed
+ No additional findings are generated for its controls
+ The related AWS Config rules that Security Hub created are removed

When you enable a security standard, all of the controls for that standard are enabled by default\. You can then disable individual controls\. See [Disabling and enabling individual controls](securityhub-standards-enable-disable-controls.md)\.

## Disabling a security standard \(Console\)<a name="securityhub-standard-disable-console"></a>

On the **Security standards** page, each enabled standard includes an option to disable the standard\.

**To disable a standard**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to disable the standard\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard you want to disable, choose **Disable**\.

## Disabling a security standard \(API\)<a name="securityhub-standard-disable-api"></a>

To disable a security standard programmatically, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchDisableStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchDisableStandards.html) operation\.

## Enabling a security standard \(Console\)<a name="securityhub-standard-enable-console"></a>

On the **Security standards** page, each disabled standard includes an option to enable the standard\.

**To enable a security standard**

1. Make sure that you have enabled AWS Config in the master account and all of the member accounts\. See [AWS Config requirements for running security checks](securityhub-standards-awsconfigrules.md)\.

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to disable the standard\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard you want to enable, choose **Enable**\.

## Enabling a security standard \(API\)<a name="securityhub-standard-enable-api"></a>

To enable a security standard programmatically, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchEnableStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchEnableStandards.html) operation\.