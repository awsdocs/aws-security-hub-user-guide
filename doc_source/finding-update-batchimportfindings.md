# Using BatchImportFindings to create and update findings<a name="finding-update-batchimportfindings"></a>

Finding providers use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) API operation to create new findings and to update information about the findings they created\. They cannot update findings that they did not create\.

Customers, SIEMs, ticketing tools, and SOAR tools use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to make updates related to their processing of findings from finding providers\. See [Using BatchUpdateFindings to update a finding](finding-update-batchupdatefindings.md)\.

AWS Security Hub can only accept finding updates for accounts that have Security Hub enabled\. The finding provider also must be enabled\. If Security Hub is disabled, or the finding provider integration is not enabled, then the findings are returned in the `FailedFindings` list, with an `InvalidAccess` error\.

The payload for a [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) call cannot be larger than 6 MB\.

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

## Using the batch\-import\-findings command from the AWS CLI<a name="batchimportfindings-command-line"></a>

In the AWS Command Line Interface, you use the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-import-findings.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-import-findings.html) command to create or update findings\.

You provide each finding as a JSON object\.

**Example**

```
aws securityhub batch-import-findings --findings '                  
    [{
        "AwsAccountId": "123456789012",
        "CreatedAt": "2019-08-07T17:05:54.832Z",
        "Description": "Vulnerability in a CloudTrail trail",
        "GeneratorId": "TestGeneratorId",
        "Id": "Id1",
        "ProductArn": "arn:aws:securityhub:us-west-1:123456789012:product/123456789012/default",
        "Resources": [
            {
                "Id": "arn:aws:cloudtrail:us-west-1:123456789012:trail/TrailName",
                "Partition": "aws",
                "Region": "us-west-1",
                "Type": "AwsCloudTrailTrail"
            }
        ],
        "SchemaVersion": "2018-10-08",
        "Severity": {
            "Normalized": 0,
            "Product": 0
        },
        "Title": "CloudTrail trail vulnerability",
        "Types": [
            "Software and Configuration Checks/Vulnerabilities/CVE"
        ],
        "UpdatedAt": "2020-06-02T16:05:54.832Z"
    }]'
```