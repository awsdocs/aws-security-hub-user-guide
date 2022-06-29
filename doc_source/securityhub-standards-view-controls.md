# Viewing details for a standard<a name="securityhub-standards-view-controls"></a>

The details page for a standard contains the list of controls in the standard\. It also shows the overall score for the standard\.

You can view and filter the list of controls, and perform the following actions:
+ [Enable or disable a control](securityhub-standards-enable-disable-controls.md)
+ [View the details for a control](securityhub-standards-control-details.md)\. The control details page includes the list of findings for the control\. See [Viewing and taking action on control findings](securityhub-control-manage-findings.md)\.

## Displaying the details page for an enabled standard \(console\)<a name="standard-details-display-console"></a>

From the **Security standards** page, you can display a details page for the standard\. You can only display details for an enabled standard\. You cannot display details for a disabled standard\.

This also applies to administrator accounts\. Administrator accounts that do not have a standard enabled for their individual account cannot view the details for that standard\. They cannot see the aggregated security score and status information across the member accounts that do have the standard enabled\.

**To display the list of controls for an enabled standard \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard that you want to display the details for, choose **View results**\.

## Information on the standard details page<a name="standard-details-overview"></a>

At the top of the details page is the overall score for the standard\. The score is the percentage of passed controls relative to the number of enabled controls for the standard that have data\. Security Hub typically calculates the initial security score within 30 minutes after your first visit to the **Summary** page or **Security standards** page on the Security Hub console\. Scores are only generated for standards that are enabled when you visit those pages\. To view a list of standards that are currently enabled, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html) API operation\. In addition, AWS Config resource recording must be configured for scores to appear\. After first\-time score generation, Security Hub updates the security score every 24 hours\. Security Hub displays a timestamp to indicate when a security score was last updated\. See [Determining the security score for a security standard](standards-security-score.md)\.

**Note**  
It can take up to 24 hours for first\-time security scores to be generated in the China Regions and AWS GovCloud \(US\) Region\.

Next to the overall score is a chart that summarizes the control statuses\. The chart shows the percentage of failed and passed controls\. When you pause on the chart, the pop\-up displays the following:
+ The number of failed controls for each severity
+ The number of controls with a status of **Unknown** 
+ The number of passed controls

At the bottom of the details page is the list of controls for the standard\. The control list is organized and sorted based on the current overall status of the control and the severity assigned to each control\. Security Hub updates the control statuses every 24 hours\. A timestamp on each tab indicates when the control statuses were most recently updated\. See [Determining the overall status of a control from its findings](controls-overall-status.md)\.

For administrator accounts, the score and statuses are aggregated across the administrator account and all member accounts\.

All of the data on the **Security standards** details pages is specific to the current Region unless you have  set an aggregation Region\. If you have set an aggregation Region, the security scores are cross\-regional, accounting  for findings in all linked Regions\. The compliance status of controls on the standards details pages also reflect findings from  linked Regions, and the number of security checks includes findings from linked Regions\.

## Filtering and sorting the controls<a name="standard-details-filter-controls"></a>

The control list for a standard uses tabs to provide built\-in filtering for the list based on the control status\. You can also filter the list based on the ID, title, and severity\.

The **All enabled** tab lists all of the enabled controls for the standard\. For administrator accounts, **All enabled** contains controls that are enabled in either their account or in any member account\.

On the **Failed**, **Unknown**, **No data**, and **Passed** tabs, the controls from the **All enabled** tab are filtered to only include controls with that status\.

The **Disabled** tab contains the list of disabled controls\. For administrator accounts, the **Disabled** tab lists controls that are not enabled in either their account or any of their member accounts\.

For standalone accounts and member accounts, the lists of enabled and disabled controls are updated in real time to reflect which controls are enabled and disabled\. The overall status and the number of passed and failed checks for each control are updated every 24 hours\.

For administrator accounts, all of the information, including the lists, is updated every 24 hours\.

For each control, the control list contains the following information:
+ The overall status of the control \(see [Determining the overall status of a control from its findings](controls-overall-status.md)\)
+ The severity assigned to the control
+ The control identifier and title
+ The number of failed active findings and the total number of active findings\. If applicable, the **Failed checks** column also lists the number of findings with a status of **Unknown**\.

In addition to the built\-in filters on each tab, you can filter the lists using values from the following fields:
+ **Status**
+ **Severity**
+ **ID**
+ **Title**

You can sort each list using any of the columns\. By default, the **All enabled** tab is sorted so that failed controls are at the top of the list\. This helps you to immediately focus on issues that require remediation\.

Within each status, and on the remaining tabs, the controls are sorted by default in descending order by severity\. In other words, critical controls are first, followed by high, then medium, then low severity controls\.

## Additional tabs for administrator accounts<a name="standard-details-admin-additional-tabs"></a>

For an administrator account, the lists on the first six tabs contain aggregated information across both the administrator account and their member accounts\. For example, a control is listed on the **All enabled** tab if at least one of the accounts has the control enabled\. A control is listed on the **Disabled** tab only if none of the accounts has the control enabled\.

All of the information on these tabs is updated every 24 hours\.

Administrator accounts also see the following additional tabs:
+ **Enabled controls for this account** lists the controls that are enabled for the administrator account\.
+ **Disabled controls for this account** lists the controls that are disabled for the administrator account\.

These lists are updated in real time to reflect the controls that the administrator account has enabled or disabled\.

## Downloading the control list<a name="standard-details-download-controls"></a>

You can download the current page of the control list to a `.csv` file\.

If you filtered the control list, then the downloaded file only includes the controls that match the filter\.

If you chose a specific control from the list, then the downloaded file only includes that control\.

To download the current page of the control list or the currently selected control, choose **Download**\.

## Viewing the controls for an enabled standard \(Security Hub API, AWS CLI\)<a name="standards-view-controls-api"></a>

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