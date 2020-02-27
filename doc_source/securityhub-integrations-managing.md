# Managing Product Integrations<a name="securityhub-integrations-managing"></a>

The **Integrations** page provides access to all of the available AWS and third\-party product integrations\. The AWS Security Hub API also provides operations to allow you to manage integrations\.

## Viewing and Filtering the List of Integrations<a name="securityhub-integrations-view-filter"></a>

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

## Enabling an Integration<a name="securityhub-integration-enable"></a>

On the **Integrations** page, each integration provides the required steps to enable the integration\.

For most of the integrations with other AWS services, the only required step is to enable the other service\. The integration information includes a link to the service home page\. When you enable the other service, a resource\-level permission that allows Security Hub to receive findings from the service is then automatically created and applied\.

For third\-party product integrations, you may need to purchase the integration from the AWS Marketplace, and then configure the integration\. The integration information provides links to perform those tasks\.

If more than one version of a product is available in AWS Marketplace, select the version to subscribe to and then choose **Continue to Subscribe**\. For example, some products offer a standard version and an AWS GovCloud \(US\) version\.

When you enable a product integration, a resource policy is automatically attached to that product subscription\. This resource policy defines the permissions that Security Hub needs to import findings from that product\.

## Disabling and Enabling the Flow of Findings from an Integration \(Console\)<a name="securityhub-integration-findings-flow-console"></a>

On the **Integrations** page, for integrations that send findings, the **Status** field indicates whether you are currently accepting findings\.

To stop accepting findings, choose **Stop accepting findings**\.

To resume accepting findings, choose **Accept findings**\.

## Disabling and Enabling the Flow of Findings from an Integration \(API\)<a name="securityhub-integration-findings-flow-api"></a>

To use the API to stop receiving findings from an integration, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableImportFindingsForProduct.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableImportFindingsForProduct.html) operation\. To disable the import of findings, you need the ARN for your subscription\. To get the subscription ARNs for your currently enabled integrations, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListEnabledProductsForImport.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListEnabledProductsForImport.html) operation\.

To use the API to enable receiving findings from an integration, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableImportFindingsForProduct.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableImportFindingsForProduct.html) operation\. To enable the import of findings from an integration, you need the product ARN\. To get the ARNs for the available integrations, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeProducts.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeProducts.html) operation\.

## Viewing the Findings from an Integration<a name="securityhub-integration-view-findings"></a>

For integrations that you are accepting findings for \(**Status** is **Accepting findings**\), to view a list of findings, choose **See findings**\.

The findings list shows the active findings for the selected integration\. To view the details panel for a finding, choose the finding title\.

From the findings list, you can archive findings or send them to a custom action\.

The custom action must be associated with a CloudWatch rule for the `Security Hub Findings - Custom Action` event type\. See [Automating AWS Security Hub with CloudWatch Events](securityhub-cloudwatch-events.md)\.

**To take action on findings**

1. Select the check box for each finding to take action on\.

1. To archive the findings, from the **Actions** menu, choose **Archive**\.

1. To send the findings to a custom action, from the **Actions** menu, choose the custom action\.