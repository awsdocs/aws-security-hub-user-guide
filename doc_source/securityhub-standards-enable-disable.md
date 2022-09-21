# Disabling or enabling a security standard<a name="securityhub-standards-enable-disable"></a>

You can disable or enable each supported security standard in Security Hub\. Some security standards are enabled by default, but you can opt out of auto\-enabled standards\.

Security Hub is Regional\. When you enable or disable a security standard, it is enabled or disabled only in the current Region or in the Regions that you specify\.

When you disable a security standard, the following occurs:
+ The checks for its controls are no longer performed\.
+ No additional findings are generated for its controls\.
+ Existing findings are archived automatically after three to five days \(note that this is best effort and not guaranteed\)\.
+ The related AWS Config rules that Security Hub created are removed\.

  This normally occurs within a few minutes after you disable the standard, but might take longer\.

  If the first request to delete the AWS Config rules fails, then Security Hub retries every 12 hours\. However, if you disabled Security Hub or you do not have any other standards enabled, then Security Hub cannot retry the request, meaning that it cannot delete the AWS Config rules\. If this occurs, and you need to have AWS Config rules removed, contact AWS Support\.

Before you enable any security standards, make sure that you have enabled AWS Config and configured resource recording\. See [Enabling and configuring AWS Config](securityhub-prereq-config.md)\.

When you enable a security standard, all of the controls for that standard are enabled by default\. You can then disable individual controls\. See [Disabling and enabling individual controls](securityhub-standards-enable-disable-controls.md)\.

When you enable Security Hub, Security Hub calculates the initial security score for a standard within 30 minutes after your first visit to the **Summary** page or **Security standards** page on the Security Hub console\. Scores are only generated for standards that are enabled when you visit those pages\. In addition, AWS Config resource recording must be configured for scores to appear\. After first\-time score generation, Security Hub updates the security score every 24 hours\. Security Hub displays a timestamp to indicate when a security score was last updated\. To view a list of standards that are currently enabled, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html) API operation\.

**Note**  
It can take up to 24 hours for first\-time security scores to be generated in the China Regions and AWS GovCloud \(US\) Region\.

## Auto\-enabled security standards<a name="securityhub-auto-enabled-standards"></a>

Security Hub automatically enables default security standards for new accounts\. In addition, if you use the integration with AWS Organizations, Security Hub automatically enables default security standards for new member accounts\. You can opt of auto\-enabled standards\.

Currently, the default security standards that are automatically enabled are the AWS Foundational Security Best Practices \(FSBP\) standard and the Center for Internet Security \(CIS\) v1\.2\.0 AWS Foundations Benchmark\.

### Opt out of auto\-enabled standards<a name="Opt-out-of-auto-enabled-standards"></a>

The following opt\-out steps apply only if you use the integration with AWS Organizations\. If you do not use this integration, you can opt out of a default standard when you first enable Security Hub, or you can follow the steps for [disabling a standard](#securityhub-standard-disable-console)\.

**To opt out of auto\-enabled standards \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Log into the administrator account\.

1. On the Security Hub navigation bar, choose **Settings**\.

1. On the **Accounts** tab, turn off **Auto\-enable standards**\.

**To opt out of auto\-enabled standards \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateOrganizationConfiguration.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateOrganizationConfiguration.html) operation from the Security Hub administrator account\. The default value for the `AutoEnabledStandards` parameter is equal to `DEFAULT`\. To opt out of auto\-enabled standards in new member accounts, set `AutoEnableStandards` equal to `NONE`\.
+ **AWS CLI** – At the command line, run the `update-organization-configuration` command\.

  ```
  aws securityhub update-organization-configuration --auto-enable-standards
  ```

## Disabling a security standard<a name="securityhub-standard-disable-console"></a>

On the **Security standards** page, each enabled standard includes an option to disable the standard\. Follow these steps to disable a standard\.

**To disable a security standard \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to disable the standard\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard you want to disable, choose **Disable**\.

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

## Enabling a security standard<a name="securityhub-standard-enable-console"></a>

On the **Security standards** page, each disabled standard includes an option to enable the standard\. Follow these steps to enable a standard\.

**To enable a security standard \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to enable the standard\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard you want to enable, choose **Enable**\.

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