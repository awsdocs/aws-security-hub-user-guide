# RelatedFindings<a name="asff-relatedfindings"></a>

The `RelatedFindings` object provides a list of findings that are related to the current finding\.

For [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) requests, finding providers should use the `RelatedFindings` object under [`FindingProviderFields`](asff-findingproviderfields.md)\.

To view descriptions of `RelatedFindings` attributes, see [RelatedFinding](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_RelatedFinding.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"RelatedFindings": [
    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", 
      "Id": "123e4567-e89b-12d3-a456-426655440000" },
    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", 
      "Id": "AcmeNerfHerder-111111111111-x189dx7824" }
]
```