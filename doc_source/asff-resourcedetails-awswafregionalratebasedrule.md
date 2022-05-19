# AwsWafRegionalRateBasedRule<a name="asff-resourcedetails-awswafregionalratebasedrule"></a>

The `AwsWafRegionalRateBasedRule` object contains details about a rate\-based rule for Regional resources\. A rate\-based rule provides settings to indicate when to allow, block, or count a request\. Rate\-based rules include the number of requests that arrive over a specified period of time\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsWafRegionalRateBasedRule` object\. To view descriptions of `AwsWafRegionalRateBasedRule` attributes, see [AwsWafRegionalRateBasedRuleDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsWafRegionalRateBasedRuleDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsWafRegionalRateBasedRule":{
    "MatchPredicates" : [{
        "DataId" : "391b7a7e-5f00-40d2-b114-3f27ceacbbb0",
        "Negated" : "True",
        "Type" : "IPMatch" ,
    }],
    "MetricName" : "MetricName",
    "Name" : "Test",
    "RateKey" : "IP",
    "RateLimit" : 235000,
    "RuleId" : "5dfb4085-f103-4ec6-b39a-d4a0dae5f47f"
}
```

The following is a list of valid value examples for `AwsWafRegionalRateBasedRule` attributes:
+ `MatchPredicates Type`

  Valid values: `IPMatch` \| `ByteMatch` \| `SqlInjectionMatch` \| `GeoMatch` \| `SizeConstraint` \| `XssMatch` \| `RegexMatch`