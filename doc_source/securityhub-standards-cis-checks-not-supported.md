# CIS AWS Foundations Benchmark security checks that are not supported in Security Hub<a name="securityhub-standards-cis-checks-not-supported"></a>

This section summarizes CIS requirements that are not currently supported in Security Hub\.

## CIS AWS Foundations Benchmark v1\.2\.0 security checks that are not supported in Security Hub<a name="securityhub-standards-cis1.2-checks-not-supported"></a>

The following CIS AWS Foundations Benchmark v1\.2\.0 requirements are *not* currently supported in Security Hub\.

### Manual checks that aren't supported<a name="cis1.2-unsupported-manual-checks"></a>

Security Hub focuses on automated security checks\. As a result, Security Hub doesn't support the following requirements of CIS AWS Foundations Benchmark v1\.2\.0 because they require manual checks of your resources:
+ 1\.15 – Ensure security questions are registered in the AWS account 
+ 1\.17 – Maintain current contact details 
+ 1\.18 – Ensure security contact information is registered 
+ 1\.19 – Ensure IAM instance roles are used for AWS resource access from instances
+ 1\.21 – Do not setup access keys during initial user setup for all IAM users that have a console password
+ 4\.4 – Ensure routing tables for VPC peering are "least access"

Security Hub supports all automated checks for CIS AWS Foundations Benchmark v1\.2\.0\.

## CIS AWS Foundations Benchmark v1\.4\.0 security checks that are not supported in Security Hub<a name="securityhub-standards-cis1.4-checks-not-supported"></a>

The following CIS AWS Foundations Benchmark v1\.4\.0 requirements are *not* currently supported in Security Hub\.

### Manual checks that aren't supported<a name="cis1.4-unsupported-manual-checks"></a>

Security Hub focuses on automated security checks\. As a result, Security Hub doesn't support the following requirements of CIS AWS Foundations Benchmark v1\.4\.0 because they require manual checks of your resources:
+ 1\.1 – Maintain current contact details 
+ 1\.2 – Ensure security contact information is registered 
+ 1\.3 – Ensure security questions are registered in the AWS account 
+ 1\.11 – Do not setup access keys during initial user setup for all IAM users that have a console password
+ 1\.18 – Ensure IAM instance roles are used for AWS resource access from instances
+ 1\.21 – Ensure IAM users are managed centrally via identity federation or AWS Organizations for multi\-account environments
+ 2\.1\.4 – Ensure all data in Amazon S3 has been discovered, classified and secured when required
+ 5\.4 – Ensure routing tables for VPC peering are "least access"

### Automated checks that aren't supported<a name="cis1.4-unsupported-automated-checks"></a>

Security Hub doesn't support the following requirements of CIS AWS Foundations Benchmark v1\.4\.0 that rely on automated checks:
+ 1\.13 – Ensure there is only one active access key available for any single IAM user
+ 1\.15 – Ensure IAM users receive permissions only through groups
+ 1\.19 – Ensure that all the expired SSL/TLS certificates stored in IAM are removed
+ 1\.20 – Ensure that IAM Access Analyzer is enabled for all Regions
+ 2\.1\.3 – Ensure MFA Delete is enabled on S3 buckets
+ 3\.10 – Ensure that Object\-level logging for write events is enabled for S3 bucket
+ 3\.11 – Ensure that Object\-level logging for read events is enabled for S3 bucket
+ 4\.1 – Ensure a log metric filter and alarm exist for unauthorized API calls
+ 4\.2 – Ensure a log metric filter and alarm exist for Management Console sign\-in without MFA
+ 4\.3 – Ensure a log metric filter and alarm exist for usage of 'root' account \(this is similar to automated requirement [1\.7 – Eliminate use of the 'root user for administrative and daily tasks](securityhub-cis-controls-1.4.0.md#securityhub-cis1.4-controls-1.7), which is supported in Security Hub\)
+ 4\.15 – Ensure a log metric filter and alarm exists for AWS Organizations changes
+ 5\.2 – Ensure no security groups allow ingress from 0\.0\.0\.0/0 to remote server administration ports