# Filtering, sorting, and downloading control findings<a name="control-finding-list"></a>

You can filter the list of control findings based on compliance status by using the filtering tabs\. You can also filter the list based on other finding field values, and download findings from the list\.

## Filtering and sorting the control finding list<a name="control-finding-list-filter-sort"></a>

The **All checks** tab lists all active findings that have a workflow status of `NEW`, `NOTIFIED`, or `RESOLVED`\. By default, the list is sorted so that failed findings are at the top of the list\. This sort order helps you prioritize findings that need to be addressed\.

The lists on the **Failed**, **Unknown**, and **Passed** tabs are filtered based on the value of `Compliance.Status`\. The lists also only include active findings that have a workflow status of `NEW`, `NOTIFIED`, or `RESOLVED`\.

The **Suppressed** tab contains a list of active findings that have a workflow status of `SUPPRESSED`\.

In addition to the built\-in filters on each tab, you can filter the lists using values from the following fields:
+ Account ID
+ Workflow status
+ Compliance status
+ Resource ID
+ Resource type

You can sort each list using any of the columns\.

## Downloading the control finding list<a name="control-finding-list-download"></a>

If you navigate to **Security standards** and choose a standard, you see a list of controls for the standard\. Choosing a control from the list takes you to the control details page\. From here, you can download control findings to a \.csv file\.

If you filter the finding list, then the download only includes the controls that match the filter\.

If you select specific findings from the list, then the download only includes the selected findings\.

To download the findings, choose **Download**\.

Downloading findings calls the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html#securityhub-GetFindings-request-MaxResults](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html#securityhub-GetFindings-request-MaxResults) API\. Use the `MaxResults` parameter to limit the number of findings that are returned if you have a large number of findings in your account\.