# Security controls and standards in AWS Security Hub<a name="securityhub-standards"></a>

AWS Security Hub consumes, aggregates, and analyzes security findings from various supported AWS and third\-party products\.

Security Hub also generates its own findings by running automated and continuous security checks against rules\. The rules are represented by *security controls*\. The controls, may turn, may be enabled in one or more *security standards*\. The controls help you determine whether the requirements in a\-standard are being met\.

Security checks against controls generate findings that you can use to monitor your security posture and identify specific AWS accounts or resources that require attention\. Each control is related to an AWS service and resource\. For example, security checks against the [CloudTrail\.4](cloudtrail-controls.md#cloudtrail-4) control determine whether you have configured log file validation on your AWS CloudTrail logs\. For more information about controls, see [Viewing and managing security controls](controls-view-manage.md)\.

You can enable a control in one or more enabled Security Hub standards\. When you enable a standard, Security Hub automatically enables the controls that apply to the standard\. Security standards allow you to focus on a specific compliance framework\. Security Hub defines the controls that apply to each standard\. For more information about security standards, see [Viewing and managing security standards](standards-view-manage.md)\.

Based on the results of security checks, Security Hub calculates an overall security score and standard\-specific security scores\. These scores help you understand your security posture\. For more information about scores, see [How security scores are calculated](standards-security-score.md#standard-security-score-calculation)\.

For information about Security Hub pricing for security checks, see [Security Hub pricing](http://aws.amazon.com/security-hub/pricing/)\.

**Topics**
+ [Prerequisite: IAM permissions](iam-permissions-controls-standards.md)
+ [How AWS Security Hub runs and uses security checks](securityhub-controls-finding-generation.md)
+ [Security Hub standards reference](standards-reference.md)
+ [Security Hub controls reference](securityhub-controls-reference.md)
+ [Viewing and managing security standards](standards-view-manage.md)
+ [Viewing and managing security controls](controls-view-manage.md)