# Aggregating findings across Regions<a name="finding-aggregation"></a>

With cross\-Region finding aggregation, you can aggregate findings from multiple Regions to a single aggregation Region\. You can then manage all of those findings from the aggregation Region\.

**Note**  
Cross\-Region finding aggregation is not supported in the China Regions or in AWS GovCloud \(US\)\.

For example, suppose you aggregate findings from US West \(Oregon\) and US West \(N\. California\) to US East \(N\. Virginia\)\. When you view the **Findings** page in US East \(N\. Virginia\), you see the findings for all three Regions\.

In the aggregation Region, the **Summary** page provides a view of your active findings across linked Regions\. See [Viewing a cross\-Region summary of findings by severity](findings-view-summary.md)\. Other **Summary** page panels that analyze findings also display information from across the linked Regions\.

The following pages do not yet support finding aggregation\. The content on these pages, including the list of findings for a control, is always specific to the current Region\.
+ **Standards**
+ Standard details
+ Control details

**Topics**
+ [How finding aggregation works](finding-aggregation-overview.md)
+ [Viewing the current finding aggregation configuration](finding-aggregation-view-config.md)
+ [Enabling finding aggregation](finding-aggregation-enable.md)
+ [Updating the finding aggregation configuration](finding-aggregation-update.md)
+ [Stopping finding aggregation](finding-aggregation-stop.md)