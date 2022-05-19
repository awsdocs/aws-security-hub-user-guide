# Viewing the current cross\-Region aggregation configuration<a name="finding-aggregation-view-config"></a>

You can view the current cross\-Region aggregation configuration from any Region\. The configuration includes the aggregation Region, the linked Regions, and whether to automatically link new Regions\.

## Viewing the cross\-Region aggregation configuration \(console\)<a name="finding-aggregation-view-config-console"></a>

The **Regions** tab of the **Settings** page displays the current cross\-Region aggregation configuration\. You can view the configuration from any Region\. Member accounts can also view the cross\-Region configuration that the administrator account configured\.

If cross\-Region aggregation is not enabled, then the **Regions** tab displays the option to enable cross\-Region aggregation\. See [Enabling cross\-Region aggregation](finding-aggregation-enable.md)\. Only administrator accounts and standalone accounts can enable cross\-Region aggregation\.

If cross\-Region aggregation is enabled, then the **Regions** tab displays the following information:
+ The aggregation Region
+ Whether to automatically aggregate findings, insights, control statuses, and security scores from new Regions that Security Hub supports and that you opt into
+ The list of linked Regions

## Viewing the current cross\-Region aggregation configuration \(Security Hub API, AWS CLI\)<a name="finding-aggregation-view-config-api"></a>

You can use the Security Hub API or AWS CLI to view the current cross\-Region aggregation configuration\. You can view the cross\-Region aggregation configuration from any Region\.

**To view the current cross\-Region aggregation configuration \(Security Hub API, AWS CLI\)**
+ **Security Hub API:** Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindingAggregator.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindingAggregator.html) API\. When you make the request, you must provide the finding aggregator ARN\. To obtain the finding aggregator ARN, use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListFindingAggregators.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListFindingAggregators.html)\.
+ **AWS CLI:** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/get-finding-aggregator.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/get-finding-aggregator.html) command\. To obtain the finding aggregator ARN, use [https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-finding-aggregators.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-finding-aggregators.html)\.

  ```
  aws securityhub get-finding-aggregator --finding-aggregator-arn <finding aggregator ARN>
  ```