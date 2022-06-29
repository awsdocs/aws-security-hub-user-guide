# AwsWafRule<a name="asff-resourcedetails-awswafrule"></a>

`AwsWafRule` provides information about an AWS WAF rule\. A rule identifies the web requests that you want to allow, block, or count\.

The following is an example `AwsWafRule` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsApiGatewayV2Stage` attributes, see [AwsWafRuleDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsWafRuleDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsWafRule": {
    "MetricName": "AwsWafRule_Metric_1",
    "Name": "AwsWafRule_Name_1",
    "PredicateList": [{
        "DataId": "cdd225da-32cf-4773-1dc2-3bca3ed9c19c",
        "Negated": false,
        "Type": "GeoMatch"
    }],
    "RuleId": "8f651760-24fa-40a6-a9ed-4b60f1de953e"
}
```