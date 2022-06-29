# Remediation<a name="asff-remediation"></a>

The `Remediation` object provides information about recommended remediation steps to address the finding\.

To view descriptions of `Remediation` attributes, see [Remediation](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Remediation.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"Remediation": {
    "Recommendation": {
        "Text": "Run sudo yum update and cross your fingers and toes.",
        "Url": "http://myfp.com/recommendations/dangerous_things_and_how_to_fix_them.html"
    }
}
```