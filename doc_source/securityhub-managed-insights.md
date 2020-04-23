# Managed insights<a name="securityhub-managed-insights"></a>

AWS Security Hub provides several managed insights\.

You cannot edit or delete Security Hub managed insights\. You can [view and take action on the insight results and findings](securityhub-insights-view-take-action.md)\. You can also [use a managed insight as the basis for a new custom insight](securityhub-custom-insights.md#securityhub-custom-insight-frrom-managed)\.

As with all insights, a managed insight only returns results if you have enabled product integrations or security standards that can produce matching findings\.

In the current release, Security Hub offers the following managed insights:


|  Insight name  |  Grouped by  |  Finding filters  | 
| --- | --- | --- | 
|  1\. AWS resources with the most findings  |  Resource identifier  |  Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  2\. S3 buckets with public write or read permissions  |  Resource identifier  |  Type starts with `Effects/Data Exposure` Resource type is `AwsS3Bucket` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  3\. AMIs that are generating the most findings  |  EC2 instance image ID  |  Resource type is `AwsEc2Instance` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  4\. EC2 instances involved in known Tactics, Techniques, and Procedures \(TTPs\)  |  Resource ID  |  Type starts with `TTPs` Resource type is `AwsEc2Instance` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  5\. AWS users with the most suspicious activity  |  IAM access key user name  |  Resource type is `AwsIamAccessKey` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  6\. AWS resources instances that don't meet security standards / best practices  |  Resource ID  |  Type is `Software and Configuration Checks/Industry and Regulatory Standards/AWS Security Best Practices` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  7\. AWS resources associated with potential data exfiltration  |  Resource ID  |  Type starts with Effects/Data Exfiltration/ Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  8\. AWS resources associated with unauthorized resource consumption  |  Resource ID  |  Type starts with `Effects/Resource Consumption` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  9\. S3 buckets that don't meet security standards / best practice  |  Resource ID  |  Resource type is `AwsS3Bucket` Type is `Software and Configuration Checks/Industry and Regulatory Standards/AWS Security Best Practices` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  10\. S3 buckets with sensitive data  |  Resource ID  |  Resource type is `AwsS3Bucket` Type starts with `Sensitive Data Identifications/` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  11\. Credentials that may have leaked  |  Resource ID  |  Type starts with `Sensitive Data Identifications/Passwords/` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  12\. EC2 instances that have missing security patches for important vulnerabilities  |  Resource ID  |  Type starts with `Software and Configuration Checks/Vulnerabilities/CVE` Resource type is `AwsEc2Instance` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  13\. EC2 instances with general unusual behavior  |  Resource ID  |  Type starts with `Unusual Behaviors` Resource type is `AwsEc2Instance` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`\.  | 
|  14\. EC2 instances that have ports accessible from the Internet  |  Resource ID  |  Type starts with `Software and Configuration Checks/AWS Security Best Practices/Network Reachability` Resource type is `AwsEc2Instance` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  15\. EC2 instances that don't meet security standards / best practices  |  Resource ID  |  Type starts with one of the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-managed-insights.html) Resource type is `AwsEc2Instance` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  16\. EC2 instances that are open to the Internet  |  Resource ID  |  Type starts with `Software and Configuration Checks/AWS Security Best Practices/Network Reachability` Resource type is `AwsEc2Instance` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  17\. EC2 instances associated with adversary reconnaissance  |  Resource ID  |  Type starts with TTPs/Discovery/Recon Resource type is `AwsEc2Instance` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  18\. AWS resources that are associated with malware  |  Resource ID  |  Type starts with one of the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-managed-insights.html) Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  19\. AWS resources associated with cryptocurrency issues  |  Resource ID  |  Type starts with one of the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-managed-insights.html) Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  20\. AWS resources with unauthorized access attempts  |  Resource ID  |  Type starts with one of the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-managed-insights.html) Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  21\. Threat Intel indicators with the most hits in the last week  |   |  Created within the last 7 days  | 
|  22\. Top accounts by counts of findings  |  AWS account ID  |  Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  23\. Top products by counts of findings  |  Product ARN  |  Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  24\. Severity by counts of findings  |  Severity label  |  Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  25\. Top S3 buckets by counts of findings  |  Resource ID  |  Resource type is `AwsS3Bucket` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  26\. Top EC2 instances by counts of findings  |  Resource ID  |  Resource type is `AwsEc2Instance` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  27\. Top AMIs by counts of findings  |  EC2 instance image ID  |  Resource type is `AwsEc2Instance` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  28\. Top IAM users by counts of findings  |  IAM access key user name  |  Resource type is `AwsIamAccessKey` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  29\. Top resources by counts of failed CIS checks  |  Resource ID  |  Generator ID starts with `arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0/rule` Updated in the last day Compliance status is `FAILED` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  30\. Top integrations by counts of findings  |  Product ARN  |  Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 
|  31\. Resources with the most failed security checks  |  Resource ID  |  Updated in the last day Compliance status is `FAILED` Record state is `ACTIVE` Workflow status is `NEW` or `NOTIFIED`  | 