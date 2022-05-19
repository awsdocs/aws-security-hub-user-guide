# Available AWS service integrations<a name="securityhub-internal-providers"></a>

Security Hub supports integrations with several AWS services\.

**Note**  
Some integrations are not available in all Regions\.  
If an integration is not supported, it is not listed on the **Integrations** page\.  
See also [Integrations that are supported in China \(Beijing\) and China \(Ningxia\)](securityhub-regions.md#securityhub-regions-integration-support-china) and [Integrations that are supported in AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\)](securityhub-regions.md#securityhub-regions-integration-support-govcloud)\.

With the exception of sensitive data findings from Amazon Macie, you are automatically opted into all other AWS service integrations with Security Hub\. If you have turned on Security Hub and the other service, no other step is needed to activate the integration between the two services\.

Here are the details about each AWS service integration\.

## AWS Audit Manager \(Sends findings\)<a name="integration-aws-audit-manager"></a>

Security Hub sends control findings to Audit Manager\. These findings help Audit Manager users to prepare for audits\.

To learn more about Audit Manager, see the [https://docs.aws.amazon.com/audit-manager/latest/userguide/what-is.html](https://docs.aws.amazon.com/audit-manager/latest/userguide/what-is.html)\. [AWS Security Hub checks supported by AWS Audit Manager](https://docs.aws.amazon.com/audit-manager/latest/userguide/control-data-sources-ash.html) lists the controls for which Security Hub sends findings to Audit Manager\.

## AWS Chatbot \(Sends findings\)<a name="integration-chatbot"></a>

AWS Chatbot is an interactive agent that helps you to monitor and interact with your AWS resources in your Slack channels and Amazon Chime chat rooms\.

Security Hub sends findings to AWS Chatbot\.

To learn more about the AWS Chatbot integration with Security Hub, see the [Security Hub integration overview](https://docs.aws.amazon.com/chatbot/latest/adminguide/related-services.html#security-hub) in the *AWS Chatbot Administrator Guide*\.

## Amazon Detective \(Linked from Security Hub\)<a name="integration-amazon-detective"></a>

Detective automatically collects log data from your AWS resources and uses machine learning, statistical analysis, and graph theory to help you visualize and conduct faster and more efficient security investigations\.

The Security Hub integration with Detective allows you to pivot from Amazon GuardDuty findings in Security Hub into Detective\. You can then use the Detective tools and visualizations to investigate them\. The integration does not require any additional configuration in Security Hub or Detective\.

For GuardDuty finding types, the finding details include an **Investigate in Detective** subsection\. That subsection contains the link to Detective\. See [Pivoting to an entity profile or finding overview from Amazon GuardDuty or AWS Security Hub](https://docs.aws.amazon.com/detective/latest/userguide/profile-pivot-from-service.html) in the *Amazon Detective User Guide*\.

If cross\-Region aggregation is enabled, then when you pivot from the aggregation Region, Detective opens in the Region where the finding originated\.

If a link does not work, then for troubleshooting advice, see [Troubleshooting the pivot](https://docs.aws.amazon.com/detective/latest/userguide/profile-pivot-from-service.html#profile-pivot-troubleshooting)\.

## AWS Firewall Manager \(Sends findings\)<a name="integration-aws-firewall-manager"></a>

Firewall Manager sends findings to Security Hub when a WAF policy for resources or a web ACL rule is not in compliance\. Firewall Manager also sends findings when AWS Shield Advanced is not protecting resources, or when an attack is identified\.

If you are already using Firewall Manager, Security Hub automatically enables this integration\. You do not need to take any additional action to begin to receive findings from Firewall Manager\.

To learn more about the integration, view the **Integrations** page in the Security Hub console\.

To learn more about Firewall Manager, see the [https://docs.aws.amazon.com/waf/latest/developerguide/](https://docs.aws.amazon.com/waf/latest/developerguide/)\.

## Amazon GuardDuty \(Sends findings\)<a name="integration-amazon-guardduty"></a>

GuardDuty sends findings to Security Hub for all of the supported finding types\.

New findings from GuardDuty are sent to Security Hub within 5 minutes\. Updates to findings are sent based on the **Updated findings** setting for Amazon EventBridge in GuardDuty settings\.

When you generate GuardDuty sample findings using the GuardDuty **Settings** page, Security Hub receives the sample findings and omits the prefix '\[Sample\]' in the finding type\. For example, the sample finding type in GuardDuty "\[SAMPLE\] Recon:IAMUser/ResourcePermissions" is displayed as "Recon:IAMUser/ResourcePermissions” in Security Hub\.

For more information about the GuardDuty integration, see [Integration with AWS Security Hub](https://docs.aws.amazon.com/guardduty/latest/ug/securityhub-integration.html) in the *Amazon GuardDuty User Guide*\.

## AWS Health \(Sends findings\)<a name="integration-health"></a>

AWS Health provides ongoing visibility into your resource performance and the availability of your AWS services and accounts\. You can use AWS Health events to learn how service and resource changes might affect your applications that run on AWS\.

The integration with AWS Health does not use `BatchImportFindings`\. Instead, AWS Health uses service\-to\-service event messaging to send findings to Security Hub\.

For more information about the integration, see the following sections\.

### How AWS Health sends findings to Security Hub<a name="integration-health-how"></a>

In Security Hub, security issues are tracked as findings\. Some findings come from issues that are detected by other AWS services or by third\-party partners\. Security Hub also has a set of rules that it uses to detect security issues and generate findings\.

Security Hub provides tools to manage findings from across all of these sources\. You can view and filter lists of findings and view details for a finding\. See [Viewing finding lists and details in AWS Security Hub](securityhub-findings-viewing.md)\. You can also track the status of an investigation into a finding\. See [Taking action on findings in AWS Security Hub](securityhub-findings-taking-action.md)\.

All findings in Security Hub use a standard JSON format called the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. The ASFF includes details about the source of the issue, the affected resources, and the current status of the finding\.

AWS Health is one of the AWS services that sends findings to Security Hub\.

#### Types of findings that AWS Health sends to Security Hub<a name="integration-health-how-types"></a>

Once the integration is enabled, AWS Health sends all security\-related findings it generates to Security Hub\. The findings are sent to Security Hub using the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. Security\-related findings are defined as the following:
+ Any finding associated with an AWS security service
+ Any finding with the words **security**, **abuse**, or **certificate** in the AWS Health **typeCode**
+ Any finding where the AWS Health service is **risk** or **abuse**

##### Sending AWS Health findings to Security Hub<a name="integration-health-how-types-send-findings"></a>

When you choose to accept findings from AWS Health, Security Hub will automatically assign the permissions necessary to receive the findings from AWS Health\. Security Hub uses service\-to\-service level permissions that provide you with a safe, easy way to enable this integration and import findings from AWS Health via Amazon EventBridge on your behalf\. Choosing ‘Accept Findings’ grants Security Hub permission to consume findings from AWS Health\.

##### Latency for sending findings<a name="integration-health-how-types-latency"></a>

When AWS Health creates a new finding, it is usually sent to Security Hub within five minutes\.

##### Retrying when Security Hub is not available<a name="integration-health-how-types-retrying"></a>

AWS Health sends findings to Security Hub on a best\-effort basis through EventBridge\. When an event isn't successfully delivered to Security Hub, EventBridge retries sending the event for 24 hours\.

##### Updating existing findings in Security Hub<a name="integration-health-how-types-updating"></a>

After AWS Health sends a finding to Security Hub, it can send updates to the same finding to reflect additional observations of the finding activity to Security Hub\. 

##### Regions in which findings exist<a name="integration-health-how-types-regions"></a>

For global events, AWS Health sends findings to Security Hub in us\-east\-1 \(AWS partition\), cn\-northwest\-1 \(China partition\), and gov\-us\-west\-1 \(GovCloud partition\)\. AWS Health sends region\-specific events to Security Hub in the same region or regions where the events occur\.

### Viewing AWS Health findings in Security Hub<a name="integration-health-view"></a>

To view your AWS Health findings in Security Hub, choose **Findings** from the navigation panel\. To filter the findings to display only AWS Health findings, choose **Health** from the **Product name** field\.

#### Interpreting AWS Health finding names in Security Hub<a name="integration-health-view-interpret-finding-names"></a>

Health sends the findings to Security Hub using the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. AWS Health finding uses a different event pattern compared to Security Hub ASFF format\. The table below details all the AWS Health finding fields with their ASFF counterpart as they appear in Security Hub\.


| Health finding type | ASFF finding type | Hardcoded value | 
| --- | --- | --- | 
| account | AwsAccountId |   | 
| detail\.startTime | CreatedAt |   | 
| detail\.eventDescription\.latestDescription | Description |   | 
| detail\.eventTypeCode | GeneratorId |   | 
| detail\.eventArn \(including account\) \+ hash of detail\.startTime | Id |   | 
| "arn:aws:securityhub:<region>::product/aws/health" | ProductArn |   | 
| account or resourceId | Resources\[i\]\.id |   | 
|   | Resources\[i\]\.Type | "Other" | 
|   | SchemaVersion | "2018\-10\-08" | 
|   | Severity\.Label | See "Interpreting Severity Label" below | 
| “AWS Health \-" detail\.eventTypeCode | Title |   | 
| \- | Types | \["Software and Configuration Checks"\] | 
| event\.time | UpdatedAt |   | 
| URL of the event on Health console | SourceUrl |   | 

#### Interpreting severity label<a name="integration-health-view-interpret-severity"></a>

The severity label in the ASFF finding is determined using the following logic:
+ Severity **CRITICAL** if the service field in the Health finding has value ‘Risk’ OR the typeCode field in the Health finding has value “AWS\_S3\_OPEN\_ACCESS\_BUCKET\_NOTIFICATION” OR “AWS\_SHIELD\_INTERNET\_TRAFFIC\_LIMITATIONS\_PLACED\_IN\_RESPONSE\_TO\_DDOS\_ATTACK“ OR ”AWS\_SHIELD\_IS\_RESPONDING\_TO\_A\_DDOS\_ATTACK\_AGAINST\_YOUR\_AWS\_RESOURCES”
+ Severity **HIGH** if the service field in the Health finding has value ‘Abuse’ OR the typeCode field in the Health finding contains value “SECURITY\_NOTIFICATION” OR “ABUSE\_DETECTION”
+ Severity **MEDIUM** if the service field in the Health finding is any of the following \- ACM, CLOUDHSM, CLOUDTRAIL, CONFIG, CONTROLTOWER, CONFIG, DETECTIVE, EVENTS, GUARDDUTY, IAM, INSPECTOR, KMS, MACIE, SES, SECURITYHUB, SHIELD, SSO, COGNITO, IOTDEVICEDEFENDER, NETWORKFIREWALL, ROUTE53, WAF, FIREWALLMANAGER, SECRETSMANAGER, BACKUP, AUDITMANAGER, ARTIFACT, CLOUDENDURE, CODEGURU, ORGANIZATIONS, DIRECTORYSERVICE, RESOURCEMANAGER, CLOUDWATCH, DRS, INSPECTOR2, RESILIENCEHUB, or the **typeCode** field in the Health finding contains value “CERTIFICATE” OR “END\_OF\_SUPPORT”

#### Typical finding from AWS Health<a name="integration-health-view-typical-finding"></a>

AWS Health sends findings to Security Hub using the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. The following is an example of a typical finding from AWS Health\.

**Note**  
If the description is more than 1024 characters, it will be truncated to 1024 characters and will say “\(truncated\)” at the end\.

```
{
            "SchemaVersion": "2018-10-08",
            "Id": "arn:aws:health:us-east-1:123456789012:event/SES/AWS_SES_CMF_PENDING_TO_SUCCESS/AWS_SES_CMF_PENDING_TO_SUCCESS_303388638044_33fe2115-8dad-40ce-b533-78e29f49de96/101F7FBAEFC663977DA09CFF56A29236602834D2D361E6A8CA5140BFB3A69B30",
            "ProductArn": "arn:aws:securityhub:us-east-1::product/aws/health",
            "GeneratorId": "AWS_SES_CMF_PENDING_TO_SUCCESS",
            "AwsAccountId": "123456789012",
            "Types": [
                "Software and Configuration Checks"
            ],
            "CreatedAt": "2022-01-07T16:34:04.000Z",
            "UpdatedAt": "2022-01-07T19:17:43.000Z",
            "Severity": {
                "Label": "MEDIUM",
                "Normalized": 40
            },
            "Title": "AWS Health - AWS_SES_CMF_PENDING_TO_SUCCESS",
            "Description": "Congratulations! Amazon SES has successfully detected the MX record required to use 4557227d-9257-4e49-8d5b-18a99ced4be9.cmf.pinpoint.sysmon-iad.adzel.com as a custom MAIL FROM domain for verified identity cmf.pinpoint.sysmon-iad.adzel.com in AWS region US East (N. Virginia).\\n\\nYou can now use this MAIL FROM domain with cmf.pinpoint.sysmon-iad.adzel.com and any other verified identity that is configured to use it. For information about how to configure a verified identity to use a custom MAIL FROM domain, see http://docs.aws.amazon.com/ses/latest/DeveloperGuide/mail-from-set.html .\\n\\nPlease note that this email only applies to AWS region US East (N. Virginia).",
            "SourceUrl": "https://phd.aws.amazon.com/phd/home#/event-log?eventID=arn:aws:health:us-east-1::event/SES/AWS_SES_CMF_PENDING_TO_SUCCESS/AWS_SES_CMF_PENDING_TO_SUCCESS_303388638044_33fe2115-8dad-40ce-b533-78e29f49de96",
            "ProductFields": {
                "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-1::product/aws/health/arn:aws:health:us-east-1::event/SES/AWS_SES_CMF_PENDING_TO_SUCCESS/AWS_SES_CMF_PENDING_TO_SUCCESS_303388638044_33fe2115-8dad-40ce-b533-78e29f49de96",
                "aws/securityhub/ProductName": "Health",
                "aws/securityhub/CompanyName": "AWS"
            },
            "Resources": [
                {
                    "Type": "Other",
                    "Id": "4557227d-9257-4e49-8d5b-18a99ced4be9.cmf.pinpoint.sysmon-iad.adzel.com"
                }
            ],
            "WorkflowState": "NEW",
            "Workflow": {
                "Status": "NEW"
            },
            "RecordState": "ACTIVE",
            "FindingProviderFields": {
                "Severity": {
                    "Label": "MEDIUM"
                },
                "Types": [
                    "Software and Configuration Checks"
                ]
            }
        }
    ]
}
```

### Enabling and configuring the integration<a name="integration-health-enable"></a>

To use the integration with Security Hub, you must enable Security Hub\. For information on how to enable Security Hub, see [Setting up AWS Security Hub](securityhub-settingup.md)\.

When you enable both AWS Health and Security Hub, the integration is enabled automatically\. AWS Health immediately begins to send findings to Security Hub\.

### Stopping the publication of findings to Security Hub<a name="integration-health-stop"></a>

To stop sending findings to Security Hub, you can use either the Security Hub console or the API\.

See [Disabling and enabling the flow of findings from an integration \(console\)](securityhub-integrations-managing.md#securityhub-integration-findings-flow-console) or [Disabling the flow of findings from an integration \(Security Hub API, AWS CLI\)](securityhub-integrations-managing.md#securityhub-integration-findings-flow-disable-api)\.

## IAM Access Analyzer \(Sends findings\)<a name="integration-iam-access-analyzer"></a>

With IAM Access Analyzer, all findings are sent to Security Hub\.

IAM Access Analyzer uses logic\-based reasoning to analyze resource\-based policies that are applied to supported resources in your account\. IAM Access Analyzer generates a finding when it detects a policy statement that allows an external principal access to a resource in your account\.

To learn more, see [Integration with AWS Security Hub](https://docs.aws.amazon.com/IAM/latest/UserGuide/access-analyzer-securityhub-integration.html) in the *IAM User Guide*\.

## Amazon Inspector \(Sends findings\)<a name="integration-amazon-inspector"></a>

Amazon Inspector is a vulnerability management service that continuously scans your AWS workloads for vulnerabilities\. Amazon Inspector automatically discovers and scans EC2 instances and container images that reside in Amazon Elastic Container Registry \(Amazon ECR\)\. The scan looks for software vulnerabilities and unintended network exposure\.

When you enable both Amazon Inspector and Security Hub, the integration is enabled automatically\. Amazon Inspector begins to send findings to Security Hub\. Amazon Inspector sends all of the findings it generates to Security Hub\.

For more information about the integration, see [Integration with AWS Security Hub](https://docs.aws.amazon.com/inspector/latest/user/securityhub-integration.html) in the *Amazon Inspector User Guide*\.

Security Hub can also receive findings from Amazon Inspector Classic\. Amazon Inspector Classic sends findings to Security Hub that are generated through assessment runs for all supported rules packages\.

For more information about the integration, see [Integration with AWS Security Hub](https://docs.aws.amazon.com/inspector/latest/userguide/securityhub-integration.html) in the *Amazon Inspector Classic User Guide*\.

Findings for Amazon Inspector and Amazon Inspector Classic use the same product ARN\. Amazon Inspector findings have the following entry in `ProductFields`:

```
"aws/inspector/ProductVersion": "2",
```

## Amazon Macie \(Sends findings\)<a name="integration-amazon-macie"></a>

A finding from Macie can indicate that there is a potential policy violation or that sensitive data, such as personally identifiable information \(PII\), is present in data that your organization stores in Amazon S3\.

By default, Macie sends only policy findings to Security Hub\. You can configure the integration to also send sensitive data findings to Security Hub\. 

In Security Hub, the finding type for a policy or sensitive data finding is changed to a value that is compatible with ASFF\. For example, the `Policy:IAMUser/S3BucketPublic` finding type in Macie is displayed as `Effects/Data Exposure/Policy:IAMUser-S3BucketPublic` in Security Hub\.

Macie also sends generated sample findings to Security Hub\. For sample findings, the name of the affected resource is `macie-sample-finding-bucket` and the value for the `Sample` field is `true`\.

For more information, see [Amazon Macie integration with AWS Security Hub](https://docs.aws.amazon.com/macie/latest/user/securityhub-integration.html) in the *Amazon Macie User Guide*\.

Previously, Security Hub also received findings from Amazon Macie Classic, which has been discontinued and is no longer available\. Macie Classic sent basic and custom findings \(*alerts*\) to Security Hub from the **S3 bucket properties** and **S3 objects** indices\. Macie Classic did not send data classifications or alerts from the **CloudTrail data** index\.

## AWS Systems Manager Explorer and OpsCenter \(Receives and updates findings\)<a name="integration-ssm-explorer-opscenter"></a>

AWS Systems Manager Explorer and OpsCenter receive findings from Security Hub, and update those findings in Security Hub\.

Explorer provides you with a customizable dashboard, providing key insights and analysis into the operational health and performance of your AWS environment\.

OpsCenter provides you with a central location to view, investigate, and resolve operational work items\.

For more information about Explorer and OpsCenter, see [Operations management](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-ops-center.html) in the *AWS Systems Manager User Guide*\.

## AWS Systems Manager Patch Manager \(Sends findings\)<a name="patch-manager"></a>

AWS Systems Manager Patch Manager sends findings to Security Hub when instances in a customer's fleet go out of compliance with their patch compliance standard\.

Patch Manager automates the process of patching managed instances with both security related and other types of updates\. 

For more information about using Patch Manager, see [AWS Systems Manager Patch Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-patch.html) in the *AWS Systems Manager User Guide*\.

## AWS Trusted Advisor \(Receives findings\)<a name="integration-trusted-advisor"></a>

Trusted Advisor draws upon best practices learned from serving hundreds of thousands of AWS customers\. Trusted Advisor inspects your AWS environment, and then makes recommendations when opportunities exist to save money, improve system availability and performance, or help close security gaps\.

When you enable both Trusted Advisor and Security Hub, the integration is updated automatically\.

Security Hub sends the results of its AWS Foundational Security Best Practices checks to Trusted Advisor\.

For more information about the Security Hub integration with Trusted Advisor, see [Viewing AWS Security Hub controls in AWS Trusted Advisor](https://docs.aws.amazon.com/awssupport/latest/user/security-hub-controls-with-trusted-advisor.html) in the *AWS Support User Guide*\.