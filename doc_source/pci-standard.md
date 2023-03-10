# Payment Card Industry Data Security Standard \(PCI DSS\)<a name="pci-standard"></a>

The Payment Card Industry Data Security Standard \(PCI DSS\) in Security Hub provides a set of AWS security best practices for handling cardholder data\. You can use this standard to discover security vulnerabilities in resources that handle cardholder data\. Security Hub currently scopes the controls at the account level\. We recommend that you enable these controls in all of your accounts that have resources that store, process, or transmit cardholder data\. 

This standard was validated by AWS Security Assurance Services LLC \(AWS SAS\), which is a team of Qualified Security Assessors \(QSAs\) certified to provide PCI DSS guidance, and assessments by the PCI DSS Security Standards Council \(PCI SSC\)\. AWS SAS has confirmed that the automated checks can assist a customer in preparing for a PCI DSS assessment\. 

## Controls that apply to PCI DSS<a name="pci-controls"></a>

 [\[AutoScaling\.1\] Auto Scaling groups associated with a Classic Load Balancer should use load balancer health checks](autoscaling-controls.md#autoscaling-1) 

 [\[CloudTrail\.2\] CloudTrail should have encryption at\-rest enabled](cloudtrail-controls.md#cloudtrail-2) 

 [\[CloudTrail\.3\] CloudTrail should be enabled](cloudtrail-controls.md#cloudtrail-3) 

 [\[CloudTrail\.4\] CloudTrail log file validation should be enabled](cloudtrail-controls.md#cloudtrail-4) 

 [\[CloudTrail\.5\] CloudTrail trails should be integrated with Amazon CloudWatch Logs](cloudtrail-controls.md#cloudtrail-5) 

 [\[CloudWatch\.1\] A log metric filter and alarm should exist for usage of the "root" user](cloudwatch-controls.md#cloudwatch-1) 

 [\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](codebuild-controls.md#codebuild-1) 

 [\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](codebuild-controls.md#codebuild-2) 

 [\[Config\.1\] AWS Config should be enabled](config-controls.md#config-1) 

 [\[DMS\.1\] Database Migration Service replication instances should not be public](dms-controls.md#dms-1) 

 [\[EC2\.1\] Amazon EBS snapshots should not be publicly restorable](ec2-controls.md#ec2-1) 

 [\[EC2\.12\] Unused Amazon EC2 EIPs should be removed](ec2-controls.md#ec2-12) 

 [\[EC2\.13\] Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22](ec2-controls.md#ec2-13) 

 [\[EC2\.2\] The VPC default security group should not allow inbound and outbound traffic](ec2-controls.md#ec2-2) 

 [\[EC2\.6\] VPC flow logging should be enabled in all VPCs](ec2-controls.md#ec2-6) 

 [\[ELB\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](elb-controls.md#elb-1) 

 [\[ES\.1\] Elasticsearch domains should have encryption at\-rest enabled](es-controls.md#es-1) 

 [\[ES\.2\] Elasticsearch domains should be in a VPC](es-controls.md#es-2) 

 [\[GuardDuty\.1\] GuardDuty should be enabled](guardduty-controls.md#guardduty-1) 

 [\[IAM\.1\] IAM policies should not allow full "\*" administrative privileges](iam-controls.md#iam-1) 

 [\[IAM\.2\] IAM users should not have IAM policies attached](iam-controls.md#iam-2) 

 [\[IAM\.4\] IAM root user access key should not exist](iam-controls.md#iam-4) 

 [\[IAM\.6\] Hardware MFA should be enabled for the root user](iam-controls.md#iam-6) 

 [\[IAM\.8\] Unused IAM user credentials should be removed](iam-controls.md#iam-8) 

 [\[IAM\.9\] Virtual MFA should be enabled for the root user](iam-controls.md#iam-9) 

 [\[IAM\.10\] Password policies for IAM users should have strong AWS Configurations](iam-controls.md#iam-10) 

 [\[IAM\.19\] MFA should be enabled for all IAM users](iam-controls.md#iam-19) 

 [\[KMS\.4\] AWS KMS key rotation should be enabled](kms-controls.md#kms-4) 

 [\[Lambda\.1\] Lambda function policies should prohibit public access](lambda-controls.md#lambda-1) 

 [\[Lambda\.3\] Lambda functions should be in a VPC](lambda-controls.md#lambda-3) 

 [\[Opensearch\.1\] OpenSearch domains should have encryption at rest enabled](opensearch-controls.md#opensearch-1) 

 [\[Opensearch\.2\] OpenSearch domains should be in a VPC](opensearch-controls.md#opensearch-2) 

 [\[RDS\.1\] RDS snapshot should be private](rds-controls.md#rds-1) 

 [\[RDS\.2\] RDS DB Instances should prohibit public access, as determined by the PubliclyAccessible AWS Configuration](rds-controls.md#rds-2) 

 [\[Redshift\.1\] Amazon Redshift clusters should prohibit public access](redshift-controls.md#redshift-1) 

 [\[S3\.1\] S3 Block Public Access setting should be enabled](s3-controls.md#s3-1) 

 [\[S3\.2\] S3 buckets should prohibit public read access](s3-controls.md#s3-2) 

 [\[S3\.3\] S3 buckets should prohibit public write access](s3-controls.md#s3-3) 

 [\[S3\.4\] S3 buckets should have server\-side encryption enabled](s3-controls.md#s3-4) 

 [\[S3\.5\] S3 buckets should require requests to use Secure Socket Layer](s3-controls.md#s3-5) 

 [\[S3\.7\] S3 buckets should have cross\-Region replication enabled](s3-controls.md#s3-7) 

 [\[SageMaker\.1\] Amazon SageMaker notebook instances should not have direct internet access](sagemaker-controls.md#sagemaker-1) 

 [\[SSM\.1\] Amazon EC2 instances should be managed by AWS Systems Manager](ssm-controls.md#ssm-1) 

 [\[SSM\.2\] Amazon EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation](ssm-controls.md#ssm-2) 

 [\[SSM\.3\] Amazon EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT](ssm-controls.md#ssm-3) 