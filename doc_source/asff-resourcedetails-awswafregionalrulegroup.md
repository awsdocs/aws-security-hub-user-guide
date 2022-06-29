# AwsWafRegionalRuleGroup<a name="asff-resourcedetails-awswafregionalrulegroup"></a>

The `AwsWafRegionalRuleGroup` object provides details about an AWS WAF Regional rule group\. A rule group is a collection of predefined rules that you add to a web access control list \(web ACL\)\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsWafRegionalRuleGroup` object\. To view descriptions of `AwsWafRegionalRuleGroup` attributes, see [AwsWafRegionalRuleGroupDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsWafRegionalRuleGroupDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsWafRegionalRuleGroup": { 
    "MetricName": "SampleWAF_Metric_1",
    "Name": "bb-WAFClassicRuleGroupWithRuleCompliant",
    "RuleGroupId": "2012ca6d-e66d-4d9b-b766-bfb03ad77cfb",
    "Rules": [{
        "Action": {
            "Type": "ALLOW"
        }
    }],
        "Priority": 1,
        "RuleId": "cdd225da-32cf-4773-8dc5-3bca3ed9c19c",
        "Type": "REGULAR"
}
```