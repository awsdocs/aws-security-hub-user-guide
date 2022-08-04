# Filtering, sorting, and downloading the control finding list<a name="control-finding-list"></a>

The control finding list uses tabs to provide built\-in filtering for the list based on the finding status\. You can also filter the list based on other finding values, and download findings from the list\.

## Filtering and sorting the control finding list<a name="control-finding-list-filter-sort"></a>

The **All checks** tab lists all active findings that have a workflow status of `NEW`, `NOTIFIED`, or `RESOLVED`\. By default, the list is sorted so that failed findings are at the top of the list\. This sort order calls attention to findings that need to be addressed\.

The lists on the **Failed**, **Unknown**, and **Passed** tabs are filtered based on the value of `Compliance.Status`\. The lists also only include active findings that have a workflow status of `NEW`, `NOTIFIED`, or `RESOLVED`\.

The **Suppressed** tab contains a list of active findings that have a workflow status of SUPPRESSED\.

In addition to the built\-in filters on each tab, you can filter the lists using values from the following fields:
+ Account ID
+ Workflow status
+ Compliance status
+ Resource ID
+ Resource type

You can sort each list using any of the columns\.

## Downloading the control finding list<a name="control-finding-list-download"></a>

If you navigate to **Security standards** and choose a standard, you see a list of controls for the standard\. Choosing a control from the list takes you to the control details page\. From here, you can download the current page of control findings to a \.csv file\.

If you filtered the finding list, then the download only includes the controls that match the filter\.

If you selected specific findings from the list, then the download only includes the selected findings\.

To download the current page of the list or the selected findings, choose **Download**\.