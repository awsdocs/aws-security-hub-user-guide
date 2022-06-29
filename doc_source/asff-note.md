# Note<a name="asff-note"></a>

The `Note` object adds a user\-defined note to the finding\.

A finding provider can provide an initial note for a finding but cannot add notes after that\. A note can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

To view descriptions of `Note` attributes, see [Note](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Note.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"Note": {
    "Text": "Don't forget to check under the mat.",
    "UpdatedBy": "jsmith",
    "UpdatedAt": "2018-08-31T00:15:09Z"
}
```