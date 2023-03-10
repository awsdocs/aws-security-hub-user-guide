# Enabling and disabling security standards<a name="securityhub-standards-enable-disable"></a>

You can enable or disable each security standard that's available in Security Hub\. Some security standards are enabled automatically, but you can opt out of auto\-enabled standards\.

When you enable or disable a security standard, it is enabled or disabled only in the current AWS Region and AWS account\.

Before you enable any security standards, make sure that you have enabled AWS Config and configured resource recording\. Otherwise, Security Hub may not be able to generate findings for the controls that apply to the standard\. For more information, see [Enabling and configuring AWS Config](securityhub-prereq-config.md)\.

## Enabling a security standard<a name="securityhub-standard-enable-console"></a>

When you enable a security standard, all of the controls that apply to the standard are automatically enabled in it\. You can then choose to disable and re\-enable controls in any or all standards\. Disabling a control stops findings for the control from being generated, and the control is ignored when calculating security scores\.

When you enable Security Hub, Security Hub calculates the initial security score for a standard within 30 minutes after your first visit to the **Summary** page or **Security standards** page on the Security Hub console\. Scores are only generated for standards that are enabled when you visit those pages\. In addition, AWS Config resource recording must be configured for scores to appear\. After first\-time score generation, Security Hub updates the security score every 24 hours\. Security Hub displays a timestamp to indicate when a security score was last updated\. To view a list of standards that are currently enabled, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html) API operation\.

**Note**  
It can take up to 24 hours for first\-time security scores to be generated in the China Regions and AWS GovCloud \(US\) Region\.

Choose your preferred access method, and follow these steps to enable a standard\.

------
#### [ Security Hub console ]

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to enable the standard\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard you want to enable, choose **Enable**\. This also enables all controls within that standard\.

------
#### [ Security Hub API ]

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchEnableStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchEnableStandards.html)\.

1. Provide the Amazon Resource Name \(ARN\) of the standard that you want to enable\. To obtain the standard ARN, run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandards.html)\.

------
#### [ AWS CLI ]

1. Run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-enable-standards.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-enable-standards.html) command\.

1. Provide the Amazon Resource Name \(ARN\) of the standard that you want to enable\.

   ```
   aws securityhub batch-enable-standards --standards-subscription-requests '{"StandardsArn": "standard ARN"}'
   ```

   **Example**

   ```
   aws securityhub batch-enable-standards --standards-subscription-requests '{"StandardsArn":"arn:aws:securityhub:us-east-1::standards/aws-foundational-security-best-practices/v/1.0.0"}'
   ```

------

## Automatically enabled security standards<a name="securityhub-auto-enabled-standards"></a>

Security Hub automatically enables default security standards for new accounts\. In addition, if you use the integration with AWS Organizations, Security Hub automatically enables default security standards for new member accounts\. You can turn off auto\-enabled standards if you prefer to manually enable standards\.

Currently, the default security standards that are automatically enabled are the AWS Foundational Security Best Practices \(FSBP\) standard and the Center for Internet Security \(CIS\) AWS Foundations Benchmark v1\.2\.0\.

### Turning off automatically enabled standards<a name="Opt-out-of-auto-enabled-standards"></a>

The following steps apply only if you use the integration with AWS Organizations\. If you do not use this integration, you can turn off a default standard when you first enable Security Hub, or you can follow the steps for [disabling a standard](#securityhub-standard-disable-console)\.

------
#### [ Security Hub console ]

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

   Sign in using the credentials of the administrator account\.

1. On the Security Hub navigation bar, choose **Settings**\.

1. On the **Accounts** tab, turn off **Auto\-enable standards**\.

------
#### [ Security Hub API ]

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateOrganizationConfiguration.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateOrganizationConfiguration.html) from the Security Hub administrator account\.

1. To turn off auto\-enabled standards in new member accounts, set `AutoEnableStandards` equal to `NONE`\.

------
#### [ AWS CLI ]

1. Run the `update-organization-configuration` command\.

1. Include the `auto-enable-standards` parameter to turn off auto\-enabled standards\.

   ```
   aws securityhub update-organization-configuration --auto-enable-standards
   ```

------

## Disabling a security standard<a name="securityhub-standard-disable-console"></a>

When you disable a security standard, the following occurs:
+ All of the controls that apply to the standard are also disabled unless they are associated with another standard\.
+ Checks for the disabled controls are no longer performed, and no additional findings are generated for the disabled controls\.
+ Existing findings for disabled controls are archived automatically after three to five days \(note that this is best effort and not guaranteed\)\.
+ The AWS Config rules that Security Hub created for the disabled controls are removed\.

  This normally occurs within a few minutes after you disable the standard, but might take longer\.

  If the first request to delete the AWS Config rules fails, then Security Hub retries every 12 hours\. However, if you disabled Security Hub or you do not have any other standards enabled, then Security Hub cannot retry the request, meaning that it cannot delete the AWS Config rules\. If this occurs, and you need to have AWS Config rules removed, contact AWS Support\.

Choose your preferred access method, and follow the steps to disable a standard\. You can disable one or more standards in a single request\.

------
#### [ Security Hub console ]

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to disable the standard\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard you want to disable, choose **Disable**\.

------
#### [ Security Hub API ]

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchDisableStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchDisableStandards.html)\.

1. For each standard you want to disable, provide the standard subscription ARN\. To get the subscription ARNs for your enabled standards, run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html)\.

------
#### [ AWS CLI ]

1. Run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-disable-standards.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-disable-standards.html) command\.

1. For each standard you want to disable, provide the standard subscription ARN\.

   ```
   aws securityhub batch-disable-standards --standards-subscription-arns "standard subscription ARN"
   ```

   **Example**

   ```
   aws securityhub batch-disable-standards --standards-subscription-arns "arn:aws:securityhub:us-west-1:123456789012:subscription/aws-foundational-security-best-practices/v/1.0.0"
   ```

------