# AWS Foundational Security Best Practices \(FSBP\) standard<a name="fsbp-standard"></a>

The AWS Foundational Security Best Practices standard is a set of controls that detect when your AWS accounts and resources deviate from security best practices\. 

The standard lets you continuously evaluate all of your AWS accounts and workloads to quickly identify areas of deviation from best practices\. It provides actionable and prescriptive guidance about how to improve and maintain your organization’s security posture\.

 The controls include security best practices for resources from multiple AWS services\. Each control is also assigned a category that reflects the security function that it applies to\. For more information, see [Control categories](control-categories.md)\.

## Controls that apply to FSBP<a name="fsbp-controls"></a>

 [\[Account\.1\] Security contact information should be provided for an AWS account\.](account-controls.md#account-1) 

 [\[ACM\.1\] Imported and ACM\-issued certificates should be renewed after a specified time period](acm-controls.md#acm-1) 

 [\[APIGateway\.1\] API Gateway REST and WebSocket API execution logging should be enabled](apigateway-controls.md#apigateway-1) 

 [\[APIGateway\.2\] API Gateway REST API stages should be configured to use SSL certificates for backend authentication](apigateway-controls.md#apigateway-2) 

 [\[APIGateway\.3\] API Gateway REST API stages should have AWS X\-Ray tracing enabled](apigateway-controls.md#apigateway-3) 

 [\[APIGateway\.4\] API Gateway should be associated with a WAF Web ACL](apigateway-controls.md#apigateway-4) 

 [\[APIGateway\.5\] API Gateway REST API cache data should be encrypted at rest](apigateway-controls.md#apigateway-5) 

 [\[APIGateway\.8\] API Gateway routes should specify an authorization type](apigateway-controls.md#apigateway-8) 

 [\[APIGateway\.9\] Access logging should be configured for API Gateway V2 Stages](apigateway-controls.md#apigateway-9) 

 [\[AutoScaling\.1\] Auto Scaling groups associated with a Classic Load Balancer should use load balancer health checks](autoscaling-controls.md#autoscaling-1) 

 [\[AutoScaling\.2\] Amazon Amazon EC2 Auto Scaling group should cover multiple Availability Zones](autoscaling-controls.md#autoscaling-2) 

 [\[AutoScaling\.3\] Auto Scaling group launch AWS Configurations should AWS Configure Amazon EC2 instances to require Instance Metadata Service Version 2 \(IMDSv2\)](autoscaling-controls.md#autoscaling-3) 

 [\[AutoScaling\.4\] Auto Scaling group launch AWS Configuration should not have a metadata response hop limit greater than 1](autoscaling-controls.md#autoscaling-4) 

 [\[Autoscaling\.5\] Amazon Amazon EC2 instances launched using Auto Scaling group launch AWS Configurations should not have Public IP addresses](autoscaling-controls.md#autoscaling-5) 

 [\[AutoScaling\.6\] Auto Scaling groups should use multiple instance types in multiple Availability Zones](autoscaling-controls.md#autoscaling-6) 

 [\[AutoScaling\.9\] Amazon EC2 Auto Scaling groups should use Amazon EC2 launch templates](autoscaling-controls.md#autoscaling-9) 

 [\[CloudFormation\.1\] CloudFormation stacks should be integrated with Simple Notification Service \(SNS\)](cloudformation-controls.md#cloudformation-1) 

 [\[CloudFront\.1\] CloudFront distributions should have a default root object configured](cloudfront-controls.md#cloudfront-1) 

 [\[CloudFront\.2\] CloudFront distributions should have origin access identity enabled](cloudfront-controls.md#cloudfront-2) 

 [\[CloudFront\.3\] CloudFront distributions should require encryption in transit](cloudfront-controls.md#cloudfront-3) 

 [\[CloudFront\.4\] CloudFront distributions should have origin failover configured](cloudfront-controls.md#cloudfront-4) 

 [\[CloudFront\.5\] CloudFront distributions should have logging enabled](cloudfront-controls.md#cloudfront-5) 

 [\[CloudFront\.6\] CloudFront distributions should have WAF enabled](cloudfront-controls.md#cloudfront-6) 

 [\[CloudFront\.7\] CloudFront distributions should use custom SSL/TLS certificates](cloudfront-controls.md#cloudfront-7) 

 [\[CloudFront\.8\] CloudFront distributions should use SNI to serve HTTPS requests](cloudfront-controls.md#cloudfront-8) 

 [\[CloudFront\.9\] CloudFront distributions should encrypt traffic to custom origins](cloudfront-controls.md#cloudfront-9) 

 [\[CloudFront\.10\] CloudFront distributions should not use deprecated SSL protocols between edge locations and custom origins](cloudfront-controls.md#cloudfront-10) 

 [\[CloudFront\.12\] CloudFront distributions should not point to non\-existent S3 origins](cloudfront-controls.md#cloudfront-12) 

 [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1) 

 [\[CloudTrail\.2\] CloudTrail should have encryption at\-rest enabled](cloudtrail-controls.md#cloudtrail-2) 

 [\[CloudTrail\.4\] CloudTrail log file validation should be enabled](cloudtrail-controls.md#cloudtrail-4) 

 [\[CloudTrail\.5\] CloudTrail trails should be integrated with Amazon CloudWatch Logs](cloudtrail-controls.md#cloudtrail-5) 

 [\[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth](codebuild-controls.md#codebuild-1) 

 [\[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials](codebuild-controls.md#codebuild-2) 

 [\[CodeBuild\.3\] CodeBuild S3 logs should be encrypted](codebuild-controls.md#codebuild-3) 

 [\[CodeBuild\.4\] CodeBuild project environments should have a logging AWS Configuration](codebuild-controls.md#codebuild-4) 

 [\[CodeBuild\.5\] CodeBuild project environments should not have privileged mode enabled](codebuild-controls.md#codebuild-5) 

 [\[Config\.1\] AWS Config should be enabled](config-controls.md#config-1) 

 [\[DMS\.1\] Database Migration Service replication instances should not be public](dms-controls.md#dms-1) 

 [\[DynamoDB\.1\] DynamoDB tables should automatically scale capacity with demand](dynamodb-controls.md#dynamodb-1) 

 [\[DynamoDB\.2\] DynamoDB tables should have point\-in\-time recovery enabled](dynamodb-controls.md#dynamodb-2) 

 [\[DynamoDB\.3\] DynamoDB Accelerator \(DAX\) clusters should be encrypted at rest](dynamodb-controls.md#dynamodb-3) 

 [\[EC2\.1\] Amazon EBS snapshots should not be publicly restorable](ec2-controls.md#ec2-1) 

 [\[EC2\.2\] The VPC default security group should not allow inbound and outbound traffic](ec2-controls.md#ec2-2) 

 [\[EC2\.3\] Attached Amazon EBS volumes should be encrypted at\-rest](ec2-controls.md#ec2-3) 

 [\[EC2\.4\] Stopped Amazon EC2 instances should be removed after a specified time period](ec2-controls.md#ec2-4) 

 [\[EC2\.6\] VPC flow logging should be enabled in all VPCs](ec2-controls.md#ec2-6) 

 [\[EC2\.7\] Amazon EBS default encryption should be enabled](ec2-controls.md#ec2-7) 

 [\[EC2\.8\] Amazon EC2 instances should use Instance Metadata Service Version 2 \(IMDSv2\)](ec2-controls.md#ec2-8) 

 [\[EC2\.9\] Amazon EC2 instances should not have a public IPv4 address](ec2-controls.md#ec2-9) 

 [\[EC2\.10\] Amazon EC2 should be configured to use VPC endpoints that are created for the Amazon EC2 service](ec2-controls.md#ec2-10) 

 [\[EC2\.15\] Amazon EC2 subnets should not automatically assign public IP addresses](ec2-controls.md#ec2-15) 

 [\[EC2\.16\] Unused Network Access Control Lists should be removed](ec2-controls.md#ec2-16) 

 [\[EC2\.17\] Amazon EC2 instances should not use multiple ENIs](ec2-controls.md#ec2-17) 

 [\[EC2\.18\] Security groups should only allow unrestricted incoming traffic for authorized ports](ec2-controls.md#ec2-18) 

 [\[EC2\.19\] Security groups should not allow unrestricted access to ports with high risk](ec2-controls.md#ec2-19) 

 [\[EC2\.20\] Both VPN tunnels for an AWS Site\-to\-Site VPN connection should be up](ec2-controls.md#ec2-20) 

 [\[EC2\.21\] Network ACLs should not allow ingress from 0\.0\.0\.0/0 to port 22 or port 3389](ec2-controls.md#ec2-21) 

 [\[EC2\.22\] Unused Amazon EC2 security groups should be removed](ec2-controls.md#ec2-22) 

 [\[EC2\.23\] Amazon EC2 Transit Gateways should not automatically accept VPC attachment requests](ec2-controls.md#ec2-23) 

 [\[EC2\.24\] Amazon EC2 paravirtual instance types should not be used](ec2-controls.md#ec2-24) 

 [\[EC2\.25\] Amazon EC2 launch templates should not assign public IPs to network interfaces](ec2-controls.md#ec2-25) 

 [\[ECR\.1\] ECR private repositories should have image scanning configured](ecr-controls.md#ecr-1) 

 [\[ECR\.2\] ECR private repositories should have tag immutability configured](ecr-controls.md#ecr-2) 

 [\[ECR\.3\] ECR repositories should have at least one lifecycle policy configured](ecr-controls.md#ecr-3) 

 [\[ECS\.1\] Amazon ECS task definitions should have secure networking modes and user definitions\.](ecs-controls.md#ecs-1) 

 [\[ECS\.2\] ECS services should not have public IP addresses assigned to them automatically](ecs-controls.md#ecs-2) 

 [\[ECS\.3\] ECS task definitions should not share the host's process namespace](ecs-controls.md#ecs-3) 

 [\[ECS\.4\] ECS containers should run as non\-privileged](ecs-controls.md#ecs-4) 

 [\[ECS\.5\] ECS containers should be limited to read\-only access to root filesystems](ecs-controls.md#ecs-5) 

 [\[ECS\.8\] Secrets should not be passed as container environment variables](ecs-controls.md#ecs-8) 

 [\[ECS\.10\] ECS Fargate services should run on the latest Fargate platform version](ecs-controls.md#ecs-10) 

 [\[ECS\.12\] ECS clusters should use Container Insights](ecs-controls.md#ecs-12) 

 [\[EFS\.1\] Elastic File System should be configured to encrypt file data at\-rest using AWS KMS](efs-controls.md#efs-1) 

 [\[EFS\.2\] Amazon EFS volumes should be in backup plans](efs-controls.md#efs-2) 

 [\[EFS\.3\] EFS access points should enforce a root directory](efs-controls.md#efs-3) 

 [\[EFS\.4\] EFS access points should enforce a user identity](efs-controls.md#efs-4) 

 [\[EKS\.2\] EKS clusters should run on a supported Kubernetes version](eks-controls.md#eks-2) 

 [\[ElastiCache\.1\] ElastiCache for Redis clusters should have automatic backups scheduled](elasticache-controls.md#elasticache-1) 

 [\[ElastiCache\.2\] Minor version upgrades should be automatically applied to ElastiCache for Redis cache clusters](elasticache-controls.md#elasticache-2) 

 [\[ElastiCache\.3\] ElastiCache for Redis replication groups should have automatic failover enabled](elasticache-controls.md#elasticache-3) 

 [\[ElastiCache\.4\] ElastiCache for Redis replication groups should be encrypted at rest](elasticache-controls.md#elasticache-4) 

 [\[ElastiCache\.5\] ElastiCache for Redis replication groups should be encrypted in transit](elasticache-controls.md#elasticache-5) 

 [\[ElastiCache\.6\] ElastiCache for Redis replication groups before version 6\.0 should use Redis AUTH](elasticache-controls.md#elasticache-6) 

 [\[ElastiCache\.7\] ElastiCache clusters should not use the default subnet group](elasticache-controls.md#elasticache-7) 

 [\[ElasticBeanstalk\.1\] Elastic Beanstalk environments should have enhanced health reporting enabled](elasticbeanstalk-controls.md#elasticbeanstalk-1) 

 [\[ElasticBeanstalk\.2\] Elastic Beanstalk managed platform updates should be enabled](elasticbeanstalk-controls.md#elasticbeanstalk-2) 

 [\[ELB\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS](elb-controls.md#elb-1) 

 [\[ELB\.2\] Classic Load Balancers with SSL/HTTPS listeners should use a certificate provided by AWS Certificate Manager](elb-controls.md#elb-2) 

 [\[ELB\.3\] Classic Load Balancer listeners should be configured with HTTPS or TLS termination](elb-controls.md#elb-3) 

 [\[ELB\.4\] Application Load Balancer should be configured to drop http headers](elb-controls.md#elb-4) 

 [\[ELB\.5\] Application and Classic Load Balancers logging should be enabled](elb-controls.md#elb-5) 

 [\[ELB\.6\] Application Load Balancer deletion protection should be enabled](elb-controls.md#elb-6) 

 [\[ELB\.7\] Classic Load Balancers should have connection draining enabled](elb-controls.md#elb-7) 

 [\[ELB\.8\] Classic Load Balancers with SSL listeners should use a predefined security policy that has strong AWS Configuration](elb-controls.md#elb-8) 

 [\[ELB\.9\] Classic Load Balancers should have cross\-zone load balancing enabled](elb-controls.md#elb-9) 

 [\[ELB\.10\] Classic Load Balancer should span multiple Availability Zones](elb-controls.md#elb-10) 

 [\[ELB\.12\] Application Load Balancer should be configured with defensive or strictest desync mitigation mode](elb-controls.md#elb-12) 

 [\[ELB\.13\] Application, Network and Gateway Load Balancers should span multiple Availability Zones](elb-controls.md#elb-13) 

 [\[ELB\.14\] Classic Load Balancer should be configured with defensive or strictest desync mitigation mode](elb-controls.md#elb-14) 

 [\[EMR\.1\] Amazon Elastic MapReduce cluster master nodes should not have public IP addresses](emr-controls.md#emr-1) 

 [\[ES\.1\] Elasticsearch domains should have encryption at\-rest enabled](es-controls.md#es-1) 

 [\[ES\.2\] Elasticsearch domains should be in a VPC](es-controls.md#es-2) 

 [\[ES\.3\] Elasticsearch domains should encrypt data sent between nodes](es-controls.md#es-3) 

 [\[ES\.4\] Elasticsearch domain error logging to CloudWatch Logs should be enabled](es-controls.md#es-4) 

 [\[ES\.5\] Elasticsearch domains should have audit logging enabled](es-controls.md#es-5) 

 [\[ES\.6\] Elasticsearch domains should have at least three data nodes](es-controls.md#es-6) 

 [\[ES\.7\] Elasticsearch domains should be configured with at least three dedicated master nodes](es-controls.md#es-7) 

 [\[ES\.8\] Connections to Elasticsearch domains should be encrypted using TLS 1\.2](es-controls.md#es-8) 

 [\[GuardDuty\.1\] GuardDuty should be enabled](guardduty-controls.md#guardduty-1) 

 [\[IAM\.1\] IAM policies should not allow full "\*" administrative privileges](iam-controls.md#iam-1) 

 [\[IAM\.2\] IAM users should not have IAM policies attached](iam-controls.md#iam-2) 

 [\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](iam-controls.md#iam-3) 

 [\[IAM\.4\] IAM root user access key should not exist](iam-controls.md#iam-4) 

 [\[IAM\.5\] MFA should be enabled for all IAM users that have a console password](iam-controls.md#iam-5) 

 [\[IAM\.6\] Hardware MFA should be enabled for the root user](iam-controls.md#iam-6) 

 [\[IAM\.7\] Password policies for IAM users should have strong AWS Configurations](iam-controls.md#iam-7) 

 [\[IAM\.8\] Unused IAM user credentials should be removed](iam-controls.md#iam-8) 

 [\[IAM\.21\] IAM customer managed policies that you create should not allow wildcard actions for services](iam-controls.md#iam-21) 

 [\[Kinesis\.1\] Kinesis streams should be encrypted at rest](kinesis-controls.md#kinesis-1) 

 [\[KMS\.1\] IAM customer managed policies should not allow decryption actions on all KMS keys](kms-controls.md#kms-1) 

 [\[KMS\.2\] IAM principals should not have IAM inline policies that allow decryption actions on all KMS keys](kms-controls.md#kms-2) 

 [\[KMS\.3\] AWS KMS keys should not be deleted unintentionally](kms-controls.md#kms-3) 

 [\[Lambda\.1\] Lambda function policies should prohibit public access](lambda-controls.md#lambda-1) 

 [\[Lambda\.2\] Lambda functions should use supported runtimes](lambda-controls.md#lambda-2) 

 [\[Lambda\.5\] VPC Lambda functions should operate in more than one Availability Zone](lambda-controls.md#lambda-5) 

 [\[NetworkFirewall\.3\] Network Firewall policies should have at least one rule group associated](networkfirewall-controls.md#networkfirewall-3) 

 [\[NetworkFirewall\.4\] The default stateless action for Network Firewall policies should be drop or forward for full packets](networkfirewall-controls.md#networkfirewall-4) 

 [\[NetworkFirewall\.5\] The default stateless action for Network Firewall policies should be drop or forward for fragmented packets](networkfirewall-controls.md#networkfirewall-5) 

 [\[NetworkFirewall\.6\] Stateless Network Firewall rule group should not be empty](networkfirewall-controls.md#networkfirewall-6) 

 [\[Opensearch\.1\] OpenSearch domains should have encryption at rest enabled](opensearch-controls.md#opensearch-1) 

 [\[Opensearch\.2\] OpenSearch domains should be in a VPC](opensearch-controls.md#opensearch-2) 

 [\[Opensearch\.3\] OpenSearch domains should encrypt data sent between nodes](opensearch-controls.md#opensearch-3) 

 [\[Opensearch\.4\] OpenSearch domain error logging to CloudWatch Logs should be enabled](opensearch-controls.md#opensearch-4) 

 [\[Opensearch\.5\] OpenSearch domains should have audit logging enabled](opensearch-controls.md#opensearch-5) 

 [\[Opensearch\.6\] OpenSearch domains should have at least three data nodes](opensearch-controls.md#opensearch-6) 

 [\[Opensearch\.7\] OpenSearch domains should have fine\-grained access control enabled](opensearch-controls.md#opensearch-7) 

 [\[Opensearch\.8\] Connections to OpenSearch domains should be encrypted using TLS 1\.2](opensearch-controls.md#opensearch-8) 

 [\[RDS\.1\] RDS snapshot should be private](rds-controls.md#rds-1) 

 [\[RDS\.2\] RDS DB Instances should prohibit public access, as determined by the PubliclyAccessible AWS Configuration](rds-controls.md#rds-2) 

 [\[RDS\.3\] RDS DB instances should have encryption at\-rest enabled](rds-controls.md#rds-3) 

 [\[RDS\.4\] RDS cluster snapshots and database snapshots should be encrypted at rest](rds-controls.md#rds-4) 

 [\[RDS\.5\] RDS DB instances should be configured with multiple Availability Zones](rds-controls.md#rds-5) 

 [\[RDS\.6\] Enhanced monitoring should be configured for RDS DB instances](rds-controls.md#rds-6) 

 [\[RDS\.7\] RDS clusters should have deletion protection enabled](rds-controls.md#rds-7) 

 [\[RDS\.8\] RDS DB instances should have deletion protection enabled](rds-controls.md#rds-8) 

 [\[RDS\.9\] Database logging should be enabled](rds-controls.md#rds-9) 

 [\[RDS\.10\] IAM authentication should be configured for RDS instances](rds-controls.md#rds-10) 

 [\[RDS\.11\] RDS instances should have automatic backups enabled](rds-controls.md#rds-11) 

 [\[RDS\.12\] IAM authentication should be configured for RDS clusters](rds-controls.md#rds-12) 

 [\[RDS\.13\] RDS automatic minor version upgrades should be enabled](rds-controls.md#rds-13) 

 [\[RDS\.14\] Amazon Aurora clusters should have backtracking enabled](rds-controls.md#rds-14) 

 [\[RDS\.15\] RDS DB clusters should be configured for multiple Availability Zones](rds-controls.md#rds-15) 

 [\[RDS\.16\] RDS DB clusters should be configured to copy tags to snapshots](rds-controls.md#rds-16) 

 [\[RDS\.17\] RDS DB instances should be configured to copy tags to snapshots](rds-controls.md#rds-17) 

 [\[RDS\.18\] RDS instances should be deployed in a VPC](rds-controls.md#rds-18) 

 [\[RDS\.19\] An RDS event notifications subscription should be configured for critical cluster events](rds-controls.md#rds-19) 

 [\[RDS\.20\] An RDS event notifications subscription should be configured for critical database instance events](rds-controls.md#rds-20) 

 [\[RDS\.21\] An RDS event notifications subscription should be configured for critical database parameter group events](rds-controls.md#rds-21) 

 [\[RDS\.22\] An RDS event notifications subscription should be configured for critical database security group events](rds-controls.md#rds-22) 

 [\[RDS\.23\] RDS instances should not use a database engine default port](rds-controls.md#rds-23) 

 [\[RDS\.24\] RDS Database clusters should use a custom administrator username](rds-controls.md#rds-24) 

 [\[RDS\.25\] RDS database instances should use a custom administrator username](rds-controls.md#rds-25) 

 [\[Redshift\.1\] Amazon Redshift clusters should prohibit public access](redshift-controls.md#redshift-1) 

 [\[Redshift\.2\] Connections to Amazon Redshift clusters should be encrypted in transit](redshift-controls.md#redshift-2) 

 [\[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled](redshift-controls.md#redshift-3) 

 [\[Redshift\.4\] Amazon Redshift clusters should have audit logging enabled](redshift-controls.md#redshift-4) 

 [\[Redshift\.6\] Amazon Redshift should have automatic upgrades to major versions enabled](redshift-controls.md#redshift-6) 

 [\[Redshift\.7\] Redshift clusters should use enhanced VPC routing](redshift-controls.md#redshift-7) 

 [\[Redshift\.8\] Amazon Redshift clusters should not use the default Admin username](redshift-controls.md#redshift-8) 

 [\[Redshift\.9\] Redshift clusters should not use the default database name](redshift-controls.md#redshift-9) 

 [\[S3\.1\] S3 Block Public Access setting should be enabled](s3-controls.md#s3-1) 

 [\[S3\.2\] S3 buckets should prohibit public read access](s3-controls.md#s3-2) 

 [\[S3\.3\] S3 buckets should prohibit public write access](s3-controls.md#s3-3) 

 [\[S3\.4\] S3 buckets should have server\-side encryption enabled](s3-controls.md#s3-4) 

 [\[S3\.5\] S3 buckets should require requests to use Secure Socket Layer](s3-controls.md#s3-5) 

 [\[S3\.6\] S3 permissions granted to other AWS accounts in bucket policies should be restricted](s3-controls.md#s3-6) 

 [\[S3\.8\] S3 Block Public Access setting should be enabled at the bucket\-level](s3-controls.md#s3-8) 

 [\[S3\.9\] S3 bucket server access logging should be enabled](s3-controls.md#s3-9) 

 [\[S3\.10\] S3 buckets with versioning enabled should have lifecycle policies configured](s3-controls.md#s3-10) 

 [\[S3\.11\] S3 buckets should have event notifications enabled](s3-controls.md#s3-11) 

 [\[S3\.12\] S3 access control lists \(ACLs\) should not be used to manage user access to buckets](s3-controls.md#s3-12) 

 [\[S3\.13\] S3 buckets should have lifecycle policies configured](s3-controls.md#s3-13) 

 [\[SageMaker\.1\] Amazon SageMaker notebook instances should not have direct internet access](sagemaker-controls.md#sagemaker-1) 

 [\[SageMaker\.2\] SageMaker notebook instances should be launched in a custom VPC](sagemaker-controls.md#sagemaker-2) 

 [\[SageMaker\.3\] Users should not have root access to SageMaker notebook instances](sagemaker-controls.md#sagemaker-3) 

 [\[SecretsManager\.1\] Secrets Manager secrets should have automatic rotation enabled](secretsmanager-controls.md#secretsmanager-1) 

 [\[SecretsManager\.2\] Secrets Manager secrets configured with automatic rotation should rotate successfully](secretsmanager-controls.md#secretsmanager-2) 

 [\[SecretsManager\.3\] Remove unused Secrets Manager secrets](secretsmanager-controls.md#secretsmanager-3) 

 [\[SecretsManager\.4\] Secrets Manager secrets should be rotated within a specified number of days](secretsmanager-controls.md#secretsmanager-4) 

 [\[SNS\.1\] SNS topics should be encrypted at\-rest using AWS KMS](sns-controls.md#sns-1) 

 [\[SNS\.2\] Logging of delivery status should be enabled for notification messages sent to a topic](sns-controls.md#sns-2) 

 [\[SQS\.1\] Amazon SQS queues should be encrypted at rest](sqs-controls.md#sqs-1) 

 [\[SSM\.1\] Amazon EC2 instances should be managed by AWS Systems Manager](ssm-controls.md#ssm-1) 

 [\[SSM\.2\] Amazon EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation](ssm-controls.md#ssm-2) 

 [\[SSM\.3\] Amazon EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT](ssm-controls.md#ssm-3) 

 [\[SSM\.4\] SSM documents should not be public](ssm-controls.md#ssm-4) 

 [\[WAF\.1\] AWS WAF Classic Global Web ACL logging should be enabled](waf-controls.md#waf-1) 

 [\[WAF\.2\] A WAF Regional rule should have at least one condition](waf-controls.md#waf-2) 

 [\[WAF\.3\] A WAF Regional rule group should have at least one rule](waf-controls.md#waf-3) 

 [\[WAF\.4\] A WAF Regional web ACL should have at least one rule or rule group](waf-controls.md#waf-4) 

 [\[WAF\.6\] A WAF global rule should have at least one condition](waf-controls.md#waf-6) 

 [\[WAF\.7\] A WAF global rule group should have at least one rule](waf-controls.md#waf-7) 

 [\[WAF\.8\] A WAF global web ACL should have at least one rule or rule group](waf-controls.md#waf-8) 

 [\[WAF\.10\] A WAFV2 web ACL should have at least one rule or rule group](waf-controls.md#waf-10) 