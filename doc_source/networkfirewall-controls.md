# AWS Network Firewall controls<a name="networkfirewall-controls"></a>

These controls are related to Network Firewall resources\.

## \[NetworkFirewall\.3\] Network Firewall policies should have at least one rule group associated<a name="networkfirewall-3"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure Network Configuration

**Severity:** Medium

**Resource type:** `AWS::NetworkFirewall::FirewallPolicy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-rule-group-associated.html](https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-rule-group-associated.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a Network Firewall policy has any stateful or stateless rule groups associated\. The control fails if stateless or stateful rule groups are not assigned\.

A firewall policy defines how your firewall monitors and handles traffic in Amazon Virtual Private Cloud \(Amazon VPC\)\. Configuration of stateless and stateful rule groups helps to filter packets and traffic flows, and defines default traffic handling\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="networkfirewall-3-remediation"></a>

To add a rule group to a Network Firewall policy, see [Updating a firewall policy](https://docs.aws.amazon.com/network-firewall/latest/developerguide/firewall-policy-updating.html) in the *AWS Network Firewall Developer Guide*\. For information about creating and managing rule groups, see [Rule groups in AWS Network Firewall](https://docs.aws.amazon.com/network-firewall/latest/developerguide/rule-groups.html)\.

## \[NetworkFirewall\.4\] The default stateless action for Network Firewall policies should be drop or forward for full packets<a name="networkfirewall-4"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure Network Configuration

**Severity:** Medium

**Resource type:** `AWS::NetworkFirewall::FirewallPolicy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-default-action-full-packets.html](https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-default-action-full-packets.html)

**Schedule type:** Change triggered

**Parameters:**
+ `statelessDefaultActions: aws:drop,aws:forward_to_sfe`

This control checks whether the default stateless action for full packets for a Network Firewall policy is drop or forward\. The control passes if `Drop` or `Forward` is selected, and fails if `Pass` is selected\.

A firewall policy defines how your firewall monitors and handles traffic in Amazon VPC\. You configure stateless and stateful rule groups to filter packets and traffic flows\. Defaulting to `Pass` can allow unintended traffic\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="networkfirewall-4-remediation"></a>

**To change the firewall policy:**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, under **Network Firewall**, choose **Firewall policies**\.

1. Select the name of the firewall policy that you want to edit\. This takes you to the firewall policy's details page\.

1. In **Stateless Default Actions**, choose **Edit**\. Then choose **Drop** or **Forward to stateful rule groups** as the **Default actions for full packets**\.

## \[NetworkFirewall\.5\] The default stateless action for Network Firewall policies should be drop or forward for fragmented packets<a name="networkfirewall-5"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure Network Configuration

**Severity:** Medium

**Resource type:** `AWS::NetworkFirewall::FirewallPolicy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-default-action-fragment-packets.html](https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-default-action-fragment-packets.html)

**Schedule type:** Change triggered

**Parameters:**
+ `statelessFragDefaultActions (Required) : aws:drop, aws:forward_to_sfe`

This control checks whether the default stateless action for fragmented packets for a Network Firewall policy is drop or forward\. The control passes if `Drop` or `Forward` is selected, and fails if `Pass` is selected\.

A firewall policy defines how your firewall monitors and handles traffic in Amazon VPC\. You configure stateless and stateful rule groups to filter packets and traffic flows\. Defaulting to `Pass` can allow unintended traffic\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="networkfirewall-5-remediation"></a>

**To change the firewall policy:**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, under **Network Firewall**, choose **Firewall policies**\.

1. Select the name of the firewall policy that you want to edit\. This takes you to the firewall policy's details page\.

1. In **Stateless Default Actions**, choose **Edit**\. Then choose **Drop** or **Forward to stateful rule groups** as the **Default actions for fragmented packets**\.

## \[NetworkFirewall\.6\] Stateless Network Firewall rule group should not be empty<a name="networkfirewall-6"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(5\)

**Category:** Protect > Secure Network Configuration

**Severity:** Medium

**Resource type:** `AWS::NetworkFirewall::RuleGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/netfw-stateless-rule-group-not-empty.html](https://docs.aws.amazon.com/config/latest/developerguide/netfw-stateless-rule-group-not-empty.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if a stateless rule group in AWS Network Firewall contains rules\. The rule will fail if there are no rules in the rule group\.

A rule group contains rules that define how your firewall processes traffic in your VPC\. An empty stateless rule group, when present in a firewall policy, might give the impression that the rule group will process traffic\. However, when the stateless rule group is empty, it does not process traffic\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="networkfirewall-6-remediation"></a>

**To add rules to a Network Firewall rule group:**

1. Sign in to the AWS Management Console and open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)

1. In the navigation pane, under **Network Firewall**, choose **Network Firewall rule groups**\.

1. In the **Network Firewall rule groups** page, choose the name of the rule group that you want to edit\. This takes you to the firewall rule groups details page\.

1. For stateless rule groups, choose **Edit Rules** to add rules to the rule group\.