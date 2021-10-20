# Enabling finding aggregation<a name="finding-aggregation-enable"></a>

You must enable finding aggregation from the Region that will be the aggregation Region\.

You cannot use a Region that is disabled by default as your aggregation Region\. For a list of Regions that are disabled by default, see [Enabling a Region](https://docs.aws.amazon.com/general/latest/gr/rande-manage.html#rande-manage-enable) in the *AWS General Reference*\.

## Enabling finding aggregation \(console\)<a name="finding-aggregation-enable-console"></a>

When you enable finding aggregation, you choose your linked Regions\. You also choose whether to automatically link new Regions when Security Hub begins to support them and you have opted into them\.

**To enable finding aggregation**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Change to the Region that you want to use as the aggregation Region\.

1. In the Security Hub navigation menu, choose **Settings**, then choose **Regions**\.

1. Under **Finding aggregation**, choose **Configure finding aggregation**\.

   By default, the aggregation Region is set to **No aggregation Region**\.

1. Under **Aggregation Region**, choose the radio button to designate the current Region as the aggregation Region\.

1. Under **Linked Regions**, select the Regions to aggregate findings from\.

1. To automatically aggregate findings from new Regions in the partition as Security Hub supports them and you opt into them, select **Link future Regions**\.

1. Choose **Save**\.

## Enabling finding aggregation \(Security Hub API, AWS CLI\)<a name="finding-aggregation-enable-api"></a>

You can use the Security Hub API to enable finding aggregation\.

To enable finding aggregation from the Security Hub API, you create a finding aggregator\. You must create the finding aggregator from the Region that you want to use as the aggregation Region\.

When you use the API to enable finding aggregation, you choose one of the following options:
+ **Aggregate findings from all Regions\.**

  With this option, Security Hub automatically aggregates findings from new Regions when Security Hub supports them and you opt into them\.
+ **Aggregate findings from all Regions except for a specified list of excluded Regions\.**

  With this option, Security Hub automatically aggregates findings from new Regions when Security Hub supports them and you opt into them\.
+ **Aggregate findings only from a specific list of Regions\.**

  With this option, Security Hub does not automatically aggregate findings from new Regions\.

**To create the finding aggregator \(Security Hub API, AWS CLI\)**
+ **Security Hub API:** From the Region that you want to use as the aggregation Region, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateFindingAggregator.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateFindingAggregator.html) operation\. For `RegionLinkingMode`, the options are as follows:
  + `ALL_REGIONS` – Aggregates findings from all Regions\. Also aggregates findings from new Regions as they are supported and you opt into them\.
  + `ALL_REGIONS_EXCEPT_SPECIFIED` – Aggregates findings from all Regions except for Regions that you want to exclude\. Also aggregates findings from new Regions as they are supported and you opt into them\. Use `Regions` to provide the list of Regions to exclude from aggregation\.
  + `SPECIFIED_REGIONS` – Aggregates findings from a selected list of Regions\. Does not aggregate findings automatically from new Regions\. Use `Regions` to provide the list of Regions to aggregate from\.
+ **AWS CLI:** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/create-finding-aggregator.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/create-finding-aggregator.html) command\.

  ```
  aws securityhub create-finding-aggregator --region <aggregation Region> --region-linking-mode ALL_REGIONS | ALL_REGIONS_EXCEPT_SPECIFIED | SPECIFIED_REGIONS --regions <Region list>
  ```

  In the following example, finding aggregation is configured for selected Regions\. The aggregation Region is US East \(N\. Virginia\)\. The linked Regions are US West \(N\. California\) and US West \(Oregon\)\.

  ```
  aws securityhub create-finding-aggregator --region us-east-1 --region-linking-mode SPECIFIED_REGIONS --regions us-west-1,us-west-2
  ```