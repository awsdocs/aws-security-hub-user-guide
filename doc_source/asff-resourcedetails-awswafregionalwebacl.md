# AwsWafRegionalWebAcl<a name="asff-resourcedetails-awswafregionalwebacl"></a>

`AwsWafRegionalWebAcl` provides details about a Regional web access control list \(web ACL\)\. A web ACL contains the rules that identify the requests that you want to allow, block, or count\.

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