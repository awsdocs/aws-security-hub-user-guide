# AWS Config Requirements for Running Security Standards Checks<a name="securityhub-standards-awsconfigrules"></a>

To run security standards checks on your environment's resources, AWS Security Hub either uses steps specified by the standard, or uses specific AWS Config managed rules\. These AWS Config managed rules are referred to as service\-linked rules, because they are enabled and controlled by the Security Hub service\.

## Enabling AWS Config for Security Hub<a name="securityhub-standards-awsconfig-enabling"></a>

For the standards to be functional in Security Hub, before you enable a security standard, you must also enable AWS Config in your Security Hub accounts\.

Security Hub does not manage AWS Config for you\. If you already have AWS Config enabled, you can continue configuring its settings through the AWS Config console or APIs\.

If you don't have AWS Config enabled, you can enable it manually, or you can use the AWS CloudFormation "Enable AWS Config" template in AWS CloudFormation StackSets Sample Templates\. If you use the Security Hub [multi\-account, multi\-region enablement script](https://github.com/awslabs/aws-securityhub-multiaccount-scripts), it also enables AWS Config for you\.

**Important**  
If you enable AWS Config in your Security Hub master account, this does not automatically enable AWS Config in the Security Hub member accounts for this master account\.  
If you want Security Hub to generate findings against security standards for the resources in a Security Hub member account, you must enable AWS Config in that member account\.

**Important**  
When you turn on the AWS Config recorder as part of enabling AWS Config, choose to record all resources supported in a given Region, including global resources\.  
For more information, see [Getting Started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.

## How Security Hub Generates AWS Config Service\-Linked Rules for Security Standards<a name="securityhub-standards-generate-awsconfigrules"></a>

After you enable a security standard, Security Hub automatically creates the AWS Config service\-linked rules that it needs to run checks against the enabled controls\.

For every control that uses an AWS Config service\-linked rule or rules, Security Hub creates instances of the required rules in your AWS environment\. These service\-linked rules are specific to Security Hub\. It creates these service\-linked rules even if other instances of the same rules already exist\.

**Note**  
For AWS Config managed rules, the limit is 150 rules per account per Region\. However, when you enable a security standard in Security Hub, the service\-linked AWS Config rules that are automatically created do not count towards that limit\. You can enable a security standard even if you already have 150 AWS Config managed rules in your account\.  
For service\-linked rules such as the ones that Security Hub adds for security standards, the limit is 150 rules per account per Region\. This is in addition to the 150\-rule limit on AWS Config managed rules\.

For information about the specific AWS Config managed rules that Security Hub uses for each CIS AWS Foundations control, see [CIS AWS Foundations Controls](securityhub-cis-controls.md)\. For the list of required AWS Config resources for CIS AWS Foundations controls, see [AWS Config Resources Required for CIS Controls](securityhub-standards-cis-config-resources.md)\.

For information about the specific AWS Config managed rules that Security Hub uses for each Payment Card Industry Data Security Standard \(PCI DSS\) control, see [PCI DSS Controls](securityhub-pci-controls.md)\. For the list of required AWS Config resources for PCI DSS controls, see [AWS Config Resources Required for PCI DSS Controls](securityhub-standards-pci-config-resources.md)\.

When you view the details for a security standard finding that is based on an AWS Config rule, to navigate to the associated AWS Config rule, choose **Compliance rules**\. Findings from controls that are not based on AWS Config rules do not display the link\. To navigate to the AWS Config rule, you must also have an IAM permission in the selected account to navigate to AWS Config\.