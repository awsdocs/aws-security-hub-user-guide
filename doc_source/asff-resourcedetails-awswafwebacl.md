# AwsWafWebAcl<a name="asff-resourcedetails-awswafwebacl"></a>

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