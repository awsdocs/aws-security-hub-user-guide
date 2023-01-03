# AwsWaf<a name="asff-resourcedetails-awswaf"></a>

The following are examples of the AWS Security Finding Format for `AwsWaf` resources\.

## AwsWafRateBasedRule<a name="asff-resourcedetails-awswafratebasedrule"></a>

The `AwsWafRateBasedRule` object contains details about an AWS WAF rate\-based rule for global resources\. An AWS WAF rate\-based rule provides settings to indicate when to allow, block, or count a request\. Rate\-based rules include the number of requests that arrive over a specified period of time\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsWafRateBasedRule` object\. To view descriptions of `AwsWafRateBasedRule` attributes, see [AwsWafRateBasedRuleDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsWafRateBasedRuleDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsWafRateBasedRule":{
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

## AwsWafRegionalRateBasedRule<a name="asff-resourcedetails-awswafregionalratebasedrule"></a>

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

## AwsWafRegionalRule<a name="asff-resourcedetails-awswafregionalrule"></a>

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

## AwsWafRegionalRuleGroup<a name="asff-resourcedetails-awswafregionalrulegroup"></a>

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

## AwsWafRegionalWebAcl<a name="asff-resourcedetails-awswafregionalwebacl"></a>

`AwsWafRegionalWebAcl` provides details about an AWS WAF Regional web access control list \(web ACL\)\. A web ACL contains the rules that identify the requests that you want to allow, block, or count\.

The following is an example `AwsWafRegionalWebAcl` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsApiGatewayV2Stage` attributes, see [AwsWafRegionalWebAclDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsWafRegionalWebAclDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsWafRegionalWebAcl": {
    "DefaultAction": "ALLOW",
    "MetricName" : "web-regional-webacl-metric-1",
    "Name": "WebACL_123",
    "RulesList": [
        {
            "Action": {
                "Type": "Block"
            },
            "Priority": 3,
            "RuleId": "24445857-852b-4d47-bd9c-61f05e4d223c",
            "Type": "REGULAR",
            "ExcludedRules": [
                {
                    "ExclusionType": "Exclusion",
                    "RuleId": "Rule_id_1"
                }
            ],
            "OverrideAction": {
                "Type": "OVERRIDE"
            }
        }
    ],
    "WebAclId": "443c76f4-2e72-4c89-a2ee-389d501c1f67"
}
```

## AwsWafRule<a name="asff-resourcedetails-awswafrule"></a>

`AwsWafRule` provides information about an AWS WAF rule\. An AWS WAF rule identifies the web requests that you want to allow, block, or count\.

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

## AwsWafRuleGroup<a name="asff-resourcedetails-awswafrulegroup"></a>

`AwsWafRuleGroup` provides information about an AWS WAF rule group\. An AWS WAF rule group is a collection of predefined rules that you add to a web access control list \(web ACL\)\.

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

## AwsWafv2RuleGroup<a name="asff-resourcedetails-awswafv2rulegroup"></a>

The `AwsWafv2RuleGroup` object provides details about an AWS WAFV2 rule group\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsWafv2RuleGroup` object\. To view descriptions of `AwsWafv2RuleGroup` attributes, see [AwsWafv2RuleGroupDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsWafv2RuleGroupDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsWafv2RuleGroup": {
    "Arn": "arn:aws:wafv2:us-east-1:123456789012:global/rulegroup/wafv2rulegroupasff/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
    "Capacity": 1000,
    "Description": "Resource for ASFF",
    "Id": "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
    "Name": "wafv2rulegroupasff",
    "Rules": [{
    	"Action": {
    	"Allow": {
    		"CustomRequestHandling": {
    			"InsertHeaders": [
    				{
    				"Name": "AllowActionHeader1Name",
    				"Value": "AllowActionHeader1Value"
    				},
    				{
    				"Name": "AllowActionHeader2Name",
    				"Value": "AllowActionHeader2Value"
    				}
    			]
    		}
    	},
    	"Name": "RuleOne",
    	"Priority": 1,
    	"VisibilityConfig": {
    		"CloudWatchMetricsEnabled": true,
    		"MetricName": "rulegroupasff",
    		"SampledRequestsEnabled": false
    	}
    }],
    "VisibilityConfig": {
    	"CloudWatchMetricsEnabled": true,
    	"MetricName": "rulegroupasff",
    	"SampledRequestsEnabled": false
    }
}
```

## AwsWafWebAcl<a name="asff-resourcedetails-awswafwebacl"></a>

The `AwsWafWebAcl` object provides details about an AWS WAF web ACL\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsWafWebAcl` object\. To view descriptions of `AwsWafWebAcl` attributes, see [AwsWafWebAclDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsWafWebAclDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsWafWebAcl": {
    "DefaultAction": "ALLOW",
    "Name": "MyWafAcl",
    "Rules": [
        {
            "Action": {
                "Type": "ALLOW"
            },
            "ExcludedRules": [
                {
                    "RuleId": "5432a230-0113-5b83-bbb2-89375c5bfa98"
                }
            ],
            "OverrideAction": {
                "Type": "NONE"
            },
            "Priority": 1,
            "RuleId": "5432a230-0113-5b83-bbb2-89375c5bfa98",
            "Type": "REGULAR"
        }
    ],
    "WebAclId": "waf-1234567890"
}
```

## AwsWafv2WebAcl<a name="asff-resourcedetails-awswafv2webacl"></a>

The `AwsWafv2WebAcl` object provides details about an AWS WAFV2 web ACL\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsWafv2WebAcl` object\. To view descriptions of `AwsWafv2WebAcl` attributes, see [AwsWafv2WebAclDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsWafv2WebAclDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsWafv2WebAcl": {
    "Arn": "arn:aws:wafv2:us-east-1:123456789012:regional/webacl/WebACL-RoaD4QexqSxG/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
    "Capacity": 1326,
    "CaptchaConfig": {
    	"ImmunityTimeProperty": {
    		"ImmunityTime": 500
    	}
    },
    "DefaultAction": {
    	"Block": {}
    },
    "Description": "Web ACL for JsonBody testing",
    "ManagedbyFirewallManager": false,
    "Name": "WebACL-RoaD4QexqSxG",
    "Rules": [{
    	"Action": {
    		"RuleAction": {
    			"Block": {}
    		}
    	},
    	"Name": "TestJsonBodyRule",
    	"Priority": 1,
    	"VisibilityConfig": {
    		"SampledRequestsEnabled": true,
    		"CloudWatchMetricsEnabled": true,
    		"MetricName": "JsonBodyMatchMetric"
    	}
    }],
    "VisibilityConfig": {
    	"SampledRequestsEnabled": true,
    	"CloudWatchMetricsEnabled": true,
    	"MetricName": "TestingJsonBodyMetric"
    }
}
```