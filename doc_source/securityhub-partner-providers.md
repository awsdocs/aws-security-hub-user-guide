# Available third\-party partner product integrations<a name="securityhub-partner-providers"></a>

AWS Security Hub is integrated with the following third\-party products\. For each provider, the list indicates how the integration interacts with findings\. An integration can perform the following actions:
+ Send findings that it generates to Security Hub\.
+ Receive findings from Security Hub\.
+ Update findings in Security Hub\. Integrations that receive findings from Security Hub might also update those findings\.

If applicable, the list also specifies the product ARN\. Integrations that send findings to Security Hub always have an ARN\.

**Note**  
Some integrations are not available in Africa \(Cape Town\), China \(Beijing\), China \(Ningxia\), Europe \(Milan\), AWS GovCloud \(US\-East\), or AWS GovCloud \(US\-West\)\.  
If an integration is not supported, it is not listed on the console **Integrations** page  
See also [Integrations that are supported in China \(Beijing\) and China \(Ningxia\)](securityhub-regions.md#securityhub-regions-integration-support-china) and [Integrations that are supported in AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\)](securityhub-regions.md#securityhub-regions-integration-support-govcloud)\.

If you have a security solution and are interested in becoming a Security Hub partner, send an email to securityhub\-partners@amazon\.com\. In the message, provide your company name, product name, AWS Partner Network \(APN\) tier level, and contact information\.

To become a Security Hub partner, you must meet one of the following criteria:
+ You are an AWS Select Tier Partner or above\.
+ You have joined the [AWS ISV Partner Path](http://aws.amazon.com/partners/isv/), and the product that you use for Security Hub integration has completed an [AWS Foundational Technical Review \(FTR\)](http://aws.amazon.com/partners/foundational-technical-review/)\. The product is then granted a "Reviewed by AWS" badge\.

To get started, read through the [https://docs.aws.amazon.com/securityhub/latest/partnerguide/integration-overview.html](https://docs.aws.amazon.com/securityhub/latest/partnerguide/integration-overview.html)\. After you review the onboarding information, you can begin to work on your product manifest\.

**[https://3coresec.com/aws](https://3coresec.com/aws) – 3CORESec NTA**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/3coresec/3coresec`  
3CORESec provides managed detection services for both on\-premises and AWS systems\. Their integration with Security Hub allows visibility into threats such as malware, privilege escalation, lateral movement, and improper network segmentation\.  
[Partner documentation](https://docs.google.com/document/d/1TPUuuyoAVrMKRVnGKouRy384ZJ1-3xZTnruHkIHJqWQ/edit?usp=sharing)

**[https://www.alertlogic.com/solutions/platform/aws-security/](https://www.alertlogic.com/solutions/platform/aws-security/) – SIEMless Threat Management**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:733251395267:product/alertlogic/althreatmanagement`  
Get the right level of coverage: vulnerability and asset visibility, threat detection and incident management, AWS WAF, and assigned SOC analyst options\.  
[Partner documentation](https://docs.alertlogic.com/configure/aws-security-hub.htm)

**[https://blog.aquasec.com/aqua-aws-security-hub](https://blog.aquasec.com/aqua-aws-security-hub) – Aqua Cloud Native Security Platform**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/aquasecurity/aquasecurity`  
Aqua Cloud Native Security Platform \(CSP\) provides full lifecycle security for container\-based and serverless applications, from your CI/CD pipeline to runtime production environments\.  
[Partner documentation](https://github.com/aquasecurity/aws-security-hub-plugin)

**[https://github.com/aquasecurity/kube-bench/blob/master/README.md](https://github.com/aquasecurity/kube-bench/blob/master/README.md) – Kube\-bench**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/aqua-security/kube-bench`  
Kube\-bench is an open\-source tool that runs the Center for Internet Security \(CIS\) Kubernetes Benchmark against your environment\.  
[Partner documentation](https://github.com/aquasecurity/kube-bench/blob/master/README.md)

**[http://aws.amazon.com/marketplace/seller-profile?id=797425f4-6823-4cf6-82b5-634f9a9ec347](http://aws.amazon.com/marketplace/seller-profile?id=797425f4-6823-4cf6-82b5-634f9a9ec347) – Armor Anywhere**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:679703615338:product/armordefense/armoranywhere`  
Armor Anywhere delivers managed security and compliance for AWS\.

**[https://www.atlassian.com/software/jira/service-management](https://www.atlassian.com/software/jira/service-management) \- Jira Service Management**  
**Integration type:** Receive and update  
The AWS Service Management Connector for Jira sends findings from Security Hub to Jira\. Jira issues are created based on the findings\. When the Jira issues are updated, the corresponding findings are updated in Security Hub\.  
For an overview of the integration and how it works, watch the video [AWS Security Hub – Bidirectional integration with Atlassian Jira Service Management](https://www.youtube.com/watch?v=uEKwu0M8S3M)\.  
[Partner documentation](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/integrations-jiraservicedesk.html)

**[https://www.atlassian.com/software/opsgenie](https://www.atlassian.com/software/opsgenie) – Opsgenie**  
**Integration type:** Receive  
Opsgenie is a modern incident management solution for operating always\-on services, empowering development and operations teams to plan for service disruptions and stay in control during incidents\.  
Integrating with Security Hub ensures that mission critical security\-related incidents are routed to the appropriate teams for immediate resolution\.  
[Partner documentation](https://docs.opsgenie.com/docs/amazon-security-hub-integration-bidirectional)

**[https://go.attackiq.com/BD-AWS-Security-Hub_LP.html](https://go.attackiq.com/BD-AWS-Security-Hub_LP.html) – AttackIQ**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/attackiq/attackiq-platform`  
AttackIQ Platform emulates real adversarial behavior aligned with the MITRE ATT&CK Framework to help validate and improve your overall security posture\.  
[Partner documentation](https://github.com/AttackIQ/attackiq.github.io)

**[http://aws.amazon.com/marketplace/pp/B07KF2X7QJ](http://aws.amazon.com/marketplace/pp/B07KF2X7QJ) – Cloud Security Guardian**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:151784055945:product/barracuda/cloudsecurityguardian`  
Barracuda Cloud Security Sentry helps organizations stay secure while building applications in, and moving workloads to, the public cloud\.

**[https://github.com/bigexchange/aws-security-hub](https://github.com/bigexchange/aws-security-hub) – BigID Enterprise**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/bigid/bigid-enterprise`  
The BigID Enterprise Privacy Management Platform helps companies manage and protect sensitive data \(PII\) across all their systems\.  
[Partner documentation](https://github.com/bigexchange/aws-security-hub)

**[https://bluehexagon.ai/solutions/secure-my-aws-workloads/](https://bluehexagon.ai/solutions/secure-my-aws-workloads/) – Blue Hexagon for AWS**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/blue-hexagon/blue-hexagon-for-aws`  
Blue Hexagon is a real time threat detection platform\. It uses deep learning principles to detect known and unknown threats, including malware and network anomalies\.  
[Partner documentation](https://bluehexagonai.atlassian.net/wiki/spaces/BHDOC/pages/395935769/Deploying+Blue+Hexagon+with+AWS+Traffic+Mirroring#DeployingBlueHexagonwithAWSTrafficMirroringDeployment-Integrations)

**[https://www.capitissolutions.com/security-hub-integration/](https://www.capitissolutions.com/security-hub-integration/) – C2VS**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/capitis/c2vs`  
C2VS is a customizable compliance solution designed to automatically identify your application\-specific misconfigurations and their root cause\.  
[Partner documentation](https://www.capitissolutions.com/security-hub-configuration/)

**[http://aws.amazon.com/marketplace/pp/B087Y37BTD](http://aws.amazon.com/marketplace/pp/B087Y37BTD) – Caveonix Cloud**  
  
**Integration type:** Send and receive  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/caveonix/caveonix-cloud`  
Caveonix Cloud is a SaaS risk mitigation platform that delivers automated compliance and hybrid\-cloud security posture management for comprehensive workload protection\.  
[Partner documentation](https://www.caveonix.com/support/aws-security-hub)

**[http://aws.amazon.com/marketplace/seller-profile?id=a979fc8a-dd48-42c8-84cc-63d5d50e3a2f](http://aws.amazon.com/marketplace/seller-profile?id=a979fc8a-dd48-42c8-84cc-63d5d50e3a2f) – CloudGuard IaaS**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:758245563457:product/checkpoint/cloudguard-iaas`  
Check Point CloudGuard easily extends comprehensive threat prevention security to AWS while protecting assets in the cloud\.  
[Partner documentation](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk140412)

**[http://aws.amazon.com/marketplace/seller-profile?id=a979fc8a-dd48-42c8-84cc-63d5d50e3a2f](http://aws.amazon.com/marketplace/seller-profile?id=a979fc8a-dd48-42c8-84cc-63d5d50e3a2f) – CloudGuard Posture Management**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:634729597623:product/checkpoint/dome9-arc`  
A SaaS platform that delivers verifiable cloud network security, advanced IAM protection, and comprehensive compliance and governance\.

**[https://cloudcustodian.io/docs/aws/topics/securityhub.html](https://cloudcustodian.io/docs/aws/topics/securityhub.html) – Cloud Custodian**  
**Integration type:** Send and receive  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/cloud-custodian/cloud-custodian`  
Cloud Custodian enables users to be well managed in the cloud\. The simple YAML DSL allows easily defined rules to enable a well\-managed cloud infrastructure that's both secure and cost optimized\.  
[Partner documentation](https://cloudcustodian.io/docs/aws/topics/securityhub.html)

**[https://cloudstoragesec.com/](https://cloudstoragesec.com/) – Antivirus for Amazon S3**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/cloud-storage-security/antivirus-for-amazon-s3`  
Cloud Storage Security provides cloud native anti\-malware and antivirus scanning for Amazon S3 objects\.  
Antivirus for Amazon S3 offers real time and scheduled scans of objects and files in Amazon S3 for malware and threats\. It provides visibility and remediation for problem and infected files\.  
[Partner documentation](https://help.cloudstoragesec.com/console-overview/console-settings/#send-scan-result-findings-to-aws-security-hub)

**[https://www.cloudtamer.io/partners/aws/](https://www.cloudtamer.io/partners/aws/) – cloudtamer\.io**  
**Integration type:** Send and receive  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/cloudtamerio/cloudtamerio`  
cloudtamer\.io is a complete cloud governance solution for AWS\. cloudtamer\.io gives stakeholders visibility into cloud operations and helps cloud users manage accounts, control budget and cost, and ensure continuous compliance\.

**[http://aws.amazon.com/marketplace/seller-profile?id=f4fb055a-5333-4b6e-8d8b-a4143ad7f6c7](http://aws.amazon.com/marketplace/seller-profile?id=f4fb055a-5333-4b6e-8d8b-a4143ad7f6c7) – CrowdStrike Falcon**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:517716713836:product/crowdstrike/crowdstrike-falcon`  
The CrowdStrike Falcon single, lightweight sensor unifies next\-generation antivirus, endpoint detection and response, and 24/7 managed hunting through the cloud\.

**[https://www.cyberark.com/solutions/digital-transformation/cloud-virtualization-security/](https://www.cyberark.com/solutions/digital-transformation/cloud-virtualization-security/) – Privileged Threat Analytics**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:749430749651:product/cyberark/cyberark-pta`  
Privileged Threat Analytics collect, detect, alert, and respond to high\-risk activity and behavior of privileged accounts to contain in\-progress attacks\.  
[Partner documentation](https://cyberark-customers.force.com/mplace/s/#a352J000000dZATQA2-a392J000001Z3eaQAC)

**[https://disruptops.com/securityhub/](https://disruptops.com/securityhub/) – DisruptOPS**  
**Integration type:** Send and receive  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/disruptops-inc/disruptops`  
The DisruptOps Security Operations Platform helps organizations maintain best security practices in your cloud through the use of automated guardrails\.

**[https://www.fireeye.com/solutions/helix.html](https://www.fireeye.com/solutions/helix.html) – FireEye Helix**  
**Integration type:** Receive  
FireEye Helix is a cloud\-hosted security operations platform that allows organizations to take control of any incident from alert to fix\.

**[https://www.forcepoint.com/platform/technology-partners/securing-your-amazon-web-services-aws-workloads](https://www.forcepoint.com/platform/technology-partners/securing-your-amazon-web-services-aws-workloads) – Forcepoint CASB**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:365761988620:product/forcepoint/forcepoint-casb`  
Forcepoint CASB allows you to discover cloud application use, analyze risk, and enforce appropriate controls for SaaS and custom applications\.  
[Partner documentation](https://frcpnt.com/casb-securityhub)

**[https://www.forcepoint.com/product/cloud-security-gateway](https://www.forcepoint.com/product/cloud-security-gateway) – Forcepoint Cloud Security Gateway**  
**Integration type:** Send  
Product ARN: `arn:aws:securityhub:<REGION>::product/forcepoint/forcepoint-cloud-security-gateway`  
Forcepoint Cloud Security Gateway is a converged cloud security service that provides visibility, control, and threat protection for users and data, wherever they are\.  
[Partner documentation](https://forcepoint.github.io/docs/csg_and_aws_security_hub/#forcepoint-cloud-security-gateway-and-aws-security-hub)

**[https://www.forcepoint.com/platform/technology-partners/securing-your-amazon-web-services-aws-workloads](https://www.forcepoint.com/platform/technology-partners/securing-your-amazon-web-services-aws-workloads) – Forcepoint DLP**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:365761988620:product/forcepoint/forcepoint-dlp`  
Forcepoint DLP addresses human\-centric risk with visibility and control everywhere your people work and everywhere your data resides\.  
[Partner documentation](https://frcpnt.com/dlp-securityhub)

**[https://www.forcepoint.com/platform/technology-partners/securing-your-amazon-web-services-aws-workloads](https://www.forcepoint.com/platform/technology-partners/securing-your-amazon-web-services-aws-workloads) – Forcepoint NGFW**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:365761988620:product/forcepoint/forcepoint-ngfw`  
Forcepoint NGFW lets you connect your AWS environment into your enterprise network with the scalability, protection, and insights needed to manage your network and respond to threats\.  
[Partner documentation](https://frcpnt.com/ngfw-securityhub)

**[http://aws.amazon.com/marketplace/seller-profile?id=21127457-7622-49be-81a6-4cb5dd77a088](http://aws.amazon.com/marketplace/seller-profile?id=21127457-7622-49be-81a6-4cb5dd77a088) – Centra 4\.0**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:324264561773:product/guardicore/guardicore`  
Guardicore Centra provides flow visualization, micro\-segmentation, and breach detection for workloads in modern data centers and clouds\.

**[http://aws.amazon.com/marketplace/seller-profile?id=21127457-7622-49be-81a6-4cb5dd77a088](http://aws.amazon.com/marketplace/seller-profile?id=21127457-7622-49be-81a6-4cb5dd77a088) – Infection Monkey**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:324264561773:product/guardicore/aws-infection-monkey`  
Infection Monkey is an attack simulation tool designed to test networks against attackers\.  
[Partner documentation](https://www.guardicore.com/infectionmonkey/docs/usage/integrations/aws-security-hub/)

**[http://aws.amazon.com/marketplace/seller-profile?id=10857e7c-011b-476d-b938-b587deba31cf](http://aws.amazon.com/marketplace/seller-profile?id=10857e7c-011b-476d-b938-b587deba31cf) – Vulnerability Intelligence**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/hackerone/vulnerability-intelligence`  
The HackerOne platform partners with the global hacker community to uncover the most relevant security issues\. Vulnerability Intelligence enables your organization to go beyond automated scanning\. It shares vulnerabilities that HackerOne ethical hackers have validated and provided steps to reproduce\.  
[Partner documentation](https://docs.hackerone.com/programs/aws-security-hub-integration.html)

**[https://helecloud.com/managed-security-and-compliance-services/](https://helecloud.com/managed-security-and-compliance-services/) – Managed Security**  
**Integration type:** Receive  
HeleCloud is a Managed Services Provider, taking care of your AWS infrastructure so that you can focus on your core business\.

**[https://www.ibm.com/security/security-intelligence/qradar/securing-the-cloud](https://www.ibm.com/security/security-intelligence/qradar/securing-the-cloud) – QRadar**  
**Integration type:** Receive  
**Product ARN:** `arn:aws:securityhub:<REGION>:949680696695:product/ibm/qradar-siem`  
IBM QRadar SIEM provides security teams with the ability to quickly and accurately detect, prioritize, investigate, and respond to threats\.  
[Partner documentation](https://www.ibm.com/docs/en/qradar-common?topic=configuration-integrating-aws-security-hub)

**[https://aws.amazon.com/marketplace/pp/prodview-ol6txkzkdyacc](https://aws.amazon.com/marketplace/pp/prodview-ol6txkzkdyacc) – MVISION Cloud Native Application Protection Platform \(CNAPP\)**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:297986523463:product/mcafee-skyhigh/mcafee-mvision-cloud-aws`  
McAfee MVISION Cloud Native Application Protection Platform \(CNAPP\) offers Cloud Security Posture Management \(CSPM\) and Cloud Workload Protection Platform \(CWPP\) for your AWS environment\.  
[Partner documentation](https://success.myshn.net/Cloud_Native_Application_Protection_Platform_(IaaS)/Amazon_Web_Services_(AWS)/Integrate_MVISION_Cloud_with_AWS_Security_Hub)

**[http://aws.amazon.com/marketplace/pp/B07RM918H7](http://aws.amazon.com/marketplace/pp/B07RM918H7) – MicroFocus Arcsight**  
**Integration type:** Receive  
ArcSight accelerates effective threat detection and response in real time, integrating event correlation and supervised and unsupervised analytics with response automation and orchestration\.  
[Partner documentation](https://community.microfocus.com/cyberres/productdocs/w/connector-documentation/2768/smartconnector-for-amazon-web-services-security-hub)

**[http://aws.amazon.com/marketplace/pp/prodview-reujxcu2cv3f4?qid=1608874215786&sr=0-1&ref_=srh_res_product_title](http://aws.amazon.com/marketplace/pp/prodview-reujxcu2cv3f4?qid=1608874215786&sr=0-1&ref_=srh_res_product_title) – NETSCOUT Cyber Investigator**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:us-east-1::product/netscout/netscout-cyber-investigator`  
NETSCOUT Cyber Investigator is an enterprise\-wide network threat, risk investigation, and forensic analysis platform that helps to reduce the impact of cyber threats on businesses\.  
[Partner documentation](https://www.netscout.com/solutions/cyber-investigator-aws)

**[http://aws.amazon.com/marketplace/pp/prodview-5sf6wkximaixc?ref_=srh_res_product_title](http://aws.amazon.com/marketplace/pp/prodview-5sf6wkximaixc?ref_=srh_res_product_title) – PagerDuty**  
**Integration type:** Receive  
The PagerDuty digital operations management platform empowers teams to proactively mitigate customer\-impacting issues by automatically turning any signal into the right insight and action\.  
AWS users can use the PagerDuty set of AWS integrations to scale their AWS and hybrid environments with confidence\.  
When coupled with Security Hub aggregated and organized security alerts, PagerDuty allows teams to automate their threat response process and quickly set up custom actions to prevent potential issues\.  
PagerDuty users who are undertaking a cloud migration project can move quickly, while decreasing the impact of issues that occur throughout the migration lifecycle\.  
[Partner documentation](https://support.pagerduty.com/docs/aws-security-hub-integration-guide-pagerduty)

**[http://aws.amazon.com/marketplace/seller-profile?id=0ed48363-5064-4d47-b41b-a53f7c937314](http://aws.amazon.com/marketplace/seller-profile?id=0ed48363-5064-4d47-b41b-a53f7c937314) – Cortex XSOAR**  
**Integration type:** Receive  
Cortex XSOAR is a Security Orchestration, Automation, and Response \(SOAR\) platform that integrates with your entire security product stack to accelerate incident response and security operations\.  
[Partner documentation](https://xsoar.pan.dev/docs/reference/integrations/aws---security-hub)

**[http://aws.amazon.com/marketplace/seller-profile?id=0ed48363-5064-4d47-b41b-a53f7c937314](http://aws.amazon.com/marketplace/seller-profile?id=0ed48363-5064-4d47-b41b-a53f7c937314) – Prisma Cloud Compute**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:496947949261:product/twistlock/twistlock-enterprise`  
Prisma Cloud Compute is a cloud native cybersecurity platform that protects VMs, containers, and serverless platforms\.  
[Partner documentation](https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/alerts/aws_security_hub.html)

**[http://aws.amazon.com/marketplace/seller-profile?id=0ed48363-5064-4d47-b41b-a53f7c937314](http://aws.amazon.com/marketplace/seller-profile?id=0ed48363-5064-4d47-b41b-a53f7c937314) – Prisma Cloud Enterprise**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:188619942792:product/paloaltonetworks/redlock`  
Protects your AWS deployment with cloud security analytics, advanced threat detection, and compliance monitoring\.  
[Partner documentation](https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin/configure-external-integrations-on-prisma-cloud/integrate-prisma-cloud-with-aws-security-hub)

**[https://github.com/PaloAltoNetworks/pan_aws_security_hub](https://github.com/PaloAltoNetworks/pan_aws_security_hub) – VM\-Series**  
**Integration type:** Receive  
Palo Alto VM\-Series integration with Security Hub collects threat intelligence and sends it to the VM\-Series next\-generation firewall as an automatic security policy update that blocks malicious IP address activity\.  
[Partner documentation](https://github.com/PaloAltoNetworks/pan_aws_security_hub)

**[https://github.com/toniblyx/prowler/#security-hub-integration](https://github.com/toniblyx/prowler/#security-hub-integration)**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/prowler/prowler`  
Prowler is an open source security tool to perform AWS checks related to security best practices, hardening, and continuous monitoring\.  
[Partner documentation](https://github.com/toniblyx/prowler/#security-hub-integration)

**[https://www.qualys.com/public-cloud/#aws](https://www.qualys.com/public-cloud/#aws) – Vulnerability Management**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:805950163170:product/qualys/qualys-vm`  
Qualys Vulnerability Management \(VM\) continuously scans and identifies vulnerabilities, protecting your assets\.  
[Partner documentation](https://qualys-secure.force.com/discussions/s/article/000005831)

**[https://www.rackspace.com/managed-aws/capabilities/security](https://www.rackspace.com/managed-aws/capabilities/security) – Cloud Native Security**  
**Integration type:** Receive  
Rackspace Technology provides managed security services on top of native AWS security products for 24x7x365 monitoring by Rackspace SOC, advanced analysis, and threat remediation\.

**[https://www.rapid7.com/partners/technology-partners/amazon-web-services/](https://www.rapid7.com/partners/technology-partners/amazon-web-services/) – InsightConnect**  
**Integration type:** Receive  
Rapid7 InsightConnect is a security orchestration and automation solution that enables your team to optimize SOC operations with little to no code\.  
[Partner documentation](https://docs.rapid7.com/insightconnect/aws-security-hub/)

**[https://www.rapid7.com/partners/technology-partners/amazon-web-services/](https://www.rapid7.com/partners/technology-partners/amazon-web-services/) – InsightVM**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:336818582268:product/rapid7/insightvm`  
Rapid7 InsightVM provides vulnerability management for modern environments, allowing you to efficiently find, prioritize, and remediate vulnerabilities\.  
[Partner documentation](https://docs.rapid7.com/insightvm/aws-security-hub/)

**[https://community.rsa.com/docs/DOC-111898](https://community.rsa.com/docs/DOC-111898) – RSA Archer**  
**Integration type:** Receive  
RSA Archer IT and Security Risk Management allows you to determine which assets are critical to your business, establish and communicate security policies and standards, detect and respond to attacks, identify and remediate security deficiencies, and establish clear IT risk management best practices\.  
[Partner documentation](https://community.rsa.com/docs/DOC-111898)

**[http://aws.amazon.com/marketplace/pp/B08P2HR2Z7](http://aws.amazon.com/marketplace/pp/B08P2HR2Z7) – SecureCloudDB**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/secureclouddb/secureclouddb`  
SecureCloudDB is a cloud native database security tool that provides comprehensive visibility of internal and external security postures and activity\. It flags security violations and provides remediation on exploitable database vulnerabilities\.  
[Partner documentation](https://help.secureclouddb.com/guide/aws/security_hub.html)

**[https://docs.aws.amazon.com/servicecatalog/latest/adminguide/integrations-servicenow.html](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/integrations-servicenow.html) – ITSM**  
**Integration type:** Receive and update  
The ServiceNow integration with Security Hub allows security findings from Security Hub to be viewed within ServiceNow ITSM\. You can also configure ServiceNow to automatically create an incident or problem when it receives a finding from Security Hub\.  
Any updates to these incidents and problems result in updates to the findings in Security Hub\.  
For an overview of the integration and how it works, watch the video [AWS Security Hub \- Bidirectional integration with ServiceNow ITSM](https://www.youtube.com/watch?v=OYTi0sjEggE)\.

**[https://github.com/aws-samples/aws-securityhub-to-slack](https://github.com/aws-samples/aws-securityhub-to-slack) – Slack**  
**Integration type:** Receive  
Slack is a layer of the business technology stack that brings together people, data, and applications\. It is a single place where people can effectively work together, find important information, and access hundreds of thousands of critical applications and services to do their best work\.  
[Partner documentation](https://docs.aws.amazon.com/chatbot/latest/adminguide/related-services.html)

**[https://www.sophos.com/en-us/lp/aws-security-hub-integration.aspx](https://www.sophos.com/en-us/lp/aws-security-hub-integration.aspx) – Server Protection**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:062897671886:product/sophos/sophos-server-protection`  
Sophos Server Protection defends the critical applications and data at the core of your organization, using comprehensive defense\-in\-depth techniques\.  
[Partner documentation](https://support.sophos.com/support/s/article/KB-000036466?language=en_US)

**[https://www.splunk.com/en_us/form/stay-afloat-using-aws-security-hub.html](https://www.splunk.com/en_us/form/stay-afloat-using-aws-security-hub.html) – Splunk Enterprise**  
**Integration type:** Receive  
**Product ARN:** `arn:aws:securityhub:<REGION>:112543817624:product/splunk/splunk-enterprise`  
Splunk uses Amazon CloudWatch Events as a consumer of Security Hub findings\. Send your data to Splunk for advanced security analytics and SIEM\.  
[Partner documentation](https://github.com/splunk/splunk-for-securityHub)

**[https://www.splunk.com/en_us/form/stay-afloat-using-aws-security-hub.html](https://www.splunk.com/en_us/form/stay-afloat-using-aws-security-hub.html) – Splunk Phantom**  
**Integration type:** Receive  
With the Splunk Phantom application for AWS Security Hub, findings are sent to Phantom for automated context enrichment with additional threat intelligence information or to perform automated response actions\.  
[Partner documentation](https://splunkphantom.s3.amazonaws.com/phantom-sechub-setup.html)

**[http://aws.amazon.com/marketplace/pp/B07RP4B4P1](http://aws.amazon.com/marketplace/pp/B07RP4B4P1) – StackRox Kubernetes Security**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/stackrox/kubernetes-security`  
StackRox helps enterprises secure their container and Kubernetes deployments at scale by enforcing their compliance and security policies across the entire container life cycle – build, deploy, and run\.

**[https://www.sumologic.com/application/aws-security-hub/](https://www.sumologic.com/application/aws-security-hub/) – Machine Data Analytics**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:956882708938:product/sumologicinc/sumologic-mda`  
Sumo Logic is a secure, machine data analytics platform that enables development and security operations teams to build, run, and secure their AWS applications\.  
[Partner documentation](https://help.sumologic.com/07Sumo-Logic-Apps/01Amazon_and_AWS/AWS_Security_Hub)

**[https://www.broadcom.com/products/cyber-security/endpoint/hybrid-cloud/cloud-workload-protection](https://www.broadcom.com/products/cyber-security/endpoint/hybrid-cloud/cloud-workload-protection) – Cloud Workload Protection**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:754237914691:product/symantec-corp/symantec-cwp`  
Cloud Workload Protection provides complete protection for your Amazon EC2 instances with antimalware, intrusion prevention, and file integrity monitoring\.  
[Partner documentation](https://help.symantec.com/cs/scwp/SCWP/v130271667_v111037498/Intergration-with-AWS-Security-Hub/?locale=EN_US&sku=CWP_COMPUTE)

**[https://cloudsec.sysdig.com/aws/](https://cloudsec.sysdig.com/aws/) – Sysdig Secure for cloud**  
**Integration type:** Send  
**Product ARN:** arn:aws:securityhub:*<REGION>*::product/sysdig/sysdig\-secure\-for\-cloud  
Sysdig Secure for cloud supports asset discovery, risk management, Cloud Security Posture Management \(CSPM\), compliance, automatic vulnerability scanning for Amazon Elastic Container Registry \(ECR\) and Fargate, and threat detection based on CloudTrail\. You can deploy all of these as a single security platform\.  
[Partner documentation](https://cloudsec.sysdig.com/aws/security_hub)

**[https://www.tenable.com/](https://www.tenable.com/) – Tenable\.io**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>:422820575223:product/tenable/tenable-io`  
Accurately identify, investigate, and prioritize vulnerabilities\. Managed in the cloud\.  
[Partner documentation](https://github.com/tenable/Security-Hub)

**[https://aws.amazon.com/marketplace/pp/B07S65ZLPQ](https://aws.amazon.com/marketplace/pp/B07S65ZLPQ)**  
**Integration type:** Receive  
ThreatModeler is an automated threat modeling solution that secures and scales the enterprise software and cloud development life cycle\.  
[Partner documentation](https://threatmodeler-setup-quickstart.s3.amazonaws.com/ThreatModeler+Setup+Guide/ThreatModeler+Setup+%26+Deployment+Guide.pdf)

**[https://turbot.com/features/](https://turbot.com/features/) – Turbot**  
**Integration type:** Send and receive  
**Product ARN:** `arn:aws:securityhub:<REGION>:453761072151:product/turbot/turbot`  
Turbot ensures that your cloud infrastructure is secure, compliant, scalable, and cost optimized\.  
[Partner documentation](https://turbot.com/blog/2018/11/aws-security-hub/)

**Vectra AI – Cognito Detect**  
**Integration type:** Send  
**Product ARN:** `arn:aws:securityhub:<REGION>::product/vectra-ai/cognito-detect`  
Vectra is transforming cybersecurity by applying advanced AI to detect and respond to hidden cyberattackers before they can steal or cause damage\.  
[Partner documentation](https://cognito-resource-guide.s3.us-west-2.amazonaws.com/Vectra_AWS_SecurityHub_Integration_Guide.pdf)