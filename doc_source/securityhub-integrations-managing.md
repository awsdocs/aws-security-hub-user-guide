# Managing product integrations<a name="securityhub-integrations-managing"></a>

The **Integrations** page in the AWS Management Console provides access to all of the available AWS and third\-party product integrations\. The AWS Security Hub API also provides operations to allow you to manage integrations\.

**Note**  
Some integrations are not available in AWS GovCloud \(US\-East\) or AWS GovCloud \(US\-West\)\. If an integration is not supported, it is not listed on the **Integrations** page\.

## Viewing and filtering the list of integrations \(console\)<a name="securityhub-integrations-view-filter"></a>

From the **Integrations** page, you can view and filter the list of integrations\.

**To view the list of integrations**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Integrations**\.

On the **Integrations** page, the integrations with other AWS services are listed first, followed by the integrations with third\-party products\.

For each integration, the **Integrations** page provides the following information\.
+ The name of the company
+ The name of the product
+ A description of the integration
+ The categories that the integration applies to
+ How to enable the integration
+ The current status of the integration

You can filter the list by entering text from the following fields\.
+ Company name
+ Product name
+ Integration description
+ Categories

## Viewing information about product integrations \(Security Hub API, AWS CLI\)<a name="securityhub-integrations-view-api"></a>

To view information about product integrations, you can use an API call or the AWS Command Line Interface\. You can display information about all product integrations, or information about the product integrations that you have enabled\.

**To view information about all available product integrations \(Security Hub API, AWS CLI\)**
+ **Security Hub API ** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeProducts.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeProducts.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/describe-products.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/describe-products.html) command\.

  ```
  aws securityhub describe-products
  ```

**To view information about product integrations you have enabled \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListEnabledProductsForImport.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListEnabledProductsForImport.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-enabled-products-for-import.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/list-enabled-products-for-import.html) command\.

  ```
  aws securityhub list-enabled-products-for-import
  ```

## Enabling an integration<a name="securityhub-integration-enable"></a>

On the **Integrations** page, each integration provides the required steps to enable the integration\.

For most of the integrations with other AWS services, the only required step is to enable the other service\. The integration information includes a link to the service home page\. When you enable the other service, a resource\-level permission that allows Security Hub to receive findings from the service is then automatically created and applied\.

For third\-party product integrations, you may need to purchase the integration from the AWS Marketplace, and then configure the integration\. The integration information provides links to perform those tasks\.

If more than one version of a product is available in AWS Marketplace, select the version to subscribe to and then choose **Continue to Subscribe**\. For example, some products offer a standard version and an AWS GovCloud \(US\) version\.

When you enable a product integration, a resource policy is automatically attached to that product subscription\. This resource policy defines the permissions that Security Hub needs to receive findings from that product\.

## Disabling and enabling the flow of findings from an integration \(console\)<a name="securityhub-integration-findings-flow-console"></a>

On the **Integrations** page, for integrations that send findings, the **Status** information indicates whether you are currently accepting findings\.

To stop accepting findings, choose **Stop accepting findings**\.

To resume accepting findings, choose **Accept findings**\.

## Disabling the flow of findings from an integration \(Security Hub API, AWS CLI\)<a name="securityhub-integration-findings-flow-disable-api"></a>

To disable the flow of findings from an integration, you can use an API call or the AWS Command Line Interface\.

**To disable the flow of findings from an integration \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableImportFindingsForProduct.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableImportFindingsForProduct.html) operation\. To identify the integration to disable, you need the ARN of your subscription\. To obtain the subscription ARNs for your enabled integrations, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListEnabledProductsForImport.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListEnabledProductsForImport.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/disable-import-findings-for-product.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/disable-import-findings-for-product.html) command\.

  ```
  aws securityhub disable-import-findings-for-product --product-subscription-arn <subscription ARN>
  ```

  **Example**

  ```
  aws securityhub disable-import-findings-for-product --product-subscription-arn "arn:aws:securityhub:us-west-1:123456789012:product-subscription/crowdstrike/crowdstrike-falcon"
  ```

## Enabling the flow of findings from an integration \(Security Hub API, AWS CLI\)<a name="securityhub-integration-findings-flow-enable-api"></a>

To enable the flow of findings from an integration, you can use an API call or the AWS Command Line Interface\.

**To enable the flow of findings from an integration \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableImportFindingsForProduct.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableImportFindingsForProduct.html) operation\. To enable Security Hub to receive findings from an integration, you need the product ARN\. To obtain the ARNs for the available integrations, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeProducts.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeProducts.html) operation\.
+ AWS CLI**:** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/enable-import-findings-for-product.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/enable-import-findings-for-product.html) command\.

  ```
  aws securityhub enable-import-findings-for-product --product-arn <integration ARN>
  ```

  **Example**

  ```
  aws securityhub enable-import-findings-for product --product-arn "arn:aws:securityhub:us-east-1:123456789333:product/crowdstrike/crowdstrike-falcon"
  ```

## Viewing the findings from an integration<a name="securityhub-integration-view-findings"></a>

For integrations that you accept findings for \(**Status** is **Accepting findings**\), to view a list of findings, choose **See findings**\.

The findings list shows the active findings for the selected integration that have a workflow status of `NEW` or `NOTIFIED`\.

From the findings list, you can perform the following actions\.
+ [Change the filters and grouping for the list](findings-filtering-grouping.md)
+ [View details for individual findings](finding-view-details.md)
+ [Update the workflow status of findings](finding-workflow-status.md)
+ [Send findings to custom actions](finding-send-to-custom-action.md)