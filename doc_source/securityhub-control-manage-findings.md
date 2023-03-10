# Viewing and taking action on control findings<a name="securityhub-control-manage-findings"></a>

The control details page displays a list of active findings for a control\. The list does not include archived findings\.

The control details page supports finding aggregation\. If you have set an aggregation Region, the control status and list of security checks on the control details page include checks from all linked AWS Regions\.

The list provides tools to filter and sort the findings, so that you can focus on more urgent findings first\. A finding may include links to resource details in the related service console\. For controls that are based on AWS Config rules, you can view details about the rule and the configuration timeline\.

You can also use the AWS Security Hub API to retrieve a list of findings\. For more information, see [Retrieving finding details \(programmatic\)](finding-view-details.md#finding-retrieve-api-cli)\.

**Topics**
+ [Viewing details about a control finding and finding resource](control-finding-resource-details.md)
+ [Sample control findings](sample-control-findings.md)
+ [Filtering, sorting, and downloading control findings](control-finding-list.md)
+ [Taking action on control findings](control-finding-take-action.md)