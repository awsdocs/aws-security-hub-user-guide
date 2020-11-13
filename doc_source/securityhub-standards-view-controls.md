# Viewing the list of controls for a standard<a name="securityhub-standards-view-controls"></a>

The **Security standards** page displays the available security standards for AWS Security Hub\.

For each enabled standard, you can display a details page, which includes the list of controls in the standard\.

You can view and filter the list of controls, and perform the following actions:
+ [Enable or disable the control](securityhub-standards-enable-disable-controls.md)
+ [View the details for a control](securityhub-standards-control-details.md)\. The control details page includes the list of findings for the control\. See [Viewing and taking action on control findings](securityhub-control-manage-findings.md)\.

## Displaying the details page for an enabled standard \(console\)<a name="securityhub-standards-display-control-list"></a>

From the **Security standards** page, you can display a details page for the standard\. You can only display details for an enabled standard\. You cannot display details for a disabled standard\.

At the top of the details page is the overall score for the standard\. The overall score is the percentage of passed controls relative to the number of enabled controls that have data\.

Next to the overall score is a chart that summarizes the control statuses\. The chart shows the percentage of failed and passed controls\. When you pause on the chart, the pop\-up displays the number of failed controls for each severity, the number of controls with a status of **Unknown**, and the number of passed controls\.

At the bottom of the details page is the list of controls for the standard\. The control list is organized and sorted based on the current overall status of the control and the severity assigned to each control\.

**To display the list of controls for an enabled standard**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard that you want to display the details for, choose **View results**\.

## Filtering and sorting the controls for an enabled standard<a name="securityhub-standards-filter-controls"></a>

The control list for a standard uses tabs to provide built\-in filtering for the list based on the control status\. You can also filter the list based on the ID, title, and severity\.

The **All enabled** tab lists all of the enabled controls for the standard\. By default, the list is sorted so that failed controls are at the top of the list\. This sort order calls attention to controls that need to be addressed\.

The lists on the **Failed**, **Unknown**, **No data**, and **Passed** tabs are filtered to only include enabled controls with that status\.

The **Disabled** tab contains the list of disabled controls\.

For each control, the control list contains the following information:
+ The overall status of the control \(see [Determining the overall status of a control from its findings](securityhub-standards-results.md#securityhub-standards-results-status)\)
+ The severity assigned to the control
+ The control identifier and title
+ The number of failed active findings and the total number of active findings\. If applicable, the **Failed checks** column also lists the number of findings with a status of **Unknown**\.

In addition to the built\-in filters on each tab, you can filter the lists using text in the following fields:
+ **Status**
+ **Severity**
+ **ID**
+ **Title**

You can sort each list using any of the columns\. By default, the **All checks** tab is sorted so that failed controls are at the top of the list\. This allows you to immediately focus on issues that require remediation\.

Within each status, and on the remaining tabs, the controls are sorted by default in descending order by severity\. In other words, critical controls are first, followed by high, then medium, then low severity controls\.

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

## Downloading the control list<a name="securityhub-standards-download-controls"></a>

You can download the control list to a \.csv file\.

If you filtered the control list, then the downloaded file only includes the controls that match the filter\.

If you chose a specific control from the list, then the downloaded file only includes that control\.

To download the control list or the currently selected control, choose **Download**\.