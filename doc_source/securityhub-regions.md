# Supported Regions<a name="securityhub-regions"></a>

To view the Regions that AWS Security Hub is available in, see [Security Hub Service Endpoints](https://docs.aws.amazon.com/general/latest/gr/sechub.html)\.

## Integrations not supported in all Regions<a name="securityhub-regions-integration-support"></a>

Some integrations are not available in all Regions\. If an integration is not supported, it is not listed on the **Integrations** page\.

## Controls that are not supported in all Regions<a name="securityhub-regions-control-support"></a>

The following Regions do not support all of the Security Hub controls\. For each Region, the list provides the controls that are not supported\.

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
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
[\[DMS\.1\] Database Migration Service replication instances should not be public](securityhub-standards-fsbp-controls.md#fsbp-dms-1)  
[\[EC2\.1\] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone](securityhub-standards-fsbp-controls.md#fsbp-ec2-1)  
[\[EC2\.3\] Attached EBS volumes should be encrypted at\-rest](securityhub-standards-fsbp-controls.md#fsbp-ec2-3)  
[\[EC2\.4\] Stopped EC2 instances should be removed after a specified time period](securityhub-standards-fsbp-controls.md#fsbp-ec2-4)  
[\[EC2\.8\] EC2 instances should use IMDSv2](securityhub-standards-fsbp-controls.md#fsbp-ec2-8)  
[\[EFS\.1\] Amazon EFS should be configured to encrypt file data at\-rest using AWS KMS](securityhub-standards-fsbp-controls.md#fsbp-efs-1)  
[\[ELBv2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](securityhub-standards-fsbp-controls.md#fsbp-elbv2-1)  
[\[EMR\.1\] Amazon EMR cluster master nodes should not have public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-emr-1)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](securityhub-standards-fsbp-controls.md#fsbp-iam-3)  
[\[IAM\.4\] IAM root user access key should not exist](securityhub-standards-fsbp-controls.md#fsbp-iam-4)  
[\[RDS\.1\] RDS snapshots should be private](securityhub-standards-fsbp-controls.md#fsbp-rds-1)  
[\[S3\.1\] S3 Block Public Access setting should be enabled](securityhub-standards-fsbp-controls.md#fsbp-s3-1)  
[\[SageMaker\.1\] SageMaker notebook instances should not have direct internet access](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)  
[\[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)  
[\[SSM\.3\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT ](securityhub-standards-fsbp-controls.md#fsbp-ssm-3)

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
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
[\[DMS\.1\] Database Migration Service replication instances should not be public](securityhub-standards-fsbp-controls.md#fsbp-dms-1)  
[\[EC2\.1\] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone](securityhub-standards-fsbp-controls.md#fsbp-ec2-1)  
[\[EC2\.3\] Attached EBS volumes should be encrypted at\-rest](securityhub-standards-fsbp-controls.md#fsbp-ec2-3)  
[\[EC2\.4\] Stopped EC2 instances should be removed after a specified time period](securityhub-standards-fsbp-controls.md#fsbp-ec2-4)  
[\[EC2\.8\] EC2 instances should use IMDSv2](securityhub-standards-fsbp-controls.md#fsbp-ec2-8)  
[\[EFS\.1\] Amazon EFS should be configured to encrypt file data at\-rest using AWS KMS](securityhub-standards-fsbp-controls.md#fsbp-efs-1)  
[\[ELBv2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](securityhub-standards-fsbp-controls.md#fsbp-elbv2-1)  
[\[EMR\.1\] Amazon EMR cluster master nodes should not have public IP addresses](securityhub-standards-fsbp-controls.md#fsbp-emr-1)  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](securityhub-standards-fsbp-controls.md#fsbp-iam-3)  
[\[RDS\.1\] RDS snapshots should be private](securityhub-standards-fsbp-controls.md#fsbp-rds-1)  
[\[S3\.1\] S3 Block Public Access setting should be enabled](securityhub-standards-fsbp-controls.md#fsbp-s3-1)  
[\[SageMaker\.1\] SageMaker notebook instances should not have direct internet access](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)  
[\[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)  
[\[SSM\.3\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT ](securityhub-standards-fsbp-controls.md#fsbp-ssm-3)

### Middle East \(Bahrain\)<a name="securityhub-control-support-mesouth1"></a>

The following controls are not supported in Middle East \(Bahrain\)\.

**[Payment Card Industry Data Security Standard \(PCI DSS\)](securityhub-standards-pcidss.md)**  
[\[PCI\.GuardDuty\.1\] GuardDuty should be enabled](securityhub-pci-controls.md#pcidss-guardduty-1)  
[\[PCI\.S3\.6\] S3 Block Public Access setting should be enabled](securityhub-pci-controls.md#pcidss-s3-6)

**[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)**  
[\[GuardDuty\.1\] GuardDuty should be enabled](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  
[\[RDS\.7\] RDS clusters should have deletion protection enabled](securityhub-standards-fsbp-controls.md#fsbp-rds-7)  
[\[S3\.1\] S3 Block Public Access setting should be enabled](securityhub-standards-fsbp-controls.md#fsbp-s3-1)  
[\[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)

### South America \(São Paulo\)<a name="securityhub-control-support-sasouth1"></a>

The following controls are not supported in South America \(São Paulo\)\.

[AWS Foundational Security Best Practices standard](securityhub-standards-fsbp.md)  
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
[\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  
[\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  
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
[\[IAM\.6\] Hardware MFA should be enabled for the root user](securityhub-standards-fsbp-controls.md#fsbp-iam-6)