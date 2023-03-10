# Enabling and disabling controls in specific standards<a name="controls-configure"></a>

When you enable a standard in AWS Security Hub, all of the controls that apply to it are automatically enabled in that standard \(the exception to this is service\-managed standards\)\. You can then disable and re\-enable specific controls in the standard\.

The details page for a standard contains the list of applicable controls for the standard, and information about which controls are currently enabled in and disabled in that standard\.

On the standards details page, you can also enable and disable controls in a specific standard\. You must enable and disable controls separately in each AWS account and AWS Region\. When you enable or disable a control, it only impacts the current account and Region\.

**Note**  
You can enable and disable controls in each Region by using the Security Hub console, Security Hub API, or AWS CLI\. If you have set an aggregation Region, you see controls from all linked Regions\. If a control is available in a linked Region but not in the aggregation Region, you cannot enable or disable that control from the aggregation Region\. For multi\-account and multi\-Region control disablement scripts, refer to [Disabling Security Hub controls in a multi\-account environment](http://aws.amazon.com/blogs/security/disabling-security-hub-controls-in-a-multi-account-environment/)\.

## Enabling a control in a specific standard<a name="enable-controls-standard"></a>

To enable a control in a standard, you must first enable at least one standard to which the control applies\. For more information about enabling a standard, see [Enabling and disabling security standards](securityhub-standards-enable-disable.md)\. When you enable a control in a standard, AWS Security Hub starts to generate findings for that control\. Security Hub also includes the [control status](controls-overall-status.md#controls-overall-status-values) in the calculation of the security score for the standard\. Even if you enable a control in multiple standards, you'll receive a single finding per security check across standards if you turn on consolidated control findings\. For more information, see [Consolidated control findings](controls-findings-create-update.md#consolidated-control-findings)\.

To enable a control in a standard, the control must be available in your current Region\. For more information, see [Availability of controls by Region](securityhub-regions.md#securityhub-regions-control-support)\.

Follow these steps to enable a Security Hub control in a *specific* standard\. In lieu of the following steps, you can also use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html) API action to enable controls in a specific standard\. For instructions on enabling a control in *all* standards, see [Enabling a control in all standards](securityhub-standards-enable-disable-controls.md#enable-controls-all-standards)\.

------
#### [ Security Hub console ]

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Choose **Security standards** from the navigation pane\.

1. Choose **View results** for the relevant standard\.

1. Select a control\.

1. Choose **Enable Control** \(this option doesn't appear for a control that's already enabled\)\. Confirm by choosing **Enable**\.

------
#### [ Security Hub API ]

1. Run `[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListSecurityControlDefinitions.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListSecurityControlDefinitions.html)`, and provide a standard ARN to get a list of available controls for a specific standard\. To obtain a standard ARN, run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandards.html)\. This API returns standard\-agnostic security control IDs, not standard\-specific control IDs\.

   **Example request:**

   ```
   {
       "StandardsArn": "arn:aws:securityhub:::standards/aws-foundational-security-best-practices/v/1.0.0"
   }
   ```

1. Run `[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListStandardsControlAssociations.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListStandardsControlAssociations.html)`, and provide a specific control ID to return the current enablement status of a control in each standard\.

   **Example request:**

   ```
   {
       "SecurityControlId": "IAM.1"
   }
   ```

1. Run `[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateStandardsControlAssociations.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateStandardsControlAssociations.html)`\. Provide the ARN of the standard that you want to enable the control in\.

1. Set the `AssociationStatus` parameter equal to `ENABLED`\.

   **Example request:**

   ```
   {
       "StandardsControlAssociationUpdates": [{"SecurityControlId": "IAM.1", "StandardsArn": "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0", "AssociationStatus": "ENABLED"}]
   }
   ```

------
#### [ AWS CLI ]

1. Run the `[https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-security-control-definitions.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-security-control-definitions.html)` command, and provide a standard ARN to get a list of available controls for a specific standard\. To obtain a standard ARN, run `describe-standards`\. This command returns standard\-agnostic security control IDs, not standard\-specific control IDs\.

   ```
   aws securityhub --region us-east-1 list-security-control-definitions --standards-arn "arn:aws:securityhub:us-east-1::standards/aws-foundational-security-best-practices/v/1.0.0"
   ```

1. Run the `[https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-standards-control-associations.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-standards-control-associations.html)` command, and provide a specific control ID to return the current enablement status of a control in each standard\.

   ```
   aws securityhub  --region us-east-1 list-standards-control-associations --security-control-id CloudTrail.1
   ```

1. Run the `[https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-update-standards-control-associations.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-update-standards-control-associations.html)` command\. Provide the ARN of the standard that you want to enable the control in\.

1. Set the `AssociationStatus` parameter equal to `ENABLED`\.

   ```
   aws securityhub  --region us-east-1 batch-update-standards-control-associations --standards-control-association-updates '[{"SecurityControlId": "CloudTrail.1", "StandardsArn": "arn:aws:securityhub:us-east-1::standards/aws-foundational-security-best-practices/v/1.0.0", "AssociationStatus": "ENABLED"}]'
   ```

------

## Disabling a control in a specific standard<a name="disable-controls-standard"></a>

When you disable a control in a standard, Security Hub stops generating findings for the control\. The control status is no longer used in calculating the security score for the standard\. 

One way to disable a control is by disabling all standards that the control applies to\. When you disable a standard, all of the controls that apply to the standard are disabled \(however, those controls may still remain enabled in other standards\)\. For information about disabling a standard, see [Enabling and disabling security standards](securityhub-standards-enable-disable.md)\.

When you disable a control by disabling a standard that it applies to, the following occurs:
+ Security checks for the control are no longer performed for that standard\. This means the control status won't affect the standard security score \(Security Hub will continue running security checks for the control if it is enabled in other standards\)\.
+ No additional findings are generated for that control\.
+ Existing findings are archived automatically after 3\-5 days \(note that this is best effort and not guaranteed\)\.
+ The related AWS Config rules that Security Hub created are removed\.

When you disable a standard, Security Hub does not track which controls were disabled\. If you subsequently enable the standard again, all of the controls that apply to it are automatically enabled\. In addition, disabling a control is a one\-time action\. Suppose you disable a control, and then you enable a standard which was previously disabled\. If the standard includes that control, it will be enabled in that standard\. When you enable a standard in Security Hub, all of the controls that apply to that standard are automatically enabled\.

Instead of disabling a control by disabling a standard that it applies to, you can just disable the control in one or more specific standards\.

To reduce finding noise, it can be useful to disable controls that aren't relevant to your environment\. For recommendations of which controls to disable, see [Security Hub controls that you might want to disable](controls-to-disable.md)\.

Follow these steps to disable a control in *specific* standards\. In lieu of the following steps, you can also use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html) API action to disable controls in a specific standard\. For instructions on disabling a control in all standards, see [Enabling and disabling controls in all standards](securityhub-standards-enable-disable-controls.md)\.

------
#### [ Security Hub console ]

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Choose **Security standards** from the navigation pane\. Choose **View results** for the relevant standard\.

1. Select a control\.

1. Choose **Disable Control** \(this option doesn't appear for a control that's already disabled\)\.

1. Provide a reason for disabling the control, and confirm by choosing **Disable**\.

------
#### [ Security Hub API ]

1. Run `[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListSecurityControlDefinitions.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListSecurityControlDefinitions.html)`, and provide a standard ARN to get a list of available controls for a specific standard\. To obtain a standard ARN, run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandards.html)\. This API returns standard\-agnostic security control IDs, not standard\-specific control IDs\.

   **Example request:**

   ```
   {
       "StandardsArn": "arn:aws:securityhub:::standards/aws-foundational-security-best-practices/v/1.0.0"
   }
   ```

1. Run `[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListStandardsControlAssociations.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListStandardsControlAssociations.html)`, and provide a specific control ID to return the current enablement status of a control in each standard\.

   **Example request:**

   ```
   {
       "SecurityControlId": "IAM.1"
   }
   ```

1. Run `[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateStandardsControlAssociations.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateStandardsControlAssociations.html)`\. Provide the ARN of the standard in which you want to disable the control\.

1. Set the `AssociationStatus` parameter equal to `DISABLED`\. If you follow these steps for a control that's already disabled, the API returns an HTTP status code 200 response\.

   **Example request:**

   ```
   {
       "StandardsControlAssociationUpdates": [{"SecurityControlId": "IAM.1", "StandardsArn": "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0", "AssociationStatus": "DISABLED",  "UpdatedReason": "Not applicable to environment"}]
   }
   ```

------
#### [ AWS CLI ]

1. Run the `[https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-security-control-definitions.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-security-control-definitions.html)` command, and provide a standard ARN to get a list of available controls for a specific standard\. To obtain a standard ARN, run `describe-standards`\. This command returns standard\-agnostic security control IDs, not standard\-specific control IDs\.

   ```
   aws securityhub --region us-east-1 list-security-control-definitions --standards-arn "arn:aws:securityhub:us-east-1::standards/aws-foundational-security-best-practices/v/1.0.0"
   ```

1. Run the `[https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-standards-control-associations.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-standards-control-associations.html)` command, and provide a specific control ID to return the current enablement status of a control in each standard\.

   ```
   aws securityhub  --region us-east-1 list-standards-control-associations --security-control-id CloudTrail.1
   ```

1. Run the `[https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-update-standards-control-associations.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-update-standards-control-associations.html)` command\. Provide the ARN of the standard in which you want to disable the control\.

1. Set the `AssociationStatus` parameter equal to `DISABLED`\. If you follow these steps for a control that's already enabled, the command returns an HTTP status code 200 response\.

   ```
   aws securityhub  --region us-east-1 batch-update-standards-control-associations --standards-control-association-updates '[{"SecurityControlId": "CloudTrail.1", "StandardsArn": "arn:aws:securityhub:us-east-1::standards/aws-foundational-security-best-practices/v/1.0.0", "AssociationStatus": "DISABLED", "UpdatedReason": "Not applicable to environment"}]'
   ```

------