# Center for Internet Security \(CIS\) AWS Foundations Benchmark v1\.2\.0 and v1\.4\.0<a name="cis-aws-foundations-benchmark"></a>

The CIS AWS Foundations Benchmark serves as a set of security configuration best practices for AWS\. These industry\-accepted best practices provide you with clear, step\-by\-step implementation and assessment procedures\. Ranging from operating systems to cloud services and network devices, the controls in this benchmark help you protect the specific systems that your organization uses\. 

AWS Security Hub supports CIS AWS Foundations Benchmark v1\.2\.0 and v1\.4\.0\.



## Center for Internet Security \(CIS\) AWS Foundations Benchmark v1\.2\.0<a name="cis1v2-standard"></a>

Security Hub has satisfied the requirements of CIS Security Software Certification and has been awarded CIS Security Software Certification for the following CIS Benchmarks: 
+ CIS Benchmark for CIS AWS Foundations Benchmark, v1\.2\.0, Level 1
+ CIS Benchmark for CIS AWS Foundations Benchmark, v1\.2\.0, Level 2

### Controls that apply to CIS AWS Foundations Benchmark v1\.2\.0<a name="cis1v2-controls"></a>

 [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1) 

 [\[CloudTrail\.2\] CloudTrail should have encryption at\-rest enabled](cloudtrail-controls.md#cloudtrail-2) 

 [\[CloudTrail\.4\] CloudTrail log file validation should be enabled](cloudtrail-controls.md#cloudtrail-4) 

 [\[CloudTrail\.5\] CloudTrail trails should be integrated with Amazon CloudWatch Logs](cloudtrail-controls.md#cloudtrail-5) 

 [\[CloudTrail\.6\] Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible](cloudtrail-controls.md#cloudtrail-6) 

 [\[CloudTrail\.7\] Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket](cloudtrail-controls.md#cloudtrail-7) 

 [\[CloudWatch\.1\] A log metric filter and alarm should exist for usage of the "root" user](cloudwatch-controls.md#cloudwatch-1) 

 [\[CloudWatch\.2\] Ensure a log metric filter and alarm exist for unauthorized API calls](cloudwatch-controls.md#cloudwatch-2) 

 [\[CloudWatch\.3\] Ensure a log metric filter and alarm exist for Management Console sign\-in without MFA](cloudwatch-controls.md#cloudwatch-3) 

 [\[CloudWatch\.4\] Ensure a log metric filter and alarm exist for IAM policy changes](cloudwatch-controls.md#cloudwatch-4) 

 [\[CloudWatch\.5\] Ensure a log metric filter and alarm exist for CloudTrail AWS Configuration changes](cloudwatch-controls.md#cloudwatch-5) 

 [\[CloudWatch\.6\] Ensure a log metric filter and alarm exist for AWS Management Console authentication failures](cloudwatch-controls.md#cloudwatch-6) 

 [\[CloudWatch\.7\] Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer managed keys](cloudwatch-controls.md#cloudwatch-7) 

 [\[CloudWatch\.8\] Ensure a log metric filter and alarm exist for S3 bucket policy changes](cloudwatch-controls.md#cloudwatch-8) 

 [\[CloudWatch\.9\] Ensure a log metric filter and alarm exist for AWS Config configuration changes](cloudwatch-controls.md#cloudwatch-9) 

 [\[CloudWatch\.10\] Ensure a log metric filter and alarm exist for security group changes](cloudwatch-controls.md#cloudwatch-10) 

 [\[CloudWatch\.11\] Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)](cloudwatch-controls.md#cloudwatch-11) 

 [\[CloudWatch\.12\] Ensure a log metric filter and alarm exist for changes to network gateways](cloudwatch-controls.md#cloudwatch-12) 

 [\[CloudWatch\.13\] Ensure a log metric filter and alarm exist for route table changes](cloudwatch-controls.md#cloudwatch-13) 

 [\[CloudWatch\.14\] Ensure a log metric filter and alarm exist for VPC changes](cloudwatch-controls.md#cloudwatch-14) 

 [\[Config\.1\] AWS Config should be enabled](config-controls.md#config-1) 

 [\[EC2\.2\] The VPC default security group should not allow inbound and outbound traffic](ec2-controls.md#ec2-2) 

 [\[EC2\.6\] VPC flow logging should be enabled in all VPCs](ec2-controls.md#ec2-6) 

 [\[EC2\.13\] Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22](ec2-controls.md#ec2-13) 

 [\[EC2\.14\] Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389](ec2-controls.md#ec2-14) 

 [\[IAM\.1\] IAM policies should not allow full "\*" administrative privileges](iam-controls.md#iam-1) 

 [\[IAM\.2\] IAM users should not have IAM policies attached](iam-controls.md#iam-2) 

 [\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](iam-controls.md#iam-3) 

 [\[IAM\.4\] IAM root user access key should not exist](iam-controls.md#iam-4) 

 [\[IAM\.5\] MFA should be enabled for all IAM users that have a console password](iam-controls.md#iam-5) 

 [\[IAM\.6\] Hardware MFA should be enabled for the root user](iam-controls.md#iam-6) 

 [\[IAM\.8\] Unused IAM user credentials should be removed](iam-controls.md#iam-8) 

 [\[IAM\.9\] Virtual MFA should be enabled for the root user](iam-controls.md#iam-9) 

 [\[IAM\.11\] Ensure IAM password policy requires at least one uppercase letter](iam-controls.md#iam-11) 

 [\[IAM\.12\] Ensure IAM password policy requires at least one lowercase letter](iam-controls.md#iam-12) 

 [\[IAM\.13\] Ensure IAM password policy requires at least one symbol](iam-controls.md#iam-13) 

 [\[IAM\.14\] Ensure IAM password policy requires at least one number](iam-controls.md#iam-14) 

 [\[IAM\.15\] Ensure IAM password policy requires minimum password length of 14 or greater](iam-controls.md#iam-15) 

 [\[IAM\.16\] Ensure IAM password policy prevents password reuse](iam-controls.md#iam-16) 

 [\[IAM\.17\] Ensure IAM password policy expires passwords within 90 days or less](iam-controls.md#iam-17) 

 [\[IAM\.18\] Ensure a support role has been created to manage incidents with AWS Support](iam-controls.md#iam-18) 

 [\[IAM\.20\] Avoid the use of the root user](iam-controls.md#iam-20) 

 [\[KMS\.4\] AWS KMS key rotation should be enabled](kms-controls.md#kms-4) 

## Center for Internet Security \(CIS\) AWS Foundations Benchmark v1\.4\.0<a name="cis1v4-standard"></a>

Security Hub supports v1\.4\.0 of the CIS AWS Foundations Benchmark\.

### Controls that apply to CIS AWS Foundations Benchmark v1\.4\.0<a name="cis1v4-controls"></a>

 [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1) 

 [\[CloudTrail\.2\] CloudTrail should have encryption at\-rest enabled](cloudtrail-controls.md#cloudtrail-2) 

 [\[CloudTrail\.4\] CloudTrail log file validation should be enabled](cloudtrail-controls.md#cloudtrail-4) 

 [\[CloudTrail\.5\] CloudTrail trails should be integrated with Amazon CloudWatch Logs](cloudtrail-controls.md#cloudtrail-5) 

 [\[CloudTrail\.6\] Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible](cloudtrail-controls.md#cloudtrail-6) 

 [\[CloudTrail\.7\] Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket](cloudtrail-controls.md#cloudtrail-7) 

 [\[CloudWatch\.1\] A log metric filter and alarm should exist for usage of the "root" user](cloudwatch-controls.md#cloudwatch-1) 

 [\[CloudWatch\.4\] Ensure a log metric filter and alarm exist for IAM policy changes](cloudwatch-controls.md#cloudwatch-4) 

 [\[CloudWatch\.5\] Ensure a log metric filter and alarm exist for CloudTrail AWS Configuration changes](cloudwatch-controls.md#cloudwatch-5) 

 [\[CloudWatch\.6\] Ensure a log metric filter and alarm exist for AWS Management Console authentication failures](cloudwatch-controls.md#cloudwatch-6) 

 [\[CloudWatch\.7\] Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer managed keys](cloudwatch-controls.md#cloudwatch-7) 

 [\[CloudWatch\.8\] Ensure a log metric filter and alarm exist for S3 bucket policy changes](cloudwatch-controls.md#cloudwatch-8) 

 [\[CloudWatch\.9\] Ensure a log metric filter and alarm exist for AWS Config configuration changes](cloudwatch-controls.md#cloudwatch-9) 

 [\[CloudWatch\.10\] Ensure a log metric filter and alarm exist for security group changes](cloudwatch-controls.md#cloudwatch-10) 

 [\[CloudWatch\.11\] Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)](cloudwatch-controls.md#cloudwatch-11) 

 [\[CloudWatch\.12\] Ensure a log metric filter and alarm exist for changes to network gateways](cloudwatch-controls.md#cloudwatch-12) 

 [\[CloudWatch\.13\] Ensure a log metric filter and alarm exist for route table changes](cloudwatch-controls.md#cloudwatch-13) 

 [\[CloudWatch\.14\] Ensure a log metric filter and alarm exist for VPC changes](cloudwatch-controls.md#cloudwatch-14) 

 [\[Config\.1\] AWS Config should be enabled](config-controls.md#config-1) 

 [\[EC2\.2\] The VPC default security group should not allow inbound and outbound traffic](ec2-controls.md#ec2-2) 

 [\[EC2\.6\] VPC flow logging should be enabled in all VPCs](ec2-controls.md#ec2-6) 

 [\[EC2\.7\] Amazon EBS default encryption should be enabled](ec2-controls.md#ec2-7) 

 [\[EC2\.21\] Network ACLs should not allow ingress from 0\.0\.0\.0/0 to port 22 or port 3389](ec2-controls.md#ec2-21) 

 [\[IAM\.1\] IAM policies should not allow full "\*" administrative privileges](iam-controls.md#iam-1) 

 [\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](iam-controls.md#iam-3) 

 [\[IAM\.4\] IAM root user access key should not exist](iam-controls.md#iam-4) 

 [\[IAM\.5\] MFA should be enabled for all IAM users that have a console password](iam-controls.md#iam-5) 

 [\[IAM\.6\] Hardware MFA should be enabled for the root user](iam-controls.md#iam-6) 

 [\[IAM\.9\] Virtual MFA should be enabled for the root user](iam-controls.md#iam-9) 

 [\[IAM\.15\] Ensure IAM password policy requires minimum password length of 14 or greater](iam-controls.md#iam-15) 

 [\[IAM\.16\] Ensure IAM password policy prevents password reuse](iam-controls.md#iam-16) 

 [\[IAM\.18\] Ensure a support role has been created to manage incidents with AWS Support](iam-controls.md#iam-18) 

 [\[IAM\.22\] IAM user credentials unused for 45 days should be removed](iam-controls.md#iam-22) 

 [\[KMS\.4\] AWS KMS key rotation should be enabled](kms-controls.md#kms-4) 

 [\[RDS\.3\] RDS DB instances should have encryption at\-rest enabled](rds-controls.md#rds-3) 

 [\[S3\.1\] S3 Block Public Access setting should be enabled](s3-controls.md#s3-1) 

 [\[S3\.4\] S3 buckets should have server\-side encryption enabled](s3-controls.md#s3-4) 

 [\[S3\.5\] S3 buckets should require requests to use Secure Socket Layer](s3-controls.md#s3-5) 

 [\[S3\.8\] S3 Block Public Access setting should be enabled at the bucket\-level](s3-controls.md#s3-8) 

## CIS AWS Foundations Benchmark v1\.2\.0 compared to v1\.4\.0<a name="cis1.4-vs-cis1.2"></a>

This section summarizes the differences between the Center for Internet Security \(CIS\) AWS Foundations Benchmark v1\.4\.0 and v1\.2\.0\. Security Hub supports both versions of this standard\.

**Note**  
We recommend upgrading to CIS AWS Foundations Benchmark v1\.4\.0 to stay current on security best practices, but you may have both v1\.4\.0 and v1\.2\.0 enabled at the same time\. For more information, see [Enabling and disabling security standards](securityhub-standards-enable-disable.md)\. If you want to upgrade to v1\.4\.0, it's best to enable v1\.4\.0 first before disabling v1\.2\.0\. If you use the Security Hub integration with AWS Organizations to centrally manage multiple accounts and you want to batch enable v1\.4\.0 across all of them \(and optionally disable v1\.2\.0\), you can run a [Security Hub multi\-account script](https://github.com/awslabs/aws-securityhub-multiaccount-scripts/tree/master/cis14-enable) from the administrator account\.

### Controls that exist in CIS AWS Foundations Benchmark v1\.4\.0, but not in v1\.2\.0<a name="cis1.4-added"></a>

The following controls were added in CIS AWS Foundations Benchmark v1\.4\.0\. These controls are *not* included in CIS AWS Foundations Benchmark v1\.2\.0\.


| Security control ID | CISv1\.4\.0 requirement | Control title | 
| --- | --- | --- | 
|  [IAM\.22](iam-controls.md#iam-22)  |  1\.12  |  Ensure credentials unused for 45 days or greater are disabled  | 
|  [S3\.4](s3-controls.md#s3-4)  |  2\.1\.1  |  Ensure all S3 buckets employ encryption\-at\-rest  | 
|  [S3\.5](s3-controls.md#s3-5)  |  2\.1\.2  |  Ensure S3 bucket policy is set to deny HTTP requests  | 
|  [S3\.1](s3-controls.md#s3-1)  |  2\.1\.5\.1  |  S3 Block Public Access setting should be enabled  | 
|  [S3\.8](s3-controls.md#s3-8)  |  2\.1\.5\.2  |  S3 Block Public Access setting should be enabled at the bucket level  | 
|  [EC2\.7](ec2-controls.md#ec2-7)  |  2\.2\.1  |  Ensure EBS volume encryption is enabled  | 
|  [RDS\.3](rds-controls.md#rds-3)  |  2\.3\.1  |  Ensure that encryption is enabled for RDS Instances  | 
|  [EC2\.21](ec2-controls.md#ec2-21)  |  5\.1  |  Ensure no Network ACLs allow ingress from 0\.0\.0\.0/0 to remote server administration ports  | 

### Controls that exist in CIS AWS Foundations Benchmark v1\.2\.0, but not in v1\.4\.0<a name="cis1.2-only"></a>

The following controls exist only in CIS AWS Foundations Benchmark v1\.2\.0\. These controls are *not* included in CIS AWS Foundations Benchmark v1\.4\.0\.


| Security control ID | CISv1\.2\.0 requirement | Control title | Reason not included in v1\.4\.0 | 
| --- | --- | --- | --- | 
|  [IAM\.8](iam-controls.md#iam-8)  |  1\.3  |  Ensure credentials unused for 90 days or greater are disabled  |  See instead, [\[IAM\.22\] IAM user credentials unused for 45 days should be removed](iam-controls.md#iam-22)  | 
|  [IAM\.11](iam-controls.md#iam-11)  |  1\.5  |  Ensure IAM password policy requires at least one uppercase letter  |  Not a requirement in CISv1\.4\.0  | 
|  [IAM\.12](iam-controls.md#iam-12)  |  1\.6  |  Ensure IAM password policy requires at least one lowercase letter  |  Not a requirement in CISv1\.4\.0  | 
|  [IAM\.13](iam-controls.md#iam-13)  |  1\.7  |  Ensure IAM password policy requires at least one symbol  |  Not a requirement in CISv1\.4\.0  | 
|  [IAM\.14](iam-controls.md#iam-14)  |  1\.8  |  Ensure IAM password policy requires at least one number  |  Not a requirement in CISv1\.4\.0  | 
|  [IAM\.17](iam-controls.md#iam-17)  |  1\.11  |  Ensure IAM password policy expires passwords within 90 days or less  |  Not a requirement in CISv1\.4\.0  | 
|  [IAM\.2](iam-controls.md#iam-2)  |  1\.16  |  Ensure IAM policies are attached only to groups or roles  |  Automated check that Security Hub doesn't support  | 
|  [CloudWatch\.2](cloudwatch-controls.md#cloudwatch-2)  |  3\.1  |  Ensure a log metric filter and alarm exist for unauthorized API calls  |  Automated check that Security Hub doesn't support  | 
|  [CloudWatch\.3](cloudwatch-controls.md#cloudwatch-3)  |  3\.2  |  Ensure a log metric filter and alarm exist for AWS Management Console sign\-in without MFA  |  Automated check that Security Hub doesn't support  | 
|  [EC2\.13](ec2-controls.md#ec2-13)  |  4\.1  |  Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 22  |  See instead, [\[EC2\.21\] Network ACLs should not allow ingress from 0\.0\.0\.0/0 to port 22 or port 3389](ec2-controls.md#ec2-21)  | 
|  [EC2\.14](ec2-controls.md#ec2-14)  |  4\.2  |  Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389  |  Automated check that Security Hub doesn't support  | 

### Controls that exist in CIS AWS Foundations Benchmark v1\.2\.0 and v1\.4\.0<a name="cis-controls-all-versions"></a>

The following controls exist in both CIS AWS Foundations Benchmark v1\.2\.0 and v1\.4\.0\. However, the controls IDs and some of the control titles differ in each version\.


| Security control ID | CISv1\.2\.0 requirement | Control title in CISv1\.2\.0 | CISv1\.4\.0 requirement | Control title in CISv1\.4\.0 | 
| --- | --- | --- | --- | --- | 
|  [CloudWatch\.1](cloudwatch-controls.md#cloudwatch-1)  |  1\.1  |  Avoid the use of the root user  |  1\.7  |  Eliminate use of the root user for administrative and daily tasks  | 
|  [IAM\.5](iam-controls.md#iam-5)  |  1\.2  |  Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password  |  1\.10  |  Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password  | 
|  [IAM\.3](iam-controls.md#iam-3)  |  1\.4  |  Ensure access keys are rotated every 90 days or less  |  1\.14  |  Ensure access keys are rotated every 90 days or less  | 
|  [IAM\.15](iam-controls.md#iam-15)  |  1\.9  |  Ensure IAM password policy requires minimum password length of 14 or greater  |  1\.8  |  Ensure IAM password policy requires minimum length of 14 or greater  | 
|  [IAM\.16](iam-controls.md#iam-16)  |  1\.10  |  Ensure IAM password policy prevents password reuse  |  1\.9  |  Ensure IAM password policy prevents password reuse  | 
|  [IAM\.4](iam-controls.md#iam-4)  |  1\.12  |  Ensure no root user access key exists  |  1\.4  |  Ensure no root user account access key exists  | 
|  [IAM\.9](iam-controls.md#iam-9)  |  1\.13  |  Ensure MFA is enabled for the root user  |  1\.5  |  Ensure MFA is enabled for the root user account  | 
|  [IAM\.6](iam-controls.md#iam-6)  |  1\.14  |  Ensure hardware MFA is enabled for the root user  |  1\.6  |  Ensure hardware MFA is enabled for the root user account  | 
|  [IAM\.18](iam-controls.md#iam-18)  |  1\.20  |  Ensure a support role has been created to manage incidents with AWS Support  |  1\.17  |  Ensure a support role has been created to manage incidents with AWS Support  | 
|  [IAM\.1](iam-controls.md#iam-1)  |  1\.22  |  Ensure IAM policies that allow full "\*:\*" administrative privileges are not created  |  1\.16  |  Ensure IAM policies that allow full "\*:\*" administrative privileges are not attached  | 
|  [CloudTrail\.1](cloudtrail-controls.md#cloudtrail-1)  |  2\.1  |  Ensure CloudTrail is enabled in all Regions  |  3\.1  |  Ensure CloudTrail is enabled in all Regions  | 
|  [CloudTrail\.4](cloudtrail-controls.md#cloudtrail-4)  |  2\.2  |  Ensure CloudTrail log file validation is enabled  |  3\.2  |  Ensure CloudTrail log file validation is enabled  | 
|  [CloudTrail\.6](cloudtrail-controls.md#cloudtrail-6)  |  2\.3  |  Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible  |  3\.3  |  Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible  | 
|  [CloudTrail\.5](cloudtrail-controls.md#cloudtrail-5)  |  2\.4  |  Ensure CloudTrail trails are integrated with CloudWatch Logs  |  3\.4  |  Ensure CloudTrail trails are integrated with CloudWatch Logs  | 
|  [Config\.1](config-controls.md#config-1)  |  2\.5  |  Ensure AWS Config is enabled  |  3\.5  |  Ensure AWS Config is enabled in all Regions  | 
|  [CloudTrail\.7](cloudtrail-controls.md#cloudtrail-7)  |  2\.6  |  Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket  |  3\.6  |  Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket  | 
|  [CloudTrail\.2](cloudtrail-controls.md#cloudtrail-2)  |  2\.7  |  Ensure CloudTrail logs are encrypted at rest using AWS KMS keys  |  3\.7  |  Ensure CloudTrail logs are encrypted at rest using AWS KMS keys  | 
|  [KMS\.4](kms-controls.md#kms-4)  |  2\.8  |  Ensure rotation for customer\-created KMS keys is enabled  |  3\.8  |  Ensure rotation for customer\-created KMS keys is enabled  | 
|  [EC2\.6](ec2-controls.md#ec2-6)  |  2\.9  |  Ensure VPC flow logging is enabled in all VPCs  |  3\.9  |  Ensure VPC flow logging is enabled in all VPCs  | 
|  [CloudWatch\.1](cloudwatch-controls.md#cloudwatch-1)  |  3\.3  |  Ensure a log metric filter and alarm exist for usage of root user  |  1\.7  |  Eliminate use of the root user for administrative and daily tasks  | 
|  [CloudWatch\.4](cloudwatch-controls.md#cloudwatch-4)  |  3\.4  |  Ensure a log metric filter and alarm exist for IAM policy changes  |  4\.4  |  Ensure a log metric filter and alarm exist for IAM policy changes  | 
|  [CloudWatch\.5](cloudwatch-controls.md#cloudwatch-5)  |  3\.5  |  Ensure a log metric filter and alarm exist for CloudTrail configuration change  |  4\.5  |  Ensure a log metric filter and alarm exist for CloudTrail configuration change  | 
|  [CloudWatch\.6](cloudwatch-controls.md#cloudwatch-6)  |  3\.6  |  Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  |  4\.6  |  Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  | 
|  [CloudWatch\.7](cloudwatch-controls.md#cloudwatch-7)  |  3\.7  |  Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer managed keys  |  4\.7  |  Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer managed keys  | 
|  [CloudWatch\.8](cloudwatch-controls.md#cloudwatch-8)  |  3\.8  |  Ensure a log metric filter and alarm exist for S3 bucket policy changes  |  4\.8  |  Ensure a log metric filter and alarm exist for S3 bucket policy changes  | 
|  [CloudWatch\.9](cloudwatch-controls.md#cloudwatch-9)  |  3\.9  |  Ensure a log metric filter and alarm exist for AWS Config configuration changes  |  4\.9  |  Ensure a log metric filter and alarm exist for AWS Config configuration changes  | 
|  [CloudWatch\.10](cloudwatch-controls.md#cloudwatch-10)  |  3\.10  |  Ensure a log metric filter and alarm exist for security group changes  |  4\.10  |  Ensure a log metric filter and alarm exist for security group changes  | 
|  [CloudWatch\.11](cloudwatch-controls.md#cloudwatch-11)  |  3\.11  |  Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  |  4\.11  |  Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  | 
|  [CloudWatch\.12](cloudwatch-controls.md#cloudwatch-12)  |  3\.12  |  Ensure a log metric filter and alarm exist for changes to network gateways  |  4\.12  |  Ensure a log metric filter and alarm exist for changes to network gateways  | 
|  [CloudWatch\.13](cloudwatch-controls.md#cloudwatch-13)  |  3\.13  |  Ensure a log metric filter and alarm exist for route table changes  |  4\.13  |  Ensure a log metric filter and alarm exist for route table changes  | 
|  [CloudWatch\.14](cloudwatch-controls.md#cloudwatch-14)  |  3\.14  |  Ensure a log metric filter and alarm exist for VPC changes  |  4\.14  |  Ensure a log metric filter and alarm exist for VPC changes  | 
|  [EC2\.2](ec2-controls.md#ec2-2)  |  4\.3  |  Ensure the default security group of every VPC restricts all traffic  |  5\.3  |  Ensure the default security group of every VPC restricts all traffic  | 

## Finding fields format for CIS AWS Foundations Benchmark v1\.4\.0<a name="cisv1.4.0-finding-fields"></a>

When you enable CIS AWS Foundations Benchmark v1\.4\.0, you'll begin receiving findings in the AWS Security Finding Format \(ASFF\)\. For these findings, standard\-specific fields will reference v1\.4\.0\. For CIS AWS Foundations Benchmark v1\.4\.0, note the following format for [`GeneratorID`](asff-required-attributes.md#GeneratorId) and any ASFF fields that reference the standard Amazon Resource Name \(ARN\)\.
+ **Standard ARN** – `arn:aws::securityhub:region::standards/cis-aws-foundations-benchmark/v/1.4.0`
+ **`GeneratorID`** – `cis-aws-foundations-benchmark/v/1.4.0/control ID`

You can call the [GetEnabledStandards](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html) API operation to find out the ARN of a standard\.

**Note**  
When you enable CIS AWS Foundations Benchmark v1\.4\.0, Security Hub may take up to 18 hours to generate findings for controls that use the same AWS Config service\-linked rule as enabled controls in other enabled standards\. For more information, see [Schedule for running security checks](securityhub-standards-schedule.md)\.

Finding fields will differ if you've turned on consolidated control findings\. For more information about these differences, see [Impact of consolidation on ASFF fields and values](asff-changes-consolidation.md)\. For sample CIS control findings with consolidation turned on and off, see [Sample control findings](sample-control-findings.md)\.

## CIS AWS Foundations Benchmark security checks that aren't supported in Security Hub<a name="securityhub-standards-cis-checks-not-supported"></a>

This section summarizes CIS requirements that are not currently supported in Security Hub\. The Center for Internet Security \(CIS\) is an independent, nonprofit organization that establishes these requirements\.

### CIS AWS Foundations Benchmark v1\.2\.0 security checks that aren't supported in Security Hub<a name="securityhub-standards-cis1.2-checks-not-supported"></a>

The following CIS AWS Foundations Benchmark v1\.2\.0 requirements are *not* currently supported in Security Hub\.

#### Manual checks that aren't supported<a name="cis1.2-unsupported-manual-checks"></a>

Security Hub focuses on automated security checks\. As a result, Security Hub doesn't support the following requirements of CIS AWS Foundations Benchmark v1\.2\.0 because they require manual checks of your resources:
+ 1\.15 – Ensure security questions are registered in the AWS account 
+ 1\.17 – Maintain current contact details 
+ 1\.18 – Ensure security contact information is registered 
+ 1\.19 – Ensure IAM instance roles are used for AWS resource access from instances
+ 1\.21 – Do not setup access keys during initial user setup for all IAM users that have a console password
+ 4\.4 – Ensure routing tables for VPC peering are "least access"

Security Hub supports all automated checks for CIS AWS Foundations Benchmark v1\.2\.0\.

### CIS AWS Foundations Benchmark v1\.4\.0 security checks that aren't supported in Security Hub<a name="securityhub-standards-cis1.4-checks-not-supported"></a>

The following CIS AWS Foundations Benchmark v1\.4\.0 requirements are *not* currently supported in Security Hub\.

#### Manual checks that aren't supported<a name="cis1.4-unsupported-manual-checks"></a>

Security Hub focuses on automated security checks\. As a result, Security Hub doesn't support the following requirements of CIS AWS Foundations Benchmark v1\.4\.0 because they require manual checks of your resources:
+ 1\.1 – Maintain current contact details 
+ 1\.2 – Ensure security contact information is registered 
+ 1\.3 – Ensure security questions are registered in the AWS account 
+ 1\.11 – Do not setup access keys during initial user setup for all IAM users that have a console password
+ 1\.18 – Ensure IAM instance roles are used for AWS resource access from instances
+ 1\.21 – Ensure IAM users are managed centrally via identity federation or AWS Organizations for multi\-account environments
+ 2\.1\.4 – Ensure all data in Amazon S3 has been discovered, classified, and secured when required
+ 5\.4 – Ensure routing tables for VPC peering are "least access"

#### Automated checks that aren't supported<a name="cis1.4-unsupported-automated-checks"></a>

Security Hub doesn't support the following requirements of CIS AWS Foundations Benchmark v1\.4\.0 that rely on automated checks:
+ 1\.13 – Ensure there is only one active access key available for any single IAM user
+ 1\.15 – Ensure IAM users receive permissions only through groups
+ 1\.19 – Ensure that all the expired SSL/TLS certificates stored in IAM are removed
+ 1\.20 – Ensure that IAM Access Analyzer is enabled for all Regions
+ 2\.1\.3 – Ensure MFA Delete is enabled on S3 buckets
+ 3\.10 – Ensure that Object\-level logging for write events is enabled for S3 buckets
+ 3\.11 – Ensure that Object\-level logging for read events is enabled for S3 buckets
+ 4\.1 – Ensure a log metric filter and alarm exist for unauthorized API calls
+ 4\.2 – Ensure a log metric filter and alarm exist for Management Console sign\-in without MFA
+ 4\.3 – Ensure a log metric filter and alarm exist for usage of root account \(this is similar to automated requirement, **1\.7 \- Eliminate use of the root user for administrative and daily tasks**, which is supported in Security Hub\)
+ 4\.15 – Ensure a log metric filter and alarm exists for AWS Organizations changes
+ 5\.2 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to remote server administration ports
