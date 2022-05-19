# Workflow<a name="asff-workflow"></a>

The `Workflow` object provides information about the status of the investigation into a finding\.

It is not intended for finding providers\. It is only to be used by customers and by remediation, orchestration, and ticketing tools used by customers\.

The workflow status can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Customers can also update it from the console\. See [Setting the workflow status for findings](finding-workflow-status.md)\. 

`Workflow` can have the following attributes\.

**`Status`**  
Optional  
The status of your investigation into the finding\. The workflow status is specific to an individual finding\. It does not affect the generation of new findings\. For example, setting the workflow status to `SUPPRESSED` or `RESOLVED` does not prevent a new finding for the same issue\.  
**Type:** Enum  
**Valid values:** `NEW` \| `NOTIFIED` \| `RESOLVED` \| `SUPPRESSED`  
+ `NEW` – The initial state of a finding, before it is reviewed\.

  Security Hub also resets the workflow status from either `NOTIFIED` or `RESOLVED` to `NEW` in the following cases:
  + `RecordState` changes from `ARCHIVED` to `ACTIVE`\.
  + `Compliance.Status` changes from `PASSED` to `FAILED`, `WARNING`, or `NOT_AVAILABLE`\.

  These changes imply that additional investigation is required\.
+ `NOTIFIED` – Indicates that you notified the resource owner about the security issue\. Used when the initial reviewer is not the resource owner and needs intervention from the resource owner\.

  If one of the following occurs, the workflow status is changed automatically from `NOTIFIED` to `NEW`:
  + `RecordState` changes from `ARCHIVED` to `ACTIVE`\.
  + `Compliance.Status` changes from `PASSED` to `FAILED`, `WARNING`, or `NOT_AVAILABLE`\.
+ `RESOLVED` – The finding was reviewed and remediated and is now considered resolved\.

  The finding remains `RESOLVED` unless one of the following occurs:
  + `RecordState` changes from `ARCHIVED` to `ACTIVE`\.
  + `Compliance.Status` changes from `PASSED` to `FAILED`, `WARNING`, or `NOT_AVAILABLE`\.

  In those cases, the workflow status is automatically reset to `NEW`\.

  For findings from controls, if `Compliance.Status` is `PASSED`, then Security Hub automatically sets the workflow status to `RESOLVED`\.
+ `SUPPRESSED` – Indicates that you reviewed the finding and do not believe that any action is needed\.

  The workflow status of a `SUPPRESSED` finding does not change if `RecordState` changes from `ARCHIVED` to `ACTIVE`\.