# Workflow<a name="asff-workflow"></a>

The `Workflow` object provides information about the status of the investigation into a finding\.

It is not intended for finding providers\. It is only to be used by customers and by remediation, orchestration, and ticketing tools used by customers\.

The workflow status can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Customers can also update it from the console\. See [Setting the workflow status for findings](finding-workflow-status.md)\.

To view descriptions of `Workflow` attributes, see [Workflow](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Workflow.html) in the *AWS Security Hub API Reference*\.