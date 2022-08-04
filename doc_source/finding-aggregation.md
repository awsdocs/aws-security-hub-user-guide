# Cross\-Region aggregation<a name="finding-aggregation"></a>

With cross\-Region aggregation, you can aggregate findings, finding updates, insights, control compliance statuses, and security scores from multiple Regions to a single aggregation Region\. You can then manage all of this data from the aggregation Region\.

**Note**  
Cross\-Region aggregation is available with limitations in AWS GovCloud \(US\) and the China Regions\. In AWS GovCloud \(US\), cross\-Region aggregation is supported only for findings, finding updates, and insights across AWS GovCloud \(US\)\. Specifically, you can only aggregate findings, finding updates, and insights between AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\)\. In the China Regions, cross\-Region aggregation is supported only for findings, finding updates, and insights across the China Regions\. Specifically, you can only aggregate findings, finding updates, and insights between China \(Beijing\) and China \(Ningxia\)\.

Suppose you set US East \(N\. Virginia\) as an aggregation Region, and US West \(Oregon\) and US West \(N\. California\) as your linked Regions\. When you view the **Findings** page in US East \(N\. Virginia\), you see the findings from all three Regions\. Updates to those findings are also reflected in all three Regions\.

In the aggregation Region, the **Summary** page provides a view of your active findings across linked Regions\. See [Viewing a cross\-Region summary of findings by severity](findings-view-summary.md)\. Other **Summary** page panels that analyze findings also display information from across the linked Regions\.

Your security scores in the aggregation Region are calculated by comparing the number of passed controls to the number of enabled controls in all linked Regions\. In addition, if a control is enabled in at least one linked Region, it is visible on the **Security standards** details pages of the aggregation Region\. The compliance status of controls on the standards details pages reflects findings across linked Regions\. If a security check associated with a control fails in one or more linked Regions, the compliance status of that control shows as **Failed** on the standards details pages of the aggregation Region\. The number of security checks includes findings from all linked Regions\.

The enablement status of a control must be modified in each Region\. If a control is enabled in a linked Region but disabled in the aggregation Region, you can see the compliance status of the control from the aggregation Region, but you cannot enable or disable that control from the aggregation Region\.

To view cross\-Region security scores and compliance statuses, add the following permissions to your IAM policies:
+ `ListSecurityControlDefinitions`
+ `BatchGetStandardsControlAssociations`
+ `BatchUpdateStandardsControlAssociations`

Note that these IAM permission names do not directly correspond to current Security Hub APIs \.

**Topics**
+ [How cross\-Region aggregation works](finding-aggregation-overview.md)
+ [Viewing the current cross\-Region aggregation configuration](finding-aggregation-view-config.md)
+ [Enabling cross\-Region aggregation](finding-aggregation-enable.md)
+ [Updating the cross\-Region aggregation configuration](finding-aggregation-update.md)
+ [Stopping cross\-Region aggregation](finding-aggregation-stop.md)