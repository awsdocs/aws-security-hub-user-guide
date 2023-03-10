# How Security Hub uses AWS Config rules to run security checks<a name="securityhub-standards-awsconfigrules"></a>

To run security checks on your environment's resources, AWS Security Hub either uses steps specified by the standard, or uses specific AWS Config rules\. Some rules are managed rules, which are managed by AWS Config\. Other rules are custom rules that Security Hub develops\.

AWS Config rules that Security Hub uses for controls are referred to as service\-linked rules, because they are enabled and controlled by the Security Hub service\.

To enable checks against these AWS Config rules, you must first enable AWS Config for your account and enable resource recording for required resources\. For information about how to enable AWS Config, see [Enabling and configuring AWS Config](securityhub-prereq-config.md)\. For information about required resource recording, see [AWS Config resources required to generate control findings](controls-config-resources.md)

## How Security Hub generates the service\-linked rules<a name="securityhub-standards-generate-awsconfigrules"></a>

For every control that uses an AWS Config service\-linked rule, Security Hub creates instances of the required rules in your AWS environment\.

These service\-linked rules are specific to Security Hub\. It creates these service\-linked rules even if other instances of the same rules already exist\. The service\-linked rule adds `securityhub`before the original rule name, and a unique identifier after the rule name\. For example, for the original AWS Config managed rule `vpc-flow-logs-enabled`, the service\-linked rule name would be something like `securityhub-vpc-flow-logs-enabled-12345`\.

There are limits on the number of AWS Config rules that can be used to evaluate controls\. Custom AWS Config rules that Security Hub creates don't count towards that limit\. You can enable a security standard even if you've already reached the AWS Config limit for managed rules in your account\. To learn more about AWS Config rule limits, see [Service Limits](https://docs.aws.amazon.com/config/latest/developerguide/configlimits.html) in the *AWS Config Developer Guide*\.

## Viewing details about the AWS Config rules for controls<a name="securityhub-standards-view-config-rule-details"></a>

For controls that use AWS Config managed rules, the control description includes a link to the AWS Config rule details\. Custom rules aren't linked from the control description\. For control descriptions, see [Security Hub controls reference](securityhub-controls-reference.md)\. Select a control from the list to see its description\.

For findings generated from those controls, the finding details include a link to the associated AWS Config rule\. Note that to navigate to the AWS Config rule from finding details, you must also have an IAM permission in the selected account to navigate to AWS Config\.

The finding details on the **Findings** page, **Insights** page, and **Integrations** page include a **Rules** link to the AWS Config rule details\. See [Viewing finding details](finding-view-details.md)\.

On the control details page, the **Investigate** column of the finding list contains a link to the AWS Config rule details\. See [Viewing the AWS Config rule for a finding resource](control-finding-resource-details.md#control-finding-view-config-rule)\.