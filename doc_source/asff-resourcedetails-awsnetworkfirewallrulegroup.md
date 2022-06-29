# AwsNetworkFirewallRuleGroup<a name="asff-resourcedetails-awsnetworkfirewallrulegroup"></a>

The `AwsNetworkFirewallRuleGroup` object provides details about an AWS Network Firewall rule group\. Rule groups are used to inspect and control network traffic\. * Stateless* rule groups apply to individual packets\. * Stateful* rule groups apply to packets in the context of their traffic flow\.

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
    "Description": "Example rule group",
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