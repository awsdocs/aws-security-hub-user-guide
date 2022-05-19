# Stopping cross\-Region aggregation<a name="finding-aggregation-stop"></a>

Stop cross\-Region aggregation if you no longer want to aggregate data or if you want to change the aggregation Region\.

When you stop cross\-Region aggregation, Security Hub stops aggregating data\. It does not remove any existing aggregated data from the aggregation Region\.

## Stopping cross\-Region aggregation \(console\)<a name="finding-aggregation-stop-console"></a>

You must stop cross\-Region aggregation from the current aggregation Region\.

In Regions other than the aggregation Region, the **Finding aggregation** panel displays a message that you must edit the configuration in the aggregation Region\. Choose this message to display a link to switch to the aggregation Region\.

**To stop cross\-Region aggregation**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Change to the current aggregation Region\.

1. In the Security Hub navigation menu, choose **Settings**, then choose **Regions**\.

1. Under **Finding aggregation**, choose **Edit**\.

1. Under **Aggregation Region**, choose **No aggregation Region**\.

1. Choose **Save**\.

1. On the confirmation dialog, in the confirmation field, type **Confirm**\.

1. Choose **Confirm**\.

## Stopping cross\-Region aggregation \(Security Hub API, AWS CLI\)<a name="finding-aggregation-stop-api"></a>

You can use the Security Hub API to stop cross\-Region aggregation\. You must stop cross\-Region aggregation from the aggregation Region\.

**To stop cross\-Region aggregation \(Security Hub API, AWS CLI\)**
+ **Security Hub API:** Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DeleteFindingAggregator.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DeleteFindingAggregator.html) operation\. To identify the finding aggregator to delete, you provide the finding aggregator ARN\. To obtain the finding aggregator ARN, use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListFindingAggregators.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListFindingAggregators.html)\.
+ **AWS CLI:** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/delete-finding-aggregator.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/delete-finding-aggregator.html) command\.

  ```
  aws securityhub delete-finding-aggregator <finding aggregator ARN> --region <aggregation Region>
  ```