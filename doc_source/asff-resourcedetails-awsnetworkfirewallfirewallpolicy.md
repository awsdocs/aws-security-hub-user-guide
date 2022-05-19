# AwsNetworkFirewallFirewallPolicy<a name="asff-resourcedetails-awsnetworkfirewallfirewallpolicy"></a>

The `AwsNetworkFirewallFirewallPolicy` object provides details about a firewall policy\. A firewall policy defines the behavior of a network firewall\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsNetworkFirewallFirewallPolicy` object\. To view descriptions of `AwsNetworkFirewallFirewallPolicy` attributes, see [AwsNetworkFirewallFirewallPolicyDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsNetworkFirewallFirewallPolicyDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsNetworkFirewallFirewallPolicy": {
   "FirewallPolicy": {  
    "StatefulRuleGroupReferences": [
        {
            "ResourceArn": "arn:aws:network-firewall:us-east-1:444455556666:stateful-rulegroup/PatchesOnly"
        }
    ],
    "StatelessDefaultActions": [ "aws:forward_to_sfe" ],
    "StatelessFragmentDefaultActions": [ "aws:forward_to_sfe" ],
    "StatelessRuleGroupReferences": [
       {
          "Priority": 1,
          "ResourceArn": "arn:aws:network-firewall:us-east-1:444455556666:stateless-rulegroup/Stateless-1"
       }
     ]
   },
   "FirewallPolicyArn": "arn:aws:network-firewall:us-east-1:444455556666:firewall-policy/InitialFirewall",
   "FirewallPolicyId": "9ceeda22-6050-4048-a0ca-50ce47f0cc65",
   "FirewallPolicyName": "InitialFirewall",
   "Description": "Initial firewall"
}
```