# Getting started with Security Hub<a name="securityhub-get-started"></a>

You can use Security Hub in the following ways:

**Security Hub console**  
Sign in to the AWS Management Console and open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

**Security Hub API**  
To access Security Hub programmatically, use the Security Hub API, which allows you to issue HTTPS requests directly to the service\. For more information, see the [AWS Security Hub API Reference](https://docs.aws.amazon.com/securityhub/1.0/APIReference/)\.

When you enable Security Hub, it begins to consume, aggregate, organize, and prioritize findings from AWS services that you have enabled, such as [Amazon GuardDuty](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html), [Amazon Inspector](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_introduction.html), and [Amazon Macie](https://docs.aws.amazon.com/macie/latest/user/what-is-macie.html)\. You can also enable integrations with AWS partner security products\. Those partner products can then also send findings to Security Hub\. See [Product integrations in AWS Security Hub](securityhub-findings-providers.md)\.

Security Hub also generates its own findings by running continuous, automated security checks based on AWS best practices and supported industry standards\. See [Security standards and controls in AWS Security Hub](securityhub-standards.md)\.

Security Hub then correlates and consolidates findings across providers to help you to prioritize the most significant findings\. See [Viewing findings in AWS Security Hub](securityhub-findings-viewing.md) and [Taking action on findings in AWS Security Hub](securityhub-findings-taking-action.md)\.

You can also create *insights* in Security Hub\. An insight is a collection of findings that are grouped together when you apply a **Group by** filter\. Insights help you identify common security issues that may require remediation action\. Security Hub includes several managed insights, or you can create your own custom insights\. See [Insights in AWS Security Hub](securityhub-insights.md)\.

**Important**  
Security Hub only detects and consolidates findings that are generated after you enable Security Hub\. It does not retroactively detect and consolidate security findings that were generated before you enabled Security Hub\.  
Security Hub only receives and processes findings from the Region where you enabled Security Hub in your account\.  
For full compliance with CIS AWS Foundations Benchmark security checks, you must enable Security Hub in all AWS Regions\.