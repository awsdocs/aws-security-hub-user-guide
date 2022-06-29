# ThreatIntelIndicators<a name="asff-threatintelindicators"></a>

This is an example of threat intelligence details that are related to a finding\.

This object is an array of up to five threat intelligence indicator objects\.

To view descriptions of `ThreatIntelIndicators` attributes, see [ThreatIntelIndicator](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ThreatIntelIndicator.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"ThreatIntelIndicators": [
  {
    "Type": "IPV4_ADDRESS",
    "Value": "8.8.8.8",
    "Category": "BACKDOOR",
    "LastObservedAt": "2018-09-27T23:37:31Z",
    "Source": "Threat Intel Weekly",
    "SourceUrl": "http://threatintelweekly.org/backdoors/8888"
  }
]
```