# AwsWafRuleGroup<a name="asff-resourcedetails-awswafrulegroup"></a>

`AwsWafRuleGroup` provides information about an AWS WAF rule group\. A rule group is a collection of predefined rules that you add to a web access control list \(web ACL\)\.

The following is an example `AwsWafRuleGroup` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsApiGatewayV2Stage` attributes, see [AwsWafRuleGroupDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsWafRuleGroupDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsWafRuleGroup": {
    "MetricName": "SampleWAF_Metric_1",
    "Name": "bb-WAFRuleGroupWithRuleCompliant",
    "RuleGroupId": "2012ca6d-e66d-4d9b-b766-bfb03ad77cfb",
    "Rules": [{
        "Action": {
            "Type": "ALLOW",
        },
        "Priority": 1,
        "RuleId": "cdd225da-32cf-4773-8dc5-3bca3ed9c19c",
        "Type": "REGULAR"
    }]
}
```