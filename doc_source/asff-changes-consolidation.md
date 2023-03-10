# Impact of consolidation on ASFF fields and values<a name="asff-changes-consolidation"></a>

Security Hub offers two types of consolidation:
+ **Consolidated controls view \(always on; can't be turned off\)** – Each control has a single identifier across standards\. The **Controls** page of the Security Hub console displays all your controls across standards\.
+  **Consolidated control findings \(can be turned on or off\)** – When consolidated control findings is turned on, Security Hub produces a single finding for a security check even when a check is shared across multiple standards\. This is intended to reduce finding noise\. Consolidated control findings is turned *on* for you by default if you enable Security Hub on or after February 23, 2023\. Otherwise, it's turned off by default\. However, consolidated control findings is turned on in Security Hub member accounts only if it's turned on in the administrator account\. If the feature is turned off in the administrator account, it's turned off in member accounts\. For instructions on turning on this feature, see [Turning on consolidated control findings](controls-findings-create-update.md#turn-on-consolidated-control-findings)\.

**Note**  
Consolidated controls view and consolidated control findings aren't currently supported in the AWS GovCloud \(US\) Region and China Regions\. In these Regions, you receive separate findings for each standard when a control applies to multiple standards\. In addition, the following ASFF changes don't impact these Regions\. For a list of control IDs and titles in these Regions, see the second and third columns in [How consolidation impacts control IDs and titles](#securityhub-findings-format-changes-ids-titles)\. 

Both features bring changes to control finding fields and values in the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. This section summarizes those changes\.

## Consolidated controls view – ASFF changes<a name="securityhub-findings-format-consolidated-controls-view"></a>

The consolidated controls view feature introduces the following changes to control finding fields and values in the ASFF\.

If your workflows don’t rely on the values of these control finding fields, no action is required\.

If you have workflows that rely on the specific values of these control finding fields, update your workflows to use the new values\.


|  ASFF field  |  Sample value before consolidated controls view  |  Sample value after consolidated controls view, plus description of change  | 
| --- | --- | --- | 
|  Compliance\.SecurityControlId  |  Not applicable \(new field\)  |  EC2\.2 Introduces a single control ID across standards\. `ProductFields.RuleId` still provides the standard\-based control ID for CIS v1\.2\.0 controls\. `ProductFields.ControlId` still provides the standard\-based control ID for controls in other standards\.  | 
|  Compliance\.AssociatedStandards  |  Not applicable \(new field\)  |  \[\{"StandardsId": "standards/aws\-foundational\-security\-best\-practices/v/1\.0\.0"\}\] Shows which standards a control is enabled in\.  | 
|  ProductFields\.ArchivalReasons:0/Description  |  Not applicable \(new field\)  |  "The finding is in an ARCHIVED state because consolidated control findings has been turned on or off\. This causes findings in the previous state to be archived when new findings are being generated\." Describes why Security Hub has archived existing findings\.  | 
|  ProductFields\.ArchivalReasons:0/ReasonCode  |  Not applicable \(new field\)  |  "CONSOLIDATED\_CONTROL\_FINDINGS\_UPDATE" Provides the reason why Security Hub has archived existing findings\.  | 
|  ProductFields\.RecommendationUrl  |  https://docs\.aws\.amazon\.com/console/securityhub/PCI\.EC2\.2/remediation  |  https://docs\.aws\.amazon\.com/console/securityhub/EC2\.2/remediation This field no longer references a standard\.  | 
|  Remediation\.Recommendation\.Text  |  "For directions on how to fix this issue, consult the AWS Security Hub PCI DSS documentation\."  |  "For directions on how to correct this issue, consult the AWS Security Hub controls documentation\." This field no longer references a standard\.  | 
|  Remediation\.Recommendation\.Url  |  https://docs\.aws\.amazon\.com/console/securityhub/PCI\.EC2\.2/remediation  |  https://docs\.aws\.amazon\.com/console/securityhub/EC2\.2/remediation This field no longer references a standard\.  | 

## Consolidated control findings – ASFF changes<a name="securityhub-findings-format-consolidated-control-findings"></a>

If you turn on consolidated control findings, you may be impacted by the following changes to control finding fields and values in the ASFF\. These changes are in addition to the changes previously described for consolidated controls view\. 

If your workflows don’t rely on the values of these control finding fields, no action is required\.

If you have workflows that rely on the specific values of these control finding fields, update your workflows to use the new values\.


|  ASFF field  |  Example value before turning on consolidated control findings  |  Example value after turning on consolidated control findings, and description of change  | 
| --- | --- | --- | 
| GeneratorId |  aws\-foundational\-security\-best\-practices/v/1\.0\.0/Config\.1  |  security\-control/Config\.1 This field will no longer reference a standard\.  | 
|  Title  |  PCI\.Config\.1 AWS Config should be enabled  |  AWS Config should be enabled This field will no longer reference a standard\.  | 
|  Id  |  arn:aws:securityhub:eu\-central\-1:123456789012:subscription/pci\-dss/v/3\.2\.1/PCI\.IAM\.5/finding/ab6d6a26\-a156\-48f0\-9403\-115983e5a956  |  arn:aws:securityhub:eu\-central\-1:123456789012:security\-control/iam\.9/finding/ab6d6a26\-a156\-48f0\-9403\-115983e5a956 This field will no longer reference a standard\.  | 
|  ProductFields\.ControlId  |  PCI\.EC2\.2  |  Removed\. See Compliance\.SecurityControlId instead\. This field is removed in favor of a single, standard\-agnostic control ID\.  | 
|  ProductFields\.RuleId  |  1\.3  |  Removed\. See Compliance\.SecurityControlId instead\. This field is removed in favor of a single, standard\-agnostic control ID\.  | 
|  Description  |  This PCI DSS control checks whether AWS Config is enabled in the current account and region\.  |  This AWS control checks whether AWS Config is enabled in the current account and region\. This field will no longer reference a standard\.  | 
|  Severity  |  "Severity": \{ "Product": 90, "Label": "CRITICAL", "Normalized": 90, "Original": "CRITICAL" \}  |  "Severity": \{ "Label": "CRITICAL", "Normalized": 90, "Original": "CRITICAL" \} Security Hub will no longer use the Product field to describe the severity of a finding\.  | 
|  Types  |  \["Software and Configuration Checks/Industry and Regulatory Standards/PCI\-DSS"\]  |  \["Software and Configuration Checks/Industry and Regulatory Standards"\] This field will no longer reference a standard\.  | 
|  Compliance\.RelatedRequirements  |  \["PCI DSS 10\.5\.2", "PCI DSS 11\.5"\]  |  \["PCI DSS v3\.2\.1/10\.5\.2", "PCI DSS v3\.2\.1/11\.5", "CIS AWS Foundations Benchmark v1\.2\.0/2\.5"\] This field will show related requirements in all enabled standards\.  | 
|  CreatedAt  |  2022\-05\-05T08:18:13\.138Z  |  2022\-09\-25T08:18:13\.138Z Format will remain the same, but value will reset when you turn on consolidated control findings\.  | 
|  FirstObservedAt  |  2022\-05\-07T08:18:13\.138Z  |  2022\-09\-28T08:18:13\.138Z Format will remain the same, but value will reset when you turn on consolidated control findings\.  | 
|  ProductFields\.RecommendationUrl  |  https://docs\.aws\.amazon\.com/console/securityhub/EC2\.2/remediation  |  Removed\. See Remediation\.Recommendation\.Url instead\.  | 
|  ProductFields\.StandardsArn  |  arn:aws:securityhub:::standards/aws\-foundational\-security\-best\-practices/v/1\.0\.0  |  Removed\. See Compliance\.AssociatedStandards instead\.  | 
|  ProductFields\.StandardsControlArn  |  arn:aws:securityhub:us\-east\-1:123456789012:control/aws\-foundational\-security\-best\-practices/v/1\.0\.0/Config\.1  |  Removed\. Security Hub will generate one finding for a security check across standards\.  | 
|  ProductFields\.StandardsGuideArn  |  arn:aws:securityhub:::ruleset/cis\-aws\-foundations\-benchmark/v/1\.2\.0  |  Removed\. See Compliance\.AssociatedStandards instead\.  | 
|  ProductFields\.StandardsGuideSubscriptionArn  |  arn:aws:securityhub:us\-east\-2:123456789012:subscription/cis\-aws\-foundations\-benchmark/v/1\.2\.0  |  Removed\. Security Hub will generate one finding for a security check across standards\.  | 
|  ProductFields\.StandardsSubscriptionArn  |  arn:aws:securityhub:us\-east\-1:123456789012:subscription/aws\-foundational\-security\-best\-practices/v/1\.0\.0  |  Removed\. Security Hub will generate one finding for a security check across standards\.  | 
|  ProductFields\.aws/securityhub/FindingId  |  arn:aws:securityhub:us\-east\-1::product/aws/securityhub/arn:aws:securityhub:us\-east\-1:123456789012:subscription/aws\-foundational\-security\-best\-practices/v/1\.0\.0/Config\.1/finding/751c2173\-7372\-4e12\-8656\-a5210dfb1d67  |  arn:aws:securityhub:us\-east\-1::product/aws/securityhub/arn:aws:securityhub:us\-east\-1:123456789012:security\-control/Config\.1/finding/751c2173\-7372\-4e12\-8656\-a5210dfb1d67 This field will no longer reference a standard\.  | 

### New values for customer\-provided ASFF fields after turning on consolidated control findings<a name="consolidated-controls-view-customer-provided-values"></a>

If you turn on [consolidated control findings](controls-findings-create-update.md#consolidated-control-findings), Security Hub generates one finding across standards and archives the original findings \(separate findings for each standard\)\. To view archived findings, you can visit the **Findings** page of the Security Hub console with the **Record state** filter set to **ARCHIVED**, or use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html) API action\. Updates you’ve made to the original findings in the Security Hub console or using the [BatchUpdateFindings](https://docs.aws.amazon.com/securityhub/latest/userguide/finding-update-batchupdatefindings.html) API won't be preserved in the new findings \(if needed, you can recover this data by referring to the archived findings\)\.


|  Customer\-provided ASFF field  |  Description of change after turning on consolidated control findings  | 
| --- | --- | 
|  Confidence  |  Resets to empty state\.  | 
|  Criticality  |  Resets to empty state\.  | 
|  Note  |  Resets to empty state\.  | 
|  RelatedFindings  |  Resets to empty state\.  | 
|  Severity  |  Default severity of the finding \(matches the severity of the control\)\.  | 
|  Types  |  Resets to standard\-agnostic value\.  | 
|  UserDefinedFields  |  Resets to empty state\.  | 
|  VerificationState  |  Resets to empty state\.  | 
|  Workflow  |  New failed findings have a default value of NEW\. New passed findings have a default value of RESOLVED\.  | 

## Generator IDs before and after turning on consolidated control findings<a name="securityhub-findings-format-changes-generator-ids"></a>

Here's a list of generator ID changes for controls when you turn on consolidated control findings\. These apply to controls that Security Hub supported as of February 15, 2023\.


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
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ACM\.1  |  security\-control/ACM\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/APIGateway\.1  |  security\-control/APIGateway\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/APIGateway\.2  |  security\-control/APIGateway\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/APIGateway\.3  |  security\-control/APIGateway\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/APIGateway\.4  |  security\-control/APIGateway\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/APIGateway\.5  |  security\-control/APIGateway\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/AutoScaling\.1  |  security\-control/AutoScaling\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/AutoScaling\.2  |  security\-control/AutoScaling\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/AutoScaling\.3  |  security\-control/AutoScaling\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/AutoScaling\.4  |  security\-control/AutoScaling\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Autoscaling\.5  |  security\-control/Autoscaling\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/AutoScaling\.6  |  security\-control/AutoScaling\.6  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/AutoScaling\.9  |  security\-control/AutoScaling\.9  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/CloudTrail\.1  |  security\-control/CloudTrail\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/CloudTrail\.2  |  security\-control/CloudTrail\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/CloudTrail\.4  |  security\-control/CloudTrail\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/CloudTrail\.5  |  security\-control/CloudTrail\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/CodeBuild\.1  |  security\-control/CodeBuild\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/CodeBuild\.2  |  security\-control/CodeBuild\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/CodeBuild\.4  |  security\-control/CodeBuild\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/CodeBuild\.5  |  security\-control/CodeBuild\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/DMS\.1  |  security\-control/DMS\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/DynamoDB\.1  |  security\-control/DynamoDB\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/DynamoDB\.2  |  security\-control/DynamoDB\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.1  |  security\-control/EC2\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.2  |  security\-control/EC2\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.3  |  security\-control/EC2\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.4  |  security\-control/EC2\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.6  |  security\-control/EC2\.6  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.7  |  security\-control/EC2\.7  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.8  |  security\-control/EC2\.8  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.9  |  security\-control/EC2\.9  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.10  |  security\-control/EC2\.10  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.15  |  security\-control/EC2\.15  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.16  |  security\-control/EC2\.16  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.17  |  security\-control/EC2\.17  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.18  |  security\-control/EC2\.18  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.19  |  security\-control/EC2\.19  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.20  |  security\-control/EC2\.20  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.21  |  security\-control/EC2\.21  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EC2\.22  |  security\-control/EC2\.22  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECR\.1  |  security\-control/ECR\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECR\.2  |  security\-control/ECR\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECR\.3  |  security\-control/ECR\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECS\.1  |  security\-control/ECS\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECS\.2  |  security\-control/ECS\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECS\.3  |  security\-control/ECS\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECS\.4  |  security\-control/ECS\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECS\.5  |  security\-control/ECS\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECS\.8  |  security\-control/ECS\.8  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECS\.10  |  security\-control/ECS\.10  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ECS\.12  |  security\-control/ECS\.12  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EFS\.1  |  security\-control/EFS\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EFS\.2  |  security\-control/EFS\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EFS\.3  |  security\-control/EFS\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EFS\.4  |  security\-control/EFS\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EKS\.2  |  security\-control/EKS\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.2  |  security\-control/ELB\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.3  |  security\-control/ELB\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.4  |  security\-control/ELB\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.5  |  security\-control/ELB\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.6  |  security\-control/ELB\.6  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.7  |  security\-control/ELB\.7  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.8  |  security\-control/ELB\.8  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.9  |  security\-control/ELB\.9  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.10  |  security\-control/ELB\.10  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.12  |  security\-control/ELB\.12  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.13  |  security\-control/ELB\.13  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELB\.14  |  security\-control/ELB\.14  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ELBv2\.1  |  security\-control/ELBv2\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/EMR\.1  |  security\-control/EMR\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ES\.1  |  security\-control/ES\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ES\.2  |  security\-control/ES\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ES\.3  |  security\-control/ES\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ES\.4  |  security\-control/ES\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ES\.5  |  security\-control/ES\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ES\.6  |  security\-control/ES\.6  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ES\.7  |  security\-control/ES\.7  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ES\.8  |  security\-control/ES\.8  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ElasticBeanstalk\.1  |  security\-control/ElasticBeanstalk\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/ElasticBeanstalk\.2  |  security\-control/ElasticBeanstalk\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/GuardDuty\.1  |  security\-control/GuardDuty\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/IAM\.1  |  security\-control/IAM\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/IAM\.2  |  security\-control/IAM\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/IAM\.3  |  security\-control/IAM\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/IAM\.4  |  security\-control/IAM\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/IAM\.5  |  security\-control/IAM\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/IAM\.6  |  security\-control/IAM\.6  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/IAM\.7  |  security\-control/IAM\.7  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/IAM\.8  |  security\-control/IAM\.8  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/IAM\.21  |  security\-control/IAM\.21  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Kinesis\.1  |  security\-control/Kinesis\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/KMS\.1  |  security\-control/KMS\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/KMS\.2  |  security\-control/KMS\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/KMS\.3  |  security\-control/KMS\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Lambda\.1  |  security\-control/Lambda\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Lambda\.2  |  security\-control/Lambda\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Lambda\.5  |  security\-control/Lambda\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/NetworkFirewall\.3  |  security\-control/NetworkFirewall\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/NetworkFirewall\.4  |  security\-control/NetworkFirewall\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/NetworkFirewall\.5  |  security\-control/NetworkFirewall\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/NetworkFirewall\.6  |  security\-control/NetworkFirewall\.6  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Opensearch\.1  |  security\-control/Opensearch\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Opensearch\.2  |  security\-control/Opensearch\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Opensearch\.3  |  security\-control/Opensearch\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Opensearch\.4  |  security\-control/Opensearch\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Opensearch\.5  |  security\-control/Opensearch\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Opensearch\.6  |  security\-control/Opensearch\.6  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Opensearch\.7  |  security\-control/Opensearch\.7  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Opensearch\.8  |  security\-control/Opensearch\.8  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.1  |  security\-control/RDS\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.2  |  security\-control/RDS\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.3  |  security\-control/RDS\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.4  |  security\-control/RDS\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.5  |  security\-control/RDS\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.6  |  security\-control/RDS\.6  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.8  |  security\-control/RDS\.8  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.9  |  security\-control/RDS\.9  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.10  |  security\-control/RDS\.10  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.11  |  security\-control/RDS\.11  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.13  |  security\-control/RDS\.13  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.17  |  security\-control/RDS\.17  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.18  |  security\-control/RDS\.18  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.19  |  security\-control/RDS\.19  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.20  |  security\-control/RDS\.20  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.21  |  security\-control/RDS\.21  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.22  |  security\-control/RDS\.22  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.23  |  security\-control/RDS\.23  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/RDS\.25  |  security\-control/RDS\.25  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Redshift\.1  |  security\-control/Redshift\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Redshift\.2  |  security\-control/Redshift\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Redshift\.4  |  security\-control/Redshift\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Redshift\.6  |  security\-control/Redshift\.6  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Redshift\.7  |  security\-control/Redshift\.7  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Redshift\.8  |  security\-control/Redshift\.8  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/Redshift\.9  |  security\-control/Redshift\.9  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.1  |  security\-control/S3\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.2  |  security\-control/S3\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.3  |  security\-control/S3\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.4  |  security\-control/S3\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.5  |  security\-control/S3\.5  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.6  |  security\-control/S3\.6  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.8  |  security\-control/S3\.8  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.9  |  security\-control/S3\.9  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.10  |  security\-control/S3\.10  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.11  |  security\-control/S3\.11  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.12  |  security\-control/S3\.12  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/S3\.13  |  security\-control/S3\.13  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SageMaker\.1  |  security\-control/SageMaker\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SecretsManager\.1  |  security\-control/SecretsManager\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SecretsManager\.2  |  security\-control/SecretsManager\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SecretsManager\.3  |  security\-control/SecretsManager\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SecretsManager\.4  |  security\-control/SecretsManager\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SNS\.1  |  security\-control/SNS\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SNS\.2  |  security\-control/SNS\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SQS\.1  |  security\-control/SQS\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SSM\.1  |  security\-control/SSM\.1  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SSM\.2  |  security\-control/SSM\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SSM\.3  |  security\-control/SSM\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/SSM\.4  |  security\-control/SSM\.4  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/WAF\.2  |  security\-control/WAF\.2  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/WAF\.3  |  security\-control/WAF\.3  | 
|  service\-managed\-aws\-control\-tower/v/1\.0\.0/WAF\.4  |  security\-control/WAF\.4  | 

## How consolidation impacts control IDs and titles<a name="securityhub-findings-format-changes-ids-titles"></a>

Consolidated controls view and consolidated control findings impact some control IDs and titles as these values are now consistent across standards \(the terms *security control ID* and *security control title* refer to these standard\-agnostic values\)\. See the complete list of changes in the following table\. IDs and titles for controls that apply to the AWS Foundational Security Best Practices \(FSBP\) standard remain the same before and after these feature releases\.

The Security Hub console displays security control IDs and security control titles, regardless of whether consolidated control findings is turned on or off in your account\. However, Security Hub findings reference security control IDs and security control titles only if consolidated control findings is turned on in your account\. If consolidated control findings is turned off in your account, Security Hub findings reference standard control IDs and standard control titles\. For more information about how consolidation impacts control findings, see [Sample control findings](sample-control-findings.md)\.

For controls that are part of [Service\-Managed Standard: AWS Control Tower](service-managed-standard-aws-control-tower.md), the prefix `CT.` is removed from the control ID and title in findings when consolidated control findings is turned on\.

Consolidated controls view and consolidated control findings aren't currently supported in the AWS GovCloud \(US\) Region and China Regions\. In these Regions, Security Hub uses the standard control IDs and titles\.


| Standard | Standard control ID | Standard control title | Security control ID | Security control title | 
| --- | --- | --- | --- | --- | 
|  CIS v1\.2\.0  |  1\.1  |  1\.1 Avoid the use of the root user  |  [CloudWatch\.1](cloudwatch-controls.md#cloudwatch-1)  |  A log metric filter and alarm should exist for usage of the root user  | 
|  CIS v1\.2\.0  |  1\.1  |  1\.1 Avoid the use of the root user  |  [IAM\.20](iam-controls.md#iam-20)  |  Avoid the use of the root user  | 
|  CIS v1\.2\.0  |  1\.1  |  1\.10 Ensure IAM password policy prevents password reuse  |  [IAM\.16](iam-controls.md#iam-16)  |  Ensure IAM password policy prevents password reuse  | 
|  CIS v1\.2\.0  |  1\.11  |  1\.11 Ensure IAM password policy expires passwords within 90 days or less  |  [IAM\.17](iam-controls.md#iam-17)  |  Ensure IAM password policy expires passwords within 90 days or less  | 
|  CIS v1\.2\.0  |  1\.12  |  1\.12 Ensure no root user access key exists  |  [IAM\.4](iam-controls.md#iam-4)  |  IAM root user access key should not exist  | 
|  CIS v1\.2\.0  |  1\.13  |  1\.13 Ensure MFA is enabled for the root user  |  [IAM\.9](iam-controls.md#iam-9)  |  Virtual MFA should be enabled for the root user  | 
|  CIS v1\.2\.0  |  1\.14  |  1\.14 Ensure hardware MFA is enabled for the root user  |  [IAM\.6](iam-controls.md#iam-6)  |  Hardware MFA should be enabled for the root user  | 
|  CIS v1\.2\.0  |  1\.16  |  1\.16 Ensure IAM policies are attached only to groups or roles  |  [IAM\.2](iam-controls.md#iam-2)  |  IAM users should not have IAM policies attached  | 
|  CIS v1\.2\.0  |  1\.2  |  1\.2 Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password  |  [IAM\.5](iam-controls.md#iam-5)  |  MFA should be enabled for all IAM users that have a console password  | 
|  CIS v1\.2\.0  |  1\.2  |  1\.20 Ensure a support role has been created to manage incidents with AWS Support  |  [IAM\.18](iam-controls.md#iam-18)  |  Ensure a support role has been created to manage incidents with AWS Support  | 
|  CIS v1\.2\.0  |  1\.22  |  1\.22 Ensure IAM policies that allow full "\*:\*" administrative privileges are not created  |  [IAM\.1](iam-controls.md#iam-1)  |  IAM policies should not allow full "\*" administrative privileges  | 
|  CIS v1\.2\.0  |  1\.3  |  1\.3 Ensure credentials unused for 90 days or greater are disabled  |  [IAM\.8](iam-controls.md#iam-8)  |  Unused IAM user credentials should be removed  | 
|  CIS v1\.2\.0  |  1\.4  |  1\.4 Ensure access keys are rotated every 90 days or less  |  [IAM\.3](iam-controls.md#iam-3)  |  IAM users' access keys should be rotated every 90 days or less  | 
|  CIS v1\.2\.0  |  1\.5  |  1\.5 Ensure IAM password policy requires at least one uppercase letter  |  [IAM\.11](iam-controls.md#iam-11)  |  Ensure IAM password policy requires at least one uppercase letter  | 
|  CIS v1\.2\.0  |  1\.6  |  1\.6 Ensure IAM password policy requires at least one lowercase letter  |  [IAM\.12](iam-controls.md#iam-12)  |  Ensure IAM password policy requires at least one lowercase letter  | 
|  CIS v1\.2\.0  |  1\.7  |  1\.7 Ensure IAM password policy requires at least one symbol  |  [IAM\.13](iam-controls.md#iam-13)  |  Ensure IAM password policy requires at least one symbol  | 
|  CIS v1\.2\.0  |  1\.8  |  1\.8 Ensure IAM password policy requires at least one number  |  [IAM\.14](iam-controls.md#iam-14)  |  Ensure IAM password policy requires at least one number  | 
|  CIS v1\.2\.0  |  1\.9  |  1\.9 Ensure IAM password policy requires minimum password length of 14 or greater  |  [IAM\.15](iam-controls.md#iam-15)  |  Ensure IAM password policy requires minimum password length of 14 or greater  | 
|  CIS v1\.2\.0  |  2\.1  |  2\.1 Ensure CloudTrail is enabled in all regions  |  [CloudTrail\.1](cloudtrail-controls.md#cloudtrail-1)  |  CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events  | 
|  CIS v1\.2\.0  |  2\.2  |  2\.2 Ensure CloudTrail log file validation is enabled  |  [CloudTrail\.4](cloudtrail-controls.md#cloudtrail-4)  |  CloudTrail log file validation should be enabled  | 
|  CIS v1\.2\.0  |  2\.3  |  2\.3 Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible  |  [CloudTrail\.6](cloudtrail-controls.md#cloudtrail-6)  |  Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible  | 
|  CIS v1\.2\.0  |  2\.4  |  2\.4 Ensure CloudTrail trails are integrated with CloudWatch Logs  |  [CloudTrail\.5](cloudtrail-controls.md#cloudtrail-5)  |  CloudTrail trails should be integrated with Amazon CloudWatch Logs  | 
|  CIS v1\.2\.0  |  2\.5  |  2\.5 Ensure AWS Config is enabled  |  [Config\.1](config-controls.md#config-1)  |  AWS Config should be enabled  | 
|  CIS v1\.2\.0  |  2\.6  |  2\.6 Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket  |  [CloudTrail\.7](cloudtrail-controls.md#cloudtrail-7)  |  Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket  | 
|  CIS v1\.2\.0  |  2\.7  |  2\.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs  |  [CloudTrail\.2](cloudtrail-controls.md#cloudtrail-2)  |  CloudTrail should have encryption at\-rest enabled  | 
|  CIS v1\.2\.0  |  2\.8  |  2\.8 Ensure rotation for customer created CMKs is enabled  |  [KMS\.4](kms-controls.md#kms-4)  |  Customer master key \(CMK\) rotation should be enabled  | 
|  CIS v1\.2\.0  |  2\.9  |  2\.9 Ensure VPC flow logging is enabled in all VPCs  |  [EC2\.6](ec2-controls.md#ec2-6)  |  VPC flow logging should be enabled in all VPCs  | 
|  CIS v1\.2\.0  |  3\.1  |  3\.1 Ensure a log metric filter and alarm exist for unauthorized API calls  |  [CloudWatch\.2](cloudwatch-controls.md#cloudwatch-2)  |  Ensure a log metric filter and alarm exist for unauthorized API calls  | 
|  CIS v1\.2\.0  |  3\.1  |  3\.10 Ensure a log metric filter and alarm exist for security group changes  |  [CloudWatch\.10](cloudwatch-controls.md#cloudwatch-10)  |  Ensure a log metric filter and alarm exist for security group changes  | 
|  CIS v1\.2\.0  |  3\.11  |  3\.11 Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  |  [CloudWatch\.11](cloudwatch-controls.md#cloudwatch-11)  |  Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  | 
|  CIS v1\.2\.0  |  3\.12  |  3\.12 Ensure a log metric filter and alarm exist for changes to network gateways  |  [CloudWatch\.12](cloudwatch-controls.md#cloudwatch-12)  |  Ensure a log metric filter and alarm exist for changes to network gateways  | 
|  CIS v1\.2\.0  |  3\.13  |  3\.13 Ensure a log metric filter and alarm exist for route table changes  |  [CloudWatch\.13](cloudwatch-controls.md#cloudwatch-13)  |  Ensure a log metric filter and alarm exist for route table changes  | 
|  CIS v1\.2\.0  |  3\.14  |  3\.14 Ensure a log metric filter and alarm exist for VPC changes  |  [CloudWatch\.14](cloudwatch-controls.md#cloudwatch-14)  |  Ensure a log metric filter and alarm exist for VPC changes  | 
|  CIS v1\.2\.0  |  3\.2  |  3\.2 Ensure a log metric filter and alarm exist for Management Console sign\-in without MFA  |  [CloudWatch\.3](cloudwatch-controls.md#cloudwatch-3)  |  Ensure a log metric filter and alarm exist for Management Console sign\-in without MFA  | 
|  CIS v1\.2\.0  |  3\.3  |  3\.3 Ensure a log metric filter and alarm exist for usage of root user  |  [CloudWatch\.1](cloudwatch-controls.md#cloudwatch-1)  |  A log metric filter and alarm should exist for usage of the "root" user  | 
|  CIS v1\.2\.0  |  3\.4  |  3\.4 Ensure a log metric filter and alarm exist for IAM policy changes  |  [CloudWatch\.4](cloudwatch-controls.md#cloudwatch-4)  |  Ensure a log metric filter and alarm exist for IAM policy changes  | 
|  CIS v1\.2\.0  |  3\.5  |  3\.5 Ensure a log metric filter and alarm exist for CloudTrail configuration changes  |  [CloudWatch\.5](cloudwatch-controls.md#cloudwatch-5)  |  Ensure a log metric filter and alarm exist for CloudTrail configuration changes  | 
|  CIS v1\.2\.0  |  3\.6  |  3\.6 Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  |  [CloudWatch\.6](cloudwatch-controls.md#cloudwatch-6)  |  Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  | 
|  CIS v1\.2\.0  |  3\.7  |  3\.7 Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs  |  [CloudWatch\.7](cloudwatch-controls.md#cloudwatch-7)  |  Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs  | 
|  CIS v1\.2\.0  |  3\.8  |  3\.8 Ensure a log metric filter and alarm exist for S3 bucket policy changes  |  [CloudWatch\.8](cloudwatch-controls.md#cloudwatch-8)  |  Ensure a log metric filter and alarm exist for S3 bucket policy changes  | 
|  CIS v1\.2\.0  |  3\.9  |  3\.9 Ensure a log metric filter and alarm exist for AWS Config configuration changes  |  [CloudWatch\.9](cloudwatch-controls.md#cloudwatch-9)  |  Ensure a log metric filter and alarm exist for AWS Config configuration changes  | 
|  CIS v1\.2\.0  |  4\.1  |  4\.1 Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 22  |  [EC2\.13](ec2-controls.md#ec2-13)  |  Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22  | 
|  CIS v1\.2\.0  |  4\.2  |  4\.2 Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389  |  [EC2\.14](ec2-controls.md#ec2-14)  |  Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389  | 
|  CIS v1\.2\.0  |  4\.3  |  4\.3 Ensure the default security group of every VPC restricts all traffic  |  [EC2\.2](ec2-controls.md#ec2-2)  |  The VPC default security group should not allow inbound and outbound traffic  | 
|  CIS v1\.4\.0  |  1\.1  |  1\.10 Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password  |  [IAM\.5](iam-controls.md#iam-5)  |  MFA should be enabled for all IAM users that have a console password  | 
|  CIS v1\.4\.0  |  1\.14  |  1\.14 Ensure access keys are rotated every 90 days or less  |  [IAM\.3](iam-controls.md#iam-3)  |  IAM users' access keys should be rotated every 90 days or less  | 
|  CIS v1\.4\.0  |  1\.16  |  1\.16 Ensure IAM policies that allow full "\*:\*" administrative privileges are not attached  |  [IAM\.1](iam-controls.md#iam-1)  |  IAM policies should not allow full "\*" administrative privileges  | 
|  CIS v1\.4\.0  |  1\.17  |  1\.17 Ensure a support role has been created to manage incidents with AWS Support  |  [IAM\.18](iam-controls.md#iam-18)  |  Ensure a support role has been created to manage incidents with AWS Support  | 
|  CIS v1\.4\.0  |  1\.4  |  1\.4 Ensure no root user account access key exists  |  [IAM\.4](iam-controls.md#iam-4)  |  IAM root user access key should not exist  | 
|  CIS v1\.4\.0  |  1\.5  |  1\.5 Ensure MFA is enabled for the root user account  |  [IAM\.9](iam-controls.md#iam-9)  |  Virtual MFA should be enabled for the root user  | 
|  CIS v1\.4\.0  |  1\.6  |  1\.6 Ensure hardware MFA is enabled for the root user account  |  [IAM\.6](iam-controls.md#iam-6)  |  Hardware MFA should be enabled for the root user  | 
|  CIS v1\.4\.0  |  1\.7  |  1\.7 Eliminate use of the root user for administrative and daily tasks  |  [CloudWatch\.1](cloudwatch-controls.md#cloudwatch-1)  |  A log metric filter and alarm should exist for usage of the "root" user  | 
|  CIS v1\.4\.0  |  1\.8  |  1\.8 Ensure IAM password policy requires minimum length of 14 or greater  |  [IAM\.15](iam-controls.md#iam-15)  |  Ensure IAM password policy requires minimum password length of 14 or greater  | 
|  CIS v1\.4\.0  |  1\.9  |  1\.9 Ensure IAM password policy prevents password reuse  |  [IAM\.16](iam-controls.md#iam-16)  |  Ensure IAM password policy prevents password reuse  | 
|  CIS v1\.4\.0  |  2\.1\.1  |  2\.1\.1 Ensure all S3 buckets employ encryption\-at\-rest  |  [S3\.4](s3-controls.md#s3-4)  |  S3 buckets should have server\-side encryption enabled  | 
|  CIS v1\.4\.0  |  2\.1\.2  |  2\.1\.2 Ensure S3 Bucket Policy is set to deny HTTP requests  |  [S3\.5](s3-controls.md#s3-5)  |  S3 buckets should require requests to use Secure Socket Layer  | 
|  CIS v1\.4\.0  |  2\.1\.5\.1  |  2\.1\.5\.1 S3 Block Public Access setting should be enabled  |  [S3\.1](s3-controls.md#s3-1)  |  S3 Block Public Access setting should be enabled  | 
|  CIS v1\.4\.0  |  2\.1\.5\.2  |  2\.1\.5\.2 S3 Block Public Access setting should be enabled at the bucket level  |  [S3\.8](s3-controls.md#s3-8)  |  S3 Block Public Access setting should be enabled at the bucket level  | 
|  CIS v1\.4\.0  |  2\.2\.1  |  2\.2\.1 Ensure EBS volume encryption is enabled  |  [EC2\.7](ec2-controls.md#ec2-7)  |  EBS default encryption should be enabled  | 
|  CIS v1\.4\.0  |  2\.3\.1  |  2\.3\.1 Ensure that encryption is enabled for RDS Instances  |  [RDS\.3](rds-controls.md#rds-3)  |  RDS DB instances should have encryption at\-rest enabled  | 
|  CIS v1\.4\.0  |  3\.1  |  3\.1 Ensure CloudTrail is enabled in all regions  |  [CloudTrail\.1](cloudtrail-controls.md#cloudtrail-1)  |  CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events  | 
|  CIS v1\.4\.0  |  3\.2  |  3\.2 Ensure CloudTrail log file validation is enabled  |  [CloudTrail\.4](cloudtrail-controls.md#cloudtrail-4)  |  CloudTrail log file validation should be enabled  | 
|  CIS v1\.4\.0  |  3\.4  |  3\.4 Ensure CloudTrail trails are integrated with CloudWatch Logs  |  [CloudTrail\.5](cloudtrail-controls.md#cloudtrail-5)  |  CloudTrail trails should be integrated with Amazon CloudWatch Logs  | 
|  CIS v1\.4\.0  |  3\.5  |  3\.5 Ensure AWS Config is enabled in all regions  |  [Config\.1](config-controls.md#config-1)  |  AWS Config should be enabled  | 
|  CIS v1\.4\.0  |  3\.6  |  3\.6 Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket  |  [S3\.9](s3-controls.md#s3-9)  |  S3 bucket server access logging should be enabled  | 
|  CIS v1\.4\.0  |  3\.7  |  3\.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs  |  [CloudTrail\.2](cloudtrail-controls.md#cloudtrail-2)  |  CloudTrail should have encryption at\-rest enabled  | 
|  CIS v1\.4\.0  |  3\.8  |  3\.8 Ensure rotation for customer created CMKs is enabled  |  [KMS\.4](kms-controls.md#kms-4)  |  Customer master key \(CMK\) rotation should be enabled  | 
|  CIS v1\.4\.0  |  3\.9  |  3\.9 Ensure VPC flow logging is enabled in all VPCs  |  [EC2\.6](ec2-controls.md#ec2-6)  |  VPC flow logging should be enabled in all VPCs  | 
|  CIS v1\.4\.0  |  4\.4  |  4\.4 Ensure a log metric filter and alarm exist for IAM policy changes  |  [CloudWatch\.4](cloudwatch-controls.md#cloudwatch-4)  |  Ensure a log metric filter and alarm exist for IAM policy changes  | 
|  CIS v1\.4\.0  |  4\.5  |  4\.5 Ensure a log metric filter and alarm exist for CloudTrail configuration changes  |  [CloudWatch\.5](cloudwatch-controls.md#cloudwatch-5)  |  Ensure a log metric filter and alarm exist for CloudTrail configuration changes  | 
|  CIS v1\.4\.0  |  4\.6  |  4\.6 Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  |  [CloudWatch\.6](cloudwatch-controls.md#cloudwatch-6)  |  Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  | 
|  CIS v1\.4\.0  |  4\.7  |  4\.7 Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs  |  [CloudWatch\.7](cloudwatch-controls.md#cloudwatch-7)  |  Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs  | 
|  CIS v1\.4\.0  |  4\.8  |  4\.8 Ensure a log metric filter and alarm exist for S3 bucket policy changes  |  [CloudWatch\.8](cloudwatch-controls.md#cloudwatch-8)  |  Ensure a log metric filter and alarm exist for S3 bucket policy changes  | 
|  CIS v1\.4\.0  |  4\.9  |  4\.9 Ensure a log metric filter and alarm exist for AWS Config configuration changes  |  [CloudWatch\.9](cloudwatch-controls.md#cloudwatch-9)  |  Ensure a log metric filter and alarm exist for AWS Config configuration changes  | 
|  CIS v1\.4\.0  |  4\.1  |  4\.10 Ensure a log metric filter and alarm exist for security group changes  |  [CloudWatch\.10](cloudwatch-controls.md#cloudwatch-10)  |  Ensure a log metric filter and alarm exist for security group changes  | 
|  CIS v1\.4\.0  |  4\.11  |  4\.11 Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  |  [CloudWatch\.11](cloudwatch-controls.md#cloudwatch-11)  |  Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  | 
|  CIS v1\.4\.0  |  4\.12  |  4\.12 Ensure a log metric filter and alarm exist for changes to network gateways  |  [CloudWatch\.12](cloudwatch-controls.md#cloudwatch-12)  |  Ensure a log metric filter and alarm exist for changes to network gateways  | 
|  CIS v1\.4\.0  |  4\.13  |  4\.13 Ensure a log metric filter and alarm exist for route table changes  |  [CloudWatch\.13](cloudwatch-controls.md#cloudwatch-13)  |  Ensure a log metric filter and alarm exist for route table changes  | 
|  CIS v1\.4\.0  |  4\.14  |  4\.14 Ensure a log metric filter and alarm exist for VPC changes  |  [CloudWatch\.14](cloudwatch-controls.md#cloudwatch-14)  |  Ensure a log metric filter and alarm exist for VPC changes  | 
|  CIS v1\.4\.0  |  5\.1  |  5\.1 Ensure no Network ACLs allow ingress from 0\.0\.0\.0/0 to remote server administration ports  |  [EC2\.21](ec2-controls.md#ec2-21)  |  Network ACLs should not allow ingress from 0\.0\.0\.0/0 to port 22 or port 3389  | 
|  CIS v1\.4\.0  |  5\.3  |  5\.3 Ensure the default security group of every VPC restricts all traffic  |  [EC2\.2](ec2-controls.md#ec2-2)  |  The VPC default security group should not allow inbound and outbound traffic  | 
|  PCI DSS v3\.2\.1  |  PCI\.AutoScaling\.1  |  PCI\.AutoScaling\.1 Auto scaling groups associated with a load balancer should use load balancer health checks  |  [AutoScaling\.1](autoscaling-controls.md#autoscaling-1)  |  Auto scaling groups associated with a load balancer should use load balancer health checks  | 
|  PCI DSS v3\.2\.1  |  PCI\.CloudTrail\.1  |  PCI\.CloudTrail\.1 CloudTrail logs should be encrypted at rest using AWS KMS CMKs  |  [CloudTrail\.2](cloudtrail-controls.md#cloudtrail-2)  |  CloudTrail should have encryption at\-rest enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.CloudTrail\.2  |  PCI\.CloudTrail\.2 CloudTrail should be enabled  |  [CloudTrail\.3](cloudtrail-controls.md#cloudtrail-3)  |  CloudTrail should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.CloudTrail\.3  |  PCI\.CloudTrail\.3 CloudTrail log file validation should be enabled  |  [CloudTrail\.4](cloudtrail-controls.md#cloudtrail-4)  |  CloudTrail log file validation should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.CloudTrail\.4  |  PCI\.CloudTrail\.4 CloudTrail trails should be integrated with Amazon CloudWatch Logs  |  [CloudTrail\.5](cloudtrail-controls.md#cloudtrail-5)  |  CloudTrail trails should be integrated with Amazon CloudWatch Logs  | 
|  PCI DSS v3\.2\.1  |  PCI\.CodeBuild\.1  |  PCI\.CodeBuild\.1 CodeBuild GitHub or Bitbucket source repository URLs should use OAuth  |  [CodeBuild\.1](codebuild-controls.md#codebuild-1)  |  CodeBuild GitHub or Bitbucket source repository URLs should use OAuth  | 
|  PCI DSS v3\.2\.1  |  PCI\.CodeBuild\.2  |  PCI\.CodeBuild\.2 CodeBuild project environment variables should not contain clear text credentials  |  [CodeBuild\.2](codebuild-controls.md#codebuild-2)  |  CodeBuild project environment variables should not contain clear text credentials  | 
|  PCI DSS v3\.2\.1  |  PCI\.Config\.1  |  PCI\.Config\.1 AWS Config should be enabled  |  [Config\.1](config-controls.md#config-1)  |  AWS Config should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.CW\.1  |  PCI\.CW\.1 A log metric filter and alarm should exist for usage of the "root" user  |  [CloudWatch\.1](cloudwatch-controls.md#cloudwatch-1)  |  A log metric filter and alarm should exist for usage of the "root" user  | 
|  PCI DSS v3\.2\.1  |  PCI\.DMS\.1  |  PCI\.DMS\.1 Database Migration Service replication instances should not be public  |  [DMS\.1](dms-controls.md#dms-1)  |  Database Migration Service replication instances should not be public  | 
|  PCI DSS v3\.2\.1  |  PCI\.EC2\.1  |  PCI\.EC2\.1 EBS snapshots should not be publicly restorable  |  [EC2\.1](ec2-controls.md#ec2-1)  |  EBS snapshots should not be publicly restorable  | 
|  PCI DSS v3\.2\.1  |  PCI\.EC2\.2  |  PCI\.EC2\.2 VPC default security group should prohibit inbound and outbound traffic  |  [EC2\.2](ec2-controls.md#ec2-2)  |  The VPC default security group should not allow inbound and outbound traffic  | 
|  PCI DSS v3\.2\.1  |  PCI\.EC2\.4  |  PCI\.EC2\.4 Unused EC2 EIPs should be removed  |  [EC2\.12](ec2-controls.md#ec2-12)  |  Unused EC2 EIPs should be removed  | 
|  PCI DSS v3\.2\.1  |  PCI\.EC2\.5  |  PCI\.EC2\.5 Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22  |  [EC2\.13](ec2-controls.md#ec2-13)  |  Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22  | 
|  PCI DSS v3\.2\.1  |  PCI\.EC2\.6  |  PCI\.EC2\.6 VPC flow logging should be enabled in all VPCs  |  [EC2\.6](ec2-controls.md#ec2-6)  |  VPC flow logging should be enabled in all VPCs  | 
|  PCI DSS v3\.2\.1  |  PCI\.ELBv2\.1  |  PCI\.ELBv2\.1 Application Load Balancer should be configured to redirect all HTTP requests to HTTPS  |  [ELB\.1](elb-controls.md#elb-1)  |  Application Load Balancer should be configured to redirect all HTTP requests to HTTPS  | 
|  PCI DSS v3\.2\.1  |  PCI\.ES\.1  |  PCI\.ES\.1 Elasticsearch domains should be in a VPC  |  [ES\.2](es-controls.md#es-2)  |  Elasticsearch domains should be in a VPC  | 
|  PCI DSS v3\.2\.1  |  PCI\.ES\.2  |  PCI\.ES\.2 Elasticsearch domains should have encryption at\-rest enabled  |  [ES\.1](es-controls.md#es-1)  |  Elasticsearch domains should have encryption at\-rest enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.GuardDuty\.1  |  PCI\.GuardDuty\.1 GuardDuty should be enabled  |  [GuardDuty\.1](guardduty-controls.md#guardduty-1)  |  GuardDuty should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.1  |  PCI\.IAM\.1 IAM root user access key should not exist  |  [IAM\.4](iam-controls.md#iam-4)  |  IAM root user access key should not exist  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.2  |  PCI\.IAM\.2 IAM users should not have IAM policies attached  |  [IAM\.2](iam-controls.md#iam-2)  |  IAM users should not have IAM policies attached  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.3  |  PCI\.IAM\.3 IAM policies should not allow full "\*" administrative privileges  |  [IAM\.1](iam-controls.md#iam-1)  |  IAM policies should not allow full "\*" administrative privileges  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.4  |  PCI\.IAM\.4 Hardware MFA should be enabled for the root user  |  [IAM\.6](iam-controls.md#iam-6)  |  Hardware MFA should be enabled for the root user  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.5  |  PCI\.IAM\.5 Virtual MFA should be enabled for the root user  |  [IAM\.9](iam-controls.md#iam-9)  |  Virtual MFA should be enabled for the root user  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.6  |  PCI\.IAM\.6 MFA should be enabled for all IAM users  |  [IAM\.19](iam-controls.md#iam-19)  |  MFA should be enabled for all IAM users  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.7  |  PCI\.IAM\.7 IAM user credentials should be disabled if not used within a pre\-defined number days  |  [IAM\.8](iam-controls.md#iam-8)  |  Unused IAM user credentials should be removed  | 
|  PCI DSS v3\.2\.1  |  PCI\.IAM\.8  |  PCI\.IAM\.8 Password policies for IAM users should have strong configurations  |  [IAM\.10](iam-controls.md#iam-10)  |  Password policies for IAM users should have strong configurations  | 
|  PCI DSS v3\.2\.1  |  PCI\.KMS\.1  |  PCI\.KMS\.1 Customer master key \(CMK\) rotation should be enabled  |  [KMS\.4](kms-controls.md#kms-4)  |  Customer master key \(CMK\) rotation should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.Lambda\.1  |  PCI\.Lambda\.1 Lambda functions should prohibit public access  |  [Lambda\.1](lambda-controls.md#lambda-1)  |  Lambda function policies should prohibit public access  | 
|  PCI DSS v3\.2\.1  |  PCI\.Lambda\.2  |  PCI\.Lambda\.2 Lambda functions should be in a VPC  |  [Lambda\.3](lambda-controls.md#lambda-3)  |  Lambda functions should be in a VPC  | 
|  PCI DSS v3\.2\.1  |  PCI\.Opensearch\.1  |  PCI\.Opensearch\.1 OpenSearch domains should be in a VPC  |  [Opensearch\.2](opensearch-controls.md#opensearch-2)  |  OpenSearch domains should be in a VPC  | 
|  PCI DSS v3\.2\.1  |  PCI\.Opensearch\.2  |  PCI\.Opensearch\.2 EBS snapshots should not be publicly restorable  |  [Opensearch\.1](opensearch-controls.md#opensearch-1)  |  OpenSearch domains should have encryption at rest enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.RDS\.1  |  PCI\.RDS\.1 RDS snapshot should be private  |  [RDS\.1](rds-controls.md#rds-1)  |  RDS snapshot should be private  | 
|  PCI DSS v3\.2\.1  |  PCI\.RDS\.2  |  PCI\.RDS\.2 RDS DB Instances should prohibit public access  |  [RDS\.2](rds-controls.md#rds-2)  |  RDS DB Instances should prohibit public access, as determined by the PubliclyAccessible configuration  | 
|  PCI DSS v3\.2\.1  |  PCI\.Redshift\.1  |  PCI\.Redshift\.1 Amazon Redshift clusters should prohibit public access  |  [Redshift\.1](redshift-controls.md#redshift-1)  |  Amazon Redshift clusters should prohibit public access  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.1  |  PCI\.S3\.1 S3 buckets should prohibit public write access  |  [S3\.3](s3-controls.md#s3-3)  |  S3 buckets should prohibit public write access  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.2  |  PCI\.S3\.2 S3 buckets should prohibit public read access  |  [S3\.2](s3-controls.md#s3-2)  |  S3 buckets should prohibit public read access  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.3  |  PCI\.S3\.3 S3 buckets should have cross\-region replication enabled  |  [S3\.7](s3-controls.md#s3-7)  |  S3 buckets should have cross\-region replication enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.4  |  PCI\.S3\.4 S3 buckets should have server\-side encryption enabled  |  [S3\.4](s3-controls.md#s3-4)  |  S3 buckets should have server\-side encryption enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.5  |  PCI\.S3\.5 S3 buckets should require requests to use Secure Socket Layer  |  [S3\.5](s3-controls.md#s3-5)  |  S3 buckets should require requests to use Secure Socket Layer  | 
|  PCI DSS v3\.2\.1  |  PCI\.S3\.6  |  PCI\.S3\.6 S3 Block Public Access setting should be enabled  |  [S3\.1](s3-controls.md#s3-1)  |  S3 Block Public Access setting should be enabled  | 
|  PCI DSS v3\.2\.1  |  PCI\.SageMaker\.1  |  PCI\.SageMaker\.1 Amazon SageMaker notebook instances should not have direct internet access  |  [SageMaker\.1](sagemaker-controls.md#sagemaker-1)  |  Amazon SageMaker notebook instances should not have direct internet access  | 
|  PCI DSS v3\.2\.1  |  PCI\.SSM\.1  |  PCI\.SSM\.1 EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation  |  [SSM\.2](ssm-controls.md#ssm-2)  |  EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation  | 
|  PCI DSS v3\.2\.1  |  PCI\.SSM\.2  |  PCI\.SSM\.2 EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT  |  [SSM\.3](ssm-controls.md#ssm-3)  |  EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT  | 
|  PCI DSS v3\.2\.1  |  PCI\.SSM\.3  |  PCI\.SSM\.3 EC2 instances should be managed by AWS Systems Manager  |  [SSM\.1](ssm-controls.md#ssm-1)  |  EC2 instances should be managed by AWS Systems Manager  | 

## Updating workflows for consolidation<a name="securityhub-findings-format-changes-prepare"></a>

If your workflows don’t rely on the specific format of any control finding fields, no action is required\.

If your workflows rely on the specific format of any control finding fields noted in the tables, you will need to update your workflows\. For example, If you created a Amazon CloudWatch Events rule that triggered an action for a specific control ID \(such as invoking an AWS Lambda function if the control ID equals CIS 2\.7\), you will need to update the rule to use CloudTrail\.2, the new `Compliance.SecurityControlId` field for that control\.

If you created [custom insights](securityhub-custom-insights.md) using any of the control finding fields or values that will change, you should update those insights to use the new fields or values\.

We recommend that you wait to turn on consolidated control findings if you currently rely on the [Automated Security Response on AWS](http://aws.amazon.com/solutions/implementations/aws-security-hub-automated-response-and-remediation/) solution for predefined response and remediation actions\. This solution doesn't yet support consolidated control findings\. If you turn on consolidated control findings now, actions you deployed using the solution won't work\.