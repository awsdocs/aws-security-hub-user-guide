# AwsNetworkFirewall<a name="asff-resourcedetails-awsnetworkfirewall"></a>

The following are examples of the AWS Security Finding Format for `AwsNetworkFirewall` resources\.

## AwsNetworkFirewallFirewall<a name="asff-resourcedetails-awsnetworkfirewallfirewall"></a>

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

## AwsNetworkFirewallFirewallPolicy<a name="asff-resourcedetails-awsnetworkfirewallfirewallpolicy"></a>

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

## AwsNetworkFirewallRuleGroup<a name="asff-resourcedetails-awsnetworkfirewallrulegroup"></a>

The `AwsNetworkFirewallRuleGroup` object provides details about an AWS Network Firewall rule group\. Rule groups are used to inspect and control network traffic\. Stateless rule groups apply to individual packets\. Stateful rule groups apply to packets in the context of their traffic flow\.

Rule groups are referenced in firewall policies\.

The following examples show the AWS Security Finding Format \(ASFF\) for the `AwsNetworkFirewallRuleGroup` object\. To view descriptions of `AwsNetworkFirewallRuleGroup` attributes, see [AwsNetworkFirewallRuleGroupDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsNetworkFirewallRuleGroupDetails.html) in the *AWS Security Hub API Reference*\.

**Example – stateless rule group**

```
"AwsNetworkFirewallRuleGroup": {
    "Capacity": 600,
    "RuleGroupArn": "arn:aws:network-firewall:us-east-1:444455556666:stateless-rulegroup/Stateless-1",
    "RuleGroupId": "fb13c4df-b6da-4c1e-91ec-84b7a5487493",
    "RuleGroupName": "Stateless-1"
    "Description": "Example of a stateless rule group",
    "Type": "STATELESS",
    "RuleGroup": {
        "RulesSource": {
            "StatelessRulesAndCustomActions": {
                "CustomActions": [],
                "StatelessRules": [
                    {
                        "Priority": 1,
                        "RuleDefinition": {
                            "Actions": [
                                "aws:pass"
                            ],
                            "MatchAttributes": {
                                "DestinationPorts": [
                                    {
                                        "FromPort": 443,
                                        "ToPort": 443
                                    }
                                ],
                                "Destinations": [
                                    {
                                        "AddressDefinition": "192.0.2.0/24"
                                    }
                                ],
                                "Protocols": [
                                            6
                                ],
                                "SourcePorts": [
                                    {
                                        "FromPort": 0,
                                        "ToPort": 65535
                                    }
                                ],
                                "Sources": [
                                    {
                                         "AddressDefinition": "198.51.100.0/24"
                                    }
                                ]
                            }
                        }
                    }
                ]
            }
        }
    }
}
```

**Example – stateful rule group**

```
"AwsNetworkFirewallRuleGroup": {
    "Capacity": 100,
    "RuleGroupArn": "arn:aws:network-firewall:us-east-1:444455556666:stateful-rulegroup/tupletest",
    "RuleGroupId": "38b71c12-da80-4643-a6c5-03337f8933e0",
    "RuleGroupName": "ExampleRuleGroup",
    "Description": "Example of a stateful rule group",
    "Type": "STATEFUL",
    "RuleGroup": {
        "RuleSource": {
             "StatefulRules": [
                 {
                     "Action": "PASS",
                     "Header": {
                         "Destination": "Any",
                         "DestinationPort": "443",
                         "Direction": "ANY",
                         "Protocol": "TCP",
                         "Source": "Any",
                         "SourcePort": "Any"
                     },
                     "RuleOptions": [
                         {
                            "Keyword": "sid:1"
                         }
                     ]      
                 }
             ]
         }
    }
}
```

The following is a list of valid value examples for `AwsNetworkFirewallRuleGroup` attributes:
+ `Action`

  Valid values: `PASS` \| `DROP` \| `ALERT`
+ `Protocol`

  Valid values: `IP` \| `TCP` \| `UDP` \| `ICMP` \| `HTTP` \| `FTP` \| `TLS` \| `SMB` \| `DNS` \| `DCERPC` \| `SSH` \| `SMTP` \| `IMAP` \| `MSN` \| `KRB5` \| `IKEV2` \| `TFTP` \| `NTP` \| `DHCP`
+ `Flags`

  Valid values: `FIN` \| `SYN` \| `RST` \| `PSH` \| `ACK` \| `URG` \| `ECE` \| `CWR`
+ `Masks`

  Valid values: `FIN` \| `SYN` \| `RST` \| `PSH` \| `ACK` \| `URG` \| `ECE` \| `CWR`