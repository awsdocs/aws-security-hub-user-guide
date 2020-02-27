# Available AWS Service Integrations<a name="securityhub-internal-providers"></a>

Security Hub supports integrations with several AWS services\.

For these services, the integration allows the service to send findings to Security Hub\.
+ [AWS Firewall Manager](#integration-aws-firewall-manager)
+ [IAM Access Analyzer](#integration-iam-access-analyzer)
+ [Amazon GuardDuty](#integration-amazon-guardduty)
+ [Amazon Inspector](#integration-amazon-inspector)
+ [Amazon Macie](#integration-amazon-macie)

Security Hub also supports an integration with [Amazon Detective](#integration-amazon-detective)\. That integration allows you to pivot from Security Hub to Detective to investigate a GuardDuty finding\.

Here are the details about each AWS service integration\.

**AWS Firewall Manager**  <a name="integration-aws-firewall-manager"></a>
Firewall Manager sends findings to Security Hub when a WAF policy for resources or a Web ACL rule is not in compliance\. Firewall Manager also sends findings when Shield Advanced is not protecting resources, or when an attack is identified\.  
If you are already using Firewall Manager, Security Hub automatically enables this integration\. You do not need to take any additional action to begin to receive findings from Firewall Manager\.  
To learn more about the integration, view the **Integrations** page in the Security Hub console\.  
To learn more about Firewall Manager, see the [https://docs.aws.amazon.com/waf/latest/developerguide/](https://docs.aws.amazon.com/waf/latest/developerguide/)\.

**IAM Access Analyzer**  <a name="integration-iam-access-analyzer"></a>
With IAM Access Analyzer, all findings are sent to Security Hub\.  
IAM Access Analyzer uses logic\-based reasoning to analyze resource\-based policies applied to supported resources in your account\. IAM Access Analyzer generates a finding when it detects a policy statement that allows an external principal access to a resource in your account\.  
To learn more, see [What Is IAM Access Analyzer?](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html) in the *IAM User Guide*\.

**Amazon Detective**  <a name="integration-amazon-detective"></a>
Detective automatically collects log data from your AWS resources and uses machine learning, statistical analysis, and graph theory to help you visualize and conduct faster and more efficient security investigations\.  
The Security Hub integration with Detective allows you to pivot from Amazon GuardDuty findings in Security Hub into Detective\. You can then use the Detective tools and visualizations to investigate them\. The integration does not require any additional configuration in Security Hub or Detective\.  
For the GuardDuty finding types that Detective supports, the finding details include an **Investigate in Detective** subsection\. That subsection contains the link to Detective\. See [Pivoting to a Finding Profile from Amazon GuardDuty or AWS Security Hub](https://docs.aws.amazon.com/detective/latest/userguide/profile-pivot-from-service.html) in the *Amazon Detective User Guide*\.  
For the list of finding types that Detective supports, see [Supported Finding Types](https://docs.aws.amazon.com/detective/latest/userguide/supported-finding-types.html)\.  
If a link does not work, then for troubleshooting advice, see [Troubleshooting the Pivot](https://docs.aws.amazon.com/detective/latest/userguide/profile-pivot-from-service.html#profile-pivot-troubleshooting)\.

**Amazon GuardDuty**  <a name="integration-amazon-guardduty"></a>
With GuardDuty, Security Hub imports GuardDuty findings of all of the supported finding types\.  
New findings from GuardDuty are sent to Security Hub within 5 minutes\. Updates to findings are sent based on the **Updated findings** setting for CloudWatch Events in GuardDuty settings\.  
When you generate GuardDuty sample findings using the GuardDuty **Setting** page, Security Hub ingests the sample findings and omits the prefix '\[Sample\]' in the finding type\. For example, the sample finding type in GuardDuty "\[SAMPLE\] Recon:IAMUser/ResourcePermissions" is displayed as "Recon:IAMUser/ResourcePermissions” in Security Hub\.  
For more information about GuardDuty findings, see [Amazon GuardDuty Findings](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings.html) in the *Amazon GuardDuty User Guide*\.

**Amazon Inspector**  <a name="integration-amazon-inspector"></a>
With Amazon Inspector, Security Hub imports Amazon Inspector findings that are generated through assessment runs based on all supported rules packages\.  
For more information about Amazon Inspector rules packages and rules, see [Amazon Inspector Rules Packages and Rules](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_rule-packages.html) in the *Amazon Inspector User Guide*\.

**Amazon Macie**  <a name="integration-amazon-macie"></a>
With Macie, a finding \(currently known as an alert\) can be one of the following indices: **CloudTrail data**, **S3 bucket properties**, and **S3 objects**\.  
For more information, see [Locating and Analyzing Macie Alerts](https://docs.aws.amazon.com/macie/latest/userguide/macie-alerts.html#macie-alert-working-locate) in the *Amazon Macie User Guide*\.  
Security Hub imports Macie basic and custom alerts \(findings\) only from the **S3 bucket properties** and **S3 objects** indices\. Macie does not send data classifications\.  
Security Hub does *not* import Macie findings from the **CloudTrail data** index\.