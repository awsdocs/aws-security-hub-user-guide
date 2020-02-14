# Schedule for Running Security Standards Checks<a name="securityhub-standards-schedule"></a>

After you enable a security standard, AWS Security Hub begins to run the checks within 2 hours\.

After the initial check, the schedule for each control may be either periodic or change\-triggered\.
+ Periodic checks run automatically within 12 hours after the most recent run\. You cannot change the periodicity\.
+ Change\-triggered checks run when the associated resource changes state\.

In general, Security Hub uses change\-triggered rules whenever possible\. For a resource to use a change\-triggered rule, there must be AWS Config Configuration Item support\.

For a control that is based on a managed AWS Config rule, the control description includes a link to the rule description in the AWS Config Developer Guide\. That description includes whether the rule is change\-triggered or periodic\.

Checks that use Security Hub custom Lambda functions are always periodic\.