# How Security Hub uses AWS Config rules to run security checks<a name="securityhub-standards-awsconfigrules"></a>

To run security checks on your environment's resources, AWS Security Hub either uses steps specified by the standard, or uses specific AWS Config rules\. Some rules are managed rules, which are managed by AWS Config\. Other rules are custom rules that Security Hub develops\.

AWS Config rules that Security Hub uses for controls are referred to as service\-linked rules, because they are enabled and controlled by the Security Hub service\.

To enable checks against these AWS Config rules, every account that has Security Hub enabled must first enable AWS Config, and enable resource recording for all resources\. See [Enabling and configuring AWS Config](securityhub-prereq-config.md)\.

## How Security Hub generates the service\-linked rules<a name="securityhub-standards-generate-awsconfigrules"></a>

For every control that uses an AWS Config service\-linked rule, Security Hub creates instances of the required rules in your AWS environment\.

These service\-linked rules are specific to Security Hub\. It creates these service\-linked rules even if other instances of the same rules already exist\.

For AWS Config managed rules, the quota is 250 rules per account per Region\. The service\-linked AWS Config rules that Security Hub creates do not count towards that quota\. You can enable a security standard even if you already have 250 AWS Config managed rules in your account\.

For service\-linked rules, the quota is 250 rules per account per Region\. This is in addition to the 250\-rule quota on AWS Config managed rules\.

## Viewing details about the AWS Config rules for controls<a name="securityhub-standards-view-config-rule-details"></a>

For controls that use AWS Config managed rules, the control description includes a link to the AWS Config rule details for the associated AWS Config rule\. See [CIS AWS Foundations Benchmark controls](securityhub-cis-controls.md), [PCI DSS controls](securityhub-pci-controls.md), and [AWS Config resources required for AWS Foundational Security Best Practices controls](standards-fsbp-config-resources.md)\. Custom rules are not linked from the control description\.

For findings generated from those controls, the finding details include a link to the associated AWS Config rule\. Note that to navigate to the AWS Config rule from finding details, you must also have an IAM permission in the selected account to navigate to AWS Config\.

The finding details on the **Findings** page, **Insights** page, and **Integrations** page include a **Rules** link to the AWS Config rule details\. See [Viewing finding details \(console\)](finding-view-details.md)\.

On the control details page, the **Investigate** column of the finding list contains a link to the AWS Config rule details\. See [Viewing the AWS Config rule for a finding resource](control-finding-resource-details.md#control-finding-view-config-rule)\.