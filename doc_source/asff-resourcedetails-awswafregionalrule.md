# AwsWafRegionalRule<a name="asff-resourcedetails-awswafregionalrule"></a>

The `AwsWafRegionalRule` object provides details about an AWS WAF Regional rule \. This rule identifies the web requests that you want to allow, block, or count\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsWafRegionalRule` object\. To view descriptions of `AwsWafRegionalRule` attributes, see [AwsWafRegionalRuleDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsWafRegionalRuleDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsWafRegionalRule": { 
    "MetricName": "SampleWAF_Rule__Metric_1",
    "Name": "bb-waf-regional-rule-not-empty-conditions-compliant",
    "RuleId": "8f651760-24fa-40a6-a9ed-4b60f1de95fe",
    "PredicateList": [{
        "DataId": "127d9346-e607-4e93-9286-c1296fb5445a",
        "Negated": false,
        "Type": "GeoMatch"
    }]
}
```