# Setting the workflow status for a finding<a name="finding-workflow-status"></a>

For findings, the workflow status tracks the progress of your investigation into a finding\.

The workflow status values are as follows\.

`NEW`  
The initial state of a finding, before you review it\.

`NOTIFIED`  
Indicates that you notified the resource owner about the security issue\. You can use this status when you are not the resource owner, and you need intervention from the resource owner in order to resolve a security issue\.

`SUPPRESSED`  
The finding will not be reviewed again and will not be acted upon\.

`RESOLVED`  
The finding was reviewed and remediated and is now considered resolved\.

## Setting the workflow status \(Console\)<a name="finding-workflow-status-console"></a>

To set the workflow status from the finding details for a finding, from **Workflow status**, choose the status\.

You can also set the workflow status for multiple selected findings in the findings list\.

**To set the workflow status for multiple findings**

1. In the findings list, select the check box for each finding that you want to update\.

1. From **Change workflow status**, choose the status\.

## Setting the workflow status \(API\)<a name="finding-workflow-status-api"></a>

To set the workflow status for findings from the Security Hub API, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) API operation\.