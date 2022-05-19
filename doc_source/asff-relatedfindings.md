# RelatedFindings<a name="asff-relatedfindings"></a>

The `RelatedFindings` object provides a list of findings that are related to the current finding\.

For [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) requests, finding providers should use the `RelatedFindings` object under [`FindingProviderFields`](asff-findingproviderfields.md)\.

**Example**

```
"RelatedFindings": [
    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", 
      "Id": "123e4567-e89b-12d3-a456-426655440000" },
    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", 
      "Id": "AcmeNerfHerder-111111111111-x189dx7824" }
]
```

Each related finding object can have the following attributes\.

**`Id`**  
Required  
The product\-generated identifier for a related finding\.  
**Type:** String or ARN  
**Maximum length:** 512  
**Example**  

```
"Id": "123e4567-e89b-12d3-a456-426655440000"
```

**`ProductArn`**  
Required  
The ARN of the product that generated a related finding\.   
**Type:** ARN  
**Example**  

```
"ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty"
```