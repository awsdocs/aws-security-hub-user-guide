# Disabling or enabling a security standard<a name="securityhub-standards-enable-disable"></a>

You can disable or enable each security standard\.

Remember that Security Hub is Regional\. When you enable or disable a security standard, it is enabled or disabled only in the current Region or in the Region that you specify in an API request\.

When you disable a security standard, the following occurs:
+ The checks for its controls are no longer performed\.
+ No additional findings are generated for its controls\.
+ Existing findings are archived automatically after three days\.
+ The related AWS Config rules that Security Hub created are removed\.

  This normally occurs within a few minutes after you disable the standard, but might take longer\.

  If the first request to delete the AWS Config rules fails, then Security Hub retries every 12 hours\. However, if you disabled Security Hub or you do not have any other standards enabled, then Security Hub cannot retry the request, meaning that it cannot delete the AWS Config rules\. If this occurs, and you need to have AWS Config rules removed, contact AWS Support\.

Before you enable any security standards, make sure that you have enabled AWS Config and configured resource recording\. See [Enabling and configuring AWS Config](securityhub-prereq-config.md)\.

When you enable a security standard, all of the controls for that standard are enabled by default\. You can then disable individual controls\. See [Disabling and enabling individual controls](securityhub-standards-enable-disable-controls.md)\.

When a standard is first enabled, Security Hub cannot calculate the initial aggregated security score until the standard status is `READY`\. After that, the initial security score is available within 24 hours\. To see the current status of the standard, use the `GetEnabledStandards` API operation\.

## Disabling a security standard \(console\)<a name="securityhub-standard-disable-console"></a>

On the **Security standards** page, each enabled standard includes an option to disable the standard\.

**To disable a standard**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to disable the standard\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard you want to disable, choose **Disable**\.

## Disabling a security standard \(Security Hub API, AWS CLI\)<a name="securityhub-standard-disable-api"></a>

To disable a security standard, you can use an API call or the AWS Command Line Interface\.

**To disable a security standard \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchDisableStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchDisableStandards.html) operation\. For each standard to disable, you provide the ARN of your subscription to the standard\. To get the subscription ARNs for your enabled standards, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-disable-standards.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-disable-standards.html) command\.

  ```
  aws securityhub batch-disable-standards --standards-subscription-arns <subscription ARN>
  ```

  **Example**

  ```
  aws securityhub batch-disable-standards --standards-subscription-arns "arn:aws:securityhub:us-west-1:123456789012:subscription/aws-foundational-security-best-practices/v/1.0.0"
  ```

## Enabling a security standard \(console\)<a name="securityhub-standard-enable-console"></a>

On the **Security standards** page, each disabled standard includes an option to enable the standard\.

**To enable a security standard \(console\)**

ß

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to enable the standard\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard you want to enable, choose **Enable**\.

## Enabling a security standard \(Security Hub API, AWS CLI\)<a name="securityhub-standard-enable-api"></a>

To enable a security standard, you can use an API call or the AWS Command Line Interface\.

**To enable a security standard \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchEnableStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchEnableStandards.html) operation\. To identify a standard to enable, you must provide the standard ARN\. To obtain the standard ARN, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandards.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-enable-standards.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-enable-standards.html) command\.

  ```
  aws securityhub batch-enable-standards --standards-subscription-requests '{"StandardsArn": "<standard ARN>"}'
  ```

  **Example**

  ```
  aws securityhub batch-enable-standards --standards-subscription-requests '{"StandardsArn":"arn:aws:securityhub:us-east-1::standards/aws-foundational-security-best-practices/v/1.0.0"}'
  ```