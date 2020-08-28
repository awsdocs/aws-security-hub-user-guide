# Viewing finding details \(console\)<a name="finding-view-details"></a>

From a finding list, you can display a details pane for a finding\.

**To view the findings detail pane**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. To display a finding list, do one of the following:
   + In the Security Hub navigation pane, choose **Findings**\.
   + In the Security Hub navigation pane, choose **Insights**\. Choose an insight\. Then on the results list, choose an insight result\.
   + In the Security Hub navigation pane, choose **Integrations**\. Choose **See findings** for an integration\.

1. Choose the finding title\.

At the top of the finding details pane contains overview information about the finding, including the account, severity, dates, and status\.

**Types and Related Findings** contains information about the finding type\.

**Resources** contains information about the affected resource\.

**Remediation** displays for control findings\. It provides a link to the instructions for remediating the issue that triggered the finding\.

From the finding details pane, you can view more details and add field values to the filter\.
+ To display the complete JSON for the finding, choose the finding ID\. From **Finding JSON**, you can download the finding JSON to a file\.
+ To add a field value to the finding list filter, choose the search icon next to the field\.
+ For findings that are based on AWS Config rules, to display a list of the applicable rules, choose **Rules**\.