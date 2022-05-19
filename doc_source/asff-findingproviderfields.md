# FindingProviderFields<a name="asff-findingproviderfields"></a>

In a [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) request, finding providers use `FindingProviderFields` to provide values for attributes that should only be updated by [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

For details on how Security Hub handles updates from [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) to `FindingProviderFields` and to the corresponding top\-level attributes, see [Using FindingProviderFields](finding-update-batchimportfindings.md#batchimportfindings-findingproviderfields)\.

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

`FindingProviderFields` can contain the following attributes\.

`Confidence`  
Optional  
A finding's confidence\. Confidence is defined as the likelihood that a finding accurately identifies the behavior or issue that it was intended to identify\.  
**Type:** Integer \(range 0–100\)  
`Confidence` is scored on a 0–100 basis using a ratio scale, where 0 means 0\-percent confidence and 100 means 100\-percent confidence\.

`Criticality`  
Optional  
The level of importance that is assigned to the resources that are associated with the finding\. A score of 0 means that the underlying resources have no criticality, and a score of 100 is reserved for the most critical resources\.  
**Type:** Integer  
**Minimum value:** 0  
**Maximum value:** 100  
`Criticality` is scored on a 0–100 basis, using a ratio scale that supports only full integers\. A score of 0 means that the underlying resources have no criticality, and a score of 100 is reserved for the most critical resources\.

[`RelatedFindings`](asff-relatedfindings.md)  
Optional  
A list of related findings\.  
**Type:** Array of `RelatedFinding` objects  
**Maximum number of objects:** 10

`Severity`  
Required  
Details about the severity of the finding\.  
Finding providers can use the `Severity` object in `FindingProviderFields` to provide values for `Label` and `Original`\.  
For details on the available values for `Label` and `Original`, and guidance on how to assess severity, see the information for the [`Severity` object](asff-severity.md)\.  
**Type:** Object

`Types`  
Required  
One or more finding types in the format of *namespace/category/classifier* that classify a finding\.  
**Type:** Array of strings  
**Maximum number of strings:** 50