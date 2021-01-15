# Managed insights<a name="securityhub-managed-insights"></a>

AWS Security Hub provides several managed insights\.

You cannot edit or delete Security Hub managed insights\. You can [view and take action on the insight results and findings](securityhub-insights-view-take-action.md)\. You can also [use a managed insight as the basis for a new custom insight](securityhub-custom-insights.md#securityhub-custom-insight-frrom-managed)\.

As with all insights, a managed insight only returns results if you have enabled product integrations or security standards that can produce matching findings\.

In the current release, Security Hub offers the following managed insights:

**1\. AWS resources with the most findings**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/1`  
**Grouped by:** Resource identifier  
**Finding filters:**  
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**2\. S3 buckets with public write or read permissions**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/10`  
**Grouped by:** Resource identifier  
**Finding filters:**  
+ Type starts with `Effects/Data Exposure`
+ Resource type is `AwsS3Bucket`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**3\. AMIs that are generating the most findings**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/3`  
**Grouped by:** EC2 instance image ID  
**Finding filters:**  
+ Resource type is `AwsEc2Instance`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**4\. EC2 instances involved in known Tactics, Techniques, and Procedures \(TTPs\)**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/14`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with `TTPs`
+ Resource type is `AwsEc2Instance`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**5\. AWS principals with suspicious access key activity**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/9`  
**Grouped by:** IAM access key principal name  
**Finding filters:**  
+ Resource type is `AwsIamAccessKey`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**6\. AWS resources instances that don't meet security standards / best practices**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/6`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type is `Software and Configuration Checks/Industry and Regulatory Standards/AWS Security Best Practices`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**7\. AWS resources associated with potential data exfiltration**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/7`  
**Grouped by:**: Resource ID  
**Finding filters:**  
+ Type starts with Effects/Data Exfiltration/
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**8\. AWS resources associated with unauthorized resource consumption**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/8`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with `Effects/Resource Consumption`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**9\. S3 buckets that don't meet security standards / best practice**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/11`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Resource type is `AwsS3Bucket`
+ Type is `Software and Configuration Checks/Industry and Regulatory Standards/AWS Security Best Practices`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**10\. S3 buckets with sensitive data**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/12`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Resource type is `AwsS3Bucket`
+ Type starts with `Sensitive Data Identifications/`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**11\. Credentials that may have leaked**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/13`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with `Sensitive Data Identifications/Passwords/`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**12\. EC2 instances that have missing security patches for important vulnerabilities**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/16`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with `Software and Configuration Checks/Vulnerabilities/CVE`
+ Resource type is `AwsEc2Instance`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**13\. EC2 instances with general unusual behavior**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/17`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with `Unusual Behaviors`
+ Resource type is `AwsEc2Instance`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`\.

**14\. EC2 instances that have ports accessible from the Internet**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/18`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with `Software and Configuration Checks/AWS Security Best Practices/Network Reachability`
+ Resource type is `AwsEc2Instance`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**15\. EC2 instances that don't meet security standards / best practices**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/19`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with one of the following:
  + `Software and Configuration Checks/Industry and Regulatory Standards/`
  + `Software and Configuration Checks/AWS Security Best Practices`
+ Resource type is `AwsEc2Instance`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**16\. EC2 instances that are open to the Internet**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/21`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with `Software and Configuration Checks/AWS Security Best Practices/Network Reachability`
+ Resource type is `AwsEc2Instance`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**17\. EC2 instances associated with adversary reconnaissance**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/22`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with TTPs/Discovery/Recon
+ Resource type is `AwsEc2Instance`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**18\. AWS resources that are associated with malware**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/23`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with one of the following:
  + `Effects/Data Exfiltration/Trojan`
  + `TTPs/Initial Access/Trojan`
  + `TTPs/Command and Control/Backdoor`
  + `TTPs/Command and Control/Trojan`
  + `Software and Configuration Checks/Backdoor`
  + `Unusual Behaviors/VM/Backdoor`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**19\. AWS resources associated with cryptocurrency issues**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/24`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with one of the following:
  + `Effects/Resource Consumption/Cryptocurrency`
  + `TTPs/Command and Control/CryptoCurrency`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**20\. AWS resources with unauthorized access attempts**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/25`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Type starts with one of the following:
  + `TTPs/Command and Control/UnauthorizedAccess`
  + `TTPs/Initial Access/UnauthorizedAccess`
  + `Effects/Data Exfiltration/UnauthorizedAccess`
  + `Unusual Behaviors/User/UnauthorizedAccess`
  + `Effects/Resource Consumption/UnauthorizedAccess`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**21\. Threat Intel indicators with the most hits in the last week**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/26`  
**Finding filters:**  
+ Created within the last 7 days

**22\. Top accounts by counts of findings**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/27`  
**Grouped by:** AWS account ID  
**Finding filters:**  
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**23\. Top products by counts of findings**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/28`  
**Grouped by:** Product ARN  
**Finding filters:**  
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**24\. Severity by counts of findings**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/29`  
**Grouped by:** Severity label  
**Finding filters:**  
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**25\. Top S3 buckets by counts of findings**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/30`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Resource type is `AwsS3Bucket`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**26\. Top EC2 instances by counts of findings**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/31`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Resource type is `AwsEc2Instance`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**27\. Top AMIs by counts of findings**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/32`  
**Grouped by:** EC2 instance image ID  
**Finding filters:**  
+ Resource type is `AwsEc2Instance`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**28\. Top IAM users by counts of findings**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/33`  
**Grouped by:** IAM access key user name  
**Finding filters:**  
+ Resource type is `AwsIamAccessKey`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**29\. Top resources by counts of failed CIS checks**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/34`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Generator ID starts with `arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0/rule`
+ Updated in the last day
+ Compliance status is `FAILED`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**30\. Top integrations by counts of findings**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/35`  
**Grouped by:** Product ARN  
**Finding filters:**  
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**31\. Resources with the most failed security checks**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/36`  
**Grouped by:** Resource ID  
**Finding filters:**  
+ Updated in the last day
+ Compliance status is `FAILED`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`

**32\. IAM users with suspicious activity**  
**ARN:** `arn:aws:securityhub:::insight/securityhub/default/37`  
**Grouped by:** IAM user name  
**Finding filters:**  
+ Resource type is `AwsIamUser`
+ Record state is `ACTIVE`
+ Workflow status is `NEW` or `NOTIFIED`