# How AWS Security Hub generates findings from security checks<a name="securityhub-controls-finding-generation"></a>

For each enabled control, AWS Security Hub runs security checks\. A security check determines whether your resources are in compliance with the control requirements\.

Some checks run on a regular schedule\. Other checks only run when there is a change to the resource state\. See [Schedule for running security checks](securityhub-standards-schedule.md)\.

Many security checks use AWS Config managed rules to establish the compliance requirements\. To run these checks, you must have AWS Config enabled\. See [AWS Config requirements for running security checks](securityhub-standards-awsconfigrules.md)\. Others use custom Lambda functions\.

For each check, Security Hub creates or updates a finding\. Security Hub uses the findings to assess your security posture for each control and across an entire standard\. See [Results of security checks](securityhub-standards-results.md)\.

**Topics**
+ [AWS Config requirements for running security checks](securityhub-standards-awsconfigrules.md)
+ [Schedule for running security checks](securityhub-standards-schedule.md)
+ [Results of security checks](securityhub-standards-results.md)