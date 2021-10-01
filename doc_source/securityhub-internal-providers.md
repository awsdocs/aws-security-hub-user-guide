# Available AWS service integrations<a name="securityhub-internal-providers"></a>

Security Hub supports integrations with several AWS services\.

**Note**  
Some integrations are not available in Africa \(Cape Town\), Asia Pacific \(Hong Kong\), China \(Beijing\), China \(Ningxia\), Europe \(Milan\), AWS GovCloud \(US\-East\), or AWS GovCloud \(US\-West\)\.  
If an integration is not supported, it is not listed on the **Integrations** page\.  
See also [Integrations that are supported in China \(Beijing\) and China \(Ningxia\)](securityhub-regions.md#securityhub-regions-integration-support-china) and [Integrations that are supported in AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\)](securityhub-regions.md#securityhub-regions-integration-support-govcloud)\.

For these services, the integration allows the service to send findings to Security Hub:
+ [AWS Firewall Manager](#integration-aws-firewall-manager)
+ [Amazon GuardDuty](#integration-amazon-guardduty)
+ [IAM Access Analyzer](#integration-iam-access-analyzer)
+ [Amazon Inspector](#integration-amazon-inspector)
+ [Amazon Macie](#integration-amazon-macie)
+ [AWS Systems Manager Patch Manager](#patch-manager)

The following integrations allow Security Hub to send findings to those services:
+ [Audit Manager](#integration-aws-audit-manager)
+ [AWS Chatbot](#integration-chatbot)
+ [Systems Manager Explorer and OpsCenter](#integration-ssm-explorer-opscenter)

Explorer and OpsCenter also update findings in Security Hub\.

The [Detective integration](#integration-amazon-detective) allows you to pivot from Security Hub to Detective to investigate a GuardDuty finding\. 

Here are the details about each AWS service integration\.

**AWS Audit Manager**  <a name="integration-aws-audit-manager"></a>
Security Hub sends control findings to Audit Manager\. These findings help Audit Manager users to prepare for audits\.  
To learn more about Audit Manager, see the [https://docs.aws.amazon.com/audit-manager/latest/userguide/what-is.html](https://docs.aws.amazon.com/audit-manager/latest/userguide/what-is.html)\. [AWS Security Hub checks supported by AWS Audit Manager](https://docs.aws.amazon.com/audit-manager/latest/userguide/control-data-sources-ash.html) lists the controls for which Security Hub sends findings to Audit Manager\.

**AWS Chatbot**  <a name="integration-chatbot"></a>
AWS Chatbot is an interactive agent that helps you to monitor and interact with your AWS resources in your Slack channels and Amazon Chime chat rooms\.  
Security Hub sends findings to AWS Chatbot\.  
To learn more about the AWS Chatbot integration with Security Hub, see the [Security Hub integration overview](https://docs.aws.amazon.com/chatbot/latest/adminguide/related-services.html#security-hub) in the *AWS Chatbot Administrator Guide*\.

**Amazon Detective**  <a name="integration-amazon-detective"></a>
Detective automatically collects log data from your AWS resources and uses machine learning, statistical analysis, and graph theory to help you visualize and conduct faster and more efficient security investigations\.  
The Security Hub integration with Detective allows you to pivot from Amazon GuardDuty findings in Security Hub into Detective\. You can then use the Detective tools and visualizations to investigate them\. The integration does not require any additional configuration in Security Hub or Detective\.  
For GuardDuty finding types, the finding details include an **Investigate in Detective** subsection\. That subsection contains the link to Detective\. See [Pivoting to an entity profile or finding overview from Amazon GuardDuty or AWS Security Hub](https://docs.aws.amazon.com/detective/latest/userguide/profile-pivot-from-service.html) in the *Amazon Detective User Guide*\.  
If a link does not work, then for troubleshooting advice, see [Troubleshooting the pivot](https://docs.aws.amazon.com/detective/latest/userguide/profile-pivot-from-service.html#profile-pivot-troubleshooting)\.

**AWS Firewall Manager**  <a name="integration-aws-firewall-manager"></a>
Firewall Manager sends findings to Security Hub when a WAF policy for resources or a web ACL rule is not in compliance\. Firewall Manager also sends findings when AWS Shield Advanced is not protecting resources, or when an attack is identified\.  
If you are already using Firewall Manager, Security Hub automatically enables this integration\. You do not need to take any additional action to begin to receive findings from Firewall Manager\.  
To learn more about the integration, view the **Integrations** page in the Security Hub console\.  
To learn more about Firewall Manager, see the [https://docs.aws.amazon.com/waf/latest/developerguide/](https://docs.aws.amazon.com/waf/latest/developerguide/)\.

**Amazon GuardDuty**  <a name="integration-amazon-guardduty"></a>
GuardDuty sends findings to Security Hub for all of the supported finding types\.  
New findings from GuardDuty are sent to Security Hub within 5 minutes\. Updates to findings are sent based on the **Updated findings** setting for Amazon EventBridge in GuardDuty settings\.  
When you generate GuardDuty sample findings using the GuardDuty **Settings** page, Security Hub receives the sample findings and omits the prefix '\[Sample\]' in the finding type\. For example, the sample finding type in GuardDuty "\[SAMPLE\] Recon:IAMUser/ResourcePermissions" is displayed as "Recon:IAMUser/ResourcePermissions” in Security Hub\.  
For more information about the GuardDuty integration, see [Integration with AWS Security Hub](https://docs.aws.amazon.com/guardduty/latest/ug/securityhub-integration.html) in the *Amazon GuardDuty User Guide*\.

**IAM Access Analyzer**  <a name="integration-iam-access-analyzer"></a>
With IAM Access Analyzer, all findings are sent to Security Hub\.  
IAM Access Analyzer uses logic\-based reasoning to analyze resource\-based policies that are applied to supported resources in your account\. IAM Access Analyzer generates a finding when it detects a policy statement that allows an external principal access to a resource in your account\.  
To learn more, see [Integration with AWS Security Hub](https://docs.aws.amazon.com/IAM/latest/UserGuide/access-analyzer-securityhub-integration.html) in the *IAM User Guide*\.

**Amazon Inspector**  <a name="integration-amazon-inspector"></a>
Amazon Inspector sends Amazon Inspector findings to Security Hub that are generated through assessment runs for all supported rules packages\.  
For more information about the integration, see [Integration with AWS Security Hub](https://docs.aws.amazon.com/inspector/latest/userguide/securityhub-integration.html) in the *Amazon Inspector User Guide*\.

**Amazon Macie**  <a name="integration-amazon-macie"></a>
A finding from Macie can indicate that there is a policy violation, or that sensitive data, such as personal identifying information \(PII\) and intellectual property, is present in the data that your organization stores in Amazon S3\.  
By default, Macie only sends policy violation findings to Security Hub\. You can also configure the integration to send sensitive data findings to Security Hub\. For more information, see [Amazon Macie integration with AWS Security Hub](https://docs.aws.amazon.com/macie/latest/user/securityhub-integration.html) in the *Amazon Macie User Guide*\.  
Security Hub can also receive findings from Macie Classic\. Macie Classic sends basic and custom findings to Macie from the **S3 bucket properties** and **S3 objects** indices\. Macie Classic does not send data classifications, or findings from the **CloudTrail data** index\.  
For more information, see [Locating and analyzing Macie Classic alerts](https://docs.aws.amazon.com/macie/latest/userguide/macie-alerts.html#macie-alert-working-locate) in the *Amazon Macie Classic User Guide*\.

**AWS Systems Manager Explorer and OpsCenter**  <a name="integration-ssm-explorer-opscenter"></a>
AWS Systems Manager Explorer and OpsCenter receive findings from Security Hub, and update those findings in Security Hub\.  
Explorer provides you with a customizable dashboard, providing key insights and analysis into the operational health and performance of your AWS environment\.  
OpsCenter provides you with a central location to view, investigate, and resolve operational work items\.  
For more information about Explorer and OpsCenter, see [Operations management](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-ops-center.html) in the *AWS Systems Manager User Guide*\.

**AWS Systems Manager Patch Manager**  <a name="patch-manager"></a>
AWS Systems Manager Patch Manager sends findings to Security Hub when instances in a customer's fleet go out of compliance with their patch compliance standard\.  
Patch Manager automates the process of patching managed instances with both security related and other types of updates\.   
For more information about using Patch Manager, see [AWS Systems Manager Patch Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-patch.html) in the *AWS Systems Manager User Guide*\.