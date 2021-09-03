# Supported Regions<a name="securityhub-regions"></a>

To view the Regions that AWS Security Hub is available in, see [Security Hub Service Endpoints](https://docs.aws.amazon.com/general/latest/gr/sechub.html)\.

**Contents**
+ [AWS Organizations integration not supported in all Regions](#securityhub-regions-orgs-support)
+ [Integrations not supported in all Regions](#securityhub-regions-integration-support)
  + [Integrations that are supported in China \(Beijing\) and China \(Ningxia\)](#securityhub-regions-integration-support-china)
  + [Integrations that are supported in AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\)](#securityhub-regions-integration-support-govcloud)
+ [Controls that are not supported in all Regions](#securityhub-regions-control-support)
  + [US East \(Ohio\)](#securityhub-control-support-useast2)
  + [US West \(N\. California\)](#securityhub-control-support-uswest1)
  + [US West \(Oregon\)](#securityhub-control-support-uswest2)
  + [Africa \(Cape Town\)](#securityhub-control-support-afsouth1)
  + [Asia Pacific \(Hong Kong\)](#securityhub-control-support-apeast1)
  + [Asia Pacific \(Mumbai\)](#securityhub-control-support-apsouth1)
  + [Asia Pacific \(Osaka\)](#securityhub-control-support-apnortheast3)
  + [Asia Pacific \(Seoul\)](#securityhub-control-support-apnortheast2)
  + [Asia Pacific \(Singapore\)](#securityhub-control-support-apsoutheast1)
  + [Asia Pacific \(Sydney\)](#securityhub-control-support-apsoutheast2)
  + [Asia Pacific \(Tokyo\)](#securityhub-control-support-apnortheast1)
  + [Canada \(Central\)](#securityhub-control-support-cacentral1)
  + [China \(Beijing\)](#securityhub-control-support-cnnorth1)
  + [China \(Ningxia\)](#securityhub-control-support-cnnorthwest1)
  + [Europe \(Frankfurt\)](#securityhub-control-support-eucentral1)
  + [Europe \(Ireland\)](#securityhub-control-support-euwest1)
  + [Europe \(London\)](#securityhub-control-support-euwest2)
  + [Europe \(Milan\)](#securityhub-control-support-eusouth1)
  + [Europe \(Paris\)](#securityhub-control-support-euwest3)
  + [Europe \(Stockholm\)](#securityhub-control-support-eunorth1)
  + [Middle East \(Bahrain\)](#securityhub-control-support-mesouth1)
  + [South America \(São Paulo\)](#securityhub-control-support-sasouth1)
  + [AWS GovCloud \(US\-East\)](#securityhub-control-support-govuseast1)
  + [AWS GovCloud \(US\-West\)](#securityhub-control-support-govuswest1)

## AWS Organizations integration not supported in all Regions<a name="securityhub-regions-orgs-support"></a>

The China \(Beijing\) and China \(Ningxia\) Regions do not support the Security Hub integration with Organizations\.

## Integrations not supported in all Regions<a name="securityhub-regions-integration-support"></a>

Some integrations are not available in all Regions\. If an integration is not supported, it is not listed on the **Integrations** page\.

### Integrations that are supported in China \(Beijing\) and China \(Ningxia\)<a name="securityhub-regions-integration-support-china"></a>

The China \(Beijing\) and China \(Ningxia\) Regions only support the following [integrations with AWS services](securityhub-internal-providers.md):
+ AWS Firewall Manager
+ Amazon GuardDuty
+ IAM Access Analyzer
+ Systems Manager Explorer and OpsCenter
+ Systems Manager Patch Manager

The China \(Beijing\) and China \(Ningxia\) Regions only support the following [third\-party integrations](securityhub-partner-providers.md):
+ Cloud Custodian
+ FireEye Helix
+ Helecloud
+ IBM QRadar
+ PagerDuty
+ Palo Alto Networks Cortex XSOAR
+ Palo Alto Networks VM\-Series
+ Prowler
+ RSA Archer
+ Splunk Enterprise
+ Splunk Phantom
+ ThreatModeler

### Integrations that are supported in AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\)<a name="securityhub-regions-integration-support-govcloud"></a>

The AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\) Regions only support the following [integrations with AWS services](securityhub-internal-providers.md):
+ Amazon Detective
+ AWS Firewall Manager
+ Amazon GuardDuty
+ Amazon Inspector
+ IAM Access Analyzer

The AWS GovCloud \(US\-East\) and AWS GovCloud \(US\-West\) Regions only support the following [third\-party integrations](securityhub-partner-providers.md):
+ Atlassian Jira Service Manager
+ Atlassian OpsGenie
+ Caveonix Cloud
+ Cloud Custodian
+ Cloud Storage Security Antivirus for Amazon S3
+ cloudtamer\.io
+ CrowdStrike Falcon
+ FireEye Helix
+ Forcepoint CASB
+ Forcepoint DLP
+ Forcepoint NGFW
+ MicroFocus ArcSight
+ NETSCOUT Cyber Investigator
+ PagerDuty
+ Palo Alto Networks – Prisma Cloud Compute
+ Palo Alto Networks – Prisma Cloud Enterprise
+ Palo Alto Networks – VM\-Series
+ Prowler
+ Rackspace Technology – Cloud Native Security
+ Rapid7 InsightConnect
+ RSA Archer
+ SecureCloudDb
+ ServiceNow ITSM
+ Slack
+ ThreatModeler
+ Vectra AI Cognito Detect

## Controls that are not supported in all Regions<a name="securityhub-regions-control-support"></a>

The following Regions do not support all of the Security Hub controls\. For each Region, the list provides the controls that are not supported\.

### US East \(Ohio\)<a name="securityhub-control-support-useast2"></a>

The following controls are not supported in US East \(Ohio\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### US West \(N\. California\)<a name="securityhub-control-support-uswest1"></a>

The following controls are not supported in US West \(N\. California\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### US West \(Oregon\)<a name="securityhub-control-support-uswest2"></a>

The following controls are not supported in US West \(Oregon\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Africa \(Cape Town\)<a name="securityhub-control-support-afsouth1"></a>

The following controls are not supported in Africa \(Cape Town\)\.

**[CIS AWS Foundations Benchmark standard](securityhub-standards-cis.md)**  
[1\.4 – Ensure access keys are rotated every 90 days or less ](securityhub-cis-controls.md#securityhub-cis-controls-1.4)  
[1\.12 – Ensure no root account access key exists](securityhub-cis-controls.md#securityhub-cis-controls-1.12)  
[1\.20 \- Ensure a support role has been created to manage incidents with AWS Support ](securityhub-cis-controls.md#securityhub-cis-controls-1.20)  
[4\.1 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 22 ](securityhub-cis-controls.md#securityhub-cis-controls-4.1)  
[4\.2 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389 ](securityhub-cis-controls.md#securityhub-cis-controls-4.2)

**[Payment Card Industry Data Security Standard \(PCI DSS\)](securityhub-standards-pcidss.md)**  
[\[PCI\.CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-pci-controls.md#pcidss-codebuild-1)  
[\[PCI\.CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-pci-controls.md#pcidss-codebuild-2)  
[\[PCI\.DMS\.1\] AWS Database Migration Service replication instances should not be public](securityhub-pci-controls.md#pcidss-dms-1)  
[\[PCI\.EC2\.1\] Amazon EBS snapshots should not be publicly restorable](securityhub-pci-controls.md#pcidss-ec2-1)  
[\[PCI\.EC2\.3\] Unused EC2 security groups should be removed \(Retiring\)](securityhub-pci-controls.md#pcidss-ec2-3)  
[\[PCI\.EC2\.4\] Unused EC2 EIPs should be removed](securityhub-pci-controls.md#pcidss-ec2-4)  
[\[PCI\.EC2\.5\] Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22](securityhub-pci-controls.md#pcidss-ec2-5)  
[\[PCI\.ELBV2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](securityhub-pci-controls.md#pcidss-elbv2-1)  
[\[PCI\.GuardDuty\.1\] GuardDuty should be enabled](securityhub-pci-controls.md#pcidss-guardduty-1)  
[\[PCI\.IAM\.1\] IAM root user access key should not exist](securityhub-pci-controls.md#pcidss-iam-1)  
[\[PCI\.RDS\.1\] RDS snapshots should prohibit public access](securityhub-pci-controls.md#pcidss-rds-1)  
[\[PCI\.SageMaker\.1\] Amazon SageMaker notebook instances should not have direct internet access](securityhub-pci-controls.md#pcidss-sagemaker-1)  
[\[PCI\.SSM\.1\] Amazon EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation](securityhub-pci-controls.md#pcidss-ssm-1)  
[\[PCI\.SSM\.2\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT](securityhub-pci-controls.md#pcidss-ssm-2)

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[ACM\.1\] Imported ACM certificates should be renewed after a specified time period](securityhub-standards-fsbp-controls.md#fsbp-acm-1)  
[\[APIGateway\.1\] API Gateway REST and WebSocket API logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-apigateway-1)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
[\[DMS\.1\] AWS Database Migration Service replication instances should not be public](securityhub-standards-fsbp-controls.md#fsbp-dms-1)  
[\[EC2\.1\] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone](securityhub-standards-fsbp-controls.md#fsbp-ec2-1)  
[\[EC2\.3\] Attached EBS volumes should be encrypted at rest](securityhub-standards-fsbp-controls.md#fsbp-ec2-3)  
[\[EC2\.4\] Stopped EC2 instances should be removed after a specified time period](securityhub-standards-fsbp-controls.md#fsbp-ec2-4)  
[\[EC2\.8\] EC2 instances should use IMDSv2](securityhub-standards-fsbp-controls.md#fsbp-ec2-8)  
[\[EFS\.1\] Amazon EFS should be configured to encrypt file data at rest using AWS KMS](securityhub-standards-fsbp-controls.md#fsbp-efs-1)  
[\[EFS\.2\] Amazon EFS volumes should be in backup plans](securityhub-standards-fsbp-controls.md#fsbp-efs-2)  
[\[ELB\.4\] Application load balancers should be configured to drop HTTP headers](securityhub-standards-fsbp-controls.md#fsbp-elb-4)  
[\[ELBv2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](securityhub-standards-fsbp-controls.md#fsbp-elbv2-1)  
[\[EMR\.1\] Amazon EMR cluster master nodes should not have public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-emr-1)  
[\[ES\.3\] Elasticsearch domains should encrypt data sent between nodes](securityhub-standards-fsbp-controls.md#fsbp-es-3)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](securityhub-standards-fsbp-controls.md#fsbp-iam-3)  
[\[IAM\.4\] IAM root user access key should not exist](securityhub-standards-fsbp-controls.md#fsbp-iam-4)  
[\[RDS\.1\] RDS snapshots should be private](securityhub-standards-fsbp-controls.md#fsbp-rds-1)  
[\[RDS\.9\] Database logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-9)  
[\[RDS\.10\] IAM authentication should be configured for RDS instances](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)  
[\[S3\.1\] S3 Block Public Access setting should be enabled](securityhub-standards-fsbp-controls.md#fsbp-s3-1)  
[\[SageMaker\.1\] SageMaker notebook instances should not have direct internet access](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)  
[\[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)  
[\[SSM\.3\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT ](securityhub-standards-fsbp-controls.md#fsbp-ssm-3)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Asia Pacific \(Hong Kong\)<a name="securityhub-control-support-apeast1"></a>

The following controls are not supported in Asia Pacific \(Hong Kong\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[RDS\.10\] IAM authentication should be configured for RDS instances](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Asia Pacific \(Mumbai\)<a name="securityhub-control-support-apsouth1"></a>

The following controls are not supported in Asia Pacific \(Mumbai\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Asia Pacific \(Osaka\)<a name="securityhub-control-support-apnortheast3"></a>

The following controls are not supported in Asia Pacific \(Osaka\)\.

**[CIS AWS Foundations Benchmark standard](securityhub-standards-cis.md)**  
[1\.12 – Ensure no root account access key exists](securityhub-cis-controls.md#securityhub-cis-controls-1.12)  
[1\.20 \- Ensure a support role has been created to manage incidents with AWS Support ](securityhub-cis-controls.md#securityhub-cis-controls-1.20)  
[4\.1 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 22 ](securityhub-cis-controls.md#securityhub-cis-controls-4.1)  
[4\.2 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389 ](securityhub-cis-controls.md#securityhub-cis-controls-4.2)

**[Payment Card Industry Data Security Standard \(PCI DSS\)](securityhub-standards-pcidss.md)**  
[\[PCI\.CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-pci-controls.md#pcidss-codebuild-1)  
[\[PCI\.CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-pci-controls.md#pcidss-codebuild-2)  
[\[PCI\.DMS\.1\] AWS Database Migration Service replication instances should not be public](securityhub-pci-controls.md#pcidss-dms-1)  
[\[PCI\.EC2\.1\] Amazon EBS snapshots should not be publicly restorable](securityhub-pci-controls.md#pcidss-ec2-1)  
[\[PCI\.EC2\.3\] Unused EC2 security groups should be removed \(Retiring\)](securityhub-pci-controls.md#pcidss-ec2-3)  
[\[PCI\.EC2\.5\] Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22](securityhub-pci-controls.md#pcidss-ec2-5)  
[\[PCI\.ELBV2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](securityhub-pci-controls.md#pcidss-elbv2-1)  
[\[PCI\.ES\.1\] Elasticsearch domains should be in a VPC](securityhub-pci-controls.md#pcidss-es-1)  
[\[PCI\.ES\.2\] Elasticsearch domains should have encryption at rest enabled](securityhub-pci-controls.md#pcidss-es-2)  
[\[PCI\.GuardDuty\.1\] GuardDuty should be enabled](securityhub-pci-controls.md#pcidss-guardduty-1)  
[\[PCI\.IAM\.1\] IAM root user access key should not exist](securityhub-pci-controls.md#pcidss-iam-1)  
[\[PCI\.Lambda\.1\] Lambda functions should prohibit public access](securityhub-pci-controls.md#pcidss-lambda-1)  
[\[PCI\.Lambda\.2\] Lambda functions should be in a VPC](securityhub-pci-controls.md#pcidss-lambda-2)  
[\[PCI\.RDS\.1\] RDS snapshots should prohibit public access](securityhub-pci-controls.md#pcidss-rds-1)  
[\[PCI\.Redshift\.1\] Amazon Redshift clusters should prohibit public access](securityhub-pci-controls.md#pcidss-redshift-1)  
[\[PCI\.S3\.6\] S3 Block Public Access setting should be enabled](securityhub-pci-controls.md#pcidss-s3-6)  
[\[PCI\.SageMaker\.1\] Amazon SageMaker notebook instances should not have direct internet access](securityhub-pci-controls.md#pcidss-sagemaker-1)  
[\[PCI\.SSM\.1\] Amazon EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation](securityhub-pci-controls.md#pcidss-ssm-1)  
[\[PCI\.SSM\.2\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT](securityhub-pci-controls.md#pcidss-ssm-2)

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[APIGateway\.2\] API Gateway REST API stages should be configured to use SSL certificates for backend authentication](securityhub-standards-fsbp-controls.md#fsbp-apigateway-2)  
[\[APIGateway\.3\] API Gateway REST API stages should have AWS X\-Ray tracing enabled](securityhub-standards-fsbp-controls.md#fsbp-apigateway-3)  
[\[APIGateway\.4\] API Gateway should be associated with an AWS WAF web ACL](securityhub-standards-fsbp-controls.md#fsbp-apigateway-4)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[EC2\.15\] EC2 subnets should not automatically assign public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-ec2-15)  
[\[EC2\.16\] Unused network access control lists should be removed](securityhub-standards-fsbp-controls.md#fsbp-ec2-16)  
[\[EC2\.17\] EC2 instances should not use multiple ENIs](securityhub-standards-fsbp-controls.md#fsbp-ec2-17)  
[\[EC2\.18\] Security groups should only allow unrestricted incoming traffic for authorized ports](securityhub-standards-fsbp-controls.md#fsbp-ec2-18)  
[\[ECS\.1\] Amazon ECS task definitions should have secure networking modes and user definitions](securityhub-standards-fsbp-controls.md#fsbp-ecs-1)  
[\[ECS\.2\] Amazon ECS services should not have public IP addresses assigned to them automatically](securityhub-standards-fsbp-controls.md#fsbp-ecs-2)  
[\[ElasticBeanstalk\.1\] Elastic Beanstalk environments should have enhanced health reporting enabled](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-1)  
[\[ElasticBeanstalk\.2\] Elastic Beanstalk managed platform updates should be enabled](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-2)  
[\[ELB\.4\] Application load balancers should be configured to drop HTTP headers](securityhub-standards-fsbp-controls.md#fsbp-elb-4)  
[\[IAM\.21\] IAM customer managed policies that you create should not allow wildcard actions for services](securityhub-standards-fsbp-controls.md#fsbp-iam-21)  
[\[KMS\.3\] AWS KMS keys should not be unintentionally deleted](securityhub-standards-fsbp-controls.md#fsbp-kms-3)  
[\[Lambda\.4\] Lambda functions should have a dead\-letter queue configured \(Retiring\)](securityhub-standards-fsbp-controls.md#fsbp-lambda-4)  
[\[RDS\.9\] Database logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-9)  
[\[RDS\.10\] IAM authentication should be configured for RDS instances](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  
[\[RDS\.12\] IAM authentication should be configured for RDS clusters](securityhub-standards-fsbp-controls.md#fsbp-rds-12)  
[\[RDS\.13\] RDS automatic minor version upgrades should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-13)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[RDS\.15\] RDS DB clusters should be configured for multiple Availability Zones](securityhub-standards-fsbp-controls.md#fsbp-rds-15)  
[\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)  
[\[Redshift\.7\] Amazon Redshift clusters should use enhanced VPC routing](securityhub-standards-fsbp-controls.md#fsbp-redshift-7)  
[\[S3\.8\] S3 Block Public Access setting should be enabled at the bucket level](securityhub-standards-fsbp-controls.md#fsbp-s3-8)  
[\[SecretsManager\.3\] Remove unused Secrets Manager secrets](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-3)  
[\[SecretsManager\.4\] Secrets Manager secrets should be rotated within a specified number of days](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-4)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Asia Pacific \(Seoul\)<a name="securityhub-control-support-apnortheast2"></a>

The following controls are not supported in Asia Pacific \(Seoul\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Asia Pacific \(Singapore\)<a name="securityhub-control-support-apsoutheast1"></a>

The following controls are not supported in Asia Pacific \(Singapore\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Asia Pacific \(Sydney\)<a name="securityhub-control-support-apsoutheast2"></a>

The following controls are not supported in Asia Pacific \(Sydney\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Asia Pacific \(Tokyo\)<a name="securityhub-control-support-apnortheast1"></a>

The following controls are not supported in Asia Pacific \(Tokyo\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Canada \(Central\)<a name="securityhub-control-support-cacentral1"></a>

The following controls are not supported in Canada \(Central\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### China \(Beijing\)<a name="securityhub-control-support-cnnorth1"></a>

The following controls are not supported in China \(Beijing\)\.

**[CIS AWS Foundations Benchmark standard](securityhub-standards-cis.md)**  
[1\.13 – Ensure MFA is enabled for the "root" account ](securityhub-cis-controls.md#securityhub-cis-controls-1.13)  
[1\.14 – Ensure hardware MFA is enabled for the "root" account ](securityhub-cis-controls.md#securityhub-cis-controls-1.14)

**[Payment Card Industry Data Security Standard \(PCI DSS\)](securityhub-standards-pcidss.md)**  
[\[PCI\.GuardDuty\.1\] GuardDuty should be enabled](securityhub-pci-controls.md#pcidss-guardduty-1)  
[\[PCI\.IAM\.4\] Hardware MFA should be enabled for the root user](securityhub-pci-controls.md#pcidss-iam-4)  
[\[PCI\.IAM\.5\] Virtual MFA should be enabled for the root user](securityhub-pci-controls.md#pcidss-iam-5)  
[\[PCI\.Lambda\.1\] Lambda functions should prohibit public access](securityhub-pci-controls.md#pcidss-lambda-1)  
[\[PCI\.Lambda\.2\] Lambda functions should be in a VPC](securityhub-pci-controls.md#pcidss-lambda-2)  
[\[PCI\.SageMaker\.1\] Amazon SageMaker notebook instances should not have direct internet access](securityhub-pci-controls.md#pcidss-sagemaker-1)

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[ACM\.1\] Imported ACM certificates should be renewed after a specified time period](securityhub-standards-fsbp-controls.md#fsbp-acm-1)  
[\[APIGateway\.2\] API Gateway REST API stages should be configured to use SSL certificates for backend authentication](securityhub-standards-fsbp-controls.md#fsbp-apigateway-2)  
[\[APIGateway\.3\] API Gateway REST API stages should have AWS X\-Ray tracing enabled](securityhub-standards-fsbp-controls.md#fsbp-apigateway-3)  
[\[APIGateway\.4\] API Gateway should be associated with an AWS WAF web ACL](securityhub-standards-fsbp-controls.md#fsbp-apigateway-4)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[EC2\.15\] EC2 subnets should not automatically assign public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-ec2-15)  
[\[EC2\.16\] Unused network access control lists should be removed](securityhub-standards-fsbp-controls.md#fsbp-ec2-16)  
[\[ECS\.1\] Amazon ECS task definitions should have secure networking modes and user definitions](securityhub-standards-fsbp-controls.md#fsbp-ecs-1)  
[\[ElasticBeanstalk\.1\] Elastic Beanstalk environments should have enhanced health reporting enabled](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-1)  
[\[ElasticBeanstalk\.2\] Elastic Beanstalk managed platform updates should be enabled](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-2)  
[\[ES\.3\] Elasticsearch domains should encrypt data sent between nodes](securityhub-standards-fsbp-controls.md#fsbp-es-3)  
[\[ES\.4\] Elasticsearch domain error logging to CloudWatch Logs should be enabled](securityhub-standards-fsbp-controls.md#fsbp-es-4)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.6\] Hardware MFA should be enabled for the root user](securityhub-standards-fsbp-controls.md#fsbp-iam-6)  
[\[IAM\.21\] IAM customer managed policies that you create should not allow wildcard actions for services](securityhub-standards-fsbp-controls.md#fsbp-iam-21)  
[\[Lambda\.1\] Lambda function policies should prohibit public access](securityhub-standards-fsbp-controls.md#fsbp-lambda-1)  
[\[Lambda\.2\] Lambda functions should use supported runtimes](securityhub-standards-fsbp-controls.md#fsbp-lambda-2)  
[\[RDS\.7\] RDS clusters should have deletion protection enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-7)  
[\[RDS\.10\] IAM authentication should be configured for RDS instances](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  
[\[RDS\.12\] IAM authentication should be configured for RDS clusters](securityhub-standards-fsbp-controls.md#fsbp-rds-12)  
[\[RDS\.13\] RDS automatic minor version upgrades should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-13)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[RDS\.15\] RDS DB clusters should be configured for multiple Availability Zones](securityhub-standards-fsbp-controls.md#fsbp-rds-15)  
[\[RDS\.16\] RDS DB clusters should be configured to copy tags to snapshots](securityhub-standards-fsbp-controls.md#fsbp-rds-16)  
[\[Redshift\.7\] Amazon Redshift clusters should use enhanced VPC routing](securityhub-standards-fsbp-controls.md#fsbp-redshift-7)  
[\[S3\.8\] S3 Block Public Access setting should be enabled at the bucket level](securityhub-standards-fsbp-controls.md#fsbp-s3-8)  
[\[SageMaker\.1\] SageMaker notebook instances should not have direct internet access](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)  
[\[SecretsManager\.3\] Remove unused Secrets Manager secrets](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-3)  
[\[SecretsManager\.4\] Secrets Manager secrets should be rotated within a specified number of days](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-4)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### China \(Ningxia\)<a name="securityhub-control-support-cnnorthwest1"></a>

The following controls are not supported in China \(Ningxia\)\.

**[CIS AWS Foundations Benchmark standard](securityhub-standards-cis.md)**  
[1\.13 – Ensure MFA is enabled for the "root" account ](securityhub-cis-controls.md#securityhub-cis-controls-1.13)  
[1\.14 – Ensure hardware MFA is enabled for the "root" account ](securityhub-cis-controls.md#securityhub-cis-controls-1.14)

**[Payment Card Industry Data Security Standard \(PCI DSS\)](securityhub-standards-pcidss.md)**  
[\[PCI\.GuardDuty\.1\] GuardDuty should be enabled](securityhub-pci-controls.md#pcidss-guardduty-1)  
[\[PCI\.IAM\.4\] Hardware MFA should be enabled for the root user](securityhub-pci-controls.md#pcidss-iam-4)  
[\[PCI\.IAM\.5\] Virtual MFA should be enabled for the root user](securityhub-pci-controls.md#pcidss-iam-5)  
[\[PCI\.Lambda\.1\] Lambda functions should prohibit public access](securityhub-pci-controls.md#pcidss-lambda-1)  
[\[PCI\.Lambda\.2\] Lambda functions should be in a VPC](securityhub-pci-controls.md#pcidss-lambda-2)  
[\[PCI\.SageMaker\.1\] Amazon SageMaker notebook instances should not have direct internet access](securityhub-pci-controls.md#pcidss-sagemaker-1)

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[ACM\.1\] Imported ACM certificates should be renewed after a specified time period](securityhub-standards-fsbp-controls.md#fsbp-acm-1)  
[\[APIGateway\.2\] API Gateway REST API stages should be configured to use SSL certificates for backend authentication](securityhub-standards-fsbp-controls.md#fsbp-apigateway-2)  
[\[APIGateway\.3\] API Gateway REST API stages should have AWS X\-Ray tracing enabled](securityhub-standards-fsbp-controls.md#fsbp-apigateway-3)  
[\[APIGateway\.4\] API Gateway should be associated with an AWS WAF web ACL](securityhub-standards-fsbp-controls.md#fsbp-apigateway-4)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[EC2\.15\] EC2 subnets should not automatically assign public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-ec2-15)  
[\[EC2\.16\] Unused network access control lists should be removed](securityhub-standards-fsbp-controls.md#fsbp-ec2-16)  
[\[ECS\.1\] Amazon ECS task definitions should have secure networking modes and user definitions](securityhub-standards-fsbp-controls.md#fsbp-ecs-1)  
[\[ElasticBeanstalk\.1\] Elastic Beanstalk environments should have enhanced health reporting enabled](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-1)  
[\[ElasticBeanstalk\.2\] Elastic Beanstalk managed platform updates should be enabled](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-2)  
[\[ES\.3\] Elasticsearch domains should encrypt data sent between nodes](securityhub-standards-fsbp-controls.md#fsbp-es-3)  
[\[ES\.4\] Elasticsearch domain error logging to CloudWatch Logs should be enabled](securityhub-standards-fsbp-controls.md#fsbp-es-4)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.6\] Hardware MFA should be enabled for the root user](securityhub-standards-fsbp-controls.md#fsbp-iam-6)  
[\[IAM\.21\] IAM customer managed policies that you create should not allow wildcard actions for services](securityhub-standards-fsbp-controls.md#fsbp-iam-21)  
[\[Lambda\.1\] Lambda function policies should prohibit public access](securityhub-standards-fsbp-controls.md#fsbp-lambda-1)  
[\[Lambda\.2\] Lambda functions should use supported runtimes](securityhub-standards-fsbp-controls.md#fsbp-lambda-2)  
[\[Lambda\.4\] Lambda functions should have a dead\-letter queue configured \(Retiring\)](securityhub-standards-fsbp-controls.md#fsbp-lambda-4)  
[\[RDS\.7\] RDS clusters should have deletion protection enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-7)  
[\[RDS\.9\] Database logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-9)  
[\[RDS\.10\] IAM authentication should be configured for RDS instances](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  
[\[RDS\.12\] IAM authentication should be configured for RDS clusters](securityhub-standards-fsbp-controls.md#fsbp-rds-12)  
[\[RDS\.13\] RDS automatic minor version upgrades should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-13)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[RDS\.15\] RDS DB clusters should be configured for multiple Availability Zones](securityhub-standards-fsbp-controls.md#fsbp-rds-15)  
[\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)  
[\[Redshift\.7\] Amazon Redshift clusters should use enhanced VPC routing](securityhub-standards-fsbp-controls.md#fsbp-redshift-7)  
[\[S3\.8\] S3 Block Public Access setting should be enabled at the bucket level](securityhub-standards-fsbp-controls.md#fsbp-s3-8)  
[\[SageMaker\.1\] SageMaker notebook instances should not have direct internet access](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)  
[\[SecretsManager\.3\] Remove unused Secrets Manager secrets](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-3)  
[\[SecretsManager\.4\] Secrets Manager secrets should be rotated within a specified number of days](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-4)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Europe \(Frankfurt\)<a name="securityhub-control-support-eucentral1"></a>

The following controls are not supported in Europe \(Frankfurt\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Europe \(Ireland\)<a name="securityhub-control-support-euwest1"></a>

The following controls are not supported in Europe \(Ireland\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Europe \(London\)<a name="securityhub-control-support-euwest2"></a>

The following controls are not supported in Europe \(London\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Europe \(Milan\)<a name="securityhub-control-support-eusouth1"></a>

The following controls are not supported in Europe \(Milan\)\.

**[CIS AWS Foundations Benchmark standard](securityhub-standards-cis.md)**  
[1\.4 – Ensure access keys are rotated every 90 days or less ](securityhub-cis-controls.md#securityhub-cis-controls-1.4)  
[1\.20 \- Ensure a support role has been created to manage incidents with AWS Support ](securityhub-cis-controls.md#securityhub-cis-controls-1.20)  
[4\.1 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 22 ](securityhub-cis-controls.md#securityhub-cis-controls-4.1)  
[4\.2 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389 ](securityhub-cis-controls.md#securityhub-cis-controls-4.2)

**[Payment Card Industry Data Security Standard \(PCI DSS\)](securityhub-standards-pcidss.md)**  
[\[PCI\.CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-pci-controls.md#pcidss-codebuild-1)  
[\[PCI\.CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-pci-controls.md#pcidss-codebuild-2)  
[\[PCI\.DMS\.1\] AWS Database Migration Service replication instances should not be public](securityhub-pci-controls.md#pcidss-dms-1)  
[\[PCI\.EC2\.1\] Amazon EBS snapshots should not be publicly restorable](securityhub-pci-controls.md#pcidss-ec2-1)  
[\[PCI\.EC2\.3\] Unused EC2 security groups should be removed \(Retiring\)](securityhub-pci-controls.md#pcidss-ec2-3)  
[\[PCI\.EC2\.4\] Unused EC2 EIPs should be removed](securityhub-pci-controls.md#pcidss-ec2-4)  
[\[PCI\.EC2\.5\] Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22](securityhub-pci-controls.md#pcidss-ec2-5)  
[\[PCI\.ELBV2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](securityhub-pci-controls.md#pcidss-elbv2-1)  
[\[PCI\.GuardDuty\.1\] GuardDuty should be enabled](securityhub-pci-controls.md#pcidss-guardduty-1)  
[\[PCI\.RDS\.1\] RDS snapshots should prohibit public access](securityhub-pci-controls.md#pcidss-rds-1)  
[\[PCI\.S3\.6\] S3 Block Public Access setting should be enabled](securityhub-pci-controls.md#pcidss-s3-6)  
[\[PCI\.SageMaker\.1\] Amazon SageMaker notebook instances should not have direct internet access](securityhub-pci-controls.md#pcidss-sagemaker-1)  
[\[PCI\.SSM\.1\] Amazon EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation](securityhub-pci-controls.md#pcidss-ssm-1)  
[\[PCI\.SSM\.2\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT](securityhub-pci-controls.md#pcidss-ssm-2)

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[ACM\.1\] Imported ACM certificates should be renewed after a specified time period](securityhub-standards-fsbp-controls.md#fsbp-acm-1)  
[\[APIGateway\.1\] API Gateway REST and WebSocket API logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-apigateway-1)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
[\[DMS\.1\] AWS Database Migration Service replication instances should not be public](securityhub-standards-fsbp-controls.md#fsbp-dms-1)  
[\[EC2\.1\] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone](securityhub-standards-fsbp-controls.md#fsbp-ec2-1)  
[\[EC2\.3\] Attached EBS volumes should be encrypted at rest](securityhub-standards-fsbp-controls.md#fsbp-ec2-3)  
[\[EC2\.4\] Stopped EC2 instances should be removed after a specified time period](securityhub-standards-fsbp-controls.md#fsbp-ec2-4)  
[\[EC2\.8\] EC2 instances should use IMDSv2](securityhub-standards-fsbp-controls.md#fsbp-ec2-8)  
[\[EFS\.1\] Amazon EFS should be configured to encrypt file data at rest using AWS KMS](securityhub-standards-fsbp-controls.md#fsbp-efs-1)  
[\[EFS\.2\] Amazon EFS volumes should be in backup plans](securityhub-standards-fsbp-controls.md#fsbp-efs-2)  
[\[ELB\.4\] Application load balancers should be configured to drop HTTP headers](securityhub-standards-fsbp-controls.md#fsbp-elb-4)  
[\[ELBv2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](securityhub-standards-fsbp-controls.md#fsbp-elbv2-1)  
[\[EMR\.1\] Amazon EMR cluster master nodes should not have public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-emr-1)  
[\[ES\.3\] Elasticsearch domains should encrypt data sent between nodes](securityhub-standards-fsbp-controls.md#fsbp-es-3)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](securityhub-standards-fsbp-controls.md#fsbp-iam-3)  
[\[KMS\.3\] AWS KMS keys should not be unintentionally deleted](securityhub-standards-fsbp-controls.md#fsbp-kms-3)  
[\[RDS\.1\] RDS snapshots should be private](securityhub-standards-fsbp-controls.md#fsbp-rds-1)  
[\[RDS\.9\] Database logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-9)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[Redshift\.2\] Connections to Amazon Redshift clusters should be encrypted in transit](securityhub-standards-fsbp-controls.md#fsbp-redshift-2)  
[\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)  
[\[S3\.1\] S3 Block Public Access setting should be enabled](securityhub-standards-fsbp-controls.md#fsbp-s3-1)  
[\[SageMaker\.1\] SageMaker notebook instances should not have direct internet access](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)  
[\[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)  
[\[SSM\.3\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT ](securityhub-standards-fsbp-controls.md#fsbp-ssm-3)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Europe \(Paris\)<a name="securityhub-control-support-euwest3"></a>

The following controls are not supported in Europe \(Paris\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Europe \(Stockholm\)<a name="securityhub-control-support-eunorth1"></a>

The following controls are not supported in Europe \(Stockholm\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### Middle East \(Bahrain\)<a name="securityhub-control-support-mesouth1"></a>

The following controls are not supported in Middle East \(Bahrain\)\.

**[Payment Card Industry Data Security Standard \(PCI DSS\)](securityhub-standards-pcidss.md)**  
[\[PCI\.GuardDuty\.1\] GuardDuty should be enabled](securityhub-pci-controls.md#pcidss-guardduty-1)  
[\[PCI\.S3\.6\] S3 Block Public Access setting should be enabled](securityhub-pci-controls.md#pcidss-s3-6)

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[RDS\.7\] RDS clusters should have deletion protection enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-7)  
[\[RDS\.12\] IAM authentication should be configured for RDS clusters](securityhub-standards-fsbp-controls.md#fsbp-rds-12)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[RDS\.15\] RDS DB clusters should be configured for multiple Availability Zones](securityhub-standards-fsbp-controls.md#fsbp-rds-15)  
[\[RDS\.16\] RDS DB clusters should be configured to copy tags to snapshots](securityhub-standards-fsbp-controls.md#fsbp-rds-16)  
[\[Redshift\.6\] Amazon Redshift should have automatic upgrades to major versions enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-6)  
[\[S3\.1\] S3 Block Public Access setting should be enabled](securityhub-standards-fsbp-controls.md#fsbp-s3-1)  
[\[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### South America \(São Paulo\)<a name="securityhub-control-support-sasouth1"></a>

The following controls are not supported in South America \(São Paulo\)\.

[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[RDS\.7\] RDS clusters should have deletion protection enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-7)  
[\[RDS\.12\] IAM authentication should be configured for RDS clusters](securityhub-standards-fsbp-controls.md#fsbp-rds-12)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[RDS\.15\] RDS DB clusters should be configured for multiple Availability Zones](securityhub-standards-fsbp-controls.md#fsbp-rds-15)  
[\[RDS\.16\] RDS DB clusters should be configured to copy tags to snapshots](securityhub-standards-fsbp-controls.md#fsbp-rds-16)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### AWS GovCloud \(US\-East\)<a name="securityhub-control-support-govuseast1"></a>

The following controls are not supported in AWS GovCloud \(US\-East\)\.

**[CIS AWS Foundations Benchmark standard](securityhub-standards-cis.md)**  
[1\.13 – Ensure MFA is enabled for the "root" account ](securityhub-cis-controls.md#securityhub-cis-controls-1.13)  
[1\.14 – Ensure hardware MFA is enabled for the "root" account ](securityhub-cis-controls.md#securityhub-cis-controls-1.14)

**[Payment Card Industry Data Security Standard \(PCI DSS\)](securityhub-standards-pcidss.md)**  
[\[PCI\.CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-pci-controls.md#pcidss-codebuild-1)  
[\[PCI\.CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-pci-controls.md#pcidss-codebuild-2)  
[\[PCI\.GuardDuty\.1\] GuardDuty should be enabled](securityhub-pci-controls.md#pcidss-guardduty-1)  
[\[PCI\.IAM\.4\] Hardware MFA should be enabled for the root user](securityhub-pci-controls.md#pcidss-iam-4)  
[\[PCI\.IAM\.5\] Virtual MFA should be enabled for the root user](securityhub-pci-controls.md#pcidss-iam-5)  
[\[PCI\.SageMaker\.1\] Amazon SageMaker notebook instances should not have direct internet access](securityhub-pci-controls.md#pcidss-sagemaker-1)

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[APIGateway\.2\] API Gateway REST API stages should be configured to use SSL certificates for backend authentication](securityhub-standards-fsbp-controls.md#fsbp-apigateway-2)  
[\[APIGateway\.3\] API Gateway REST API stages should have AWS X\-Ray tracing enabled](securityhub-standards-fsbp-controls.md#fsbp-apigateway-3)  
[\[APIGateway\.4\] API Gateway should be associated with an AWS WAF web ACL](securityhub-standards-fsbp-controls.md#fsbp-apigateway-4)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
[\[DynamoDB\.1\] DynamoDB tables should automatically scale capacity with demand](securityhub-standards-fsbp-controls.md#fsbp-dynamodb-1)  
[\[EC2\.15\] EC2 subnets should not automatically assign public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-ec2-15)  
[\[EC2\.16\] Unused network access control lists should be removed](securityhub-standards-fsbp-controls.md#fsbp-ec2-16)  
[\[EC2\.17\] EC2 instances should not use multiple ENIs](securityhub-standards-fsbp-controls.md#fsbp-ec2-17)  
[\[ECS\.1\] Amazon ECS task definitions should have secure networking modes and user definitions](securityhub-standards-fsbp-controls.md#fsbp-ecs-1)  
[\[EFS\.2\] Amazon EFS volumes should be in backup plans](securityhub-standards-fsbp-controls.md#fsbp-efs-2)  
[\[ElasticBeanstalk\.1\] Elastic Beanstalk environments should have enhanced health reporting enabled](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-1)  
[\[ElasticBeanstalk\.2\] Elastic Beanstalk managed platform updates should be enabled](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-2)  
[\[ES\.4\] Elasticsearch domain error logging to CloudWatch Logs should be enabled](securityhub-standards-fsbp-controls.md#fsbp-es-4)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.6\] Hardware MFA should be enabled for the root user](securityhub-standards-fsbp-controls.md#fsbp-iam-6)  
[\[IAM\.21\] IAM customer managed policies that you create should not allow wildcard actions for services](securityhub-standards-fsbp-controls.md#fsbp-iam-21)  
[\[RDS\.12\] IAM authentication should be configured for RDS clusters](securityhub-standards-fsbp-controls.md#fsbp-rds-12)  
[\[RDS\.13\] RDS automatic minor version upgrades should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-13)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[RDS\.15\] RDS DB clusters should be configured for multiple Availability Zones](securityhub-standards-fsbp-controls.md#fsbp-rds-15)  
[\[Redshift\.7\] Amazon Redshift clusters should use enhanced VPC routing](securityhub-standards-fsbp-controls.md#fsbp-redshift-7)  
[\[S3\.8\] S3 Block Public Access setting should be enabled at the bucket level](securityhub-standards-fsbp-controls.md#fsbp-s3-8)  
[\[SecretsManager\.3\] Remove unused Secrets Manager secrets](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-3)  
[\[SecretsManager\.4\] Secrets Manager secrets should be rotated within a specified number of days](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-4)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)

### AWS GovCloud \(US\-West\)<a name="securityhub-control-support-govuswest1"></a>

The following controls are not supported in AWS GovCloud \(US\-West\)\.

**[CIS AWS Foundations Benchmark standard](securityhub-standards-cis.md)**  
[1\.13 – Ensure MFA is enabled for the "root" account ](securityhub-cis-controls.md#securityhub-cis-controls-1.13)  
[1\.14 – Ensure hardware MFA is enabled for the "root" account ](securityhub-cis-controls.md#securityhub-cis-controls-1.14)

**[Payment Card Industry Data Security Standard \(PCI DSS\)](securityhub-standards-pcidss.md)**  
[\[PCI\.CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-pci-controls.md#pcidss-codebuild-1)  
[\[PCI\.CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-pci-controls.md#pcidss-codebuild-2)  
[\[PCI\.IAM\.4\] Hardware MFA should be enabled for the root user](securityhub-pci-controls.md#pcidss-iam-4)  
[\[PCI\.IAM\.5\] Virtual MFA should be enabled for the root user](securityhub-pci-controls.md#pcidss-iam-5)

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[APIGateway\.2\] API Gateway REST API stages should be configured to use SSL certificates for backend authentication](securityhub-standards-fsbp-controls.md#fsbp-apigateway-2)  
[\[APIGateway\.3\] API Gateway REST API stages should have AWS X\-Ray tracing enabled](securityhub-standards-fsbp-controls.md#fsbp-apigateway-3)  
[\[APIGateway\.4\] API Gateway should be associated with an AWS WAF web ACL](securityhub-standards-fsbp-controls.md#fsbp-apigateway-4)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CloudFront\.5\] CloudFront distributions should have logging enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-5)  
[\[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-6)  
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
[\[DynamoDB\.1\] DynamoDB tables should automatically scale capacity with demand](securityhub-standards-fsbp-controls.md#fsbp-dynamodb-1)  
[\[EC2\.15\] EC2 subnets should not automatically assign public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-ec2-15)  
[\[EC2\.16\] Unused network access control lists should be removed](securityhub-standards-fsbp-controls.md#fsbp-ec2-16)  
[\[EC2\.17\] EC2 instances should not use multiple ENIs](securityhub-standards-fsbp-controls.md#fsbp-ec2-17)  
[\[ECS\.1\] Amazon ECS task definitions should have secure networking modes and user definitions](securityhub-standards-fsbp-controls.md#fsbp-ecs-1)  
[\[EFS\.2\] Amazon EFS volumes should be in backup plans](securityhub-standards-fsbp-controls.md#fsbp-efs-2)  
[\[ElasticBeanstalk\.1\] Elastic Beanstalk environments should have enhanced health reporting enabled](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-1)  
[\[ElasticBeanstalk\.2\] Elastic Beanstalk managed platform updates should be enabled](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-2)  
[\[ES\.4\] Elasticsearch domain error logging to CloudWatch Logs should be enabled](securityhub-standards-fsbp-controls.md#fsbp-es-4)  
[\[IAM\.6\] Hardware MFA should be enabled for the root user](securityhub-standards-fsbp-controls.md#fsbp-iam-6)  
[\[IAM\.21\] IAM customer managed policies that you create should not allow wildcard actions for services](securityhub-standards-fsbp-controls.md#fsbp-iam-21)  
[\[RDS\.12\] IAM authentication should be configured for RDS clusters](securityhub-standards-fsbp-controls.md#fsbp-rds-12)  
[\[RDS\.13\] RDS automatic minor version upgrades should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-13)  
[\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-14)  
[\[RDS\.15\] RDS DB clusters should be configured for multiple Availability Zones](securityhub-standards-fsbp-controls.md#fsbp-rds-15)  
[\[Redshift\.7\] Amazon Redshift clusters should use enhanced VPC routing](securityhub-standards-fsbp-controls.md#fsbp-redshift-7)  
[\[S3\.8\] S3 Block Public Access setting should be enabled at the bucket level](securityhub-standards-fsbp-controls.md#fsbp-s3-8)  
[\[SecretsManager\.3\] Remove unused Secrets Manager secrets](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-3)  
[\[SecretsManager\.4\] Secrets Manager secrets should be rotated within a specified number of days](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-4)  
[\[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-waf-1)