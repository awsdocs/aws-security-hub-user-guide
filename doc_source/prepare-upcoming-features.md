# Upcoming features: consolidated controls view and consolidated control findings<a name="prepare-upcoming-features"></a>


|  | 
| --- |
| Consolidated controls view and consolidated control findings are upcoming AWS Security Hub features, estimated for release in the first quarter of 2023, in all supported Regions except China and AWS GovCloud \(US\)\. These features are subject to change and are not yet available for use\. This section is designed to provide guidance to help you prepare for these upcoming features\. | 

 Security Hub plans to release two new features, in the first quarter of 2023, that will decouple controls from standards and streamline how you view and receive control findings\. 

The upcoming features are:
+ **Consolidated controls view** – When this feature is released, a new **Controls** page in the Security Hub console will display all your controls across standards\. This feature will also introduce a single identifier for each control across standards\.
+  **Consolidated control findings** – When consolidated control findings is turned on, Security Hub will produce a single finding for a security check even when a check is shared across multiple standards\. This is intended to reduce finding noise\. If you've already enabled Security Hub when this feature is released, it will be turned *off* for you by default\. If you enable Security Hub on or after this feature is released, it will be turned *on* for you by default\.

 Both features will bring changes to control finding fields and values in the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. These changes may impact your existing workflows\.

Here's a summary of the upcoming features and how to prepare for them\.

## Feature \#1: Consolidated controls view<a name="summary-consolidated-controls-view"></a>

Currently, controls are identified, viewed, and managed in the context of security standards\. In the Security Hub console, you first have to navigate to a specific standard to see a list of controls for that standard\. Within the AWS Foundational Security Best Practices \(FSBP\) standard, Security Hub identifies controls by the impacted AWS service and a unique number \(for example, IAM\.1\)\. For other standards, Security Hub includes the standard as part of the control identifier \(for example, CIS 1\.1 or PCI\.AutoScaling\.1\)\.

After the release of consolidated controls view, you'll be able to see a list of all your controls from a new **Controls** page on the Security Hub console\. Security Hub will also assign controls a consistent security control ID across standards\. Following the current naming convention of the AWS FSBP standard, control IDs will include the relevant service and a unique number\. For example, the control "**AWS Config should be enabled**" is currently identified as Config\.1 in the AWS FSBP standard, CIS 2\.5 in the Center for Internet Security \(CIS\) standard, and PCI\.Config\.1 in the Payment Card Industry Data Security Standard \(PCI DSS\)\. After this release, this control will have a single identifier called **Config\.1** across all standards\.

For controls that are part of the AWS Foundational Security Best Practices \(FSBP\) standard, the control identifiers stay the same as the pre\-existing values for [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_StandardsControl.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_StandardsControl.html)\.

 You'll be able to enable a control for one or more enabled standards that include the control\. You'll also be able to disable a control for one or more enabled standards\. As before, you can enable the standards that apply to your business case\. 

### Changes to control finding fields and values after the release of consolidated controls view<a name="asff-changes-consolidated-controls-view"></a>

 After the release of consolidated controls view, you may be impacted by the following changes to control finding fields and values in the ASFF\. 


|  ASFF field  |  Sample value before consolidated controls view  |  Sample value after consolidated controls view, plus description of change  | 
| --- | --- | --- | 
|  Compliance\.SecurityControlId  |  Not applicable \(new field\)  |  EC2\.2 Introduces a single control ID across standards\. `ProductFields.RuleId` will still provide the standard\-based control ID for CISv1\.2\.0 controls\. `ProductFields.ControlId` will still provide the standard\-based control ID for controls in other standards\.  | 
|  Compliance\.AssociatedStandards  |  Not applicable \(new field\)  |  \[\{"StandardsId": "standards/aws\-foundational\-security\-best\-practices/v/1\.0\.0"\}\] Shows what enabled standards a control is associated with\.  | 
|  ProductFields\.RecommendationUrl  |  https://docs\.aws\.amazon\.com/console/securityhub/PCI\.EC2\.2/remediation  |  https://docs\.aws\.amazon\.com/console/securityhub/EC2\.2/remediation This field will no longer reference a standard\.  | 
|  Remediation\.Recommendation\.Text  |  "For directions on how to fix this issue, please consult the AWS Security Hub PCI DSS documentation\."  |  "For instructions on how to fix this issue, see the AWS Security Hub documentation for EC2\.2\." This field will no longer reference a standard\.  | 
|  Remediation\.Recommendation\.Url  |  https://docs\.aws\.amazon\.com/console/securityhub/PCI\.EC2\.2/remediation  |  https://docs\.aws\.amazon\.com/console/securityhub/EC2\.2/remediation This field will no longer reference a standard\.  | 

## Feature \#2: Consolidated control findings<a name="summary-consolidated-control-findings"></a>

 Currently, multiple standards contain separate controls for the same security check\. Security Hub generates a separate finding per standard for each related control that is evaluated by the same security check\. For more information about the current behavior, see [Generating and updating control findings](controls-findings-create-update.md)\. 

 After this release, you'll be able to decrease the number of control findings by turning on consolidated control findings\. When this feature is turned on, Security Hub will generate a single finding or finding update for each security check of a control, even if the check is shared across multiple standards\.

For example, after you turn on consolidated control findings, you'll receive a single finding for a security check of Config\.1 even if this control is associated with the AWS FSBP standard, CIS standard, and PCI DSS\. If you have consolidated control findings turned off, you will receive three separate findings for a security check of Config\.1 if you’ve enabled the control for the AWS FSBP standard, CIS standard, and PCI DSS\. 

### Changes to control finding fields and values after turning on consolidated control findings<a name="asff-changes-consolidated-control-findings"></a>

 If you turn on consolidated control findings, you may be impacted by the following changes to control finding fields and values in the ASFF\. These changes are in addition to the changes previously described for consolidated controls view\. 


|  ASFF field  |  Example value before turning on consolidated control findings  |  Example value after turning on consolidated control findings, plus description of change  | 
| --- | --- | --- | 
|  GeneratorId  |  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Config\.1  |  security\-control/Config\.1 This field will no longer reference a standard\.  | 
|  Title  |  PCI\.Config\.1 AWS Config should be enabled  |  AWS Config should be enabled This field will no longer reference a standard\.  | 
|  Id  |  arn:aws:securityhub:eu\-central\-1:123456789012:subscription/pci\-dss/v/3\.2\.1/PCI\.IAM\.5/finding/ab6d6a26\-a156\-48f0\-9403\-115983e5a956  |  arn:aws:securityhub:eu\-central\-1:123456789012:security\-control/iam\.9/finding/ab6d6a26\-a156\-48f0\-9403\-115983e5a956 This field will no longer reference a standard\.  | 
|  ProductFields\.ControlId  |  PCI\.EC2\.2  |  Removed\. See Compliance\.SecurityControlId instead\. This field is removed in favor of a single, standard\-agnostic control ID\.  | 
|  ProductFields\.RuleId  |  1\.3  |  Removed\. See Compliance\.SecurityControlId instead\. This field is removed in favor of a single, standard\-agnostic control ID\.  | 
|  Description  |  This PCI DSS control checks whether AWS Config is enabled in the current account and region\.  |  This AWS control checks whether AWS Config is enabled in the current account and region\. This field will no longer reference a standard\.  | 
|  Severity  |  "Severity": \{ "Product": 90, "Label": "CRITICAL", "Normalized": 90, "Original": "CRITICAL" \}  |  "Severity": \{ "Label": "CRITICAL", "Normalized": 90, "Original": "CRITICAL" \} Security Hub will no longer use the Product field to describe the severity of a finding\.  | 
|  Types  |  \["Software and Configuration Checks/Industry and Regulatory Standards/PCI\-DSS"\]  |  \["Software and Configuration Checks/Industry and Regulatory Standards"\] This field will no longer reference a standard\.  | 
|  Compliance\. RelatedRequirements  |  \["PCI DSS 10\.5\.2", "PCI DSS 11\.5"\]  |  \["PCI DSS v3\.2\.1/10\.5\.2", "PCI DSS v3\.2\.1/11\.5", "CIS AWS Foundations Benchmark v1\.2\.0/2\.5"\] This field will show related requirements across any associated standards\.  | 
|  CreatedAt  |  2022\-05\-05T08:18:13\.138Z  |  2022\-09\-25T08:18:13\.138Z Format will remain the same, but value will reset when you turn on consolidated control findings\.  | 
|  FirstObservedAt  |  2022\-05\-07T08:18:13\.138Z  |  2022\-09\-28T08:18:13\.138Z Format will remain the same, but value will reset when you turn on consolidated control findings\.  | 
|  ProductFields\. RecommendationUrl  |  https://docs\.aws\.amazon\.com/console/securityhub/EC2\.2/remediation  |  Removed\. See Remediation\.Recommendation\.Url instead\.  | 
|  ProductFields\. StandardsArn  |  arn:aws:securityhub:::standards/aws\-foundational\-security\-best\-practices/v/1\.0\.0  |  Removed\. See Compliance\.AssociatedStandards instead\.  | 
|  ProductFields\. StandardsControlArn  |  arn:aws:securityhub:us\-east\-1:123456789012:control/aws\-foundational\-security\-best\-practices/v/1\.0\.0/Config\.1  |  Removed\. Security Hub will generate one finding for a security check across standards\.  | 
|  ProductFields\. StandardsGuideArn  |  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0  |  Removed\. See Compliance\.AssociatedStandards instead\.  | 
|  ProductFields\. StandardsGuideSubscriptionArn  |  arn:aws:securityhub:us\-east\-2:123456789012:subscription/cis\-aws\-foundations\-benchmark/v/1\.2\.0  |  Removed\. Security Hub will generate one finding for a security check across standards\.  | 
|  ProductFields\. StandardsSubscriptionArn  |  arn:aws:securityhub:us\-east\-1:123456789012:subscription/aws\-foundational\-security\-best\-practices/v/1\.0\.0  |  Removed\. Security Hub will generate one finding for a security check across standards\.  | 
|  ProductFields\.aws/securityhub/FindingId  |  arn:aws:securityhub:us\-east\-1::product/aws/securityhub/arn:aws:securityhub:us\-east\-1:123456789012:subscription/aws\-foundational\-security\-best\-practices/v/1\.0\.0/Config\.1/finding/751c2173\-7372\-4e12\-8656\-a5210dfb1d67  |  arn:aws:securityhub:us\-east\-1::product/aws/securityhub/arn:aws:securityhub:us\-east\-1:123456789012:security\-control/Config\.1/finding/751c2173\-7372\-4e12\-8656\-a5210dfb1d67 This field will no longer reference a standard\.  | 

### New values for customer\-provided finding fields after turning on consolidated control findings<a name="asff-changes-customer-provided-fields"></a>

 When you turn on consolidated control findings, Security Hub will archive the original findings and generate new findings\. To view archived findings, you can visit the **Findings** page of the Security Hub console with the **Record state** filter set to **ARCHIVED**, or use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html) API action\. Updates you’ve made to the original findings in the Security Hub console or using the [BatchUpdateFindings](https://docs.aws.amazon.com/securityhub/latest/userguide/finding-update-batchupdatefindings.html) API won't be preserved in the new findings \(if needed, you can recover this data by referring to the archived findings\)\.

The following customer\-provided finding fields will change when you turn on consolidated control findings\. 


|  Customer\-provided ASFF field  |  Description of change after turning on consolidated control findings  | 
| --- | --- | 
|  Confidence  |  Will reset to empty state\.  | 
|  Criticality  |  Will reset to empty state\.  | 
|  Note  |  Will reset to empty state\.  | 
|  RelatedFindings  |  Will reset to empty state\.  | 
|  Severity  |  Default severity of the finding \(matches the severity of the control\)\.  | 
|  Types  |  Will reset to standard\-agnostic value\.  | 
|  UserDefinedFields  |  Will reset to empty state\.  | 
|  VerificationState  |  Will reset to empty state\.  | 
|  Workflow  |  New failed findings will have a default value of NEW\. New passed findings will have a default value of RESOLVED\.  | 

## How to turn consolidated control findings on and off<a name="turn-on-consolidated-control-findings"></a>

Follow these steps to turn consolidated controls findings on and off for your account\.

 **New accounts** 

 If you enable Security Hub for an AWS account for the first time on or after consolidated control findings is released, by default consolidated control findings will be turned *on* for your account\. You can turn it off at any time\. However, we recommend keeping it turned on to minimize finding noise\.

 If you use the Security Hub integration with AWS Organizations, consolidated control findings will be turned on for new member accounts if the administrator account has turned on the feature\. If the administrator account has turned it off, it will be turned off for new member accounts as well\. 

 **Existing accounts** 

 If your Security Hub account already existed before consolidated control findings was released, your account will have consolidated control findings turned *off* by default\. You can turn it on at any time\. We recommend turning it on to minimize finding noise\. If you use Organizations, consolidated control findings will turned on or off for existing members accounts based on the settings of the administrator account\. 

**Turning consolidated control findings on and off \(Security Hub console\)**

1.  In the navigation pane, choose **Settings**\. 

1.  Choose the **General** tab\. 

1.  For **Controls**, turn on **Consolidated control findings**\. Turn it off to receive a separate finding for each standard\. 

1.  Choose **Save**\. 

 **Turning consolidated control findings on and off \(Security Hub API\)** 

 Run the `UpdateSecurityHubConfiguration` API\. Use the new `ControlFindingGenerator` attribute to change whether an account uses consolidated control findings\.
+ To turn on consolidated control findings, set `ControlFindingGenerator` equal to `SECURITY_CONTROL`\.
+ To turn it off, set `ControlFindingGenerator` equal to `STANDARD_CONTROL`\.

 **Turning consolidated control findings on and off \(AWS CLI\)** 

 Run the `update-security-hub-configuration` command\. Use the new `control-finding-generator` attribute to change whether an account uses consolidated control findings\.
+ To turn on consolidated control findings, set `control-finding-generator` equal to `SECURITY_CONTROL`\.
+ To turn it off, set `control-finding-generator` equal to `STANDARD_CONTROL`\.

## Permissions for new APIs<a name="new-api-permissions"></a>

To unlock the full capabilities of the new features, the AWS Identity and Access Management \(IAM\) role that you use for Security Hub will need permissions to call the following new API actions\. To get the necessary permissions, you can use [Security Hub managed policies](https://docs.aws.amazon.com/securityhub/latest/userguide/security-iam-awsmanpol.html)\. Alternatively, when these APIs are released, you can update custom IAM policies to include permissions for the new actions\. Custom policies should also include permissions for the existing APIs [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandardsControls.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DescribeStandardsControls.html) and [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html)\. Without adding permissions for these actions, you won't be able to call these APIs\.

Here's a summary of each new API action:
+  **`BatchGetSecurityControls`** – Returns information about a batch of controls for the current account and AWS Region\. 
+  **`ListSecurityControlDefinitions`** – Returns information about controls that apply to a specified standard\. 
+  **`ListStandardsControlAssociations`** – Identifies whether a control is currently associated with or dissociated from each enabled standard\. 
+  **`BatchGetStandardsControlAssociations`** – For a batch of controls, identifies whether each control is currently associated with or dissociated from a specified standard\. 
+  **`BatchUpdateStandardsControlAssociations`** – Used to associate a control with enabled standards that include the control, or to dissociate a control from enabled standards\. This is a batch substitute for the `UpdateStandardsControl` API if an administrator doesn’t want to allow member accounts to associate or dissociate controls\. 

After the release of these features, the Security Hub console will also use a new internal API called `BatchGetControlEvaluations`\. This API is used to show the enablement and compliance status of a control, the findings count for a control, and the overall security score for controls\. Your role will need permissions to call this API in order to view this information on the console\.

## How to prepare for control finding field and value changes<a name="recommendations-prepare-asff-changes"></a>

Consider waiting to turn on consolidated control findings if you currently rely on the [Automated Security Response on AWS](https://aws.amazon.com/solutions/implementations/aws-security-hub-automated-response-and-remediation/) solution for predefined response and remediation actions\. The solution does not yet support consolidated control findings\. If you turn it on now, any actions you deployed using the Automated Security Response solution will no longer work\.

If your workflows don’t rely on the specific format of any control finding fields, no action is required\. We recommend that you immediately turn on consolidated control findings once the feature is available\.

If you rely on the specific format of any control finding fields \(for example, for custom automation\), carefully review the upcoming finding field and value changes to ensure that your workflows will continue to function as intended\. Note that the changes noted in the [first table](#asff-changes-consolidated-controls-view) may impact you if you rely on the specified control finding fields and values\.

The changes noted in the [second table](#asff-changes-consolidated-control-findings) and [third table](#asff-changes-customer-provided-fields) will only impact you if you turn on consolidated control findings\. For instance, if you rely on `ProductFields.ControlId`, `GeneratorId`, or `Title`, you'll be impacted if you turn on consolidated control findings\. For example, if you've created an Amazon CloudWatch Events rule that triggers an action for a specific control ID \(such as invoking an AWS Lambda function if the control ID equals CIS 2\.7\), you'll need to update the rule to use CloudTrail\.2, the new `Compliance.SecurityControlId` field for that control\.

 If you've created custom insights using any of the control finding fields or values that will change \(see previous tables\), we recommend updating those insights to use the new fields or values\. 

For more information about how to prepare, see the following sections, which list generator IDs and control titles before and after the release of consolidated control findings, as well as complete sample control findings before and after the releases\.

## More information about consolidated controls view and consolidated control findings<a name="more-info-consolidated-controls-view-consolidated-control-findings"></a>

The following sections provide additional information about control finding field and value changes after the release of consolidated controls view and consolidated control findings\.

## Appendix A: GeneratorIDs before and after turning on consolidated control findings<a name="appendix-generator-ids-changes"></a>

**Note**  
This table was last updated on December 27, 2022\.


| GeneratorID before turning on consolidated control findings | GeneratorID after turning on consolidated control findings | 
| --- | --- | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.1  |  security\-control/CloudWatch\.1  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.1  |  security\-control/IAM\.20  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.10  |  security\-control/IAM\.16  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.11  |  security\-control/IAM\.17  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.12  |  security\-control/IAM\.4  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.13  |  security\-control/IAM\.9  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.14  |  security\-control/IAM\.6  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.16  |  security\-control/IAM\.2  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.2  |  security\-control/IAM\.5  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.20  |  security\-control/IAM\.18  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.22  |  security\-control/IAM\.1  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.3  |  security\-control/IAM\.8  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.4  |  security\-control/IAM\.3  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.5  |  security\-control/IAM\.11  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.6  |  security\-control/IAM\.12  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.7  |  security\-control/IAM\.13  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.8  |  security\-control/IAM\.14  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/1\.9  |  security\-control/IAM\.15  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/2\.1  |  security\-control/CloudTrail\.1  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/2\.2  |  security\-control/CloudTrail\.4  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/2\.3  |  security\-control/CloudTrail\.6  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/2\.4  |  security\-control/CloudTrail\.5  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/2\.5  |  security\-control/Config\.1  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/2\.6  |  security\-control/CloudTrail\.7  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/2\.7  |  security\-control/CloudTrail\.2  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/2\.8  |  security\-control/KMS\.4  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/2\.9  |  security\-control/EC2\.6  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.1  |  security\-control/CloudWatch\.2  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.2  |  security\-control/CloudWatch\.3  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.3  |  security\-control/CloudWatch\.1  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.4  |  security\-control/CloudWatch\.4  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.5  |  security\-control/CloudWatch\.5  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.6  |  security\-control/CloudWatch\.6  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.7  |  security\-control/CloudWatch\.7  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.8  |  security\-control/CloudWatch\.8  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.9  |  security\-control/CloudWatch\.9  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.10  |  security\-control/CloudWatch\.10  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.11  |  security\-control/CloudWatch\.11  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.12  |  security\-control/CloudWatch\.12  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.13  |  security\-control/CloudWatch\.13  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/3\.14  |  security\-control/CloudWatch\.14  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/4\.1  |  security\-control/EC2\.13  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/4\.2  |  security\-control/EC2\.14  | 
|  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0/rule/4\.3  |  security\-control/EC2\.2  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/1\.10  |  security\-control/IAM\.5  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/1\.14  |  security\-control/IAM\.3  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/1\.16  |  security\-control/IAM\.1  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/1\.17  |  security\-control/IAM\.18  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/1\.4  |  security\-control/IAM\.4  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/1\.5  |  security\-control/IAM\.9  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/1\.6  |  security\-control/IAM\.6  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/1\.7  |  security\-control/CloudWatch\.1  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/1\.8  |  security\-control/IAM\.15  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/1\.9  |  security\-control/IAM\.16  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/2\.1\.1  |  security\-control/S3\.4  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/2\.1\.2  |  security\-control/S3\.5  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/2\.1\.5\.1  |  security\-control/S3\.1  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/2\.1\.5\.2  |  security\-control/S3\.8  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/2\.2\.1  |  security\-control/EC2\.7  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/2\.3\.1  |  security\-control/RDS\.3  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/3\.1  |  security\-control/CloudTrail\.1  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/3\.2  |  security\-control/CloudTrail\.4  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/3\.4  |  security\-control/CloudTrail\.5  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/3\.5  |  security\-control/Config\.1  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/3\.6  |  security\-control/S3\.9  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/3\.7  |  security\-control/CloudTrail\.2  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/3\.8  |  security\-control/KMS\.4  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/3\.9  |  security\-control/EC2\.6  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.3  |  security\-control/CloudWatch\.1  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.4  |  security\-control/CloudWatch\.4  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.5  |  security\-control/CloudWatch\.5  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.6  |  security\-control/CloudWatch\.6  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.7  |  security\-control/CloudWatch\.7  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.8  |  security\-control/CloudWatch\.8  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.9  |  security\-control/CloudWatch\.9  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.10  |  security\-control/CloudWatch\.10  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.11  |  security\-control/CloudWatch\.11  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.12  |  security\-control/CloudWatch\.12  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.13  |  security\-control/CloudWatch\.13  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/4\.14  |  security\-control/CloudWatch\.14  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/5\.1  |  security\-control/EC2\.21  | 
|  cis\-aws\-foundations\-benchmark/v/1\.4\.0/5\.3  |  security\-control/EC2\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Account\.1  |  security\-control/Account\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ACM\.1  |  security\-control/ACM\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/APIGateway\.1  |  security\-control/APIGateway\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/APIGateway\.2  |  security\-control/APIGateway\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/APIGateway\.3  |  security\-control/APIGateway\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/APIGateway\.4  |  security\-control/APIGateway\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/APIGateway\.5  |  security\-control/APIGateway\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/APIGateway\.8  |  security\-control/APIGateway\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/APIGateway\.9  |  security\-control/APIGateway\.9  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/AutoScaling\.1  |  security\-control/AutoScaling\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/AutoScaling\.2  |  security\-control/AutoScaling\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/AutoScaling\.3  |  security\-control/AutoScaling\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/AutoScaling\.4  |  security\-control/AutoScaling\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Autoscaling\.5  |  security\-control/Autoscaling\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/AutoScaling\.6  |  security\-control/AutoScaling\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/AutoScaling\.9  |  security\-control/AutoScaling\.9  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFormation\.1  |  security\-control/CloudFormation\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.1  |  security\-control/CloudFront\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.2  |  security\-control/CloudFront\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.3  |  security\-control/CloudFront\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.4  |  security\-control/CloudFront\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.5  |  security\-control/CloudFront\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.6  |  security\-control/CloudFront\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.7  |  security\-control/CloudFront\.7  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.8  |  security\-control/CloudFront\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.9  |  security\-control/CloudFront\.9  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.10  |  security\-control/CloudFront\.10  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudFront\.12  |  security\-control/CloudFront\.12  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudTrail\.1  |  security\-control/CloudTrail\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudTrail\.2  |  security\-control/CloudTrail\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudTrail\.4  |  security\-control/CloudTrail\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CloudTrail\.5  |  security\-control/CloudTrail\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CodeBuild\.1  |  security\-control/CodeBuild\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CodeBuild\.2  |  security\-control/CodeBuild\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CodeBuild\.3  |  security\-control/CodeBuild\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CodeBuild\.4  |  security\-control/CodeBuild\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/CodeBuild\.5  |  security\-control/CodeBuild\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Config\.1  |  security\-control/Config\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/DMS\.1  |  security\-control/DMS\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/DynamoDB\.1  |  security\-control/DynamoDB\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/DynamoDB\.2  |  security\-control/DynamoDB\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/DynamoDB\.3  |  security\-control/DynamoDB\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.1  |  security\-control/EC2\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.3  |  security\-control/EC2\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.4  |  security\-control/EC2\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.6  |  security\-control/EC2\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.7  |  security\-control/EC2\.7  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.8  |  security\-control/EC2\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.9  |  security\-control/EC2\.9  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.10  |  security\-control/EC2\.10  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.15  |  security\-control/EC2\.15  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.16  |  security\-control/EC2\.16  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.17  |  security\-control/EC2\.17  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.18  |  security\-control/EC2\.18  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.19  |  security\-control/EC2\.19  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.2  |  security\-control/EC2\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.20  |  security\-control/EC2\.20  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.21  |  security\-control/EC2\.21  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.22  |  security\-control/EC2\.22  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.23  |  security\-control/EC2\.23  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.24  |  security\-control/EC2\.24  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EC2\.25  |  security\-control/EC2\.25  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECR\.1  |  security\-control/ECR\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECR\.2  |  security\-control/ECR\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECR\.3  |  security\-control/ECR\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECS\.1  |  security\-control/ECS\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECS\.10  |  security\-control/ECS\.10  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECS\.12  |  security\-control/ECS\.12  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECS\.2  |  security\-control/ECS\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECS\.3  |  security\-control/ECS\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECS\.4  |  security\-control/ECS\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECS\.5  |  security\-control/ECS\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ECS\.8  |  security\-control/ECS\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EFS\.1  |  security\-control/EFS\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EFS\.2  |  security\-control/EFS\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EFS\.3  |  security\-control/EFS\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EFS\.4  |  security\-control/EFS\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EKS\.2  |  security\-control/EKS\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ElasticBeanstalk\.1  |  security\-control/ElasticBeanstalk\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ElasticBeanstalk\.2  |  security\-control/ElasticBeanstalk\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELBv2\.1  |  security\-control/ELB\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.2  |  security\-control/ELB\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.3  |  security\-control/ELB\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.4  |  security\-control/ELB\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.5  |  security\-control/ELB\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.6  |  security\-control/ELB\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.7  |  security\-control/ELB\.7  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.8  |  security\-control/ELB\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.9  |  security\-control/ELB\.9  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.10  |  security\-control/ELB\.10  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.11  |  security\-control/ELB\.11  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.12  |  security\-control/ELB\.12  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.13  |  security\-control/ELB\.13  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ELB\.14  |  security\-control/ELB\.14  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/EMR\.1  |  security\-control/EMR\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ES\.1  |  security\-control/ES\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ES\.2  |  security\-control/ES\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ES\.3  |  security\-control/ES\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ES\.4  |  security\-control/ES\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ES\.5  |  security\-control/ES\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ES\.6  |  security\-control/ES\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ES\.7  |  security\-control/ES\.7  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/ES\.8  |  security\-control/ES\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/GuardDuty\.1  |  security\-control/GuardDuty\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/IAM\.1  |  security\-control/IAM\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/IAM\.2  |  security\-control/IAM\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/IAM\.21  |  security\-control/IAM\.21  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/IAM\.3  |  security\-control/IAM\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/IAM\.4  |  security\-control/IAM\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/IAM\.5  |  security\-control/IAM\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/IAM\.6  |  security\-control/IAM\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/IAM\.7  |  security\-control/IAM\.7  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/IAM\.8  |  security\-control/IAM\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Kinesis\.1  |  security\-control/Kinesis\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/KMS\.1  |  security\-control/KMS\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/KMS\.2  |  security\-control/KMS\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/KMS\.3  |  security\-control/KMS\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Lambda\.1  |  security\-control/Lambda\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Lambda\.2  |  security\-control/Lambda\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Lambda\.5  |  security\-control/Lambda\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/NetworkFirewall\.3  |  security\-control/NetworkFirewall\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/NetworkFirewall\.4  |  security\-control/NetworkFirewall\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/NetworkFirewall\.5  |  security\-control/NetworkFirewall\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/NetworkFirewall\.6  |  security\-control/NetworkFirewall\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Opensearch\.1  |  security\-control/Opensearch\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Opensearch\.2  |  security\-control/Opensearch\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Opensearch\.3  |  security\-control/Opensearch\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Opensearch\.4  |  security\-control/Opensearch\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Opensearch\.5  |  security\-control/Opensearch\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Opensearch\.6  |  security\-control/Opensearch\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Opensearch\.7  |  security\-control/Opensearch\.7  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Opensearch\.8  |  security\-control/Opensearch\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.1  |  security\-control/RDS\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.10  |  security\-control/RDS\.10  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.11  |  security\-control/RDS\.11  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.12  |  security\-control/RDS\.12  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.13  |  security\-control/RDS\.13  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.14  |  security\-control/RDS\.14  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.15  |  security\-control/RDS\.15  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.16  |  security\-control/RDS\.16  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.17  |  security\-control/RDS\.17  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.18  |  security\-control/RDS\.18  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.19  |  security\-control/RDS\.19  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.2  |  security\-control/RDS\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.20  |  security\-control/RDS\.20  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.21  |  security\-control/RDS\.21  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.22  |  security\-control/RDS\.22  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.23  |  security\-control/RDS\.23  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.24  |  security\-control/RDS\.24  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.25  |  security\-control/RDS\.25  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.3  |  security\-control/RDS\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.4  |  security\-control/RDS\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.5  |  security\-control/RDS\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.6  |  security\-control/RDS\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.7  |  security\-control/RDS\.7  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.8  |  security\-control/RDS\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/RDS\.9  |  security\-control/RDS\.9  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Redshift\.1  |  security\-control/Redshift\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Redshift\.2  |  security\-control/Redshift\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Redshift\.3  |  security\-control/Redshift\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Redshift\.4  |  security\-control/Redshift\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Redshift\.6  |  security\-control/Redshift\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Redshift\.7  |  security\-control/Redshift\.7  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Redshift\.8  |  security\-control/Redshift\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Redshift\.9  |  security\-control/Redshift\.9  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.1  |  security\-control/S3\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.10  |  security\-control/S3\.10  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.11  |  security\-control/S3\.11  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.12  |  security\-control/S3\.12  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.13  |  security\-control/S3\.13  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.2  |  security\-control/S3\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.3  |  security\-control/S3\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.4  |  security\-control/S3\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.5  |  security\-control/S3\.5  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.6  |  security\-control/S3\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.8  |  security\-control/S3\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/S3\.9  |  security\-control/S3\.9  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SageMaker\.1  |  security\-control/SageMaker\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SageMaker\.2  |  security\-control/SageMaker\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SageMaker\.3  |  security\-control/SageMaker\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SecretsManager\.1  |  security\-control/SecretsManager\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SecretsManager\.2  |  security\-control/SecretsManager\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SecretsManager\.3  |  security\-control/SecretsManager\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SecretsManager\.4  |  security\-control/SecretsManager\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SNS\.1  |  security\-control/SNS\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SNS\.2  |  security\-control/SNS\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SQS\.1  |  security\-control/SQS\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SSM\.1  |  security\-control/SSM\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SSM\.2  |  security\-control/SSM\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SSM\.3  |  security\-control/SSM\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/SSM\.4  |  security\-control/SSM\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/WAF\.1  |  security\-control/WAF\.1  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/WAF\.2  |  security\-control/WAF\.2  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/WAF\.3  |  security\-control/WAF\.3  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/WAF\.4  |  security\-control/WAF\.4  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/WAF\.6  |  security\-control/WAF\.6  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/WAF\.7  |  security\-control/WAF\.7  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/WAF\.8  |  security\-control/WAF\.8  | 
|  aws\-foundational\-security\-best\-practices/v/1\.0\.0/WAF\.10  |  security\-control/WAF\.10  | 
|  pci\-dss/v/3\.2\.1/PCI\.AutoScaling\.1  |  security\-control/AutoScaling\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.CloudTrail\.1  |  security\-control/CloudTrail\.2  | 
|  pci\-dss/v/3\.2\.1/PCI\.CloudTrail\.2  |  security\-control/CloudTrail\.3  | 
|  pci\-dss/v/3\.2\.1/PCI\.CloudTrail\.3  |  security\-control/CloudTrail\.4  | 
|  pci\-dss/v/3\.2\.1/PCI\.CloudTrail\.4  |  security\-control/CloudTrail\.5  | 
|  pci\-dss/v/3\.2\.1/PCI\.CodeBuild\.1  |  security\-control/CodeBuild\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.CodeBuild\.2  |  security\-control/CodeBuild\.2  | 
|  pci\-dss/v/3\.2\.1/PCI\.Config\.1  |  security\-control/Config\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.CW\.1  |  security\-control/CloudWatch\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.DMS\.1  |  security\-control/DMS\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.EC2\.1  |  security\-control/EC2\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.EC2\.2  |  security\-control/EC2\.2  | 
|  pci\-dss/v/3\.2\.1/PCI\.EC2\.4  |  security\-control/EC2\.12  | 
|  pci\-dss/v/3\.2\.1/PCI\.EC2\.5  |  security\-control/EC2\.13  | 
|  pci\-dss/v/3\.2\.1/PCI\.EC2\.6  |  security\-control/EC2\.6  | 
|  pci\-dss/v/3\.2\.1/PCI\.ELBv2\.1  |  security\-control/ELB\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.ES\.1  |  security\-control/ES\.2  | 
|  pci\-dss/v/3\.2\.1/PCI\.ES\.2  |  security\-control/ES\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.GuardDuty\.1  |  security\-control/GuardDuty\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.IAM\.1  |  security\-control/IAM\.4  | 
|  pci\-dss/v/3\.2\.1/PCI\.IAM\.2  |  security\-control/IAM\.2  | 
|  pci\-dss/v/3\.2\.1/PCI\.IAM\.3  |  security\-control/IAM\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.IAM\.4  |  security\-control/IAM\.6  | 
|  pci\-dss/v/3\.2\.1/PCI\.IAM\.5  |  security\-control/IAM\.9  | 
|  pci\-dss/v/3\.2\.1/PCI\.IAM\.6  |  security\-control/IAM\.19  | 
|  pci\-dss/v/3\.2\.1/PCI\.IAM\.7  |  security\-control/IAM\.8  | 
|  pci\-dss/v/3\.2\.1/PCI\.IAM\.8  |  security\-control/IAM\.10  | 
|  pci\-dss/v/3\.2\.1/PCI\.KMS\.1  |  security\-control/KMS\.4  | 
|  pci\-dss/v/3\.2\.1/PCI\.Lambda\.1  |  security\-control/Lambda\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.Lambda\.2  |  security\-control/Lambda\.3  | 
|  pci\-dss/v/3\.2\.1/PCI\.Opensearch\.1  |  security\-control/Opensearch\.2  | 
|  pci\-dss/v/3\.2\.1/PCI\.Opensearch\.2  |  security\-control/Opensearch\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.RDS\.1  |  security\-control/RDS\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.RDS\.2  |  security\-control/RDS\.2  | 
|  pci\-dss/v/3\.2\.1/PCI\.Redshift\.1  |  security\-control/Redshift\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.S3\.1  |  security\-control/S3\.3  | 
|  pci\-dss/v/3\.2\.1/PCI\.S3\.2  |  security\-control/S3\.2  | 
|  pci\-dss/v/3\.2\.1/PCI\.S3\.3  |  security\-control/S3\.7  | 
|  pci\-dss/v/3\.2\.1/PCI\.S3\.4  |  security\-control/S3\.4  | 
|  pci\-dss/v/3\.2\.1/PCI\.S3\.5  |  security\-control/S3\.5  | 
|  pci\-dss/v/3\.2\.1/PCI\.S3\.6  |  security\-control/S3\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.SageMaker\.1  |  security\-control/SageMaker\.1  | 
|  pci\-dss/v/3\.2\.1/PCI\.SSM\.1  |  security\-control/SSM\.2  | 
|  pci\-dss/v/3\.2\.1/PCI\.SSM\.2  |  security\-control/SSM\.3  | 
|  pci\-dss/v/3\.2\.1/PCI\.SSM\.3  |  security\-control/SSM\.1  | 

## Appendix B: Control IDs and titles before and after turning on consolidated control findings<a name="appendix-control-ids-titles-changes"></a>

**Note**  
 This table was last updated on December 27, 2022\. Controls IDs and titles won't change for controls that are only part of the FSBP standard\. 


| Standard | Control ID before turning on consolidated control findings | Title before turning on consolidated control findings | Control ID after turning on consolidated control findings | Title after turning on consolidated control findings | 
| --- | --- | --- | --- | --- | 
|  CIS v1\.2\.0  |  1\.1  |  1\.1 Avoid the use of the root user  |  CloudWatch\.1  |  A log metric filter and alarm should exist for usage of the "root" user  | 
|  CIS v1\.2\.0  |  1\.1  |  1\.1 Avoid the use of the root user  |  IAM\.20  |  Avoid the use of the root user  | 
|  CIS v1\.2\.0  |  1\.10  |  1\.10 Ensure IAM password policy prevents password reuse  |  IAM\.16  |  Ensure IAM password policy prevents password reuse  | 
|  CIS v1\.2\.0  |  1\.11  |  1\.11 Ensure IAM password policy expires passwords within 90 days or less  |  IAM\.17  |  Ensure IAM password policy expires passwords within 90 days or less  | 
|  CIS v1\.2\.0  |  1\.12  |  1\.12 Ensure no root user access key exists  |  IAM\.4  |  IAM root user access key should not exist  | 
|  CIS v1\.2\.0  |  1\.13  |  1\.13 Ensure MFA is enabled for the root user  |  IAM\.9  |  Virtual MFA should be enabled for the root user  | 
|  CIS v1\.2\.0  |  1\.14  |  1\.14 Ensure hardware MFA is enabled for the root user  |  IAM\.6  |  Hardware MFA should be enabled for the root user  | 
|  CIS v1\.2\.0  |  1\.16  |  1\.16 Ensure IAM policies are attached only to groups or roles  |  IAM\.2  |  IAM users should not have IAM policies attached  | 
|  CIS v1\.2\.0  |  1\.2  |  1\.2 Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password  |  IAM\.5  |  MFA should be enabled for all IAM users that have a console password  | 
|  CIS v1\.2\.0  |  1\.20  |  1\.20 Ensure a support role has been created to manage incidents with AWS Support  |  IAM\.18  |  Ensure a support role has been created to manage incidents with AWS Support  | 
|  CIS v1\.2\.0  |  1\.22  |  1\.22 Ensure IAM policies that allow full "\*:\*" administrative privileges are not created  |  IAM\.1  |  IAM policies should not allow full "\*" administrative privileges  | 
|  CIS v1\.2\.0  |  1\.3  |  1\.3 Ensure credentials unused for 90 days or greater are disabled  |  IAM\.8  |  Unused IAM user credentials should be removed  | 
|  CIS v1\.2\.0  |  1\.4  |  1\.4 Ensure access keys are rotated every 90 days or less  |  IAM\.3  |  IAM users' access keys should be rotated every 90 days or less  | 
|  CIS v1\.2\.0  |  1\.5  |  1\.5 Ensure IAM password policy requires at least one uppercase letter  |  IAM\.11  |  Ensure IAM password policy requires at least one uppercase letter  | 
|  CIS v1\.2\.0  |  1\.6  |  1\.6 Ensure IAM password policy requires at least one lowercase letter  |  IAM\.12  |  Ensure IAM password policy requires at least one lowercase letter  | 
|  CIS v1\.2\.0  |  1\.7  |  1\.7 Ensure IAM password policy requires at least one symbol  |  IAM\.13  |  Ensure IAM password policy requires at least one symbol  | 
|  CIS v1\.2\.0  |  1\.8  |  1\.8 Ensure IAM password policy requires at least one number  |  IAM\.14  |  Ensure IAM password policy requires at least one number  | 
|  CIS v1\.2\.0  |  1\.9  |  1\.9 Ensure IAM password policy requires minimum password length of 14 or greater  |  IAM\.15  |  Ensure IAM password policy requires minimum password length of 14 or greater  | 
|  CIS v1\.2\.0  |  2\.1  |  2\.1 Ensure CloudTrail is enabled in all regions  |  CloudTrail\.1  |  CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events  | 
|  CIS v1\.2\.0  |  2\.2  |  2\.2 Ensure CloudTrail log file validation is enabled  |  CloudTrail\.4  |  CloudTrail log file validation should be enabled  | 
|  CIS v1\.2\.0  |  2\.3  |  2\.3 Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible  |  CloudTrail\.6  |  Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible  | 
|  CIS v1\.2\.0  |  2\.4  |  2\.4 Ensure CloudTrail trails are integrated with CloudWatch Logs  |  CloudTrail\.5  |  CloudTrail trails should be integrated with Amazon CloudWatch Logs  | 
|  CIS v1\.2\.0  |  2\.5  |  2\.5 Ensure AWS Config is enabled  |  Config\.1  |  AWS Config should be enabled  | 
|  CIS v1\.2\.0  |  2\.6  |  2\.6 Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket  |  CloudTrail\.7  |  Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket  | 
|  CIS v1\.2\.0  |  2\.7  |  2\.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs  |  CloudTrail\.2  |  CloudTrail should have encryption at\-rest enabled  | 
|  CIS v1\.2\.0  |  2\.8  |  2\.8 Ensure rotation for customer created CMKs is enabled  |  KMS\.4  |  Customer master key \(CMK\) rotation should be enabled  | 
|  CIS v1\.2\.0  |  2\.9  |  2\.9 Ensure VPC flow logging is enabled in all VPCs  |  EC2\.6  |  VPC flow logging should be enabled in all VPCs  | 
|  CIS v1\.2\.0  |  3\.1  |  3\.1 Ensure a log metric filter and alarm exist for unauthorized API calls  |  CloudWatch\.2  |  Ensure a log metric filter and alarm exist for unauthorized API calls  | 
|  CIS v1\.2\.0  |  3\.10  |  3\.10 Ensure a log metric filter and alarm exist for security group changes  |  CloudWatch\.10  |  Ensure a log metric filter and alarm exist for security group changes  | 
|  CIS v1\.2\.0  |  3\.11  |  3\.11 Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  |  CloudWatch\.11  |  Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  | 
|  CIS v1\.2\.0  |  3\.12  |  3\.12 Ensure a log metric filter and alarm exist for changes to network gateways  |  CloudWatch\.12  |  Ensure a log metric filter and alarm exist for changes to network gateways  | 
|  CIS v1\.2\.0  |  3\.13  |  3\.13 Ensure a log metric filter and alarm exist for route table changes  |  CloudWatch\.13  |  Ensure a log metric filter and alarm exist for route table changes  | 
|  CIS v1\.2\.0  |  3\.14  |  3\.14 Ensure a log metric filter and alarm exist for VPC changes  |  CloudWatch\.14  |  Ensure a log metric filter and alarm exist for VPC changes  | 
|  CIS v1\.2\.0  |  3\.2  |  3\.2 Ensure a log metric filter and alarm exist for Management Console sign\-in without MFA  |  CloudWatch\.3  |  Ensure a log metric filter and alarm exist for Management Console sign\-in without MFA  | 
|  CIS v1\.2\.0  |  3\.3  |  3\.3 Ensure a log metric filter and alarm exist for usage of root user  |  CloudWatch\.1  |  A log metric filter and alarm should exist for usage of the "root" user  | 
|  CIS v1\.2\.0  |  3\.4  |  3\.4 Ensure a log metric filter and alarm exist for IAM policy changes  |  CloudWatch\.4  |  Ensure a log metric filter and alarm exist for IAM policy changes  | 
|  CIS v1\.2\.0  |  3\.5  |  3\.5 Ensure a log metric filter and alarm exist for CloudTrail configuration changes  |  CloudWatch\.5  |  Ensure a log metric filter and alarm exist for CloudTrail configuration changes  | 
|  CIS v1\.2\.0  |  3\.6  |  3\.6 Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  |  CloudWatch\.6  |  Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  | 
|  CIS v1\.2\.0  |  3\.7  |  3\.7 Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs  |  CloudWatch\.7  |  Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs  | 
|  CIS v1\.2\.0  |  3\.8  |  3\.8 Ensure a log metric filter and alarm exist for S3 bucket policy changes  |  CloudWatch\.8  |  Ensure a log metric filter and alarm exist for S3 bucket policy changes  | 
|  CIS v1\.2\.0  |  3\.9  |  3\.9 Ensure a log metric filter and alarm exist for AWS Config configuration changes  |  CloudWatch\.9  |  Ensure a log metric filter and alarm exist for AWS Config configuration changes  | 
|  CIS v1\.2\.0  |  4\.1  |  4\.1 Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 22  |  EC2\.13  |  Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22  | 
|  CIS v1\.2\.0  |  4\.2  |  4\.2 Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389  |  EC2\.14  |  Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389  | 
|  CIS v1\.2\.0  |  4\.3  |  4\.3 Ensure the default security group of every VPC restricts all traffic  |  EC2\.2  |  The VPC default security group should not allow inbound and outbound traffic  | 
|  CIS v1\.4\.0  |  1\.10  |  1\.10 Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password  |  IAM\.5  |  MFA should be enabled for all IAM users that have a console password  | 
|  CIS v1\.4\.0  |  1\.14  |  1\.14 Ensure access keys are rotated every 90 days or less  |  IAM\.3  |  IAM users' access keys should be rotated every 90 days or less  | 
|  CIS v1\.4\.0  |  1\.16  |  1\.16 Ensure IAM policies that allow full "\*:\*" administrative privileges are not attached  |  IAM\.1  |  IAM policies should not allow full "\*" administrative privileges  | 
|  CIS v1\.4\.0  |  1\.17  |  1\.17 Ensure a support role has been created to manage incidents with AWS Support  |  IAM\.18  |  Ensure a support role has been created to manage incidents with AWS Support  | 
|  CIS v1\.4\.0  |  1\.4  |  1\.4 Ensure no 'root' user account access key exists  |  IAM\.4  |  IAM root user access key should not exist  | 
|  CIS v1\.4\.0  |  1\.5  |  1\.5 Ensure MFA is enabled for the 'root' user account  |  IAM\.9  |  Virtual MFA should be enabled for the root user  | 
|  CIS v1\.4\.0  |  1\.6  |  1\.6 Ensure hardware MFA is enabled for the 'root' user account  |  IAM\.6  |  Hardware MFA should be enabled for the root user  | 
|  CIS v1\.4\.0  |  1\.7  |  1\.7 Eliminate use of the 'root' user for administrative and daily tasks  |  CloudWatch\.1  |  A log metric filter and alarm should exist for usage of the "root" user  | 
|  CIS v1\.4\.0  |  1\.8  |  1\.8 Ensure IAM password policy requires minimum length of 14 or greater  |  IAM\.15  |  Ensure IAM password policy requires minimum password length of 14 or greater  | 
|  CIS v1\.4\.0  |  1\.9  |  1\.9 Ensure IAM password policy prevents password reuse  |  IAM\.16  |  Ensure IAM password policy prevents password reuse  | 
|  CIS v1\.4\.0  |  2\.1\.1  |  2\.1\.1 Ensure all S3 buckets employ encryption\-at\-rest  |  S3\.4  |  S3 buckets should have server\-side encryption enabled  | 
|  CIS v1\.4\.0  |  2\.1\.2  |  2\.1\.2 Ensure S3 Bucket Policy is set to deny HTTP requests  |  S3\.5  |  S3 buckets should require requests to use Secure Socket Layer  | 
|  CIS v1\.4\.0  |  2\.1\.5\.1  |  2\.1\.5\.1 S3 Block Public Access setting should be enabled  |  S3\.1  |  S3 Block Public Access setting should be enabled  | 
|  CIS v1\.4\.0  |  2\.1\.5\.2  |  2\.1\.5\.2 S3 Block Public Access setting should be enabled at the bucket level  |  S3\.8  |  S3 Block Public Access setting should be enabled at the bucket level  | 
|  CIS v1\.4\.0  |  2\.2\.1  |  2\.2\.1 Ensure EBS volume encryption is enabled  |  EC2\.7  |  EBS default encryption should be enabled  | 
|  CIS v1\.4\.0  |  2\.3\.1  |  2\.3\.1 Ensure that encryption is enabled for RDS Instances  |  RDS\.3  |  RDS DB instances should have encryption at\-rest enabled  | 
|  CIS v1\.4\.0  |  3\.1  |  3\.1 Ensure CloudTrail is enabled in all regions  |  CloudTrail\.1  |  CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events  | 
|  CIS v1\.4\.0  |  3\.2  |  3\.2 Ensure CloudTrail log file validation is enabled  |  CloudTrail\.4  |  CloudTrail log file validation should be enabled  | 
|  CIS v1\.4\.0  |  3\.4  |  3\.4 Ensure CloudTrail trails are integrated with CloudWatch Logs  |  CloudTrail\.5  |  CloudTrail trails should be integrated with Amazon CloudWatch Logs  | 
|  CIS v1\.4\.0  |  3\.5  |  3\.5 Ensure AWS Config is enabled in all regions  |  Config\.1  |  AWS Config should be enabled  | 
|  CIS v1\.4\.0  |  3\.6  |  3\.6 Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket  |  S3\.9  |  S3 bucket server access logging should be enabled  | 
|  CIS v1\.4\.0  |  3\.7  |  3\.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs  |  CloudTrail\.2  |  CloudTrail should have encryption at\-rest enabled  | 
|  CIS v1\.4\.0  |  3\.8  |  3\.8 Ensure rotation for customer created CMKs is enabled  |  KMS\.4  |  Customer master key \(CMK\) rotation should be enabled  | 
|  CIS v1\.4\.0  |  3\.9  |  3\.9 Ensure VPC flow logging is enabled in all VPCs  |  EC2\.6  |  VPC flow logging should be enabled in all VPCs  | 
|  CIS v1\.4\.0  |  4\.4  |  4\.4 Ensure a log metric filter and alarm exist for IAM policy changes  |  CloudWatch\.4  |  Ensure a log metric filter and alarm exist for IAM policy changes  | 
|  CIS v1\.4\.0  |  4\.5  |  4\.5 Ensure a log metric filter and alarm exist for CloudTrail configuration changes  |  CloudWatch\.5  |  Ensure a log metric filter and alarm exist for CloudTrail configuration changes  | 
|  CIS v1\.4\.0  |  4\.6  |  4\.6 Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  |  CloudWatch\.6  |  Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  | 
|  CIS v1\.4\.0  |  4\.7  |  4\.7 Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs  |  CloudWatch\.7  |  Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs  | 
|  CIS v1\.4\.0  |  4\.8  |  4\.8 Ensure a log metric filter and alarm exist for S3 bucket policy changes  |  CloudWatch\.8  |  Ensure a log metric filter and alarm exist for S3 bucket policy changes  | 
|  CIS v1\.4\.0  |  4\.9  |  4\.9 Ensure a log metric filter and alarm exist for AWS Config configuration changes  |  CloudWatch\.9  |  Ensure a log metric filter and alarm exist for AWS Config configuration changes  | 
|  CIS v1\.4\.0  |  4\.10  |  4\.10 Ensure a log metric filter and alarm exist for security group changes  |  CloudWatch\.10  |  Ensure a log metric filter and alarm exist for security group changes  | 
|  CIS v1\.4\.0  |  4\.11  |  4\.11 Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  |  CloudWatch\.11  |  Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  | 
|  CIS v1\.4\.0  |  4\.12  |  4\.12 Ensure a log metric filter and alarm exist for changes to network gateways  |  CloudWatch\.12  |  Ensure a log metric filter and alarm exist for changes to network gateways  | 
|  CIS v1\.4\.0  |  4\.13  |  4\.13 Ensure a log metric filter and alarm exist for route table changes  |  CloudWatch\.13  |  Ensure a log metric filter and alarm exist for route table changes  | 
|  CIS v1\.4\.0  |  4\.14  |  4\.14 Ensure a log metric filter and alarm exist for VPC changes  |  CloudWatch\.14  |  Ensure a log metric filter and alarm exist for VPC changes  | 
|  CIS v1\.4\.0  |  5\.1  |  5\.1 Ensure no Network ACLs allow ingress from 0\.0\.0\.0/0 to remote server administration ports  |  EC2\.21  |  Network ACLs should not allow ingress from 0\.0\.0\.0/0 to port 22 or port 3389  | 
|  CIS v1\.4\.0  |  5\.3  |  5\.3 Ensure the default security group of every VPC restricts all traffic  |  EC2\.2  |  The VPC default security group should not allow inbound and outbound traffic  | 
|  PCI DSS v3\.2\.1  |  PCI\.AutoScaling\.1  |  PCI\.AutoScaling\.1 Auto scaling groups associated with a load balancer should use load balancer health checks  |  AutoScaling\.1  |  Auto scaling groups associated with a load balancer should use load balancer health checks  | 
|  PCI DSS v3\.2\.1  |  PCI\.CloudTrail\.1  |  PCI\.CloudTrail\.1 CloudTrail logs should be encrypted at rest using AWS KMS CMKs  |  CloudTrail\.2  |  CloudTrail should have encryption at\-rest enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.CloudTrail\.2  |  PCI\.CloudTrail\.2 CloudTrail should be enabled  |  CloudTrail\.3  |  CloudTrail should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.CloudTrail\.3  |  PCI\.CloudTrail\.3 CloudTrail log file validation should be enabled  |  CloudTrail\.4  |  CloudTrail log file validation should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.CloudTrail\.4  |  PCI\.CloudTrail\.4 CloudTrail trails should be integrated with Amazon CloudWatch Logs  |  CloudTrail\.5  |  CloudTrail trails should be integrated with Amazon CloudWatch Logs  | 
|  PCI DSS v3\.2\.1  |  PCI\.CodeBuild\.1  |  PCI\.CodeBuild\.1 CodeBuild GitHub or Bitbucket source repository URLs should use OAuth  |  CodeBuild\.1  |  CodeBuild GitHub or Bitbucket source repository URLs should use OAuth  | 
|  PCI DSS v3\.2\.1  |  PCI\.CodeBuild\.2  |  PCI\.CodeBuild\.2 CodeBuild project environment variables should not contain clear text credentials  |  CodeBuild\.2  |  CodeBuild project environment variables should not contain clear text credentials  | 
|  PCI DSS v3\.2\.1  |  PCI\.Config\.1  |  PCI\.Config\.1 AWS Config should be enabled  |  Config\.1  |  AWS Config should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.CW\.1  |  PCI\.CW\.1 A log metric filter and alarm should exist for usage of the "root" user  |  CloudWatch\.1  |  A log metric filter and alarm should exist for usage of the "root" user  | 
|  PCI DSS v3\.2\.1  |  PCI\.DMS\.1  |  PCI\.DMS\.1 Database Migration Service replication instances should not be public  |  DMS\.1  |  Database Migration Service replication instances should not be public  | 
|  PCI DSS v3\.2\.1  |  PCI\.EC2\.1  |  PCI\.EC2\.1 EBS snapshots should not be publicly restorable  |  EC2\.1  |  EBS snapshots should not be publicly restorable  | 
|  PCI DSS v3\.2\.1  |  PCI\.EC2\.2  |  PCI\.EC2\.2 VPC default security group should prohibit inbound and outbound traffic  |  EC2\.2  |  The VPC default security group should not allow inbound and outbound traffic  | 
|  PCI DSS v3\.2\.1  |  PCI\.EC2\.4  |  PCI\.EC2\.4 Unused EC2 EIPs should be removed  |  EC2\.12  |  Unused EC2 EIPs should be removed  | 
|  PCI DSS v3\.2\.1  |  PCI\.EC2\.5  |  PCI\.EC2\.5 Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22  |  EC2\.13  |  Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22  | 
|  PCI DSS v3\.2\.1  |  PCI\.EC2\.6  |  PCI\.EC2\.6 VPC flow logging should be enabled in all VPCs  |  EC2\.6  |  VPC flow logging should be enabled in all VPCs  | 
|  PCI DSS v3\.2\.1  |  PCI\.ELBv2\.1  |  PCI\.ELBv2\.1 Application Load Balancer should be configured to redirect all HTTP requests to HTTPS  |  ELB\.1  |  Application Load Balancer should be configured to redirect all HTTP requests to HTTPS  | 
|  PCI DSS v3\.2\.1  |  PCI\.ES\.1  |  PCI\.ES\.1 Elasticsearch domains should be in a VPC  |  ES\.2  |  Elasticsearch domains should be in a VPC  | 
|  PCI DSS v3\.2\.1  |  PCI\.ES\.2  |  PCI\.ES\.2 Elasticsearch domains should have encryption at\-rest enabled  |  ES\.1  |  Elasticsearch domains should have encryption at\-rest enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.GuardDuty\.1  |  PCI\.GuardDuty\.1 GuardDuty should be enabled  |  GuardDuty\.1  |  GuardDuty should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.1  |  PCI\.IAM\.1 IAM root user access key should not exist  |  IAM\.4  |  IAM root user access key should not exist  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.2  |  PCI\.IAM\.2 IAM users should not have IAM policies attached  |  IAM\.2  |  IAM users should not have IAM policies attached  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.3  |  PCI\.IAM\.3 IAM policies should not allow full "\*" administrative privileges  |  IAM\.1  |  IAM policies should not allow full "\*" administrative privileges  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.4  |  PCI\.IAM\.4 Hardware MFA should be enabled for the root user  |  IAM\.6  |  Hardware MFA should be enabled for the root user  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.5  |  PCI\.IAM\.5 Virtual MFA should be enabled for the root user  |  IAM\.9  |  Virtual MFA should be enabled for the root user  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.6  |  PCI\.IAM\.6 MFA should be enabled for all IAM users  |  IAM\.19  |  MFA should be enabled for all IAM users  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.7  |  PCI\.IAM\.7 IAM user credentials should be disabled if not used within a pre\-defined number days  |  IAM\.8  |  Unused IAM user credentials should be removed  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.8  |  PCI\.IAM\.8 Password policies for IAM users should have strong configurations  |  IAM\.10  |  Password policies for IAM users should have strong configurations  | 
|  PCI DSS v3\.2\.1  |  PCI\.KMS\.1  |  PCI\.KMS\.1 Customer master key \(CMK\) rotation should be enabled  |  KMS\.4  |  Customer master key \(CMK\) rotation should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.Lambda\.1  |  PCI\.Lambda\.1 Lambda functions should prohibit public access  |  Lambda\.1  |  Lambda function policies should prohibit public access  | 
|  PCI DSS v3\.2\.1  |  PCI\.Lambda\.2  |  PCI\.Lambda\.2 Lambda functions should be in a VPC  |  Lambda\.3  |  Lambda functions should be in a VPC  | 
|  PCI DSS v3\.2\.1  |  PCI\.Opensearch\.1  |  PCI\.Opensearch\.1 OpenSearch domains should be in a VPC  |  Opensearch\.2  |  OpenSearch domains should be in a VPC  | 
|  PCI DSS v3\.2\.1  |  PCI\.Opensearch\.2  |  PCI\.Opensearch\.2 EBS snapshots should not be publicly restorable  |  Opensearch\.1  |  OpenSearch domains should have encryption at rest enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.RDS\.1  |  PCI\.RDS\.1 RDS snapshot should be private  |  RDS\.1  |  RDS snapshot should be private  | 
|  PCI DSS v3\.2\.1  |  PCI\.RDS\.2  |  PCI\.RDS\.2 RDS DB Instances should prohibit public access  |  RDS\.2  |  RDS DB Instances should prohibit public access, as determined by the PubliclyAccessible configuration  | 
|  PCI DSS v3\.2\.1  |  PCI\.Redshift\.1  |  PCI\.Redshift\.1 Amazon Redshift clusters should prohibit public access  |  Redshift\.1  |  Amazon Redshift clusters should prohibit public access  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.1  |  PCI\.S3\.1 S3 buckets should prohibit public write access  |  S3\.3  |  S3 buckets should prohibit public write access  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.2  |  PCI\.S3\.2 S3 buckets should prohibit public read access  |  S3\.2  |  S3 buckets should prohibit public read access  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.3  |  PCI\.S3\.3 S3 buckets should have cross\-region replication enabled  |  S3\.7  |  S3 buckets should have cross\-region replication enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.4  |  PCI\.S3\.4 S3 buckets should have server\-side encryption enabled  |  S3\.4  |  S3 buckets should have server\-side encryption enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.5  |  PCI\.S3\.5 S3 buckets should require requests to use Secure Socket Layer  |  S3\.5  |  S3 buckets should require requests to use Secure Socket Layer  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.6  |  PCI\.S3\.6 S3 Block Public Access setting should be enabled  |  S3\.1  |  S3 Block Public Access setting should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.SageMaker\.1  |  PCI\.SageMaker\.1 Amazon SageMaker notebook instances should not have direct internet access  |  SageMaker\.1  |  Amazon SageMaker notebook instances should not have direct internet access  | 
|  PCI DSS v3\.2\.1  |  PCI\.SSM\.1  |  PCI\.SSM\.1 EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation  |  SSM\.2  |  EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation  | 
|  PCI DSS v3\.2\.1  |  PCI\.SSM\.2  |  PCI\.SSM\.2 EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT  |  SSM\.3  |  EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT  | 
|  PCI DSS v3\.2\.1  |  PCI\.SSM\.3  |  PCI\.SSM\.3 EC2 instances should be managed by AWS Systems Manager  |  SSM\.1  |  EC2 instances should be managed by AWS Systems Manager  | 

## Appendix C: Complete sample findings before and after feature releases<a name="appendix-sample-findings"></a>

**Note**  
These sample findings were last updated on December 27, 2022\.

You can review the following types of sample findings:
+ [Before feature releases \(current findings\)](#appendix-sample-findings-before)
+ [After the release of consolidated controls view](#appendix-sample-findings-after-consolidated-controls-view)
+ [After the release of consolidated control findings \(if feature is turned on\)](#appendix-sample-finding-after-consolidated-control-findings)

### Sample findings before feature releases<a name="appendix-sample-findings-before"></a>

 **Sample finding for CloudTrail\.2 control in the FSBP standard** 

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-2:123456789012:subscription/aws-foundational-security-best-practices/v/1.0.0/CloudTrail.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-2::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-2",
  "GeneratorId": "aws-foundational-security-best-practices/v/1.0.0/CloudTrail.2",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards/AWS-Foundational-Security-Best-Practices"
  ],
  "FirstObservedAt": "2020-08-06T02:18:23.076Z",
  "LastObservedAt": "2021-09-28T16:10:06.956Z",
  "CreatedAt": "2020-08-06T02:18:23.076Z",
  "UpdatedAt": "2021-09-28T16:10:00.093Z",
  "Severity": {
    "Product": 40,
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "MEDIUM"
  },
  "Title": "CloudTrail.2 CloudTrail should have encryption at-rest enabled",
  "Description": "This AWS control checks whether AWS CloudTrail is configured to use the server side encryption (SSE) AWS Key Management Service (AWS KMS) customer master key (CMK) encryption. The check will pass if the KmsKeyId is defined.",
  "Remediation": {
    "Recommendation": {
      "Text": "For directions on how to fix this issue, consult the AWS Security Hub Foundational Security Best Practices documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation"
    }
  },
  "ProductFields": {
    "StandardsArn": "arn:aws:securityhub:::standards/aws-foundational-security-best-practices/v/1.0.0",
    "StandardsSubscriptionArn": "arn:aws:securityhub:us-east-2:123456789012:subscription/aws-foundational-security-best-practices/v/1.0.0",
    "ControlId": "CloudTrail.2",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation",
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-fe95bf3f",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-2:123456789012:control/aws-foundational-security-best-practices/v/1.0.0/CloudTrail.2",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-2::product/aws/securityhub/arn:aws:securityhub:us-east-2:123456789012:subscription/aws-foundational-security-best-practices/v/1.0.0/CloudTrail.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsCloudTrailTrail",
      "Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
      "Partition": "aws",
      "Region": "us-east-2"
    }
  ],
  "Compliance": {
    "Status": "FAILED"
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards/AWS-Foundational-Security-Best-Practices"
    ]
  }
}
```

 **Sample finding for PCI\.CloudTrail\.1 control in PCI DSS v3\.2\.1** 

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-2:123456789012:subscription/pci-dss/v/3.2.1/PCI.CloudTrail.1/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-2::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-2",
  "GeneratorId": "pci-dss/v/3.2.1/PCI.CloudTrail.1",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards/PCI-DSS"
  ],
  "FirstObservedAt": "2020-08-06T02:18:23.089Z",
  "LastObservedAt": "2021-09-28T16:10:06.942Z",
  "CreatedAt": "2020-08-06T02:18:23.089Z",
  "UpdatedAt": "2021-09-28T16:10:00.090Z",
  "Severity": {
    "Product": 40,
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "MEDIUM"
  },
  "Title": "PCI.CloudTrail.1 CloudTrail logs should be encrypted at rest using AWS KMS CMKs",
  "Description": "This AWS control checks whether AWS CloudTrail is configured to use the server side encryption (SSE) AWS Key Management Service (AWS KMS) customer master key (CMK) encryption by checking if the KmsKeyId is defined.",
  "Remediation": {
    "Recommendation": {
      "Text": "For directions on how to fix this issue, consult the AWS Security Hub PCI DSS documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/PCI.CloudTrail.1/remediation"
    }
  },
  "ProductFields": {
    "StandardsArn": "arn:aws:securityhub:::standards/pci-dss/v/3.2.1",
    "StandardsSubscriptionArn": "arn:aws:securityhub:us-east-2:123456789012:subscription/pci-dss/v/3.2.1",
    "ControlId": "PCI.CloudTrail.1",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/PCI.CloudTrail.1/remediation",
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-fe95bf3f",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-2:123456789012:control/pci-dss/v/3.2.1/PCI.CloudTrail.1",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-2::product/aws/securityhub/arn:aws:securityhub:us-east-2:123456789012:subscription/pci-dss/v/3.2.1/PCI.CloudTrail.1/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsCloudTrailTrail",
      "Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
      "Partition": "aws",
      "Region": "us-east-2"
    }
  ],
  "Compliance": {
    "Status": "FAILED",
    "RelatedRequirements": [
      "PCI DSS 3.4"
    ]
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards/PCI-DSS"
    ]
  }
}
```

 **Sample finding for control 2\.7 in the CIS AWS Foundations Benchmark v1\.2\.0** 

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-2:123456789012:subscription/cis-aws-foundations-benchmark/v/1.2.0/2.7/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-2::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-2",
  "GeneratorId": "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0/rule/2.7",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards/CIS AWS Foundations Benchmark"
  ],
  "FirstObservedAt": "2020-08-29T04:10:06.337Z",
  "LastObservedAt": "2021-09-28T16:10:05.350Z",
  "CreatedAt": "2020-08-29T04:10:06.337Z",
  "UpdatedAt": "2021-09-28T16:10:00.087Z",
  "Severity": {
    "Product": 40,
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "MEDIUM"
  },
  "Title": "2.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs",
  "Description": "AWS Key Management Service (KMS) is a managed service that helps create and control the encryption keys used to encrypt account data, and uses Hardware Security Modules (HSMs) to protect the security of encryption keys. CloudTrail logs can be configured to leverage server side encryption (SSE) and KMS customer created master keys (CMK) to further protect CloudTrail logs. It is recommended that CloudTrail be configured to use SSE-KMS.",
  "Remediation": {
    "Recommendation": {
      "Text": "For directions on how to fix this issue, consult the AWS Security Hub CIS documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/standards-cis-2.7/remediation"
    }
  },
  "ProductFields": {
    "StandardsGuideArn": "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0",
    "StandardsGuideSubscriptionArn": "arn:aws:securityhub:us-east-2:123456789012:subscription/cis-aws-foundations-benchmark/v/1.2.0",
    "RuleId": "2.7",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/standards-cis-2.7/remediation",
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-fe95bf3f",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-2:123456789012:control/cis-aws-foundations-benchmark/v/1.2.0/2.7",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-2::product/aws/securityhub/arn:aws:securityhub:us-east-2:123456789012:subscription/cis-aws-foundations-benchmark/v/1.2.0/2.7/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsCloudTrailTrail",
      "Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
      "Partition": "aws",
      "Region": "us-east-2"
    }
  ],
  "Compliance": {
    "Status": "FAILED"
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards/CIS AWS Foundations Benchmark"
    ]
  }
}
```

 **Sample finding for control 3\.7 in the CIS AWS Foundations Benchmark v1\.4\.0** 

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-1:123456789012:subscription/cis-aws-foundations-benchmark/v/1.4.0/3.7/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-1::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-1",
  "GeneratorId": "cis-aws-foundations-benchmark/v/1.4.0/3.7",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards/CIS AWS Foundations Benchmark"
  ],
  "FirstObservedAt": "2022-10-21T22:14:48.913Z",
  "LastObservedAt": "2022-12-22T22:24:56.980Z",
  "CreatedAt": "2022-10-21T22:14:48.913Z",
  "UpdatedAt": "2022-12-22T22:24:52.409Z",
  "Severity": {
    "Product": 40,
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "MEDIUM"
  },
  "Title": "3.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs",
  "Description": "AWS CloudTrail is a web service that records AWS API calls for an account and makes those logs available to users and resources in accordance with IAM policies. AWS Key Management Service (KMS) is a managed service that helps create and control the encryption keys used to encrypt account data, and uses Hardware Security Modules (HSMs) to protect the security of encryption keys. CloudTrail logs can be configured to leverage server side encryption (SSE) and AWS KMS customer created master keys (CMK) to further protect CloudTrail logs. It is recommended that CloudTrail be configured to use SSE-KMS.",
  "Remediation": {
    "Recommendation": {
      "Text": "For directions on how to fix this issue, consult the AWS Security Hub CIS AWS Foundations Benchmark v1.4.0 Controls documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/CIS.v1.4.0.3.7/remediation"
    }
  },
  "ProductFields": {
    "StandardsArn": "arn:aws:securityhub:::standards/cis-aws-foundations-benchmark/v/1.4.0",
    "StandardsSubscriptionArn": "arn:aws:securityhub:us-east-1:123456789012:subscription/cis-aws-foundations-benchmark/v/1.4.0",
    "ControlId": "3.7",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/CIS.v1.4.0.3.7/remediation",
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-855f82d1",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-1:123456789012:control/cis-aws-foundations-benchmark/v/1.4.0/3.7",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-west-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-1::product/aws/securityhub/arn:aws:securityhub:us-east-1:123456789012:subscription/cis-aws-foundations-benchmark/v/1.4.0/3.7/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsCloudTrailTrail",
      "Id": "arn:aws:cloudtrail:us-west-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
      "Partition": "aws",
      "Region": "us-east-1"
    }
  ],
  "Compliance": {
    "Status": "FAILED",
    "RelatedRequirements": [
      "CIS AWS Foundations Benchmark v1.4.0/3.7"
    ]
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards/CIS AWS Foundations Benchmark"
    ]
  }
}
```

 **Sample finding for CT\.CloudTrail\.2 in Service\-Managed Standard: AWS Control Tower\.** 

**Note**  
This standard is available to you only if you're an AWS Control Tower user who has created the standard in AWS Control Tower\. For more information, see [Service\-Managed Standard: AWS Control Tower](service-managed-standard-aws-control-tower.md)\.

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-1:123456789012:subscription/service-managed-aws-control-tower/v/1.0.0/CloudTrail.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-1::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-1",
  "GeneratorId": "service-managed-aws-control-tower/v/1.0.0/CloudTrail.2",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards"
  ],
  "FirstObservedAt": "2022-11-17T01:25:30.296Z",
  "LastObservedAt": "2022-11-17T01:25:45.805Z",
  "CreatedAt": "2022-11-17T01:25:30.296Z",
  "UpdatedAt": "2022-11-17T01:25:30.296Z",
  "Severity": {
    "Product": 40,
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "MEDIUM"
  },
  "Title": "CT.CloudTrail.2 CloudTrail should have encryption at-rest enabled",
  "Description": "This AWS control checks whether AWS CloudTrail is configured to use the server side encryption (SSE) AWS Key Management Service (AWS KMS) customer master key (CMK) encryption. The check will pass if the KmsKeyId is defined.",
  "Remediation": {
    "Recommendation": {
      "Text": "For information on how to correct this issue, consult the AWS Security Hub controls documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation"
    }
  },
  "ProductFields": {
    "StandardsArn": "arn:aws:securityhub:::standards/service-managed-aws-control-tower/v/1.0.0",
    "StandardsSubscriptionArn": "arn:aws:securityhub:us-east-1:123456789012:subscription/service-managed-aws-control-tower/v/1.0.0",
    "ControlId": "CT.CloudTrail.2",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation",
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-fe95bf3f",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-1:123456789012:control/service-managed-aws-control-tower/v/1.0.0/CloudTrail.2",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-1::product/aws/securityhub/arn:aws:securityhub:us-east-1:123456789012:subscription/service-managed-aws-control-tower/v/1.0.0/CloudTrail.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsAccount",
      "Id": "AWS::::Account:123456789012",
      "Partition": "aws",
      "Region": "us-east-1"
    }
  ],
  "Compliance": {
    "Status": "FAILED"
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards"
    ]
  }
}
```

### Sample findings after release of consolidated controls view<a name="appendix-sample-findings-after-consolidated-controls-view"></a>

 **Sample finding for CloudTrail\.2 control in the FSBP standard** 

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-2:123456789012:subscription/aws-foundational-security-best-practices/v/1.0.0/CloudTrail.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-2::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-2",
  "GeneratorId": "aws-foundational-security-best-practices/v/1.0.0/CloudTrail.2",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards/AWS-Foundational-Security-Best-Practices"
  ],
  "FirstObservedAt": "2020-08-06T02:18:23.076Z",
  "LastObservedAt": "2021-09-28T16:10:06.956Z",
  "CreatedAt": "2020-08-06T02:18:23.076Z",
  "UpdatedAt": "2021-09-28T16:10:00.093Z",
  "Severity": {
    "Product": 40,
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "MEDIUM"
  },
  "Title": "CloudTrail.2 CloudTrail should have encryption at-rest enabled",
  "Description": "This AWS control checks whether AWS CloudTrail is configured to use the server side encryption (SSE) AWS Key Management Service (AWS KMS) customer master key (CMK) encryption. The check will pass if the KmsKeyId is defined.",
  "Remediation": {
    "Recommendation": {
      "Text": "For directions on how to correct this issue, consult the AWS Security Hub controls documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation"
    }
  },
  "ProductFields": {
    "StandardsArn": "arn:aws:securityhub:::standards/aws-foundational-security-best-practices/v/1.0.0",
    "StandardsSubscriptionArn": "arn:aws:securityhub:us-east-2:123456789012:subscription/aws-foundational-security-best-practices/v/1.0.0",
    "ControlId": "CloudTrail.2",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation",
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-fe95bf3f",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-2:123456789012:control/aws-foundational-security-best-practices/v/1.0.0/CloudTrail.2",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-west-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-2::product/aws/securityhub/arn:aws:securityhub:us-east-2:123456789012:subscription/aws-foundational-security-best-practices/v/1.0.0/CloudTrail.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsCloudTrailTrail",
      "Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
      "Partition": "aws",
      "Region": "us-east-2"
    }
  ],
  "Compliance": {
    "Status": "FAILED",
    "SecurityControlId": "CloudTrail.2",
    "AssociatedStandards": [{
      "StandardsId": "standards/aws-foundation-best-practices/v/1.0.0"
    }]
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards/AWS-Foundational-Security-Best-Practices"
    ]
  }
}
```

 **Sample finding for PCI\.CloudTrail\.1 control in PCI DSS v3\.2\.1** 

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-2:123456789012:subscription/pci-dss/v/3.2.1/PCI.CloudTrail.1/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-2::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-2",
  "GeneratorId": "pci-dss/v/3.2.1/PCI.CloudTrail.1",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards/PCI-DSS"
  ],
  "FirstObservedAt": "2020-08-06T02:18:23.089Z",
  "LastObservedAt": "2021-09-28T16:10:06.942Z",
  "CreatedAt": "2020-08-06T02:18:23.089Z",
  "UpdatedAt": "2021-09-28T16:10:00.090Z",
  "Severity": {
    "Product": 40,
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "MEDIUM"
  },
  "Title": "PCI.CloudTrail.1 CloudTrail logs should be encrypted at rest using AWS KMS CMKs",
  "Description": "This AWS control checks whether AWS CloudTrail is configured to use the server side encryption (SSE) AWS Key Management Service (AWS KMS) customer master key (CMK) encryption by checking if the KmsKeyId is defined.",
  "Remediation": {
    "Recommendation": {
      "Text": "For directions on how to correct this issue, consult the AWS Security Hub controls documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation"
    }
  },
  "ProductFields": {
    "StandardsArn": "arn:aws:securityhub:::standards/pci-dss/v/3.2.1",
    "StandardsSubscriptionArn": "arn:aws:securityhub:us-east-2:123456789012:subscription/pci-dss/v/3.2.1",
    "ControlId": "PCI.CloudTrail.1",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation",
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-fe95bf3f",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-2:123456789012:control/pci-dss/v/3.2.1/PCI.CloudTrail.1",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-2::product/aws/securityhub/arn:aws:securityhub:us-east-2:123456789012:subscription/pci-dss/v/3.2.1/PCI.CloudTrail.1/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsCloudTrailTrail",
      "Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
      "Partition": "aws",
      "Region": "us-east-2"
    }
  ],
  "Compliance": {
    "Status": "FAILED",
    "RelatedRequirements": [
      "PCI DSS 3.4"
    ],
    "SecurityControlId": "CloudTrail.2",
    "AssociatedStandards": [{
      "StandardsId": "standards/pci-dss/v/3.2.1"
    }]
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards/PCI-DSS"
    ]
  }
}
```

 **Sample finding for control 2\.7 in the CIS AWS Foundations Benchmark v1\.2\.0** 

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-2:123456789012:subscription/cis-aws-foundations-benchmark/v/1.2.0/2.7/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-2::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-2",
  "GeneratorId": "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0/rule/2.7",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards/CIS AWS Foundations Benchmark"
  ],
  "FirstObservedAt": "2020-08-29T04:10:06.337Z",
  "LastObservedAt": "2021-09-28T16:10:05.350Z",
  "CreatedAt": "2020-08-29T04:10:06.337Z",
  "UpdatedAt": "2021-09-28T16:10:00.087Z",
  "Severity": {
    "Product": 40,
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "MEDIUM"
  },
  "Title": "2.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs",
  "Description": "AWS Key Management Service (KMS) is a managed service that helps create and control the encryption keys used to encrypt account data, and uses Hardware Security Modules (HSMs) to protect the security of encryption keys. CloudTrail logs can be configured to leverage server side encryption (SSE) and KMS customer created master keys (CMK) to further protect CloudTrail logs. It is recommended that CloudTrail be configured to use SSE-KMS.",
  "Remediation": {
    "Recommendation": {
      "Text": "For directions on how to correct this issue, consult the AWS Security Hub controls documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation"
    }
  },
  "ProductFields": {
    "StandardsGuideArn": "arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0",
    "StandardsGuideSubscriptionArn": "arn:aws:securityhub:us-east-2:123456789012:subscription/cis-aws-foundations-benchmark/v/1.2.0",
    "RuleId": "2.7",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation",
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-fe95bf3f",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-2:123456789012:control/cis-aws-foundations-benchmark/v/1.2.0/2.7",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-2::product/aws/securityhub/arn:aws:securityhub:us-east-2:123456789012:subscription/cis-aws-foundations-benchmark/v/1.2.0/2.7/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsCloudTrailTrail",
      "Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
      "Partition": "aws",
      "Region": "us-east-2"
    }
  ],
  "Compliance": {
    "Status": "FAILED",
    "SecurityControlId": "CloudTrail.2",
    "AssociatedStandards": [{
      "StandardsId": "ruleset/cis-aws-foundations-benchmark/v/1.2.0"
    }]
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards/CIS AWS Foundations Benchmark"
    ]
  }
}
```

 **Sample finding for control 3\.7 in the CIS AWS Foundations Benchmark v1\.4\.0** 

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-1:123456789012:subscription/cis-aws-foundations-benchmark/v/1.4.0/3.7/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-1::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-1",
  "GeneratorId": "cis-aws-foundations-benchmark/v/1.4.0/3.7",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards/CIS AWS Foundations Benchmark"
  ],
  "FirstObservedAt": "2022-10-21T22:14:48.913Z",
  "LastObservedAt": "2022-12-22T22:24:56.980Z",
  "CreatedAt": "2022-10-21T22:14:48.913Z",
  "UpdatedAt": "2022-12-22T22:24:52.409Z",
  "Severity": {
    "Product": 40,
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "MEDIUM"
  },
  "Title": "3.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs",
  "Description": "AWS CloudTrail is a web service that records AWS API calls for an account and makes those logs available to users and resources in accordance with IAM policies. AWS Key Management Service (KMS) is a managed service that helps create and control the encryption keys used to encrypt account data, and uses Hardware Security Modules (HSMs) to protect the security of encryption keys. CloudTrail logs can be configured to leverage server side encryption (SSE) and AWS KMS customer created master keys (CMK) to further protect CloudTrail logs. It is recommended that CloudTrail be configured to use SSE-KMS.",
  "Remediation": {
    "Recommendation": {
      "Text": "For directions on how to correct this issue, consult the AWS Security Hub controls documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation"
    }
  },
  "ProductFields": {
    "StandardsArn": "arn:aws:securityhub:::standards/cis-aws-foundations-benchmark/v/1.4.0",
    "StandardsSubscriptionArn": "arn:aws:securityhub:us-east-1:123456789012:subscription/cis-aws-foundations-benchmark/v/1.4.0",
    "ControlId": "3.7",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation",
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-855f82d1",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-1:123456789012:control/cis-aws-foundations-benchmark/v/1.4.0/3.7",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-west-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-1::product/aws/securityhub/arn:aws:securityhub:us-east-1:123456789012:subscription/cis-aws-foundations-benchmark/v/1.4.0/3.7/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsCloudTrailTrail",
      "Id": "arn:aws:cloudtrail:us-west-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
      "Partition": "aws",
      "Region": "us-east-1"
    }
  ],
  "Compliance": {
    "Status": "FAILED",
    "RelatedRequirements": [
      "CIS AWS Foundations Benchmark v1.4.0/3.7"
    ],
    "SecurityControlId": "CloudTrail.2",
    "AssociatedStandards": [{
      "StandardsId": "standards/cis-aws-foundations-benchmark/v/1.4.0"
    }]
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards/CIS AWS Foundations Benchmark"
    ]
  }
}
```

**Sample finding for CT\.CloudTrail\.2 in Service\-Managed Standard: AWS Control Tower**

**Note**  
This standard is available to you only if you're an AWS Control Tower user who has created the standard in AWS Control Tower\. For more information, see [Service\-Managed Standard: AWS Control Tower](service-managed-standard-aws-control-tower.md)\.

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-1:123456789012:subscription/service-managed-aws-control-tower/v/1.0.0/CloudTrail.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-1::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-1",
  "GeneratorId": "service-managed-aws-control-tower/v/1.0.0/CloudTrail.2",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards"
  ],
  "FirstObservedAt": "2022-11-17T01:25:30.296Z",
  "LastObservedAt": "2022-11-17T01:25:45.805Z",
  "CreatedAt": "2022-11-17T01:25:30.296Z",
  "UpdatedAt": "2022-11-17T01:25:30.296Z",
  "Severity": {
    "Product": 40,
    "Label": "MEDIUM",
    "Normalized": 40,
    "Original": "MEDIUM"
  },
  "Title": "CT.CloudTrail.2 CloudTrail should have encryption at-rest enabled",
  "Description": "This AWS control checks whether AWS CloudTrail is configured to use the server side encryption (SSE) AWS Key Management Service (AWS KMS) customer master key (CMK) encryption. The check will pass if the KmsKeyId is defined.",
  "Remediation": {
    "Recommendation": {
      "Text": "For information on how to correct this issue, consult the AWS Security Hub controls documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation"
    }
  },
  "ProductFields": {
    "StandardsArn": "arn:aws:securityhub:::standards/service-managed-aws-control-tower/v/1.0.0",
    "StandardsSubscriptionArn": "arn:aws:securityhub:us-east-1:123456789012:subscription/service-managed-aws-control-tower/v/1.0.0",
    "ControlId": "CT.CloudTrail.2",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation",
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-fe95bf3f",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-1:123456789012:control/service-managed-aws-control-tower/v/1.0.0/CloudTrail.2",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-1::product/aws/securityhub/arn:aws:securityhub:us-east-1:123456789012:subscription/service-managed-aws-control-tower/v/1.0.0/CloudTrail.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsAccount",
      "Id": "AWS::::Account:123456789012",
      "Partition": "aws",
      "Region": "us-east-1"
    }
  ],
  "Compliance": {
    "Status": "FAILED",
    "SecurityControlId": "CloudTrail.2",
    "AssociatedStandards": [{
      "StandardsId": "standards/service-managed-aws-control-tower/v/1.0.0"
    }]
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards"
    ]
  }
}
```

### Sample finding when consolidated control findings is turned on<a name="appendix-sample-finding-after-consolidated-control-findings"></a>

This is an example of the single finding that Security Hub will generate for CloudTrail\.2 across standards when you turn on consolidated control findings\. 

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-2:123456789012:security-control/CloudTrail.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-2::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-2",
  "GeneratorId": "security-control/CloudTrail.2",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards"
  ],
  "FirstObservedAt": "2022-10-06T02:18:23.076Z",
  "LastObservedAt": "2022-10-28T16:10:06.956Z",
  "CreatedAt": "2022-10-06T02:18:23.076Z",
  "UpdatedAt": "2022-10-28T16:10:00.093Z",
  "Severity": {
    "Label": "MEDIUM",
    "Normalized": "40",
    "Original": "MEDIUM"
  },
  "Title": "CloudTrail should have encryption at-rest enabled",
  "Description": "This AWS control checks whether AWS CloudTrail is configured to use the server side encryption (SSE) AWS Key Management Service (AWS KMS) customer master key (CMK) encryption. The check will pass if the KmsKeyId is defined.",
  "Remediation": {
    "Recommendation": {
      "Text": "For directions on how to correct this issue, consult the AWS Security Hub controls documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/CloudTrail.2/remediation"
    }
  },
  "ProductFields": {
    "RelatedAWSResources:0/name": "securityhub-cloud-trail-encryption-enabled-fe95bf3f",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-2::product/aws/securityhub/arn:aws:securityhub:us-east-2:123456789012:security-control/CloudTrail.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  }
  "Resources": [
    {
      "Type": "AwsCloudTrailTrail",
      "Id": "arn:aws:cloudtrail:us-east-2:123456789012:trail/AWSMacieTrail-DO-NOT-EDIT",
      "Partition": "aws",
      "Region": "us-east-2"
    }
  ],
  "Compliance": {
    "Status": "FAILED",
    "RelatedRequirements": [
        "PCI DSS v3.2.1/3.4",
        "CIS AWS Foundations Benchmark v1.2.0/2.7",
        "CIS AWS Foundations Benchmark v1.4.0/3.7"
    ],
    "SecurityControlId": "CloudTrail.2",
    "AssociatedStandards": [
       { "StandardsId": "standards/aws-foundational-security-best-practices/v/1.0.0"},
       { "StandardsId": "standards/pci-dss/v/3.2.1"},
       { "StandardsId": "ruleset/cis-aws-foundations-benchmark/v/1.2.0"},
       { "StandardsId": "standards/cis-aws-foundations-benchmark/v/1.4.0"},
       { "StandardsId": "standards/service-managed-aws-control-tower/v/1.0.0"},
    ]
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "MEDIUM",
      "Normalized": "40",
      "Original": "MEDIUM"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards"
    ]
  }
}
```