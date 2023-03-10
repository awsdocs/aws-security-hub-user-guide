# Viewing details for a standard<a name="securityhub-standards-view-controls"></a>

On the AWS Security Hub console, the details page for a standard includes the following information:
+ The standard security score and a visual summary of security checks for the controls that are enabled for the standard
+ The settings to [enable or disable a control](securityhub-standards-enable-disable-controls.md) that applies to the standard
+ A list of controls that apply to the standard and their latest compliance statuses

You can also use the Security Hub API and AWS CLI to retrieve details for a standard\. The following sections explain how to get details for a standard\.

## Displaying the details page for an enabled standard \(console\)<a name="standard-details-display-console"></a>

From the **Security standards** page, you can display the details page for an enabled standard\.

If you are logged into an administrator account, you can view details for any standard that is enabled in at least one member account\.

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Security standards**\.

1. For the standard that you want to display the details for, choose **View results**\.

## Standard security score and security checks summary<a name="standard-details-overview"></a>

At the top of the standard details page is the security score for the standard\. The score is the percentage of passed controls relative to the number of enabled controls \(that have data\) for the standard\.

Security Hub typically calculates the initial security score within 30 minutes after your first visit to the **Summary** page or **Security standards** page on the Security Hub console\. Scores are only generated for standards that are enabled when you visit those pages\. To view a list of standards that are currently enabled, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html) API operation\. In addition, AWS Config resource recording must be configured for scores to appear\. After first\-time score generation, Security Hub updates the security score every 24 hours\. Security Hub displays a timestamp to indicate when a security score was last updated\. For more information, see [Determining the security score for a security standard](standards-security-score.md)\.

**Note**  
It can take up to 24 hours for first\-time security scores to be generated in the China Regions and AWS GovCloud \(US\) Region\.

Next to the score is a chart that summarizes security checks for controls that are enabled for the standard\. The chart shows the percentage of failed and passed security checks\. When you pause on the chart, the pop\-up displays the following:
+ The number of failed security checks for controls of each severity
+ The number of security checks for controls with a status of **Unknown** 
+ The number of security checks that passed

For administrator accounts, the standard score and chart are aggregated across the administrator account and all member accounts\.

All of the data on the **Security standards** details pages is specific to the current Region unless you have set an aggregation Region\. If you have set an aggregation Region, the security scores apply across Regions and include findings in all linked Regions\. The compliance status of controls on the standards details pages also reflect findings from linked Regions, and the number of security checks includes findings from linked Regions\.

## Viewing the controls in enabled standards<a name="standard-controls-list"></a>

When you visit the details page for a standard, you can view a list of security controls that apply to the standard\. This list is sorted based on the compliance status of the control and the severity assigned to each control\. Security Hub updates the control statuses and security check count every 24 hours\. A timestamp on each tab indicates when the control statuses and security check count were most recently updated\. For more information, see [Determining the overall status of a control from its findings](controls-overall-status.md)\.

For administrator accounts, the control compliance statuses and number of security checks are aggregated across the administrator account and all member accounts\.

The **All enabled** tab lists all of the controls that are currently enabled in the standard\. For administrator accounts, the **All enabled** tab includes controls that are enabled in the standard in their account or at least one member account\.

On the **Failed**, **Unknown**, **No data**, and **Passed** tabs, the controls from the **All enabled** tab are filtered to include only enabled controls with a specific status\.

The **Disabled** tab contains the list of controls that are disabled in the standard\. For administrator accounts, the **Disabled** tab includes controls that are disabled in the standard in their account and all member accounts\.

For each control, the tabs display the following information:
+ The status of the control \(see [Determining the overall status of a control from its findings](controls-overall-status.md)\)
+ The severity assigned to the control
+ The control ID and title
+ The number of failed active findings out of the total number of active findings\. If applicable, the **Failed checks** column also lists the number of findings with a status of **Unknown**\.

In addition to the search filter on each tab, you can sort the lists based on the following fields:
+ **Compliance Status**
+ **Severity**
+ **ID**
+ **Title**
+ **Failed checks**

You can sort each list using any of the columns\. By default, the **All enabled** tab is sorted so that failed controls are at the top of the list\. This helps you to immediately focus on issues that require remediation\.

On the remaining tabs, the controls are sorted by default in descending order by severity\. In other words, critical controls are first, followed by high, then medium, then low severity controls\.

Choose your preferred access method, and follow the steps to display the available controls for an enabled standard\. In lieu of these instructions, you can also use the [DescribeStandardsControl](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeStandardsControl.html) API operation\.

------
#### [ Security Hub console ]

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Choose **Security standards** in the navigation pane\.

1. Choose **View results** for a standard\. The bottom of the page lists the controls \(divided by tabs\) that apply to the standard\.

------
#### [ Security Hub API ]

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListSecurityControlDefinitions.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListSecurityControlDefinitions.html) and provide a standard Amazon Resource Name \(ARN\) to get a list of control IDs for that standard\. To obtain standard ARNs, run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandards.html)\. If you don't provide a standard ARN, this API returns all Security Hub control IDs\. This API returns standard\-agnostic security control IDs, not standard\-specific control IDs\.

   **Example request:**

   ```
   {
       "StandardsArn": "arn:aws:securityhub:::standards/aws-foundational-security-best-practices/v/1.0.0"
   }
   ```

1. Run `[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListStandardsControlAssociations.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListStandardsControlAssociations.html)` to find out whether a control is enabled in each standard that you've enabled in your account\.

1. Identify the control by providing `SecurityControlId` or `SecurityControlArn`\. Pagination parameters are optional\.

   **Example request:**

   ```
   {
       SecurityControlId: Config.1
       NextToken: lkeyusdlk-sdlflsnd-ladfterb
       MaxResults: 5
   }
   ```

------
#### [ AWS CLI ]

1. Run the `[https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-security-control-definitions.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-security-control-definitions.html)` command, and provide one or more standard ARNs to get a list of control IDs\. To obtain standard ARNs, run the `describe-standards` command\. If you don't provide a standard ARN, this command returns all Security Hub control IDs\. This command returns standard\-agnostic security control IDs, not standard\-specific control IDs\.

   ```
   aws securityhub --region us-east-1 [https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-security-control-definitions.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-security-control-definitions.html) --standards-arn "arn:aws:securityhub:us-east-1::standards/aws-foundational-security-best-practices/v/1.0.0"
   ```

1. Run the `[https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-standards-control-associations.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-standards-control-associations.html)` command to find out whether a control is enabled in each standard that you've enabled in your account\.

1. Identify the control by providing `security-control-id` or `security-control-arn`\.

   **Example command:**

   ```
   aws securityhub --region us-east-1 [https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-standards-control-associations.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-standards-control-associations.html) --security-control-id Config.1
   ```

------

## Downloading the controls list<a name="standard-details-download-controls"></a>

You can download the current page of the controls list to a `.csv` file\.

If you filtered the controls list, then the downloaded file includes only the controls that match the filter settings\.

If you chose a specific control from the list, then the downloaded file includes only that control\.

To download the current page of the controls list or the currently selected control, choose **Download**\.