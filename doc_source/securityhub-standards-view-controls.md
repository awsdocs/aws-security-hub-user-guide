# Viewing details for controls<a name="securityhub-standards-view-controls"></a>

The **Security standards** page provides access to the supported security standards in AWS Security Hub\.

For each enabled standard, you can view and filter the list of controls\. For each control, you can view a details page that includes the list of findings for the control\.

## Displaying the controls for an enabled standard \(console\)<a name="securityhub-standards-display-control-list"></a>

From the **Security standards** page, you can display the list of controls that are associated with that standard\.

**To display the list of controls for an enabled standard**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard to display the controls for, choose **View results**\.

For each control, the controls page provides the following information:
+ The control identifier and title
+ Whether the control is enabled or disabled
+ The overall status of the control \(see [Determining the overall status of a control from its findings](securityhub-standards-results.md#securityhub-standards-results-status)\)
+ The severity associated with the control
+ The number of accounts that have findings in each finding status

## Filtering the list of controls<a name="securityhub-standards-filter-controls"></a>

By default, the list of controls includes all of the controls for the selected standard\. You can filter the list based on the control identifier, description, related requirements, status, or severity\.

To filter the list of controls based on text in the identifier, description, or a related requirement, begin typing the text in the search box\. The list is updated automatically to only include controls that contain the matching text\.

To filter the list of controls based on the control status, from the menu next to the search box, choose the status to include\. For enabled controls, you can show all enabled controls or only show enabled controls that have a specific overall status \(**Passed**, **Failed**, or **Unknown**\)\. You can also choose to only display disabled standards\.

To filter the list of controls based on the control severity, from the severity menu, choose the severity to include\.

## Viewing details and findings for a control<a name="securityhub-standards-control-details"></a>

For each control, you can display the details page for that control\. The details page includes an overview and the list of findings\.

To display the details for a control, choose the control name\.

At the top of the details page is an overview of the control and its current status\.

At the bottom of the details page is the list of findings for the control\. The findings list shows the active findings for the selected control that have a workflow status of `NEW`, `NOTIFIED`, or `RESOLVED`\.

You can only filter the list based on text in the finding list\. You cannot add or remove filters, or group the findings\.

You can also perform the following actions:
+ [View details for individual findings](finding-view-details.md)\.
+ [Update the workflow status of findings](finding-workflow-status.md)\.
+ [Send findings to custom actions](finding-send-to-custom-action.md)\.

## Viewing the controls for an enabled standard \(Security Hub API, AWS CLI\)<a name="securityhub-standards-view-controls-api"></a>

To display information about the controls for an enabled standard, you can use an API call or the AWS Command Line Interface\.

**To display the controls for an enabled standard \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandardsControls.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandardsControls.html) operation\. To identify the standard to display the controls for, you provide the ARN of your subscription to the control\. To get the subscription ARNs for your enabled standards, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/describe-standards-controls.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/describe-standards-controls.html) command\.

  ```
  aws securityhub describe-standards-controls --standards-subscription-arn <subscription ARN>
  ```

  **Example**

  ```
  aws securityhub describe-standards-controls --standards-subscription-arn "arn:aws:securityhub:us-east-1:123456789012:subscription/aws-foundational-security-best-practices/v/1.0.0"
  ```