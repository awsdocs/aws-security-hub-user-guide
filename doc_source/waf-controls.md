# AWS WAF controls<a name="waf-controls"></a>

These controls are related to AWS WAF resources\.

## \[WAF\.1\] AWS WAF Classic Global Web ACL logging should be enabled<a name="waf-1"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-7\(8\)

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::WAF::WebACL`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-classic-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-classic-logging-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether logging is enabled for an AWS WAF global web ACL\. This control fails if logging is not enabled for the web ACL\.

Logging is an important part of maintaining the reliability, availability, and performance of AWS WAF globally\. It is a business and compliance requirement in many organizations, and allows you to troubleshoot application behavior\. It also provides detailed information about the traffic that is analyzed by the web ACL that is attached to AWS WAF\.

**Note**  
This control is not supported in the following Regions:  
US East \(Ohio\)
US West \(N\. California\)
US West \(Oregon\)
Africa \(Cape Town\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Osaka\)
Asia Pacific \(Seoul\)
Asia Pacific \(Singapore\)
Asia Pacific \(Sydney\)
Asia Pacific \(Tokyo\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Frankfurt\)
Europe \(Ireland\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
South America \(São Paulo\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="waf-1-remediation"></a>

You can enable logging for a web ACL from the Kinesis Data Firehose console\.

**To enable logging for a web ACL**

1. Open the Kinesis Data Firehose console at [https://console\.aws\.amazon\.com/firehose/](https://console.aws.amazon.com/firehose/)\.

1. Create a Kinesis Data Firehose delivery stream\.

   The name must start with the prefix `aws-waf-logs`\-\. For example, `aws-waf-logs-us-east-2-analytics`\.

   Create the Kinesis Data Firehose delivery stream with a `PUT` source and in the Region where you operate\. If you capture logs for Amazon CloudFront, create the delivery stream in US East \(N\. Virginia\)\. For more information, see [Creating an Amazon Kinesis Data Firehose delivery stream](https://docs.aws.amazon.com/firehose/latest/dev/basic-create.html) in the *Amazon Kinesis Data Firehose Developer Guide*\.

1. From **Services**, choose **WAF & Shield**\. Then choose **Switch to AWS WAF Classic**\.

1. From **Filter**, choose **Global \(CloudFront\)**\.

1. Choose the web ACL to enable logging for\.

1. Under **Logging**, choose **Enable logging**\.

1. Choose the Kinesis Data Firehose delivery stream that you created earlier\. You must choose a delivery stream that has a name that begins with `aws-waf-logs`\-\.

1. Choose **Enable logging**\.

## \[WAF\.2\] A WAF Regional rule should have at least one condition<a name="waf-2"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\)

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAFRegional::Rule`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-rule-not-empty.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-rule-not-empty.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF Regional rule has at least one condition\. The control fails if no conditions are present within a rule\.

A WAF Regional rule can contain multiple conditions\. The rule's conditions allow for traffic inspection and take a defined action \(allow, block, or count\)\. Without any conditions, the traffic passes without inspection\. A WAF Regional rule with no conditions, but with a name or tag suggesting allow, block, or count, could lead to the wrong assumption that one of those actions is occurring\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="waf-2-remediation"></a>

To add a condition to an empty rule, see [Adding and removing conditions in a rule](https://docs.aws.amazon.com/waf/latest/developerguide/classic-web-acl-rules-editing.html) in the *AWS WAF Developer Guide*\.

## \[WAF\.3\] A WAF Regional rule group should have at least one rule<a name="waf-3"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\)

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAFRegional::RuleGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-rulegroup-not-empty.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-rulegroup-not-empty.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF Regional rule group has at least one rule\. The control fails if no rules are present within a rule group\.

A WAF Regional rule group can contain multiple rules\. The rule's conditions allow for traffic inspection and take a defined action \(allow, block, or count\)\. Without any rules, the traffic passes without inspection\. A WAF Regional rule group with no rules, but with a name or tag suggesting allow, block, or count, could lead to the wrong assumption that one of those actions is occurring\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="waf-3-remediation"></a>

To add rules and rule conditions to an empty rule group, see [Adding and deleting rules from an AWS WAF Classic rule group](https://docs.aws.amazon.com/waf/latest/developerguide/classic-rule-group-editing.html) and [Adding and removing conditions in a rule](https://docs.aws.amazon.com/waf/latest/developerguide/classic-web-acl-rules-editing.html) in the *AWS WAF Developer Guide*\.

## \[WAF\.4\] A WAF Regional web ACL should have at least one rule or rule group<a name="waf-4"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAFRegional::WebACL`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-webacl-not-empty](https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-webacl-not-empty)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF Classic Regional web ACL contains any WAF rules or WAF rule groups\. This control fails if a web ACL does not contain any WAF rules or rule groups\.

A WAF Regional web ACL can contain a collection of rules and rule groups that inspect and control web requests\. If a web ACL is empty, the web traffic can pass without being detected or acted upon by WAF depending on the default action\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="waf-4-remediation"></a>

To add rules or rule groups to an empty Classic Regional web ACL, see [Editing a Web ACL](https://docs.aws.amazon.com/waf/latest/developerguide/classic-web-acl-editing.html) in the *AWS WAF Developer Guide*\.

## \[WAF\.6\] A WAF global rule should have at least one condition<a name="waf-6"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAF::Rule`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-global-rule-not-empty.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-global-rule-not-empty.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF global rule contains any conditions\. The control fails if no conditions are present within a rule\.

A WAF global rule can contain multiple conditions\. A rule's conditions allow for traffic inspection and take a defined action \(allow, block, or count\)\. Without any conditions, the traffic passes without inspection\. A WAF global rule with no conditions, but with a name or tag suggesting allow, block, or count, could lead to the wrong assumption that one of those actions is occurring\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="waf-6-remediation"></a>

For instructions on creating a rule and adding conditions, see [Creating a rule and adding conditions](https://docs.aws.amazon.com/waf/latest/developerguide/classic-web-acl-rules-creating.html) in the *AWS WAF Developer Guide*\.

## \[WAF\.7\] A WAF global rule group should have at least one rule<a name="waf-7"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAF::RuleGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-global-rulegroup-not-empty.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-global-rulegroup-not-empty.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF global rule group has at least one rule\. The control fails if no rules are present within a rule group\.

A WAF global rule group can contain multiple rules\. The rule's conditions allow for traffic inspection and take a defined action \(allow, block, or count\)\. Without any rules, the traffic passes without inspection\. A WAF global rule group with no rules, but with a name or tag suggesting allow, block, or count, could lead to the wrong assumption that one of those actions is occurring\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="waf-7-remediation"></a>

For instructions on adding a rule to a rule group, see [Creating an AWS WAF Classic rule group](https://docs.aws.amazon.com/waf/latest/developerguide/classic-create-rule-group.html) in the *AWS WAF Developer Guide*\.

## \[WAF\.8\] A WAF global web ACL should have at least one rule or rule group<a name="waf-8"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\)

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAF::WebACL`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-global-webacl-not-empty](https://docs.aws.amazon.com/config/latest/developerguide/waf-global-webacl-not-empty)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF global web ACL contains at least one WAF rule or WAF rule group\. The control fails if a web ACL does not contain any WAF rules or rule groups\.

A WAF global web ACL can contain a collection of rules and rule groups that inspect and control web requests\. If a web ACL is empty, the web traffic can pass without being detected or acted upon by WAF depending on the default action\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="waf-8-remediation"></a>

**To add rules or rule groups to an empty web ACL**

1. Open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Switch to AWS WAF Classic**, and then choose **Web ACLs**\.

1. For **Filter**, choose **Global \(CloudFront\)**\.

1. Choose the name of the empty web ACL\.

1. Choose **Rules**, and then choose **Edit web ACL**\.

1. For **Rules**, choose a rule or rule group, and then choose **Add rule to web ACL**\.

1. At this point, you can modify the rule order within the web ACL if you are adding multiple rules or rule groups to the web ACL\.

1. Choose **Update**\.

## \[WAF\.10\] A WAFV2 web ACL should have at least one rule or rule group<a name="waf-10"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAFv2::WebACL`

**AWS Config rule:** `wafv2-webacl-not-empty`

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a WAFV2 web access control list \(web ACL\) contains at least one WAF rule or WAF rule group\. The control fails if a web ACL does not contain any WAF rules or rule groups\.

A web ACL gives you fine\-grained control over all of the HTTP\(S\) web requests that your protected resource responds to\. A web ACL should contain a collection of rules and rule groups that inspect and control web requests\. If a web ACL is empty, the web traffic can pass without being detected or acted upon by WAF depending on the default action\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="waf-10-remediation"></a>

To add rules or rule groups to an empty WAFV2 web ACL, see [Editing a Web ACL](https://docs.aws.amazon.com/waf/latest/developerguide/web-acl-editing.html) in the *AWS WAF Developer Guide*\.

## \[WAF\.11\] AWS WAFv2 web ACL logging should be activated<a name="waf-11"></a>

**Category:** Identify > Logging

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-7\(8\)

**Severity:** Low

**Resource type:** `AWS::WAFV2::WebACL`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/wafv2-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/wafv2-logging-enabled.html) ``

**Schedule type:** Periodic

**Parameters:** None

This control checks whether logging is activated for an AWS WAFV2 web ACL\. This control fails if logging is deactivated for the web ACL\.

Logging maintains the reliability, availability, and performance of AWS WAF\. In addition, logging is a business and compliance requirement in many organizations\. By logging traffic that's analyzed by your web ACL, you can troubleshoot application behavior\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="waf-11-remediation"></a>

To activate logging for a web ACL, see [Managing logging for a web ACL](https://docs.aws.amazon.com/waf/latest/developerguide/logging-management.html) in the *AWS WAF Developer Guide*\.