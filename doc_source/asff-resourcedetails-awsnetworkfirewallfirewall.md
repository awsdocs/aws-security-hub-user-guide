# AwsNetworkFirewallFirewall<a name="asff-resourcedetails-awsnetworkfirewallfirewall"></a>

The `AwsNetworkFirewallFirewall` object contains details about an AWS Network Firewall firewall\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsNetworkFirewallFirewall` object\. To view descriptions of `AwsNetworkFirewallFirewall` attributes, see [AwsNetworkFirewallFirewallDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsNetworkFirewallFirewallDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsNetworkFirewallFirewall": {
    "DeleteProtection": false,
    "FirewallArn": "arn:aws:network-firewall:us-east-1:024665936331:firewall/testfirewall", 
    "FirewallPolicyArn": "arn:aws:network-firewall:us-east-1:444455556666:firewall-policy/InitialFirewall",
    "FirewallId": "dea7d8e9-ae38-4a8a-b022-672a830a99fa",
    "FirewallName": "testfirewall",
    "FirewallPolicyChangeProtection": false,
    "SubnetChangeProtection": false,
    "SubnetMappings": [
        {
            "SubnetId": "subnet-0183481095e588cdc"
        },
        {
            "SubnetId": "subnet-01f518fad1b1c90b0"
        }
    ],
    "VpcId": "vpc-40e83c38"
}
```