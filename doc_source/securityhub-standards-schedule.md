# Schedule for running security checks<a name="securityhub-standards-schedule"></a>

After you enable a security standard, AWS Security Hub begins to run all checks within two hours\. Most checks begin to run within 25 minutes\.

After the initial check, the schedule for each control can be either periodic or change triggered\.
+ Periodic checks run automatically within 12 hours after the most recent run\. You cannot change the periodicity\.
+ Change\-triggered checks run when the associated resource changes state\. Even if the resource does not change state, the updated at time for change\-triggered checks is refreshed every 18 hours\. This helps to indicate that the control is still enabled\.

In general, Security Hub uses change\-triggered rules whenever possible\. For a resource to use a change\-triggered rule, it must support AWS Config configuration items\.

For a control that is based on a managed AWS Config rule, the control description includes a link to the rule description in the *AWS Config Developer Guide*\. That description includes whether the rule is change triggered or periodic\.

Checks that use Security Hub custom Lambda functions are always periodic\.