# AWS Product Integrations<a name="securityhub-internal-providers"></a>

Security Hub supports integrations with these AWS services:
+ [AWS Firewall Manager](https://docs.aws.amazon.com/waf/latest/developerguide/what-is-aws-waf.html)
+ [IAM Access Analyzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html)
+ [Amazon Detective](https://docs.aws.amazon.com/detective/latest/userguide/detective-investigation-about.html)
+ [Amazon GuardDuty](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)
+ [Amazon Inspector](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_introduction.html)
+ [Amazon Macie](https://docs.aws.amazon.com/macie/latest/userguide/what-is-macie.html)

To integrate these services with Security Hub, you must enable them in your account on the console for each service\. A resource\-level permission that allows Security Hub to get findings from these services is automatically created and applied\. You do not need to configure any settings to start receiving findings from them\.

After you enable them, Security Hub starts collecting new findings in that account from these services\.

**Important**  
From the integrated services, Security Hub only receives new findings that were generated after you enabled Security Hub\. It does not receive findings that were generated before you enabled Security Hub\.

If you did not enable the supported AWS product, or you did not enable the integration in Security Hub, then no findings are sent to Security Hub\. To verify whether a product integration is enabled, check the **Integrations** page of the Security Hub console\.

AWS Firewall Manager  
Firewall Manager sends findings to Security Hub when a WAF policy for resources or a Web ACL rule is not in compliance\. Firewall Manager also sends findings when Shield Advanced is not protecting resources, or when an attack is identified\.  
If you are already using Firewall Manager, Security Hub automatically enables this integration\. You do not need to take any additional action to begin to receive findings from Firewall Manager\.  
To learn more about the integration, view the **Integrations** page in the Security Hub console\.  
To learn more about Firewall Manager, see the [AWS WAF Developer Guide](https://docs.aws.amazon.com/waf/latest/developerguide/)\.

AWS IAM Access Analyzer  
With IAM Access Analyzer, all findings are sent to Security Hub\.  
IAM Access Analyzer uses logic\-based reasoning to analyze resource\-based policies applied to supported resources in your account\. IAM Access Analyzer generates a finding when it detects a policy statement that allows an external principal access to a resource in your account\.  
To learn more, see [What is Access Analyzer?](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html)\.

Amazon Detective  
Detective automatically collects log data from your AWS resources and uses machine learning, statistical analysis, and graph theory to help you visualize and conduct faster and more efficient security investigations\.  
The initial Security Hub integration with Detective allows you to pivot from Amazon GuardDuty findings in Security Hub and into Detective to investigate them\.  
To learn more, see [Pivoting to a Finding Profile from Amazon GuardDuty or AWS Security Hub](https://docs.aws.amazon.com/detective/latest/userguide/profile-pivot-from-service.html)\.

Amazon GuardDuty  
With GuardDuty, Security Hub imports GuardDuty findings of all of the supported finding types\.  
New findings from GuardDuty are sent to Security Hub within 5 minutes\. Updates to findings are sent based on the **Updated findings** setting for CloudWatch Events in GuardDuty settings\.  
When you generate GuardDuty sample findings using the GuardDuty **Setting** page, Security Hub ingests the sample findings and omits the prefix '\[Sample\]' in the finding type\. For example, the sample finding type in GuardDuty "\[SAMPLE\] Recon:IAMUser/ResourcePermissions" is displayed as "Recon:IAMUser/ResourcePermissions” in Security Hub\.  
For more information about GuardDuty findings, see [Amazon GuardDuty Findings](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings.html)\.

Amazon Inspector  
With Amazon Inspector, Security Hub imports Amazon Inspector findings that are generated through assessment runs based on all supported rules packages\.  
For more information about Amazon Inspector rules packages and rules, see [Amazon Inspector Rules Packages and Rules](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_rule-packages.html)\.

Amazon Macie  
With Macie, a finding \(currently known as an alert\) can be one of the following indices: **CloudTrail data**, **S3 bucket properties**, and **S3 objects**\.  
For more information, see [Locating and Analyzing Macie Alerts](https://docs.aws.amazon.com/macie/latest/userguide/macie-alerts.html#macie-alert-working-locate)\.  
Security Hub imports Macie basic and custom alerts \(findings\) only from the **S3 bucket properties** and **S3 objects** indices\. Macie does not send data classifications\.  
Security Hub does *not* import Macie findings from the **CloudTrail data** index\.