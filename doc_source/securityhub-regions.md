# Supported Regions<a name="securityhub-regions"></a>

To view the Regions that AWS Security Hub is available in, see [Security Hub Service Endpoints](https://docs.aws.amazon.com/general/latest/gr/sechub.html)\.

## AWS Organizations integration not supported in all Regions<a name="securityhub-regions-orgs-support"></a>

The China \(Beijing\) and China \(Ningxia\) Regions do not support the Security Hub integration with Organizations\.

## Integrations not supported in all Regions<a name="securityhub-regions-integration-support"></a>

Some integrations are not available in all Regions\. If an integration is not supported, it is not listed on the **Integrations** page\.

The China \(Beijing\) and China \(Ningxia\) Regions only support the following integrations with AWS services:
+ Amazon GuardDuty
+ IAM Access Analyzer
+ Systems Manager Patch Manager

The China \(Beijing\) and China \(Ningxia\) Regions only support the following third\-party integrations:
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

## Controls that are not supported in all Regions<a name="securityhub-regions-control-support"></a>

The following Regions do not support all of the Security Hub controls\. For each Region, the list provides the controls that are not supported\.

### US East \(Ohio\)<a name="securityhub-control-support-useast2"></a>

The following controls are not supported in US East \(Ohio\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

### US West \(N\. California\)<a name="securityhub-control-support-uswest1"></a>

The following controls are not supported in US West \(N\. California\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

### US West \(Oregon\)<a name="securityhub-control-support-uswest2"></a>

The following controls are not supported in US West \(Oregon\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

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
[\[PCI\.EC2\.3\] Unused EC2 security groups should be removed](securityhub-pci-controls.md#pcidss-ec2-3)  
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
[\[APIGateway\.1\] API Gateway REST and HTTP API logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-apigateway-1)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
[\[DMS\.1\] Database Migration Service replication instances should not be public](securityhub-standards-fsbp-controls.md#fsbp-dms-1)  
[\[EC2\.1\] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone](securityhub-standards-fsbp-controls.md#fsbp-ec2-1)  
[\[EC2\.3\] Attached EBS volumes should be encrypted at\-rest](securityhub-standards-fsbp-controls.md#fsbp-ec2-3)  
[\[EC2\.4\] Stopped EC2 instances should be removed after a specified time period](securityhub-standards-fsbp-controls.md#fsbp-ec2-4)  
[\[EC2\.8\] EC2 instances should use IMDSv2](securityhub-standards-fsbp-controls.md#fsbp-ec2-8)  
[\[EFS\.1\] Amazon EFS should be configured to encrypt file data at rest using AWS KMS](securityhub-standards-fsbp-controls.md#fsbp-efs-1)  
[\[EFS\.2\] Amazon EFS volumes should be in backup plans](securityhub-standards-fsbp-controls.md#fsbp-efs-2)  
[\[ELB\.4\] Application load balancers should be configured to drop HTTP headers](securityhub-standards-fsbp-controls.md#fsbp-elb-4)  
[\[ELBv2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](securityhub-standards-fsbp-controls.md#fsbp-elbv2-1)  
[\[EMR\.1\] Amazon EMR cluster master nodes should not have public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-emr-1)  
[\[ES\.3\] Amazon Elasticsearch Service domains should encrypt data sent between nodes](securityhub-standards-fsbp-controls.md#fsbp-es-3)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](securityhub-standards-fsbp-controls.md#fsbp-iam-3)  
[\[IAM\.4\] IAM root user access key should not exist](securityhub-standards-fsbp-controls.md#fsbp-iam-4)  
[\[RDS\.1\] RDS snapshots should be private](securityhub-standards-fsbp-controls.md#fsbp-rds-1)  
[\[RDS\.9\] Database logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-9)  
[\[RDS\.10\] IAM authentication should be configured for RDS instances](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  
[\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)  
[\[S3\.1\] S3 Block Public Access setting should be enabled](securityhub-standards-fsbp-controls.md#fsbp-s3-1)  
[\[SageMaker\.1\] SageMaker notebook instances should not have direct internet access](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)  
[\[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)  
[\[SSM\.3\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT ](securityhub-standards-fsbp-controls.md#fsbp-ssm-3)

### Asia Pacific \(Hong Kong\)<a name="securityhub-control-support-apeast1"></a>

The following controls are not supported in Asia Pacific \(Hong Kong\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[RDS\.10\] IAM authentication should be configured for RDS instances](securityhub-standards-fsbp-controls.md#fsbp-rds-10)

### Asia Pacific \(Mumbai\)<a name="securityhub-control-support-apsouth1"></a>

The following controls are not supported in Asia Pacific \(Mumbai\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

### Asia Pacific \(Osaka\)<a name="securityhub-control-support-apnortheast3"></a>

The following controls are not supported in Asia Pacific \(Osaka\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[ELB\.4\] Application load balancers should be configured to drop HTTP headers](securityhub-standards-fsbp-controls.md#fsbp-elb-4)  
[\[RDS\.9\] Database logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-9)  
[\[RDS\.10\] IAM authentication should be configured for RDS instances](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  
[\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)

### Asia Pacific \(Seoul\)<a name="securityhub-control-support-apnortheast2"></a>

The following controls are not supported in Asia Pacific \(Seoul\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

### Asia Pacific \(Singapore\)<a name="securityhub-control-support-apsoutheast1"></a>

The following controls are not supported in Asia Pacific \(Singapore\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

### Asia Pacific \(Sydney\)<a name="securityhub-control-support-apsoutheast2"></a>

The following controls are not supported in Asia Pacific \(Sydney\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)

### Asia Pacific \(Tokyo\)<a name="securityhub-control-support-apnortheast1"></a>

The following controls are not supported in Asia Pacific \(Tokyo\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

### Canada \(Central\)<a name="securityhub-control-support-cacentral1"></a>

The following controls are not supported in Canada \(Central\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

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
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[ES\.3\] Amazon Elasticsearch Service domains should encrypt data sent between nodes](securityhub-standards-fsbp-controls.md#fsbp-es-3)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.6\] Hardware MFA should be enabled for the root user](securityhub-standards-fsbp-controls.md#fsbp-iam-6)  
[\[Lambda\.1\] Lambda function policies should prohibit public access](securityhub-standards-fsbp-controls.md#fsbp-lambda-1)  
[\[Lambda\.2\] Lambda functions should use latest runtimes](securityhub-standards-fsbp-controls.md#fsbp-lambda-2)  
[\[RDS\.7\] RDS clusters should have deletion protection enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-7)  
[\[RDS\.10\] IAM authentication should be configured for RDS instances](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  
[\[SageMaker\.1\] SageMaker notebook instances should not have direct internet access](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)

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
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[ES\.3\] Amazon Elasticsearch Service domains should encrypt data sent between nodes](securityhub-standards-fsbp-controls.md#fsbp-es-3)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.6\] Hardware MFA should be enabled for the root user](securityhub-standards-fsbp-controls.md#fsbp-iam-6)  
[\[Lambda\.1\] Lambda function policies should prohibit public access](securityhub-standards-fsbp-controls.md#fsbp-lambda-1)  
[\[Lambda\.2\] Lambda functions should use latest runtimes](securityhub-standards-fsbp-controls.md#fsbp-lambda-2)  
[\[RDS\.7\] RDS clusters should have deletion protection enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-7)  
[\[RDS\.9\] Database logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-9)  
[\[RDS\.10\] IAM authentication should be configured for RDS instances](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  
[\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)  
[\[SageMaker\.1\] SageMaker notebook instances should not have direct internet access](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)

### Europe \(Frankfurt\)<a name="securityhub-control-support-eucentral1"></a>

The following controls are not supported in Europe \(Frankfurt\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

### Europe \(Ireland\)<a name="securityhub-control-support-euwest1"></a>

The following controls are not supported in Europe \(Ireland\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

### Europe \(London\)<a name="securityhub-control-support-euwest2"></a>

The following controls are not supported in Europe \(London\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

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
[\[PCI\.EC2\.3\] Unused EC2 security groups should be removed](securityhub-pci-controls.md#pcidss-ec2-3)  
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
[\[APIGateway\.1\] API Gateway REST and HTTP API logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-apigateway-1)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
[\[DMS\.1\] Database Migration Service replication instances should not be public](securityhub-standards-fsbp-controls.md#fsbp-dms-1)  
[\[EC2\.1\] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone](securityhub-standards-fsbp-controls.md#fsbp-ec2-1)  
[\[EC2\.3\] Attached EBS volumes should be encrypted at\-rest](securityhub-standards-fsbp-controls.md#fsbp-ec2-3)  
[\[EC2\.4\] Stopped EC2 instances should be removed after a specified time period](securityhub-standards-fsbp-controls.md#fsbp-ec2-4)  
[\[EC2\.8\] EC2 instances should use IMDSv2](securityhub-standards-fsbp-controls.md#fsbp-ec2-8)  
[\[EFS\.1\] Amazon EFS should be configured to encrypt file data at rest using AWS KMS](securityhub-standards-fsbp-controls.md#fsbp-efs-1)  
[\[EFS\.2\] Amazon EFS volumes should be in backup plans](securityhub-standards-fsbp-controls.md#fsbp-efs-2)  
[\[ELB\.4\] Application load balancers should be configured to drop HTTP headers](securityhub-standards-fsbp-controls.md#fsbp-elb-4)  
[\[ELBv2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](securityhub-standards-fsbp-controls.md#fsbp-elbv2-1)  
[\[EMR\.1\] Amazon EMR cluster master nodes should not have public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-emr-1)  
[\[ES\.3\] Amazon Elasticsearch Service domains should encrypt data sent between nodes](securityhub-standards-fsbp-controls.md#fsbp-es-3)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](securityhub-standards-fsbp-controls.md#fsbp-iam-3)  
[\[KMS\.3\] AWS KMS keys should not be unintentionally deleted](securityhub-standards-fsbp-controls.md#fsbp-kms-3)  
[\[RDS\.1\] RDS snapshots should be private](securityhub-standards-fsbp-controls.md#fsbp-rds-1)  
[\[RDS\.9\] Database logging should be enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-9)  
[\[Redshift\.2\] Connections to Amazon Redshift clusters should be encrypted in transit](securityhub-standards-fsbp-controls.md#fsbp-redshift-2)  
[\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)  
[\[S3\.1\] S3 Block Public Access setting should be enabled](securityhub-standards-fsbp-controls.md#fsbp-s3-1)  
[\[SageMaker\.1\] SageMaker notebook instances should not have direct internet access](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)  
[\[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)  
[\[SSM\.3\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT ](securityhub-standards-fsbp-controls.md#fsbp-ssm-3)

### Europe \(Paris\)<a name="securityhub-control-support-euwest3"></a>

The following controls are not supported in Europe \(Paris\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

### Europe \(Stockholm\)<a name="securityhub-control-support-eunorth1"></a>

The following controls are not supported in Europe \(Stockholm\)\.

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)

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
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[RDS\.7\] RDS clusters should have deletion protection enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-7)  
[\[Redshift\.6\] Amazon Redshift should have automatic upgrades to major versions enabled](securityhub-standards-fsbp-controls.md#fsbp-redshift-6)  
[\[S3\.1\] S3 Block Public Access setting should be enabled](securityhub-standards-fsbp-controls.md#fsbp-s3-1)  
[\[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)

### South America \(São Paulo\)<a name="securityhub-control-support-sasouth1"></a>

The following controls are not supported in South America \(São Paulo\)\.

[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)  
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[RDS\.7\] RDS clusters should have deletion protection enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-7)

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
[\[CloudFront\.1\] CloudFront distributions should have a default root object configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-1)  
[\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-2)  
[\[CloudFront\.3\] CloudFront distributions should require encryption in transit](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-3)  
[\[CloudFront\.4\] CloudFront distributions should have origin failover configured](securityhub-standards-fsbp-controls.md#fsbp-cloudfront-4)  
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
[\[DynamoDB\.1\] DynamoDB tables should automatically scale capacity with demand](securityhub-standards-fsbp-controls.md#fsbp-dynamodb-1)  
[\[EFS\.2\] Amazon EFS volumes should be in backup plans](securityhub-standards-fsbp-controls.md#fsbp-efs-2)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.6\] Hardware MFA should be enabled for the root user](securityhub-standards-fsbp-controls.md#fsbp-iam-6)

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
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
[\[EFS\.2\] Amazon EFS volumes should be in backup plans](securityhub-standards-fsbp-controls.md#fsbp-efs-2)  
[\[IAM\.6\] Hardware MFA should be enabled for the root user](securityhub-standards-fsbp-controls.md#fsbp-iam-6)