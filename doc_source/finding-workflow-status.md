# Setting the workflow status for findings<a name="finding-workflow-status"></a>

For findings, the workflow status tracks the progress of your investigation into a finding\.

The workflow status has the following values:

`NEW`  
The initial state of a finding before you review it\.

`NOTIFIED`  
Indicates that you notified the resource owner about the security issue\. You can use this status when you are not the resource owner, and you need intervention from the resource owner in order to resolve a security issue\.

`SUPPRESSED`  
The finding will not be reviewed again and will not be acted upon\.

`RESOLVED`  
The finding was reviewed and remediated and is now considered resolved\.  
For findings from controls, if `Compliance.Status` is `PASSED`, then Security Hub automatically sets the workflow status to `RESOLVED`\.

## Setting the workflow status \(console\)<a name="finding-workflow-status-console"></a>

To set the workflow status from a finding details pane, from **Workflow status**, choose the status\.

You can also set the workflow status for multiple selected findings in a finding list\.

**To set the workflow status for multiple findings \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. To display a finding list, do one of the following:
   + In the Security Hub navigation pane, choose **Findings**\.
   + In the Security Hub navigation pane, choose **Insights**\. Choose an insight\. Then on the results list, choose an insight result\.
   + In the Security Hub navigation pane, choose **Integrations**\. Choose **See findings** for an integration\.
   + In the Security Hub navigation pane, choose **Security standards**\. Choose **View results** to display a list of controls\. Then choose the control name\.

1. In the finding list, select the check box for each finding that you want to update\.

1. At the top of the list, for **Workflow status**, choose the status\.

## Setting the workflow status \(Security Hub API, AWS CLI\)<a name="finding-workflow-status-api"></a>

To set the workflow status, you can use an API call or the AWS Command Line Interface\.

**To set the workflow status of a finding \(Security Hub API, AWS CLI\)**
+ **Security Hub API –** Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) operation\. To identify the finding to update, you must provide both the finding ID and the ARN of the product that generated the finding\.
+ **AWS CLI –** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-update-findings.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-update-findings.html) command\.

  ```
  batch-update-findings --finding-identifiers Id="<findingID>",ProductArn="<productARN>" --workflow Status="<workflowStatus>"
  ```

  **Example**

  ```
  aws securityhub batch-update-findings --finding-identifiers Id="arn:aws:securityhub:us-west-1:123456789012:subscription/pci-dss/v/3.2.1/PCI.Lambda.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",ProductArn="arn:aws:securityhub:us-west-1::product/aws/securityhub" --workflow Status="RESOLVED"
  ```