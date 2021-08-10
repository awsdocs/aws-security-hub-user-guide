# Using BatchImportFindings to create and update findings<a name="finding-update-batchimportfindings"></a>

Finding providers use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) API operation to create new findings and to update information about the findings they created\. They cannot update findings that they did not create\.

Customers, SIEMs, ticketing tools, and SOAR tools use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to make updates related to their processing of findings from finding providers\. See [Using BatchUpdateFindings to update a finding](finding-update-batchupdatefindings.md)\.

Whenever Security Hub receives a [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) request to either create or update a finding, it automatically generates a **Security Hub Findings \- Imported** event in Amazon EventBridge\. See [Automated response and remediation](securityhub-cloudwatch-events.md)\.

AWS Security Hub can only accept finding updates for accounts that have Security Hub enabled\. The finding provider also must be enabled\. If Security Hub is disabled, or the finding provider integration is not enabled, then the findings are returned in the `FailedFindings` list, with an `InvalidAccess` error\.

For [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html), Security Hub accepts up to 100 findings per batch, up to 240 KB per finding, and up to 6 MB per batch\. The throttle rate limit is 10 TPS per account per Region, with a burst of 30 TPS\.

## Determining whether to create or update a finding<a name="batchimportfindings-create-or-update"></a>

To determine whether to create or update a finding, Security Hub checks the `ID` field\. If the value of `ID` does not match an existing finding, then a new finding is created\.

If `ID` does match an existing finding, then Security Hub checks the `UpdatedAt` field for the update\.
+ If `UpdatedAt` on the update matches or occurs before `UpdatedAt` on the existing finding, then the update is ignored\.
+ If `UpdatedAt` on the update occurs after `UpdatedAt` on the existing finding, then the existing finding is updated\.

## Restricted attributes for BatchImportFindings<a name="batchimportfindings-restricted-fields"></a>

For an existing finding, finding providers cannot use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) to update the following attributes and objects\. These attributes can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.
+ `Note`
+ `UserDefinedFields`
+ `VerificationState`
+ `Workflow`

Security Hub ignores any content in [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) for those attributes and objects\. Customers, or other providers acting on their behalf, use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update them\.

## Using FindingProviderFields<a name="batchimportfindings-findingproviderfields"></a>

Finding providers also should not use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) to update the following attributes\.
+ `Confidence`
+ `Criticality`
+ `RelatedFindings`
+ `Severity`
+ `Types`

Instead, finding providers use the [`FindingProviderFields`](securityhub-findings-format-attributes.md#asff-findingproviderfields) object to provide values for these attributes\.

**Example**

```
"FindingProviderFields": {
    "Confidence": 42,
    "Criticality": 99,
    "RelatedFindings":[
      { 
        "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", 
        "Id": "123e4567-e89b-12d3-a456-426655440000" 
      }
    ],
    "Severity": {
        "Label": "MEDIUM", 
        "Original": "MEDIUM"
    },
    "Types": [ "Software and Configuration Checks/Vulnerabilities/CVE" ]
}
```

For [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) requests, Security Hub handles values in the top\-level attributes and in [`FindingProviderFields`](securityhub-findings-format-attributes.md#asff-findingproviderfields) as follows\.

**\(Preferred\) [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) provides a value for an attribute in [`FindingProviderFields`](securityhub-findings-format-attributes.md#asff-findingproviderfields), but does not provide a value for the corresponding top\-level attribute\.**  
For example, [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) provides `FindingProviderFields.Confidence`, but does not provide `Confidence`\. This is the preferred option for [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) requests\.  
Security Hub updates the value of the attribute in [`FindingProviderFields`](securityhub-findings-format-attributes.md#asff-findingproviderfields)\.  
It replicates the value to the top\-level attribute only if the attribute was not already updated by [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

**[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) provides a value for a top\-level attribute, but does not provide a value for the corresponding attribute in [`FindingProviderFields`](securityhub-findings-format-attributes.md#asff-findingproviderfields)\.**  
For example, [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) provides `Confidence`, but does not provide `FindingProviderFields.Confidence`\.  
Security Hub uses the value to update the attribute in [`FindingProviderFields`](securityhub-findings-format-attributes.md#asff-findingproviderfields)\. It overwrites any existing value\.  
Security Hub updates the top\-level attribute only if the attribute was not already updated by [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

**[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) provides a value for both a top\-level attribute and the corresponding attribute in [`FindingProviderFields`](securityhub-findings-format-attributes.md#asff-findingproviderfields)\.**  
For example, [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) provides both `Confidence` and `FindingProviderFields.Confidence`\.  
For a new finding, Security Hub uses the value in [`FindingProviderFields`](securityhub-findings-format-attributes.md#asff-findingproviderfields) to populate both the top\-level attribute and the corresponding attribute in [`FindingProviderFields`](securityhub-findings-format-attributes.md#asff-findingproviderfields)\. It does not use the provided top\-level attribute value\.  
For an existing finding, Security Hub uses both values\. However, it updates the top\-level attribute value only if the attribute was not already updated by [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

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
        "FindingProviderFields": {
            "Severity": {
                "Label": "INFORMATIONAL",
                "Original": "0"
            },
            "Types": [
                "Software and Configuration Checks/Vulnerabilities/CVE"
            ]
        },
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
        "Title": "CloudTrail trail vulnerability",
        "UpdatedAt": "2020-06-02T16:05:54.832Z"
    }]'
```