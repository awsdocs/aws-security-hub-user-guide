# Custom Insights<a name="securityhub-custom-insights"></a>

In Security Hub, an insight is a collection of related findings defined by an aggregation statement and optional filters\.

A custom insight is an insight that you create to track security issues and risks that are specific to your environment\.

## Creating a Custom Insight<a name="securityhub-custom-insights-create"></a>

**To create an insight**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Insights**\.

1. Choose **Create insight**\.

1. Choose the **Add filter** field and then select **Group by**\.

1. Select the attribute to use to group the findings associated with this insight and then choose **Apply**\.

   See [Available Attributes for Filtering and Grouping Insights](#securityhub-insights-filter-group-attributes)\.

1. \(Optional\) Choose any additional filters to use for this insight, define the filter criteria, and then choose **Apply** after adding each filter\.
**Note**  
For optional filters, AND logic is applied to your specified collection of filters to query your findings\. However, OR logic is applied to multiple filters that use the same attribute that is set to different values\.

   See [Available Attributes for Filtering and Grouping Insights](#securityhub-insights-filter-group-attributes)\.

1. Choose **Create insight**\.

1. Enter an **Insight name** and then choose **Create insight**\.

## Modifying a Custom Insight<a name="securityhub-custom-insights-edit"></a>

You can modify an existing insight and then save the updates, or you can choose to save it as a new insight\.

**To modify an insight**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Insights**\.

1. Choose the insight to modify and then do one or more of the following:
   + To remove a filter from the insight, choose the circled X next to the filter\.
   + To add a new filter, choose the **Add filter** field, select the attribute to use as a filter, then choose **Apply**\.

     See [Available Attributes for Filtering and Grouping Insights](#securityhub-insights-filter-group-attributes)\.
   + To change the attribute used to group findings in the insight, first choose the circled X next to **Group by** to remove the existing grouping\. Then choose the **Add filter** field, select the attribute to use for the **Group by** aggregator, then choose **Apply**\.

     See [Available Attributes for Filtering and Grouping Insights](#securityhub-insights-filter-group-attributes)\.

1. When you've finished updating the insight, choose **Save insight** and then do one of the following:
   + To replace the existing insight with your changes, choose **Update "*Insight\_Name*"** and then choose **Save insight**\.
   + To create a new insight with the updates, choose **Save new insight**, enter an **Insight name**, and then choose **Save insight**\.

If you modify the filters and the **Group by** aggregator of a managed insight, you can only save your changes as a new insight\. You can't update the filters and the **Group by** aggregator of a managed insight\.

## Available Attributes for Filtering and Grouping Insights<a name="securityhub-insights-filter-group-attributes"></a>

You can choose only one **Group by** aggregator \(one attribute/value pair\) in a Security Hub insight\.

The available attributes for filtering and grouping insights and findings include the following:
+ **Aws account Id**
+ **Company name**
+ **Compliance status**
+ **Generator ID**
+ **Malware name**
+ **Process name**
+ **Threat intel type**
+ **Product ARN**
+ **Product name**
+ **Record state**
+ **EC2 instance image ID**
+ **EC2 instance IPv4**
+ **EC2 instance IPv6**
+ **EC2 instance key name**
+ **EC2 instance subnet ID**
+ **EC2 instance type**
+ **EC2 instance VPC ID**
+ **IAM access key user name**
+ **S3 bucket owner name**
+ **Container image ID**
+ **Container image name**
+ **Container name**
+ **Resource ID**
+ **Resource type**
+ **Severity label**
+ **Source URL**
+ **Type**
+ **Verification state**
+ **Workflow state**

For the complete list of AWS Security Finding Format attributes and their descriptions, see [AWS Security Finding Format](securityhub-findings-format.md)\.

## Deleting a Custom Insight<a name="securityhub-custom-insights-delete"></a>

When you no longer want an insight, you can delete it\. You can delete your custom insights\. You can't delete managed insights\.

**To delete a custom insight**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Insights**\.

1. Locate the insight to delete, choose the more options icon \(the three dots in the top\-left corner of the card\) for the insight, and then choose **Delete**\.

## Applying an Action to Insight Findings<a name="securityhub-insights-apply-action"></a>

After you create an insight, you can use it to apply an action to associated findings\. The default action is to archive findings\. You can also define your own custom actions\.

**To apply an action to the findings in an insight**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Insights**\.

1. Choose the insight that includes findings to apply an action to\.

1. Select all of the findings to apply the action to\.

1. Choose **Actions** and then choose the action to apply\. Only **Archive** appears if you haven't defined any custom actions\.

**Note**  
You can create Security Hub custom actions to automate Security Hub with Amazon CloudWatch Events\. For more information and detailed steps on creating custom actions, see [Automating AWS Security Hub with CloudWatch Events](securityhub-cloudwatch-events.md)\.