# Using BatchImportFindings to create and update findings<a name="finding-update-batchimportfindings"></a>

Finding providers use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) API operation to create new findings and to update information about the findings they created\. They cannot update findings that they did not create\.

Customers, SIEMs, ticketing tools, and SOAR tools use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to make updates related to their processing of findings from finding providers\. See [Using BatchUpdateFindings to update a finding](finding-update-batchupdatefindings.md)\.

AWS Security Hub can only accept finding updates for accounts that have Security Hub enabled\. The finding provider also must be enabled\. If Security Hub is disabled, or the finding provider integration is not enabled, then the findings are returned in the `FailedFindings` list, with an `InvalidAccess` error\.

The payload for a [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) call cannot be larger than 6MB\.

## Determining whether to create or update a finding<a name="batchimportfindings-create-or-update"></a>

To determine whether to create or update a finding, Security Hub checks the `ID` field\. If the value of `ID` does not match an existing finding, then a new finding is created\.

If `ID` does match an existing finding, then Security Hub checks the `UpdatedAt` field for the update\.
+ If `UpdatedAt` on the update occurs before `UpdatedAt` on the existing finding, then the update is ignored\.
+ If `UpdatedAt` on the update occurs after `UpdatedAt` on the existing finding, then the existing finding is updated\.

## Restricted fields for BatchImportFindings<a name="batchimportfindings-restricted-fields"></a>

For an existing finding, finding providers cannot use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) to update the following fields and objects\. These fields can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.
+ `Confidence`
+ `Criticality`
+ `Note`
+ `RelatedFindings`
+ `Severity`
+ `Types`
+ `UserDefinedFields`
+ `VerificationState`
+ `Workflow`

Any content in those fields and objects is ignored\.