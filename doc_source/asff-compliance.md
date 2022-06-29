# Compliance<a name="asff-compliance"></a>

Contains finding details related to a control\. Only returned for findings that are generated as the result of a check that is run on a control\.

To view descriptions of `Compliance` attributes, see [Compliance](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Compliance.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"Compliance": {
    "RelatedRequirements": ["Req1", "Req2"],
    "Status": "FAILED",
    "StatusReasons": [
        {
            "ReasonCode": "CLOUDWATCH_ALARMS_NOT_PRESENT",
            "Description": "CloudWatch alarms do not exist in the account"
        }
    ]
}
```