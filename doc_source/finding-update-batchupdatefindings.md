# Using BatchUpdateFindings to update a finding<a name="finding-update-batchupdatefindings"></a>

Customers \(or SIEM, ticketing, incident management, or SOAR tools working on behalf of a customer to update findings from finding providers\) use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update information related to their processing of existing findings\. [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) cannot be used to create new findings\. It can be used to update up to 100 findings at a time\.

[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) does not change the `UpdatedAt` field for the finding\. `UpdatedAt` only reflects the most recent update from the finding provider\.

Master accounts can use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update findings for their account or for their member accounts\. For those accounts, they can only use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update the following fields and objects\.
+ `Confidence`
+ `Criticality`
+ `Note`
+ `RelatedFindings`
+ `Severity`
+ `Types`
+ `UserDefinedFields`
+ `VerificationState`
+ `Workflow`

Member accounts can only use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update the `Note` object on their findings\.