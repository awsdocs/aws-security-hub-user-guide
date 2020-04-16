# What is AWS Security Hub?<a name="what-is-securityhub"></a>

AWS Security Hub provides you with a comprehensive view of your security state in AWS and helps you check your environment against security industry standards and best practices\. Security Hub collects security data from across AWS accounts, services, and supported third\-party partner products and helps you analyze your security trends and identify the highest priority security issues\.

**Topics**
+ [Benefits of Security Hub](#securityhub-benefits)
+ [Getting started with Security Hub](#securityhub-get-started)
+ [Security Hub free trial](#securityhub-free-trial)
+ [Using Security Hub](#securityhub-accessing)

## Benefits of Security Hub<a name="securityhub-benefits"></a>
+ Security Hub reduces the effort to collect and prioritize security findings across accounts from integrated AWS services and AWS partner products\. Security Hub processes finding data using a standard findings format, which eliminates the need to manage findings data from multiple formats\. Security Hub then correlates findings across providers to prioritize the most important ones\.
+ Security Hub automatically runs continuous, account\-level configuration and security checks based on industry standards and best practices, such as the [Center for Internet Security \(CIS\) AWS Foundations Benchmarks](https://www.cisecurity.org/benchmark/amazon_web_services/)\. The result of these checks is provided as a readiness score, and specific accounts and resources that require attention are identified\.
+ Security Hub consolidates your security findings across accounts and provider products and displays results on the Security Hub console pages\. This allows you to view your overall current security status to spot trends, identify potential issues, and take the necessary remediation steps\.
+ Security Hub supports integration with Amazon CloudWatch Events, which lets you automate remediation of specific findings by defining custom actions to take when a finding is received\. You can configure custom actions to, for example, send findings to a ticketing system or to an automated remediation system\.

## Getting started with Security Hub<a name="securityhub-get-started"></a>

When you enable Security Hub, it begins to consume, aggregate, organize, and prioritize findings from AWS services, such as [Amazon GuardDuty](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html), [Amazon Inspector](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_introduction.html), and [Amazon Macie](https://docs.aws.amazon.com/macie/latest/userguide/what-is-macie.html), and from AWS partner security products\. Security Hub also generates its own findings by running continuous, automated security checks based on AWS best practices and supported industry standards\. Security Hub then correlates and consolidates findings across providers to help you to prioritize the most significant findings\.

You can also create *insights* in Security Hub\. An insight is a collection of findings that are grouped together when you apply a **Group by** filter\. Insights help you identify common security issues that may require remediation action\. Security Hub includes several managed insights, or you can create your own custom insights\.

**Important**  
Security Hub detects and consolidates only those findings from the supported AWS and partner products that are generated after you enable Security Hub\. It does not retroactively detect and consolidate security findings that were generated before you enabled it\.  
Security Hub receives and processes only those findings from the same Region where you enabled Security Hub in your account\.  
For full compliance with CIS AWS Foundations Benchmark security checks, you must enable Security Hub in all AWS Regions\.

## Security Hub free trial<a name="securityhub-free-trial"></a>

When you enable Security Hub for the first time, your AWS account is automatically enrolled in a 30\-day Security Hub free trial\. When you use Security Hub during the free trial, you are charged for usage of other services that Security Hub interacts with, such as AWS Config items\. You are not charged for AWS Config rules that are enabled by Security Hub security standards\.

You can view your usage details during your free trial in the **Usage** tab of the **Settings** page of the Security Hub console\. The usage details include the time remaining for the free trial and an estimated monthly cost for using Security Hub\. The estimated monthly cost is based on your Security Hub usage during the free trial for findings and security checks projected over a 30\-day period\.

If you are using Security Hub from the master account, the estimated monthly cost includes the costs associated with all member accounts\. If you are using Security Hub from a member account, the estimated monthly cost is only for the member account\. The estimated monthly charge is for only the current Region, not for all Regions in which Security Hub is enabled\.

You are not charged for using Security Hub until your free trial ends\. To learn more, see [Security Hub Pricing](https://aws.amazon.com/security-hub/pricing/)\.

## Using Security Hub<a name="securityhub-accessing"></a>

You can use Security Hub in the following ways:

**Security Hub console**  
Sign in to the AWS Management Console and open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

**Security Hub API**  
You can access Security Hub programmatically by using the Security Hub API, which allows you to issue HTTPS requests directly to the service\. For more information, see the [AWS Security Hub API Reference](https://docs.aws.amazon.com/securityhub/1.0/APIReference/)\.