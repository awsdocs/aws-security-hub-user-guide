# Viewing and Taking Action on Insight Results and Findings<a name="securityhub-insights-view-take-action"></a>

For each insight, AWS Security Hub first determines the findings that match the filter criteria, then uses the grouping attribute to group the matching findings\.

From the **Insights** page, you can view and take action on the results and findings\.

## Viewing and Taking Action on Insight Results \(Console\)<a name="securityhub-insight-results-console"></a>

The insight results consist of a grouped list of the results for the insight\. For example, if the insight is grouped by resource ID, then the insight results are the list of resource IDs\. Each item in the results list indicates the number of matching findings for that item\.

The results list is sorted from most to fewest matching findings\.

In addition to the results list, the insight results display a set of charts summarizing the number of matching findings for the following attributes\.
+ Severity label \- Number of findings for each severity label
+ Account ID \- Top 5 account IDs for the matching findings
+ Resource type \- Top 5 resource types for the matching findings
+ Resource ID \- Top 5 resource IDs for the matching findings
+ Product Name \- Top 5 finding providers for the matching findings

If you have configured custom actions, then you can send selected results to a custom action\. The action must be associated with a CloudWatch rule for the `Security Hub Insight Results` event type\. See [Automating AWS Security Hub with CloudWatch Events](securityhub-cloudwatch-events.md)\.

**To display and take action on the list of insight results**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Insights**\.

1. To display the list of insight results, choose the insight name\.

1. To take action on an insight result or results:

   1. Select the check box for each result to send to the custom action\.

   1. From the **Actions** menu, choose the custom action\.

## Viewing Insight Results \(API\)<a name="securityhub-insight-results-api"></a>

To retrieve the list of insight results using the API, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetInsightResults.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetInsightResults.html) operation\.

## Viewing and Taking Action on Findings for an Insight Result \(Console\)<a name="securityhub-insight-findings-console"></a>

From the insight results list, you can display the list of findings for each result\. You can then archive findings or send them to a custom action\.

The custom action must be associated with a CloudWatch rule for the `Security Hub Findings - Custom Action` event type\. See [Automating AWS Security Hub with CloudWatch Events](securityhub-cloudwatch-events.md)\.

**To display and take action on insight findings**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Insights**\.

1. To display the list of insight results, choose the insight name\.

1. To display the list of findings for an insight result, choose the item from the results list\.

1. To take action on result findings:

   1. Select the check box for each finding to take action on\.

   1. To archive the findings, from the **Actions** menu, choose **Archive**\.

   1. To send the findings to a custom action, from the **Actions** menu, choose the custom action\.