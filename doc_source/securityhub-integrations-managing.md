# Managing product integrations<a name="securityhub-integrations-managing"></a>

The **Integrations** page provides access to all of the available AWS and third\-party product integrations\. The AWS Security Hub API also provides operations to allow you to manage integrations\.

## Viewing and filtering the list of integrations<a name="securityhub-integrations-view-filter"></a>

From the **Integrations** page, you can view and filter the list integrations\.

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

You can filter the list using text from the following fields\.
+ Company name
+ Product name
+ Integration description
+ Categories

## Enabling an integration<a name="securityhub-integration-enable"></a>

On the **Integrations** page, each integration provides the required steps to enable the integration\.

For most of the integrations with other AWS services, the only required step is to enable the other service\. The integration information includes a link to the service home page\. When you enable the other service, a resource\-level permission that allows Security Hub to receive findings from the service is then automatically created and applied\.

For third\-party product integrations, you may need to purchase the integration from the AWS Marketplace, and then configure the integration\. The integration information provides links to perform those tasks\.

If more than one version of a product is available in AWS Marketplace, select the version to subscribe to and then choose **Continue to Subscribe**\. For example, some products offer a standard version and an AWS GovCloud \(US\) version\.

When you enable a product integration, a resource policy is automatically attached to that product subscription\. This resource policy defines the permissions that Security Hub needs to import findings from that product\.

## Disabling and enabling the flow of findings from an integration \(Console\)<a name="securityhub-integration-findings-flow-console"></a>

On the **Integrations** page, for integrations that send findings, the **Status** field indicates whether you are currently accepting findings\.

To stop accepting findings, choose **Stop accepting findings**\.

To resume accepting findings, choose **Accept findings**\.

## Disabling and enabling the flow of findings from an integration \(API\)<a name="securityhub-integration-findings-flow-api"></a>

To use the API to stop receiving findings from an integration, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableImportFindingsForProduct.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableImportFindingsForProduct.html) operation\. To disable the import of findings, you need the ARN for your subscription\. To get the subscription ARNs for your currently enabled integrations, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListEnabledProductsForImport.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListEnabledProductsForImport.html) operation\.

To use the API to enable receiving findings from an integration, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableImportFindingsForProduct.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableImportFindingsForProduct.html) operation\. To enable the import of findings from an integration, you need the product ARN\. To get the ARNs for the available integrations, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeProducts.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeProducts.html) operation\.

## Viewing the findings from an integration<a name="securityhub-integration-view-findings"></a>

For integrations that you are accepting findings for \(**Status** is **Accepting findings**\), to view a list of findings, choose **See findings**\.

The findings list shows the active findings for the selected integration that have a workflow status of `NEW` or `NOTIFIED`\.

From the findings list, you can perform the following actions\.
+ [Change the filters and grouping for the list](findings-filtering-grouping.md)
+ [View details for individual findings](finding-view-details.md)
+ [Update the workflow status of findings](finding-workflow-status.md)
+ [Send findings to custom actions](finding-send-to-custom-action.md)