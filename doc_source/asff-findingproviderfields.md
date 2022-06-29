# FindingProviderFields<a name="asff-findingproviderfields"></a>

In a [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) request, finding providers use `FindingProviderFields` to provide values for attributes that should only be updated by [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

For details on how Security Hub handles updates from [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) to `FindingProviderFields` and to the corresponding top\-level attributes, see [Using FindingProviderFields](finding-update-batchimportfindings.md#batchimportfindings-findingproviderfields)\.

To view descriptions of `FindingProviderFields` attributes, see [FindingProviderFields](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_FindingProviderFields.html) in the *AWS Security Hub API Reference*\.

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