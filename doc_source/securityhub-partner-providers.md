# Third\-Party Partner Product Integrations<a name="securityhub-partner-providers"></a>

After you enable Security Hub, you can configure it to import \(via automatic or manual importing\) findings from the following third\-party product integrations\.


| **Company name** | **Product name** | **Product ARN** | **Product description** | 
| --- | --- | --- | --- | 
| Alert Logic | SIEMless ThreatManagement | arn:aws:securityhub:<REGION>:733251395267:product/alertlogic/althreatmanagement | Get the right level of coverage: vulnerability and asset visibility, threat detection and incident management, WAF, and assigned SOC analyst options\. | 
| ARMOR | Armor Anywhere | arn:aws:securityhub:<REGION>:679703615338:product/armordefense/armoranywhere | Armor Anywhere delivers managed security and compliance for AWS\. | 
| Barracuda Networks | Cloud Security Guardian | arn:aws:securityhub:<REGION>:151784055945:product/barracuda/cloudsecurityguardian  | Barracuda Cloud Security Sentry helps organizations stay secure while building applications in, and moving workloads to, the public cloud\. | 
| Checkpoint | CloudGuard IaaS | arn:aws:securityhub:<REGION>:758245563457:product/checkpoint/cloudguard\-iaas  | Check Point CloudGuard easily extends comprehensive threat prevention security to AWS while protecting assets in the cloud\. | 
| Checkpoint | Dome9 Arc | arn:aws:securityhub:<REGION>:634729597623:product/checkpoint/dome9\-arc  | A SaaS platform that delivers verifiable cloud network security, advanced IAM protection, and comprehensive compliance and governance\. | 
| CrowdStrike | CrowdStrike Falcon | arn:aws:securityhub:<REGION>:517716713836:product/crowdstrike/crowdstrike\-falcon  | CrowdStrike Falcon's single lightweight sensor unifies next\-generation antivirus, endpoint detection and response, and 24/7 managed hunting via the cloud\. | 
| CyberArk | Privileged Threat Analytics | arn:aws:securityhub:<REGION>:749430749651:product/cyberark/cyberark\-pta  | Privileged Threat Analytics collect, detect, alert, and respond to high\-risk activity and behavior of privileged accounts to contain in\-progress attacks\. | 
| F5 Networks | Advanced WAF | arn:aws:securityhub:<REGION>:250871914685:product/f5networks/f5\-advanced\-waf  | Advanced WAF provides malicious bot protection, L7 DoS mitigation, API inspection, behavior analytics, and more to defend against web app attacks\. | 
| GuardiCore | Centra 4\.0 | arn:aws:securityhub:<REGION>:324264561773:product/guardicore/guardicore  | GuardiCore Centra provides flow visualization, micro\-segmentation, and breach detection for workloads in modern data centers and clouds\. | 
| GuardiCore | Infection Monkey | arn:aws:securityhub:<REGION>:324264561773:product/guardicore/aws\-infection\-monkey | Infection Monkey is an attack simulation tool designed to test networks against attackers\. | 
| IBM | QRadar SIEM | arn:aws:securityhub:<REGION>:949680696695:product/ibm/qradar\-siem  | IBM QRadar SIEM provides security teams with the ability to quickly and accurately detect, prioritize, investigate, and respond to threats\. | 
| Imperva | Attack Analytics | arn:aws:securityhub:<REGION>:955745153808:product/imperva/imperva\-attack\-analytics  | Imperva Attack Analytics correlates and distills thousands of security events into a few readable security incidents\. | 
| McAfee | MVISION Cloud for AWS | arn:aws:securityhub:<REGION>:297986523463:product/mcafee\-skyhigh/mcafee\-mvision\-cloud\-aws  | McAfee MVISION Cloud for Amazon Web Services is a comprehensive monitoring, auditing, and remediation solution for your AWS environment\. | 
| Palo Alto Networks | Redlock | arn:aws:securityhub:<REGION>:188619942792:product/paloaltonetworks/redlock  | Protects your AWS deployment with cloud security analytics, advanced threat detection, and compliance monitoring\. | 
| Qualys | Vulnerability Management | arn:aws:securityhub:<REGION>:805950163170:product/qualys/qualys\-vm  | Qualys Vulnerability Management \(VM\) continuously scans and identifies vulnerabilities, protecting your assets\. | 
| Rapid7 | InsightVM | arn:aws:securityhub:<REGION>:336818582268:product/rapid7/insightvm  | Rapid7 InsightVM provides vulnerability management for modern environments, allowing you to efficiently find, prioritize, and remediate vulnerabilities\. | 
| Sophos | Server Protection | arn:aws:securityhub:<REGION>:062897671886:product/sophos/sophos\-server\-protection  | Sophos Server Protection defends the critical applications and data at the core of your organization, using comprehensive defense\-in\-depth techniques\. | 
| Splunk | Splunk Enterprise | arn:aws:securityhub:<REGION>:112543817624:product/splunk/splunk\-enterprise  | Splunk uses Amazon CloudWatch Events as a consumer of Security Hub findings\. Send your data to Splunk for advanced security analytics and SIEM\. | 
| Sumo Logic | Machine Data Analytics | arn:aws:securityhub:<REGION>:956882708938:product/sumologicinc/sumologic\-mda  | Sumo Logic is a secure, machine data analytics platform that enables DevSecOps teams build, run, and secure their AWS applications\. | 
| Symantec | Cloud Workload Protection | arn:aws:securityhub:<REGION>:754237914691:product/symantec\-corp/symantec\-cwp  | Cloud Workload Protection provides complete protection for your Amazon EC2 instances with anti\-malware, intrusion prevention, and file integrity monitoring\. | 
| Tenable | Tenable\.io | arn:aws:securityhub:<REGION>:422820575223:product/tenable/tenable\-io | Accurately identify, investigate, and prioritize vulnerabilities\. Managed in the Cloud\.  | 
| Turbot | Turbot | arn:aws:securityhub:<REGION>:453761072151:product/turbot/turbot  | Turbot ensures that your cloud infrastructure is secure, compliant, scalable, and cost optimized\. | 
| Twistlock | Enterprise Edition | arn:aws:securityhub:<REGION>:496947949261:product/twistlock/twistlock\-enterprise  | Twistlock is a cloud native cybersecurity platform that protects VMs, containers, and serverless platforms\. | 

The following partner products only receive findings and do not have a Product ARN:


| **Company name** | **Product name** | **Product description** | 
| --- | --- | --- | 
| Palo Alto Networks | Demisto Enterprise AMI | Demisto is a Security Orchestration, Automation, and Response \(SOAR\) platform that integrates with your entire security product stack to accelerate incident response and security operations\. | 
| PagerDuty | PagerDuty | PagerDuty's digital operations management platform empowers teams to proactively mitigate customer\-impacting issues by automatically turning any signal into the right insight and action\. AWS users can use PagerDuty’s set of AWS integrations to scale their AWS and hybrid environments with confidence\. When coupled with AWS Security Hub’s aggregated and organized security alerts, PagerDuty allows teams to automate their threat response process and quickly set up custom actions to prevent potential issues\. PagerDuty users undertaking a cloud migration project can move quickly, while decreasing the impact of issues that occur throughout the migration lifecycle\. | 
| Splunk | Splunk Phantom | With the Splunk Phantom App for AWS Security Hub, findings are sent to Phantom for automated context enrichment with additional threat intelligence information or to perform automated response actions\.  | 
| Rapid7 | InsightConnect | Rapid7’s InsightConnect is a security orchestration and automation solution that enables your team to optimize SOC operations with little to no code\. | 
| Atlassian | Ops Genie | Opsgenie is a modern incident management solution for operating always\-on services, empowering Dev & Ops teams to plan for service disruptions and stay in control during incidents\. Integrating with Security Hub will ensure mission critical security related incidents are routed to the appropriate teams for immediate resolution\.  | 
| ServiceNow | ITSM | The ServiceNow Security Hub integration allows security findings from Security Hub to be viewed within ServiceNow ITSM\. | 
| ServiceNow | SecOps | The ServiceNow Security Hub integration allows both automated and manual forwarding of security findings from Security Hub to ServiceNow Security Operations\. | 
| Slack | Slack | Slack is a layer of the business technology stack that brings together people, data, and applications – a single place where people can effectively work together, find important information, and access hundreds of thousands of critical applications and services to do their best work\. | 

**To subscribe to a partner product**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Choose **Integrations** and then locate the product to integrate with Security Hub\.

1. Choose **Purchase** to open AWS Marketplace\. In AWS Marketplace, choose **Continue to Subscribe**\.
**Note**  
If more than one version of a product is available in AWS Marketplace, select the version to subscribe to and then choose **Continue to Subscribe**\. For example, some products offer a standard version and an AWS GovCloud \(US\) version\.

1. Choose **Subscribe**\.

After you subscribe to a product, you need to enable the integration with Security Hub\. When you enable a product integration, a resource policy is automatically attached to that product subscription\. This resource policy defines the permissions that Security Hub needs to import findings from that product\.

**To enable Security Hub integration with the partner product**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Locate the product to enable and then choose **Enable**\.

   You must have a subscription to the product to successfully integrate it with Security Hub\.

1. To review the configuration information from the company that creates the product, choose **Configuration instructions**\.

1. Review the policy that is assigned to the product subscription and then choose **Enable**\.