# Insights in AWS Security Hub<a name="securityhub-insights"></a>

An AWS Security Hub insight is a collection of related findings\. It identifies a security area that requires attention and intervention\. For example, an insight might point out EC2 instances that are the subject of findings that detect poor security practices\. An insight brings together findings from across finding providers\.

Each insight is defined by a group by statement and optional filters\. The group by statement indicates how to group the matching findings, and identifies the type of item that the insight applies to\. For example, if an insight is grouped by resource identifier, then the insight produces a list of resource identifiers\. The optional filters narrow down the matching findings for the insight\. For example, you might want to only see findings from specific providers or findings associated with specific types of resources\.

Security Hub offers several built\-in managed \(default\) insights\. You cannot modify or delete managed insights\.

To track security issues that are unique to your AWS environment and usage, you can create custom insights\.

An insight only returns results if you have enabled product integrations or security standards that produce matching findings\. For example, the managed insight **29\. Top resources by counts of failed CIS checks** only returns results if you enable the CIS AWS Foundations security standard\.

**Topics**
+ [Viewing and taking action on insight results and findings](securityhub-insights-view-take-action.md)
+ [Managed insights](securityhub-managed-insights.md)
+ [Managing custom insights](securityhub-custom-insights.md)