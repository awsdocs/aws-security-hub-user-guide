# Enabling cross\-Region aggregation<a name="finding-aggregation-enable"></a>

You must enable cross\-Region aggregation from the Region that will be the aggregation Region\.

You cannot use a Region that is disabled by default as your aggregation Region\. For a list of Regions that are disabled by default, see [Enabling a Region](https://docs.aws.amazon.com/general/latest/gr/rande-manage.html#rande-manage-enable) in the *AWS General Reference*\.

## Enabling cross\-Region aggregation \(console\)<a name="finding-aggregation-enable-console"></a>

When you enable cross\-Region aggregation, you choose your linked Regions\. You also choose whether to automatically link new Regions when Security Hub begins to support them and you have opted into them\.

**To enable cross\-Region aggregation**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Change to the Region that you want to use as the aggregation Region\.

1. In the Security Hub navigation menu, choose **Settings**, then choose **Regions**\.

1. Under **Finding aggregation**, choose **Configure finding aggregation**\.

   By default, the aggregation Region is set to **No aggregation Region**\.

1. Under **Aggregation Region**, choose the radio button to designate the current Region as the aggregation Region\.

1. Under **Linked Regions**, select the Regions to aggregate data from\.

1. To automatically aggregate data from new Regions in the partition as Security Hub supports them and you opt into them, select **Link future Regions**\.

1. Choose **Save**\.

## Enabling cross\-Region aggregation \(Security Hub API, AWS CLI\)<a name="finding-aggregation-enable-api"></a>

You can use the Security Hub API to enable cross\-Region aggregation\.

To enable cross\-Region aggregation from the Security Hub API, you create a finding aggregator\. You must create the finding aggregator from the Region that you want to use as the aggregation Region\.

**To create the finding aggregator \(Security Hub API, AWS CLI\)**
+ **Security Hub API:** From the Region that you want to use as the aggregation Region, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateFindingAggregator.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateFindingAggregator.html) operation\. For `RegionLinkingMode`, you choose from the following options:
  + `ALL_REGIONS` – Security Hub aggregates data from all Regions\. Security Hub also aggregates data from new Regions as they are supported and you opt into them\.
  + `ALL_REGIONS_EXCEPT_SPECIFIED` – Security Hub aggregates data from all Regions except for Regions that you want to exclude\. Security Hub also aggregates data from new Regions as they are supported and you opt into them\. Use `Regions` to provide the list of Regions to exclude from aggregation\.
  + `SPECIFIED_REGIONS` – Security Hub aggregates data from a selected list of Regions\. Security Hub does not aggregate data automatically from new Regions\. Use `Regions` to provide the list of Regions to aggregate from\.
+ **AWS CLI:** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/create-finding-aggregator.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/create-finding-aggregator.html) command\.

  ```
  aws securityhub create-finding-aggregator --region <aggregation Region> --region-linking-mode ALL_REGIONS | ALL_REGIONS_EXCEPT_SPECIFIED | SPECIFIED_REGIONS --regions <Region list>
  ```

  In the following example, cross\-Region aggregation is configured for selected Regions\. The aggregation Region is US East \(N\. Virginia\)\. The linked Regions are US West \(N\. California\) and US West \(Oregon\)\.

  ```
  aws securityhub create-finding-aggregator --region us-east-1 --region-linking-mode SPECIFIED_REGIONS --regions us-west-1,us-west-2
  ```