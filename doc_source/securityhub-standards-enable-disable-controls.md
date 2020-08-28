# Disabling and enabling individual controls<a name="securityhub-standards-enable-disable-controls"></a>

When you enable a standard, all of the controls for that standard are enabled by default\. You can then disable and enable specific controls within an enabled standard\.

When you disable a control, the following occurs:
+ The check for the control is no longer performed\.
+ No additional findings are generated for that control\.
+ The related AWS Config rules that Security Hub created are removed\.

It can be useful to turn off security checks for controls that are not relevant to your environment\. For example, you might use a single Amazon S3 bucket to log your CloudTrail logs\. If so, you can turn off controls related to CloudTrail logging in all accounts and Regions except for the account and Region where the centralized S3 bucket is located\. Disabling irrelevant controls reduces the number of irrelevant findings\. It also removes the failed check from the readiness score for the associated standard\.

Remember that Security Hub is Regional\. When you disable or enable a control, it is disabled only in the current Region or in the Region that you specify in an API request\.

Also, when you disable an entire standard, Security Hub does not track which controls were disabled\. If you subsequently enable the standard again, all of the controls are enabled\. For more information, see [Disabling or enabling a security standard](securityhub-standards-enable-disable.md)\.

## Disabling a control \(console\)<a name="securityhub-standard-control-disable-console"></a>

On the Security Hub console, each enabled control provides an option to disable that control\.

You can disable a control from the controls list, or from the control details page\.

**To disable a control \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to disable the control\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard that you want to disable controls for, choose **View results**\.

1. For the control that you want to disable, do one of the following:
   + Choose **Disable**\.
   + Choose the control title\. Then on the control details page, choose **Disable**\.

1. Enter a reason why you are disabling the control\. This can help others in your organization understand why the control is disabled\.

1. Choose **Disable**\.

## Disabling a control \(Security Hub API, AWS CLI\)<a name="securityhub-standard-control-disable-api"></a>

To disable a control, you can use an API call or the AWS Command Line Interface\.

**To disable a control \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html) operation\. To identify the control to disable, you provide the control ARN\. To retrieve the ARNs for the controls in a standard, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandardsControls.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandardsControls.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-standards-control.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-standards-control.html) command\.

  ```
  aws securityhub update-standards-control --standards-control-arn <control ARN> --control-status "DISABLED" --disabled-reason <description of reason to disable>
  ```

  **Example**

  ```
  aws securityhub update-standards-control --standards-control-arn "arn:aws:securityhub:us-east-1:123456789012:control/aws-foundational-security-best-practices/v/1.0.0/ACM.1" --control-status "DISABLED" --disabled-reason "Not applicable for my service"
  ```

## Enabling a control \(console\)<a name="securityhub-standard-control-enable-console"></a>

For a disabled control, **Disabled** appears next to the control title\.

To enable the control at any time, choose **Enable**\. The enable option is available from the control list and on the control details page\.

## Enabling a control \(Security Hub API, AWS CLI\)<a name="securityhub-standard-control-enable-api"></a>

To enable a control, you can use an API call or the AWS Command Line Interface\.

**To enable a control \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html) operation\. To identify the control to enable, you provide the control ARN\. To retrieve the ARNs for the controls in a standard, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandardsControls.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandardsControls.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-standards-control.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-standards-control.html) command\.

  ```
  aws securityhub update-standards-control--standards-control-arn <control ARN> --control-status "ENABLED"
  ```

  **Example**

  ```
  aws securityhub update-standards-control --standards-control-arn "arn:aws:securityhub:us-east-1:123456789012:control/aws-foundational-security-best-practices/v/1.0.0/ACM.1" --control-status "ENABLED"
  ```