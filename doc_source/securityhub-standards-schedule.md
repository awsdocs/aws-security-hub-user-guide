# Schedule for running security checks<a name="securityhub-standards-schedule"></a>

After you enable a security standard, AWS Security Hub begins to run all checks within two hours\. Most checks begin to run within 25 minutes\. Until a control completes its first run of checks, its status is **No data**\.

When you enable a new standard, Security Hub may take up to 18 hours to generate findings for controls that use the same underlying AWS Config service\-linked rule as enabled controls from other enabled standards\. For example, if you enable [Lambda\.1](lambda-controls.md#lambda-1) in the AWS Foundational Security Best Practices \(FSBP\) standard, Security Hub will create the service\-linked rule and typically generate findings in minutes\. After this, if you enable Lambda\.1 in the Payment Card Industry Data Security Standard \(PCI DSS\), Security Hub may take up to 18 hours to generate findings for this control because it uses the same service\-linked rule as Lambda\.1\.

After the initial check, the schedule for each control can be either periodic or change triggered\.
+ Periodic checks run automatically within 12 or 24 hours after the most recent run\. Security Hub determines the periodicity, and you can't change it\. Periodic controls capture an evaluation at the moment of execution\. 
+ Change\-triggered checks run when the associated resource changes state\. Even if the resource does not change state, the updated at time for change\-triggered checks is refreshed every 18 hours\. This helps to indicate that the control is still enabled\.

In general, Security Hub uses change\-triggered rules whenever possible\. For a resource to use a change\-triggered rule, it must support AWS Config configuration items\.

For a control that is based on a managed AWS Config rule, the control description includes a link to the rule description in the *AWS Config Developer Guide*\. That description includes whether the rule is change triggered or periodic\.

Checks that use Security Hub custom Lambda functions are always periodic\.