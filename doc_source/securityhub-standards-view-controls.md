# Viewing details for controls<a name="securityhub-standards-view-controls"></a>

The **Security standards** page provides access to the supported security standards in Security Hub\.

For each enabled standard, you can view and filter the list of controls\. For each control, you can view a details page that includes the list of findings for the control\.

## Displaying the controls for an enabled standard<a name="securityhub-standards-display-control-list"></a>

From the **Security standards** page, you can display the list of controls associated with that standard\.

**To display the list of controls for an enabled standard**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard to display the controls for, choose **View results**\.

For each control, the controls page provides the following information\.
+ The control identifier and title
+ Whether the control is enabled or disabled
+ The overall status of the control\. See [Determining the overall status of a control from its findings](securityhub-standards-results.md#securityhub-standards-results-status)\.
+ The severity associated with the control
+ The number of accounts that have findings in each finding status

## Filtering the list of controls<a name="securityhub-standards-filter-controls"></a>

By default, the list of controls includes all of the controls for the selected standard\. You can filter the list based on the control identifier, description, related requirements, status, or severity\.

To filter the list of controls based on text in the identifier, description, or a related requirement, begin typing the text\. The list is updated automatically to only include controls that contain the matching text\.

To filter the list of controls based on the control status, from the dropdown list, select the status to include\. For enabled controls, you can show all enabled controls, or only show enabled controls that have a specific overall status \(**Passed**, **Failed**, or **Unknown**\)\. You can also choose to only display disabled standards\.

To filter the list of controls based on the control severity, from the **Severity** dropdown list, select the severity to include\.

## Viewing details and findings for a control<a name="securityhub-standards-control-details"></a>

For each control, you can display the details page for that control\. The details page includes an overview and the list of findings\.

To display the details for a control, choose the control name\.

At the top of the details page is an overview of the control and its current status\.

At the bottom of the details page is the list of findings for the control\. The findings list shows the active findings for the selected control that have a workflow status of `NEW`, `NOTIFIED`, or `RESOLVED`\.

You can only filter the list based on text in the finding list\. You cannot add or remove filters, or group the findings\.

You can also perform the following actions\.
+ [View details for individual findings](finding-view-details.md)
+ [Update the workflow status of findings](finding-workflow-status.md)
+ [Send findings to custom actions](finding-send-to-custom-action.md)