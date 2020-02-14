# AWS Config Resources Required for CIS Controls<a name="securityhub-standards-cis-config-resources"></a>

To run checks for the enabled CIS AWS Foundations controls on your environment's resources, Security Hub either runs through the exact audit steps prescribed for the checks in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/) or uses specific AWS Config managed rules\.

If you don't enable all resources in AWS Config, a finding is generated for the check [2\.5 – Ensure AWS Config is enabled](securityhub-cis-controls.md#securityhub-cis-controls-2.5)\. For other CIS controls, for Security Hub to accurately report findings, you must enable the following resources in AWS Config\.
+ AWS CloudTrail trail
+ Amazon EC2 security group
+ Amazon EC2 VPC
+ IAM policy
+ IAM user
+ AWS KMS key
+ S3 bucket

When you view the details of a compliance standards rule that is based on an AWS Config rule, you can choose **Compliance rules** to open the AWS Config rule associated with the compliance check\. Only compliance checks that are based on AWS Config rules provide links to the AWS Config rule\. To navigate to the AWS Config rule, you must also have an IAM permission in the selected account to navigate to Config\.