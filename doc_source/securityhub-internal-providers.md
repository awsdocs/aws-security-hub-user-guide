# Available AWS service integrations<a name="securityhub-internal-providers"></a>

AWS Security Hub supports integrations with several AWS services\.

**Note**  
Some integrations are only available in select Regions\.  
If an integration is not supported, it is not listed on the **Integrations** page\.  
See also [Integrations that are supported in China \(Beijing\) and China \(Ningxia\)](securityhub-regions.md#securityhub-regions-integration-support-china) and [Integrations that are supported in AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\)](securityhub-regions.md#securityhub-regions-integration-support-govcloud)\.

With the exception of sensitive data findings from Amazon Macie, you're automatically opted in to all other AWS service integrations with Security Hub\. If you've turned on Security Hub and the other service, no other step is needed to activate the integration between the two services\.

The following sections provide details about each AWS service integration with Security Hub\.

## AWS Audit Manager \(Receives findings\)<a name="integration-aws-audit-manager"></a>

AWS Audit Manager receives findings from Security Hub\. These findings help Audit Manager users to prepare for audits\.

To learn more about Audit Manager, see the [https://docs.aws.amazon.com/audit-manager/latest/userguide/what-is.html](https://docs.aws.amazon.com/audit-manager/latest/userguide/what-is.html)\. [AWS Security Hub checks supported by AWS Audit Manager](https://docs.aws.amazon.com/audit-manager/latest/userguide/control-data-sources-ash.html) lists the controls for which Security Hub sends findings to Audit Manager\.

## AWS Chatbot \(Sends findings\)<a name="integration-chatbot"></a>

AWS Chatbot is an interactive agent that helps you to monitor and interact with your AWS resources in your Slack channels and Amazon Chime chat rooms\.

Security Hub sends findings to AWS Chatbot\.

To learn more about the AWS Chatbot integration with Security Hub, see the [Security Hub integration overview](https://docs.aws.amazon.com/chatbot/latest/adminguide/related-services.html#security-hub) in the *AWS Chatbot Administrator Guide*\.

## AWS Config \(Sends findings\)<a name="integration-config"></a>

AWS Config is a service that allows you to assess, audit, and evaluate the configurations of your AWS resources\. AWS Config continuously monitors and records your AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations\.

By using the integration with AWS Config, you can see the results of AWS Config managed and custom rule evaluations as findings in Security Hub\. These findings can be viewed alongside other Security Hub findings, providing a comprehensive overview of your security posture\.

AWS Config uses Amazon EventBridge to send AWS Config rule evaluations to Security Hub\. Security Hub transforms the rule evaluations into findings that follow the [AWS Security Finding Format](securityhub-findings-format.md)\. Security Hub then enriches the findings on a best effort basis by getting more information about the impacted resources, such as the Amazon Resource Name \(ARN\) and creation date\.

For more information about this integration, see the following sections\.

### How AWS Config sends findings to Security Hub<a name="integration-config-how"></a>

All findings in Security Hub use the standard JSON format of ASFF\. ASFF includes details about the origin of the finding, the affected resource, and the current status of the finding\. AWS Config sends managed and custom rule evaluations to Security Hub via EventBridge\. Security Hub transforms the rule evaluations into findings that follow ASFF and enriches the findings on a best effort basis\.

#### Types of findings that AWS Config sends to Security Hub<a name="integration-config-how-types"></a>

Once the integration is activated, AWS Config sends evaluations of all AWS Config managed rules and custom rules to Security Hub\. Only evaluations from [service\-linked AWS Config rules](securityhub-standards-awsconfigrules.md), such as those used to run checks on security controls, are excluded\.

#### Sending AWS Config findings to Security Hub<a name="integration-config-how-types-send-findings"></a>

When the integration is activated, Security Hub will automatically assign the permissions necessary to receive findings from AWS Config\. Security Hub uses service\-to\-service level permissions that provide you with a safe way to activate this integration and import findings from AWS Config via Amazon EventBridge\.

#### Latency for sending findings<a name="integration-config-how-types-latency"></a>

When AWS Config creates a new finding, you can usually view the finding in Security Hub within five minutes\.

#### Retrying when Security Hub is not available<a name="integration-config-how-types-retrying"></a>

AWS Config sends findings to Security Hub on a best\-effort basis through EventBridge\. When an event isn't successfully delivered to Security Hub, EventBridge retries delivery for up to 24 hours or 185 times, whichever comes first\.

#### Updating existing AWS Config findings in Security Hub<a name="integration-config-how-types-updating"></a>

After AWS Config sends a finding to Security Hub, it can send updates to the same finding to Security Hub to reflect additional observations of the finding activity\.

#### Regions in which AWS Config findings exist<a name="integration-config-how-types-regions"></a>

AWS Config findings occur on a Regional basis\. AWS Config sends findings to Security Hub in the same Region or Regions where the findings occur\.

## Viewing AWS Config findings in Security Hub<a name="integration-config-view"></a>

To view your AWS Config findings, choose **Findings** from the Security Hub navigation pane\. To filter the findings to display only AWS Config findings, choose **Product name** in the search bar drop down\. Enter **Config**, and choose **Apply**\.

### Interpreting AWS Config finding names in Security Hub<a name="integration-config-view-interpret-finding-names"></a>

Security Hub transforms AWS Config rule evaluations into findings that follow the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. AWS Config rule evaluations use a different event pattern compared to ASFF\. The table below maps the AWS Config rule evaluation fields with their ASFF counterpart as they appear in Security Hub\.


| Config rule evaluation finding type | ASFF finding type | Hardcoded value | 
| --- | --- | --- | 
| detail\.awsAccountId | AwsAccountId |   | 
| detail\.newEvaluationResult\.resultRecordedTime | CreatedAt |   | 
| detail\.newEvaluationResult\.resultRecordedTime | UpdatedAt |   | 
|  | ProductArn | "arn:<partition>:securityhub:<region>::product/aws/config" | 
|  | ProductName | "Config" | 
|  | CompanyName | "AWS" | 
|  | Region | "eu\-central\-1" | 
| configRuleArn | GeneratorId, ProductFields |  | 
| detail\.ConfigRuleARN/finding/hash | Id |  | 
| detail\.configRuleName | Title, ProductFields |  | 
| detail\.configRuleName | Description | "This finding is created for a resource compliance change for config rule: $\{detail\.ConfigRuleName\}" | 
| Configuration Item "ARN" or Security Hub computed ARN | Resources\[i\]\.id |  | 
| detail\.resourceType | Resources\[i\]\.Type | "AwsS3Bucket" | 
|  | Resources\[i\]\.Partition | "aws" | 
|  | Resources\[i\]\.Region | "eu\-central\-1" | 
| Configuration Item "configuration" | Resources\[i\]\.Details |  | 
|  | SchemaVersion | "2018\-10\-08" | 
|  | Severity\.Label | See "Interpreting Severity Label" below | 
|  | Types | \["Software and Configuration Checks"\] | 
| detail\.newEvaluationResult\.complianceType | Compliance\.Status | "FAILED", "NOT\_AVAILABLE", "PASSED", or "WARNING" | 

### Interpreting severity label<a name="integration-config-view-interpret-severity"></a>

All findings from AWS Config rule evaluations have a default severity label of **MEDIUM** in the ASFF\. You can update the severity label of a finding with the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) API operation\.

### Typical finding from AWS Config<a name="integration-config-view-typical-finding"></a>

Security Hub transforms AWS Config rule evaluations into findings that follow the ASFF\. The following is an example of a typical finding from AWS Config in the ASFF\.

**Note**  
If the description is more than 1024 characters, it will be truncated to 1024 characters and will say "\(truncated\)" at the end\.

```
{
	"SchemaVersion": "2018-10-08",
	"Id": "arn:aws:config:eu-central-1:123456789012:config-rule/config-rule-mburzq/finding/45g070df80cb50b68fa6a43594kc6fda1e517932",
	"ProductArn": "arn:aws:securityhub:eu-central-1::product/aws/config",
	"ProductName": "Config",
	"CompanyName": "AWS",
	"Region": "eu-central-1",
	"GeneratorId": "arn:aws:config:eu-central-1:123456789012:config-rule/config-rule-mburzq",
	"AwsAccountId": "123456789012",
	"Types": [
		"Software and Configuration Checks"
	],
	"CreatedAt": "2022-04-15T05:00:37.181Z",
	"UpdatedAt": "2022-04-19T21:20:15.056Z",
	"Severity": {
		"Label": "MEDIUM",
		"Normalized": 40
	},
	"Title": "s3-bucket-level-public-access-prohibited-config-integration-demo",
	"Description": "This finding is created for a resource compliance change for config rule: s3-bucket-level-public-access-prohibited-config-integration-demo",
	"ProductFields": {
		"aws/securityhub/ProductName": "Config",
		"aws/securityhub/CompanyName": "AWS",
		"aws/securityhub/FindingId": "arn:aws:securityhub:eu-central-1::product/aws/config/arn:aws:config:eu-central-1:123456789012:config-rule/config-rule-mburzq/finding/46f070df80cd50b68fa6a43594dc5fda1e517902",
		"aws/config/ConfigRuleArn": "arn:aws:config:eu-central-1:123456789012:config-rule/config-rule-mburzq",
		"aws/config/ConfigRuleName": "s3-bucket-level-public-access-prohibited-config-integration-demo",
		"aws/config/ConfigComplianceType": "NON_COMPLIANT"
	},
	"Resources": [{
		"Type": "AwsS3Bucket",
		"Id": "arn:aws:s3:::config-integration-demo-bucket",
		"Partition": "aws",
		"Region": "eu-central-1",
		"Details": {
			"AwsS3Bucket": {
				"OwnerId": "4edbba300f1caa608fba2aad2c8fcfe30c32ca32777f64451eec4fb2a0f10d8c",
				"CreatedAt": "2022-04-15T04:32:53.000Z"
			}
		}
	}],
	"Compliance": {
		"Status": "FAILED"
	},
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
```

## Enabling and configuring the integration<a name="integration-config-enable"></a>

To use the AWS Config integration with Security Hub, you must set up both services and add at least one managed or custom rule in AWS Config\. For information about how to set up AWS Config, see [Getting Started](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\. For information about how to set up Security Hub, see [Setting up AWS Security Hub](securityhub-settingup.md)\.

After you set up both AWS Config and Security Hub, the integration is activated automatically\. AWS Config immediately begins to send findings to Security Hub\.

## Stopping the publication of findings to Security Hub<a name="integration-config-stop"></a>

To stop sending findings to Security Hub, you can use the Security Hub console, the Security Hub API, or the AWS CLI\.

See [Disabling and enabling the flow of findings from an integration \(console\)](securityhub-integrations-managing.md#securityhub-integration-findings-flow-console) or [Disabling the flow of findings from an integration \(Security Hub API, AWS CLI\)](securityhub-integrations-managing.md#securityhub-integration-findings-flow-disable-api)\.

## Amazon Detective \(Linked from Security Hub\)<a name="integration-amazon-detective"></a>

Detective automatically collects log data from your AWS resources and uses machine learning, statistical analysis, and graph theory to help you visualize and conduct faster and more efficient security investigations\.

The Security Hub integration with Detective allows you to pivot from Amazon GuardDuty findings in Security Hub into Detective\. You can then use the Detective tools and visualizations to investigate them\. The integration does not require any additional configuration in Security Hub or Detective\.

For GuardDuty finding types, the finding details include an **Investigate in Detective** subsection\. That subsection contains the link to Detective\. See [Pivoting to an entity profile or finding overview from Amazon GuardDuty or AWS Security Hub](https://docs.aws.amazon.com/detective/latest/userguide/profile-pivot-from-service.html) in the *Amazon Detective User Guide*\.

If cross\-Region aggregation is enabled, then when you pivot from the aggregation Region, Detective opens in the Region where the finding originated\.

If a link does not work, then for troubleshooting advice, see [Troubleshooting the pivot](https://docs.aws.amazon.com/detective/latest/userguide/profile-pivot-from-service.html#profile-pivot-troubleshooting)\.

## AWS Firewall Manager \(Sends findings\)<a name="integration-aws-firewall-manager"></a>

Firewall Manager sends findings to Security Hub when a web application firewall \(WAF\) policy for resources or a web access control list \(web ACL\) rule is not in compliance\. Firewall Manager also sends findings when AWS Shield Advanced is not protecting resources, or when an attack is identified\.

If you are already using Firewall Manager, Security Hub automatically enables this integration\. You do not need to take any additional action to begin to receive findings from Firewall Manager\.

To learn more about the integration, view the **Integrations** page in the Security Hub console\.

To learn more about Firewall Manager, see the [https://docs.aws.amazon.com/waf/latest/developerguide/](https://docs.aws.amazon.com/waf/latest/developerguide/)\.

## Amazon GuardDuty \(Sends findings\)<a name="integration-amazon-guardduty"></a>

GuardDuty sends findings to Security Hub for all of the supported finding types\.

New findings from GuardDuty are sent to Security Hub within five minutes\. Updates to findings are sent based on the **Updated findings** setting for Amazon EventBridge in GuardDuty settings\.

When you generate GuardDuty sample findings using the GuardDuty **Settings** page, Security Hub receives the sample findings and omits the prefix `[Sample]` in the finding type\. For example, the sample finding type in GuardDuty `[SAMPLE] Recon:IAMUser/ResourcePermissions` is displayed as `Recon:IAMUser/ResourcePermissions` in Security Hub\.

For more information about the GuardDuty integration, see [Integration with AWS Security Hub](https://docs.aws.amazon.com/guardduty/latest/ug/securityhub-integration.html) in the *Amazon GuardDuty User Guide*\.

## AWS Health \(Sends findings\)<a name="integration-health"></a>

AWS Health provides ongoing visibility into your resource performance and the availability of your AWS services and accounts\. You can use AWS Health events to learn how service and resource changes might affect your applications that run on AWS\.

The integration with AWS Health does not use `BatchImportFindings`\. Instead, AWS Health uses service\-to\-service event messaging to send findings to Security Hub\.

For more information about the integration, see the following sections\.

### How AWS Health sends findings to Security Hub<a name="integration-health-how"></a>

In Security Hub, security issues are tracked as findings\. Some findings come from issues that are detected by other AWS services or by third\-party partners\. Security Hub also has a set of rules that it uses to detect security issues and generate findings\.

Security Hub provides tools to manage findings from across all of these sources\. You can view and filter lists of findings and view details for a finding\. See [Viewing finding lists and details in AWS Security Hub](securityhub-findings-viewing.md)\. You can also track the status of an investigation into a finding\. See [Taking action on findings in AWS Security Hub](securityhub-findings-taking-action.md)\.

All findings in Security Hub use a standard JSON format called the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. ASFF includes details about the source of the issue, the affected resources, and the current status of the finding\.

AWS Health is one of the AWS services that sends findings to Security Hub\.

#### Types of findings that AWS Health sends to Security Hub<a name="integration-health-how-types"></a>

Once the integration is enabled, AWS Health sends all security\-related findings it generates to Security Hub\. The findings are sent to Security Hub using the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. Security\-related findings are defined as the following:
+ Any finding associated with an AWS security service
+ Any finding with the words `security`,`abuse`, or `certificate` in the AWS Health **typeCode**
+ Any finding where the AWS Health service is `risk` or `abuse`

##### Sending AWS Health findings to Security Hub<a name="integration-health-how-types-send-findings"></a>

When you choose to accept findings from AWS Health, Security Hub will automatically assign the permissions necessary to receive the findings from AWS Health\. Security Hub uses service\-to\-service level permissions that provide you with a safe, easy way to enable this integration and import findings from AWS Health via Amazon EventBridge on your behalf\. Choosing **Accept Findings** grants Security Hub permission to consume findings from AWS Health\.

##### Latency for sending findings<a name="integration-health-how-types-latency"></a>

When AWS Health creates a new finding, it is usually sent to Security Hub within five minutes\.

##### Retrying when Security Hub is not available<a name="integration-health-how-types-retrying"></a>

AWS Health sends findings to Security Hub on a best\-effort basis through EventBridge\. When an event isn't successfully delivered to Security Hub, EventBridge retries sending the event for 24 hours\.

##### Updating existing findings in Security Hub<a name="integration-health-how-types-updating"></a>

After AWS Health sends a finding to Security Hub, it can send updates to the same finding to reflect additional observations of the finding activity to Security Hub\. 

##### Regions in which findings exist<a name="integration-health-how-types-regions"></a>

For global events, AWS Health sends findings to Security Hub in us\-east\-1 \(AWS partition\), cn\-northwest\-1 \(China partition\), and gov\-us\-west\-1 \(GovCloud partition\)\. AWS Health sends Region\-specific events to Security Hub in the same Region or Regions where the events occur\.

### Viewing AWS Health findings in Security Hub<a name="integration-health-view"></a>

To view your AWS Health findings in Security Hub, choose **Findings** from the navigation panel\. To filter the findings to display only AWS Health findings, choose **Health** from the **Product name** field\.

#### Interpreting AWS Health finding names in Security Hub<a name="integration-health-view-interpret-finding-names"></a>

AWS Health sends the findings to Security Hub using the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. AWS Health finding uses a different event pattern compared to Security Hub ASFF format\. The table below details all the AWS Health finding fields with their ASFF counterpart as they appear in Security Hub\.


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
+ Severity **CRITICAL** if:
  + The `service` field in the AWS Health finding has the value `Risk`
  + The `typeCode` field in the AWS Health finding has the value `AWS_S3_OPEN_ACCESS_BUCKET_NOTIFICATION`
  + The `typeCode` field in the AWS Health finding has the value `AWS_SHIELD_INTERNET_TRAFFIC_LIMITATIONS_PLACED_IN_RESPONSE_TO_DDOS_ATTACK`
  + The `typeCode` field in the AWS Health finding has the value `AWS_SHIELD_IS_RESPONDING_TO_A_DDOS_ATTACK_AGAINST_YOUR_AWS_RESOURCES`

  Severity **HIGH** if:
  + The `service` field in the AWS Health finding has the value `Abuse`
  + The `typeCode` field in the AWS Health finding contains the value `SECURITY_NOTIFICATION`
  + The `typeCode` field in the AWS Health finding contains the value `ABUSE_DETECTION`

  Severity **MEDIUM** if:
  + The `service` field in the finding is any of the following: `ACM`, `ARTIFACT`, `AUDITMANAGER`, `BACKUP`,`CLOUDENDURE`, `CLOUDHSM`, `CLOUDTRAIL`, `CLOUDWATCH`, `CODEGURGU`, `COGNITO`, `CONFIG`, `CONTROLTOWER`, `DETECTIVE`, `DIRECTORYSERVICE`, `DRS`, `EVENTS`, `FIREWALLMANAGER`, `GUARDDUTY`, `IAM`, `INSPECTOR`, `INSPECTOR2`, `IOTDEVICEDEFENDER`, `KMS`, `MACIE`, `NETWORKFIREWALL`, `ORGANIZATIONS`, `RESILIENCEHUB`, `RESOURCEMANAGER`, `ROUTE53`, `SECURITYHUB`, `SECRETSMANAGER`, `SES`, `SHIELD`, `SSO`, or `WAF`
  + The **typeCode** field in the AWS Health finding contains the value `CERTIFICATE`
  + The **typeCode** field in the AWS Health finding contains the value `END_OF_SUPPORT`

#### Typical finding from AWS Health<a name="integration-health-view-typical-finding"></a>

AWS Health sends findings to Security Hub using the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. The following is an example of a typical finding from AWS Health\.

**Note**  
If the description is more than 1024 characters, it will be truncated to 1024 characters and will say *\(truncated\)* at the end\.

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
            "Description": "Congratulations! Amazon SES has successfully detected the MX record required to use 4557227d-9257-4e49-8d5b-18a99ced4be9.cmf.pinpoint.sysmon-iad.adzel.com as a custom MAIL FROM domain for verified identity cmf.pinpoint.sysmon-iad.adzel.com in AWS Region US East (N. Virginia).\\n\\nYou can now use this MAIL FROM domain with cmf.pinpoint.sysmon-iad.adzel.com and any other verified identity that is configured to use it. For information about how to configure a verified identity to use a custom MAIL FROM domain, see http://docs.aws.amazon.com/ses/latest/DeveloperGuide/mail-from-set.html .\\n\\nPlease note that this email only applies to AWS Region US East (N. Virginia).",
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

When you set up Security Hub, the integration with AWS Health is activated automatically\. AWS Health immediately begins to send findings to Security Hub\.

### Stopping the publication of findings to Security Hub<a name="integration-health-stop"></a>

To stop sending findings to Security Hub, you can use the Security Hub console, Security Hub API, or AWS CLI\.

See [Disabling and enabling the flow of findings from an integration \(console\)](securityhub-integrations-managing.md#securityhub-integration-findings-flow-console) or [Disabling the flow of findings from an integration \(Security Hub API, AWS CLI\)](securityhub-integrations-managing.md#securityhub-integration-findings-flow-disable-api)\.

## IAM Access Analyzer \(Sends findings\)<a name="integration-iam-access-analyzer"></a>

With IAM Access Analyzer, all findings are sent to Security Hub\.

IAM Access Analyzer uses logic\-based reasoning to analyze resource\-based policies that are applied to supported resources in your account\. IAM Access Analyzer generates a finding when it detects a policy statement that allows an external principal access to a resource in your account\.

To learn more, see [Integration with AWS Security Hub](https://docs.aws.amazon.com/IAM/latest/UserGuide/access-analyzer-securityhub-integration.html) in the *IAM User Guide*\.

## Amazon Inspector \(Sends findings\)<a name="integration-amazon-inspector"></a>

Amazon Inspector is a vulnerability management service that continuously scans your AWS workloads for vulnerabilities\. Amazon Inspector automatically discovers and scans Amazon EC2 instances and container images that reside in the Amazon Elastic Container Registry\. The scan looks for software vulnerabilities and unintended network exposure\.

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