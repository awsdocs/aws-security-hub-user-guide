# Updating the cross\-Region aggregation configuration<a name="finding-aggregation-update"></a>

You can update the cross\-Region aggregation configuration to change the linked Regions for the current aggregation Region\. You can also change whether to automatically aggregate findings, insights, control statuses, and security scores from new Regions\.

When you stop aggregating data from a linked Region, Security Hub does not remove any existing aggregated data from the aggregation Region\.

You cannot use the update process to change the aggregation Region\. To change the aggregation Region, you must do the following:

1. Stop cross\-Region aggregation\. See [Stopping cross\-Region aggregation](finding-aggregation-stop.md)\.

1. Change to the Region that you want to be the new aggregation Region\.

1. Enable cross\-Region aggregation\. See [Enabling cross\-Region aggregation](finding-aggregation-enable.md)\.

## Updating the cross\-Region aggregation configuration \(console\)<a name="finding-aggregation-update-console"></a>

You must update the cross\-Region aggregation configuration from the current aggregation Region\.

In Regions other than the aggregation Region, the **Finding aggregation** panel displays a message that you must edit the configuration in the aggregation Region\. Choose this message to display a link to navigate to the aggregation Region\.

**To change the linked Regions for the current aggregation Region**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Change to the current aggregation Region\.

1. In the Security Hub navigation menu, choose **Settings**, then choose **Regions**\.

1. Under **Finding aggregation**, choose **Edit**\.

1. Under **Linked Regions**, update the selected linked Regions\.

1. If needed, change whether **Link future Regions** is selected\. This setting determines whether Security Hub automatically links new Regions as it adds support for them and you opt into them\.

1.  Choose **Save**\.

## Updating the cross\-Region aggregation configuration \(Security Hub API, AWS CLI\)<a name="finding-aggregation-update-api"></a>

You can use the Security Hub API or AWS CLI to update the cross\-Region aggregation configuration\. You must update cross\-Region aggregation from the current aggregation Region\.

You can change the Region linking mode\. If the linking mode is `ALL_REGIONS_EXCEPT_SPECIFIED` or `SPECIFIED_REGIONS`, you can change the list of excluded or included Regions\.

When you change the list of excluded or included Regions, you must provide the full list with the updates\. For example, suppose you currently aggregate findings from US East \(Ohio\), and want to also aggregate findings from US West \(Oregon\)\. When you call [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateFindingAggregator.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateFindingAggregator.html), you provide a `Regions` list that contains both US East \(Ohio\) and US West \(Oregon\)\.

**To update cross\-Region aggregation \(Security Hub API, AWS CLI\)**
+ **Security Hub API:** Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateFindingAggregator.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateFindingAggregator.html) API operation\. To identify the finding aggregator, you must provide the finding aggregator ARN\. To obtain the finding aggregator ARN, use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListFindingAggregators.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListFindingAggregators.html)\.

  You provide the Region linking mode and the updated list of excluded or included Regions\.
+ **AWS CLI:** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-finding-aggregator.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-finding-aggregator.html) command\.

  ```
  aws securityhub update-finding-aggregator --region <aggregation Region> --finding-aggregator-arn <finding aggregator ARN> --region-linking-mode ALL_REGIONS | ALL_REGIONS_EXCEPT_SPECIFIED | SPECIFIED_REGIONS --regions <Region list>
  ```

  In the following example, the cross\-Region aggregation configuration is changed to aggregation for selected Regions\. The command is run from the current aggregation Region, which is US East \(N\. Virginia\)\. The linked Regions are US West \(N\. California\) and US West \(Oregon\)\.

  ```
  aws securityhub update-finding-aggregator --region us-east-1 --finding-aggregator-arn arn:aws:securityhub:us-east-1:222222222222:finding-aggregator/123e4567-e89b-12d3-a456-426652340000 --region-linking-mode SPECIFIED_REGIONS --regions us-west-1,us-west-2
  ```