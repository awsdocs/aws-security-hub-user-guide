# Disabling and enabling individual controls<a name="securityhub-standards-enable-disable-controls"></a>

When you enable a standard, all of the controls for that standard are enabled by default\. You can then disable and enable specific controls within an enabled standard\.

When you disable a control, the following occurs:
+ The check for the control is no longer performed\.
+ No additional findings are generated for that control\.
+ Existing findings are archived automatically after three to five days \(note that this is best effort and not guaranteed\)\.
+ The related AWS Config rules that Security Hub created are removed\.

It can be useful to turn off security checks for controls that are not relevant to your environment\. For example, you might prefer to use Amazon GuardDuty instead of CloudWatch alarms to monitor for anomalous activity associated with your AWS CloudTrail logs\. You can then disable the CIS AWS Foundations Benchmark controls 3\.1\-3\.14, which focus on CloudWatch alarms\.

Disabling irrelevant controls reduces the number of irrelevant findings\. It also removes the failed check from the security score for the associated standard\.

Remember that Security Hub is Regional\. When you disable or enable a control, it is disabled only in the current Region or in the Region that you specify in the API request\.

Also, when you disable an entire standard, Security Hub does not track which controls were disabled\. If you subsequently enable the standard again, all of the controls are enabled\. For more information, see [Disabling or enabling a security standard](securityhub-standards-enable-disable.md)\.

**Note**  
You enable and disable controls on a region\-by\-region basis via the Security Hub console, API, or CLI\. If you have set an aggregation Region, you see controls from all linked Regions\. If a control is available in a linked Region but not in the aggregation Region, you cannot enable or disable that control from the aggregation Region\. For multi\-account and multi\-Region control disablement scripts, refer to [ Disabling Security Hub Controls in a multi\-account environment](http://aws.amazon.com/blogs/security/disabling-security-hub-controls-in-a-multi-account-environment/)

## Disabling a control \(console\)<a name="securityhub-standard-control-disable-console"></a>

From the Security Hub console, you can disable controls from the control list on the standard details page or from the control details page\.

**To disable a control \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to disable the control\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard that you want to disable a control for, choose **View results**\.

1. If you are an administrator account, choose **Enabled for this account**\.

   Other accounts can enable controls from any tab other than the **Disabled** tab\.

1. Do one of the following:
   + In the control list, choose the control to disable\. Then choose **Disable**\.
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

On the standard details page, the disabled controls are displayed on the **Disabled** tab\.

For administrator accounts, the **Disabled** tab contains an aggregated list across accounts\. The disabled controls for the individual administrator account are displayed on the **Disabled for this account** tab\.

You can enable a control from the controls list on the **Disabled** tab, or from the control details page\.

**To enable a disabled control \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Confirm that you are using Security Hub in the Region in which you want to disable the control\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard that you want to enable the control for, choose **View results**\.

1. Display the list of disabled controls\.

   For a member account or a standalone account, choose **Disabled**\.

   For an administrator account, choose **Disabled for this account**\.

1. Do one of the following:
   + In the control list on the **Disabled** or **Disabled for this account** tab, choose the control to enable\. Then choose **Enable**\.
   + Choose a control title\. Then on the control details page, choose **Enable**\.

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