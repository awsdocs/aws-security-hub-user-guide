# How AWS Security Hub runs and uses security checks<a name="securityhub-controls-finding-generation"></a>

For each control that you enable, AWS Security Hub runs security checks\. A security check determines whether your AWS resources are in compliance with the rules that the control includes\.

Some checks run on a periodic schedule\. Other checks only run when there is a change to the resource state\. For more information, see [Schedule for running security checks](securityhub-standards-schedule.md)\.

Many security checks use AWS Config managed or custom rules to establish the compliance requirements\. To run these checks, you must set up AWS Config\. For more information, see [How Security Hub uses AWS Config rules to run security checks](securityhub-standards-awsconfigrules.md)\. Others use custom Lambda functions, which are managed by Security Hub and are not visible to customers\.

As Security Hub runs security checks, it generates a finding when a control fails or changes status\. If you've turned on consolidated control findings, Security Hub generates a single finding even if a control is associated with more than one standard\. For more information, see [Consolidated control findings](controls-findings-create-update.md#consolidated-control-findings)\.

Security Hub uses the findings to assess each control's compliance status\. Security Hub also calculates a security score across all enabled controls and for specific standards\. For more information, see [Determining the overall status of a control from its findings](controls-overall-status.md) and [Determining the security score for a security standard](standards-security-score.md)\.

**Topics**
+ [How Security Hub uses AWS Config rules to run security checks](securityhub-standards-awsconfigrules.md)
+ [AWS Config resources required to generate control findings](controls-config-resources.md)
+ [Schedule for running security checks](securityhub-standards-schedule.md)
+ [Generating and updating control findings](controls-findings-create-update.md)
+ [Determining the overall status of a control from its findings](controls-overall-status.md)
+ [Determining the security score for a security standard](standards-security-score.md)