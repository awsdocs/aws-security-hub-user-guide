# Generating and updating control findings<a name="controls-findings-create-update"></a>

AWS Security Hub generates findings by running checks against security controls\. These findings use the AWS Security Finding Format \(ASFF\)\. Note that if the finding size exceeds the maximum of 240 KB, then the `Resource.Details` object is removed\. For controls that are backed by AWS Config resources, you can view the resource details on the AWS Config console\.

Security Hub normally charges for each security check for a control\. However, if multiple controls use the same AWS Config rule, then Security Hub only charges once for each check against the AWS Config rule\. If you turn on [consolidated control findings](#consolidated-control-findings), Security Hub generates a single finding for a security check even when the control is included in multiple enabled standards\.

For example, the AWS Config rule `iam-password-policy` is used by multiple controls in the Center for Internet Security \(CIS\) AWS Foundations Benchmark standard and the Foundational Security Best Practices standard\. Each time Security Hub runs a check against that AWS Config rule, it generates a separate finding for each related control, but only charges once for the check\.

## Consolidated control findings<a name="consolidated-control-findings"></a>

When consolidated control findings is turned on in your account, Security Hub generates a single new finding or finding update for each security check of a control, even if a control applies to multiple enabled standards\. To see a list of controls and the standards they apply to, see [Security Hub controls reference](securityhub-controls-reference.md)\. You can turn consolidated control findings on or off\. We recommend turning it on to reduce finding noise\.

**Note**  
Consolidated control findings isn't currently supported in the AWS GovCloud \(US\) Region and China Regions\. In these Regions, you receive separate findings for each standard when a control applies to multiple standards\. In addition, control IDs, titles, and other ASFF fields remain the same in these Regions and may reference specific standards\. For a list of control IDs and titles in these Regions, see the second and third columns in [How consolidation impacts control IDs and titles](asff-changes-consolidation.md#securityhub-findings-format-changes-ids-titles)\.

If you enabled Security Hub for an AWS account before February 23, 2023, you must turn on consolidated control findings by following the instructions later in this section\. If you enable Security Hub on or after February 23, 2023, consolidated control findings is automatically turned on in your account\. However, if you use the [Security Hub integration with AWS Organizations](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-accounts.html) or invited member accounts through a [manual invitation process](https://docs.aws.amazon.com/securityhub/latest/userguide/account-management-manual.html), consolidated control findings is turned on in member accounts only if it's turned on in the administrator account\. If the feature is turned off in the administrator account, it's turned off in member accounts\. This behavior applies to new and existing member accounts\. 

If you turn off consolidated control findings in your account, Security Hub generates a separate finding per security check for each enabled standard that includes a control\. For example, if four enabled standards share a control with the same underlying AWS Config rule, you receive four separate findings after a security check of the control\. If you turn on consolidated control findings, you receive only one finding\. For more information about how consolidation affects your findings, see [Sample control findings](sample-control-findings.md)\.

When you turn on consolidated control findings, Security Hub creates new standard\-agnostic findings and archives the original standard\-based findings\. Some control finding fields and values will change and may impact existing workflows\. For more information about these changes, see [Consolidated control findings – ASFF changes](asff-changes-consolidation.md#securityhub-findings-format-consolidated-control-findings)\.

Turning on consolidated control findings may also affect findings that [third\-party integrations](securityhub-partner-providers.md) receive from Security Hub\.

## Turning on consolidated control findings<a name="turn-on-consolidated-control-findings"></a>

To turn on consolidated control findings, you must be signed in to an administrator account or a standalone account\.

**Note**  
After turning on consolidated control findings, it may take up to 18 hours for Security Hub for generate new, consolidated findings and archive the original, standard\-based findings\. During that time, you may see a mix of standard\-agnostic and standard\-based findings in your account\.

------
#### [ Security Hub console ]

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**\.

1. Choose the **General** tab\.

1. For **Controls**, turn on **Consolidated control findings**\.

1. Choose **Save**\.

------
#### [ Security Hub API ]

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateSecurityHubConfiguration.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateSecurityHubConfiguration.html)\.

1. Set `ControlFindingGenerator` equal to `SECURITY_CONTROL`\.

   **Example request:**

   ```
   {
      "ControlFindingGenerator": "SECURITY_CONTROL"
   }
   ```

------
#### [ AWS CLI ]

1. Run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-security-hub-configuration.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-security-hub-configuration.html) command\.

1. Set `control-finding-generator` equal to `SECURITY_CONTROL`\.

   ```
   aws securityhub  --region us-east-1 update-security-hub-configuration --control-finding-generator SECURITY_CONTROL
   ```

------

## Turning off consolidated control findings<a name="turn-off-consolidated-control-findings"></a>

To turn off consolidated control findings, you must be signed in to an administrator account or a standalone account\.

**Note**  
After turning off consolidated control findings, it may take up to 18 hours for Security Hub for generate new, standard\-based findings and archive the consolidated findings\. During that time, you may see a mix of standard\-based and consolidated findings in your account\.

------
#### [ Security Hub console ]

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**\.

1. Choose the **General** tab\.

1. For **Controls**, choose **Edit** and turn off **Consolidated control findings**\.

1. Choose **Save**\.

------
#### [ Security Hub API ]

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateSecurityHubConfiguration.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateSecurityHubConfiguration.html)\.

1. Set `ControlFindingGenerator` equal to `STANDARD_CONTROL`\.

   **Example request:**

   ```
   {
      "ControlFindingGenerator": "STANDARD_CONTROL"
   }
   ```

------
#### [ AWS CLI ]

1. Run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-security-hub-configuration.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-security-hub-configuration.html) command\.

1. Set `control-finding-generator` equal to `STANDARD_CONTROL`\.

   ```
   aws securityhub  --region us-east-1 update-security-hub-configuration --control-finding-generator STANDARD_CONTROL
   ```

------

## `Compliance` details for control findings<a name="control-findings-asff-compliance"></a>

For findings generated by security checks of controls, the [`Compliance`](asff-top-level-attributes.md#asff-compliance) field in the AWS Security Finding Format \(ASFF\) contains details related to control findings\. The [`Compliance`](asff-top-level-attributes.md#asff-compliance) field includes the following information\.

`AssociatedStandards`  
The enabled standards that a control is enabled in\.

`RelatedRequirements`  
The list of related requirements for the control in all enabled standards\. The requirements are from the third\-party security framework for the control, such as the Payment Card Industry Data Security Standard \(PCI DSS\)\.

`SecurityControlId`  
The identifier for a control across security standards that Security Hub supports\.

`Status`  
The result of the most recent check that Security Hub ran for a given control\. The results of the previous checks are kept in an archived state for 90 days\.

`StatusReasons`  
Contains a list of reasons for the value of `Compliance.Status`\. For each reason, `StatusReasons` includes the reason code and a description\.

The following table lists the available status reason codes and descriptions\. The remediation steps depend on which control generated a finding with the reason code\. Choose a control from the [Security Hub controls reference](securityhub-controls-reference.md) to see remediation steps for that control\.


|  Reason code  |  Compliance\.Status  |  Description  | 
| --- | --- | --- | 
|  `CLOUDTRAIL_METRIC_FILTER_NOT_VALID`  |  `FAILED`  |  The multi\-Region CloudTrail trail does not have a valid metric filter\.  | 
|  `CLOUDTRAIL_METRIC_FILTERS_NOT_PRESENT`  |  `FAILED`  |  Metric filters are not present for the multi\-Region CloudTrail trail\.  | 
|  `CLOUDTRAIL_MULTI_REGION_NOT_PRESENT`  |  `FAILED`  |  The account does not have a multi\-Region CloudTrail trail with the required configuration\.  | 
|  `CLOUDTRAIL_REGION_INVAILD`  |  `WARNING`  |  Multi\-Region CloudTrail trails are not in the current Region\.  | 
|  `CLOUDWATCH_ALARM_ACTIONS_NOT_VALID`  |  `FAILED`  |  No valid alarm actions are present\.  | 
|  `CLOUDWATCH_ALARMS_NOT_PRESENT`  |  `FAILED`  |  CloudWatch alarms do not exist in the account\.  | 
|  `CONFIG_ACCESS_DENIED`  |  `NOT_AVAILABLE` AWS Config status is `ConfigError`  |  AWS Config access denied\. Verify that AWS Config is enabled and has been granted sufficient permissions\.  | 
|  `CONFIG_EVALUATIONS_EMPTY`  |  `PASSED`  |  AWS Config evaluated your resources based on the rule\. The rule did not apply to the AWS resources in its scope, the specified resources were deleted, or the evaluation results were deleted\.  | 
|  `CONFIG_RETURNS_NOT_APPLICABLE`  |  `NOT_AVAILABLE`  |  The compliance status is `NOT_AVAILABLE` because AWS Config returned a status of **Not Applicable**\. AWS Config does not provide the reason for the status\. Here are some possible reasons for the **Not Applicable** status: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/controls-findings-create-update.html)  | 
|  `CONFIG_RULE_EVALUATION_ERROR`  |  `NOT_AVAILABLE` AWS Config status is `ConfigError`  |  This reason code is used for several different types of evaluation errors\. The description provides the specific reason information\. The type of error can be one of the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/controls-findings-create-update.html)  | 
|  `CONFIG_RULE_NOT_FOUND`  |  `NOT_AVAILABLE` AWS Config status is `ConfigError`  |  The AWS Config rule is in the process of being created\.  | 
|  `INTERNAL_SERVICE_ERROR`  |  `NOT_AVAILABLE`  |  An unknown error occurred\.  | 
|  `LAMBDA_CUSTOM_RUNTIME_DETAILS_NOT_AVAILABLE`  |  FAILED  |  Security Hub is unable to perform a check against a custom Lambda runtime\.  | 
|  `S3_BUCKET_CROSS_ACCOUNT_CROSS_REGION`  |  `WARNING`  |  The finding is in a `WARNING` state, because the S3 bucket that is associated with this rule is in a different Region or account\. This rule does not support cross\-Region or cross\-account checks\. It is recommended that you disable this control in this Region or account\. Only run it in the Region or account where the resource is located\.  | 
|  `SNS_SUBSCRIPTION_NOT_PRESENT`  |  `FAILED`  |  The CloudWatch Logs metric filters do not have a valid Amazon SNS subscription\.  | 
|  `SNS_TOPIC_CROSS_ACCOUNT`  |  WARNING  |  The finding is in a `WARNING` state\. The SNS topic associated with this rule is owned by a different account\. The current account cannot obtain the subscription information\. The account that owns the SNS topic must grant to the current account the `sns:ListSubscriptionsByTopic` permission for the SNS topic\.  | 
|  `SNS_TOPIC_CROSS_ACCOUNT_CROSS_REGION`  |  `WARNING`  |  The finding is in a `WARNING` state because the SNS topic that is associated with this rule is in a different Region or account\. This rule does not support cross\-Region or cross\-account checks\. It is recommended that you disable this control in this Region or account\. Only run it in the Region or account where the resource is located\.  | 
|  `SNS_TOPIC_INVALID`  |  `FAILED`  |  The SNS topic associated with this rule is invalid\.  | 
|  `THROTTLING_ERROR`  |  `NOT_AVAILABLE`  |  The relevant API operation exceeded the allowed rate\.  | 

## `ProductFields` details for control findings<a name="control-findings-asff-productfields"></a>

When Security Hub runs security checks and generates control findings, the `ProductFields` attribute in ASFF includes the following fields:

`ArchivalReasons:0/Description`  
Describes why Security Hub has archived existing findings\.  
For example, Security Hub archives existing findings when you disable a control or standard and when you turn [consolidated control findings](#consolidated-control-findings) on or off\.

`ArchivalReasons:0/ReasonCode`  
Provides the reason why Security Hub has archived existing findings\.  
For example, Security Hub archives existing findings when you disable a control or standard and when you turn [consolidated control findings](#consolidated-control-findings) on or off\.

`StandardsGuideArn` or `StandardsArn`  
The ARN of the standard associated with the control\.  
For the CIS AWS Foundations Benchmark standard, the field is `StandardsGuideArn`\.  
For PCI DSS and AWS Foundational Security Best Practices standards, the field is `StandardsArn`\.  
These fields are removed in favor of `Compliance.AssociatedStandards` if you turn on [consolidated control findings](#consolidated-control-findings)\.

`StandardsGuideSubscriptionArn` or `StandardsSubscriptionArn`  
The ARN of the account's subscription to the standard\.  
For the CIS AWS Foundations Benchmark standard, the field is `StandardsGuideSubscriptionArn`\.  
For the PCI DSS and AWS Foundational Security Best Practices standards, the field is `StandardsSubscriptionArn`\.  
These fields are removed if you turn on [consolidated control findings](#consolidated-control-findings)\.

`RuleId` or `ControlId`  
The identifier of the control\.  
For the CIS AWS Foundations Benchmark standard, the field is `RuleId`\.  
For other standards, the field is `ControlId`\.  
These fields are removed in favor of `Compliance.SecurityControlId` if you turn on [consolidated control findings](#consolidated-control-findings)\.

`RecommendationUrl`  
The URL to the remediation information for the control\. This field is removed in favor of `Remediation.Recommendation.Url` if you turn on [consolidated control findings](#consolidated-control-findings)\.

`RelatedAWSResources:0/name`  
The name of the resource associated with the finding\.

`RelatedAWSResource:0/type`  
The type of resource associated with the control\.

`StandardsControlArn`  
The ARN of the control\. This field is removed if you turn on [consolidated control findings](#consolidated-control-findings)\.

`aws/securityhub/ProductName`  
For control\-based findings, the product name is Security Hub\.

`aws/securityhub/CompanyName`  
For control\-based findings, the company name is AWS\.

`aws/securityhub/annotation`  
A description of the issue uncovered by the control\.

`aws/securityhub/FindingId`  
The identifier of the finding\. This field doesn't reference a standard if you turn on [consolidated control findings](#consolidated-control-findings)\.

## Assigning severity to control findings<a name="control-findings-severity"></a>

The severity assigned to a Security Hub control identifies the importance of the control\. The severity of a control determines the severity label assigned to the control findings\.

### Severity criteria<a name="securityhub-standards-results-severity-criteria"></a>

The severity of a control is determined based on an assessment of the following criteria:
+ **How difficult is it for a threat actor to take advantage of the configuration weakness associated with the control?**

  The difficulty is determined by the amount of sophistication or complexity that is required to use the weakness to carry out a threat scenario\.
+ **How likely is it that the weakness will lead to a compromise of your AWS accounts or resources?**

  A compromise of your AWS accounts or resources means that confidentiality, integrity, or availability of your data or AWS infrastructure is damaged in some way\.

  The likelihood of compromise indicates how likely it is that the threat scenario will result in a disruption or breach of your AWS services or resources\.

As an example, consider the following configuration weaknesses:
+ User access keys are not rotated every 90 days\.
+ IAM root user key exists\.

Both weaknesses are equally difficult for an adversary to take advantage of\. In both cases, the adversary can use credential theft or some other method to acquire a user key\. They can then use it to access your resources in an unauthorized way\.

However, the likelihood of a compromise is much higher if the threat actor acquires the root user access key because this gives them greater access\. As a result, the root user key weakness has a higher severity\.

The severity does not take into account the criticality of the underlying resource\. Criticality is the level of importance of the resources that are associated with the finding\. For example, a resource that is associated with a mission critical application is more critical than one that is associated with nonproduction testing\. To capture resource criticality information, use the `Criticality` field of the AWS Security Finding Format \(ASFF\)\.

The following table maps the difficulty to exploit and the likelihood of compromise to the security labels\.


|  |  |  |  |  | 
| --- |--- |--- |--- |--- |
|    |  **Compromise highly likely**  |  **Compromise likely**  |  **Compromise unlikely**  |  **Compromise highly unlikely**  | 
|  **Very easy to exploit**  |  Critical  |  Critical  |  High  |  Medium  | 
|  **Somewhat easy to exploit**  |  Critical  |  High  |  Medium  |  Medium  | 
|  **Somewhat difficult to exploit**  |  High  |  Medium  |  Medium  |  Low  | 
|  **Very difficult to exploit**  |  Medium  |  Medium  |  Low  |  Low  | 

### Severity definitions<a name="securityhub-standards-results-severity-definitions"></a>

The severity labels are defined as follows\.

**Critical – The issue should be remediated immediately to avoid it escalating\.**  
For example, an open S3 bucket is considered a critical severity finding\. Because so many threat actors scan for open S3 buckets, data in exposed S3 buckets is likely to be discovered and accessed by others\.  
In general, resources that are publicly accessible are considered critical security issues\. You should treat critical findings with the utmost urgency\. You also should consider the criticality of the resource\.

**High – The issue must be addressed as a near\-term priority\.**  
For example, if a default VPC security group is open to inbound and outbound traffic, it is considered high severity\. It is somewhat easy for a threat actor to compromise a VPC using this method\. It is also likely that the threat actor will be able to disrupt or exfiltrate resources once they are in the VPC\.  
Security Hub recommends that you treat a high severity finding as a near\-term priority\. You should take immediate remediation steps\. You also should consider the criticality of the resource\.

**Medium – The issue should be addressed as a mid\-term priority\.**  
For example, lack of encryption for data in transit is considered a medium severity finding\. It requires a sophisticated man\-in\-the\-middle attack to take advantage of this weakness\. In other words, it is somewhat difficult\. It is likely that some data will be compromised if the threat scenario is successful\.  
Security Hub recommends that you investigate the implicated resource at your earliest convenience\. You also should consider the criticality of the resource\.

**Low – The issue does not require action on its own\.**  
For example, failure to collect forensics information is considered low severity\. This control can help to prevent future compromises, but the absence of forensics does not lead directly to a compromise\.  
You do not need to take immediate action on low severity findings, but they can provide context when you correlate them with other issues\.

**Informational – No configuration weakness was found\.**  
In other words, the status is `PASSED`, `WARNING`, or `NOT AVAILABLE`\.  
There is no recommended action\. Informational findings help customers to demonstrate that they are in a compliant state\.

## Rules for updating control findings<a name="securityhub-standards-results-updating"></a>

A subsequent check against a given rule might generate a new result\. For example, the status of "Avoid the use of the root user" could change from `FAILED` to `PASSED`\. In that case, a new finding is generated that contains the most recent result\.

If a subsequent check against a given rule generates a result that is identical to the current result, the existing finding is updated\. No new finding is generated\.

Security Hub automatically archives findings from controls if the associated resource is deleted, the resource does not exist, or the control is disabled\. A resource might no longer exist because the associated service is not currently used\. The findings are archived automatically based on one of the following criteria:
+ The finding is not updated for three to five days \(note that this is best effort and not guaranteed\)\.
+ The associated AWS Config evaluation returned `NOT_APPLICABLE`\.