# CIS AWS Foundations Benchmark v1\.2\.0 compared to v1\.4\.0<a name="securityhub-standards-cis1.4-vs-cis1.2"></a>

This section summarizes the differences between CIS AWS Foundations Benchmark v1\.4\.0 and v1\.2\.0\. Choose a control ID to view remediation instructions for a failed finding for that control\.

**Note**  
We recommend upgrading to CIS AWS Foundations Benchmark v1\.4\.0 to stay current on security best practices, but you may have both v1\.4\.0 and v1\.2\.0 enabled at the same time\. For more information, see [Disabling or enabling a security standard](securityhub-standards-enable-disable.md)\. If you want to upgrade to v1\.4\.0, it's best to enable v1\.4\.0 first before disabling v1\.2\.0\. If you use the Security Hub integration with AWS Organizations to centrally manage multiple accounts and wish to batch enable v1\.4\.0 across all accounts \(and disable v1\.2\.0 if you wish\), you can use a [Security Hub multi\-account script](https://github.com/awslabs/aws-securityhub-multiaccount-scripts)\. 

## Controls that were added in CIS AWS Foundations Benchmark v1\.4\.0<a name="cis1.4-added"></a>

The following controls were added in CIS AWS Foundations Benchmark v1\.4\.0\. These controls are *not* included in CIS AWS Foundations Benchmark v1\.2\.0\.


| CISv1\.4\.0 requirement | Control title | 
| --- | --- | 
|  [1\.12](securityhub-cis-controls-1.4.0.md#cis1.4-1.12-remediation)  |  Ensure credentials unused for 45 days or greater are disabled  | 
|  [2\.1\.1](securityhub-cis-controls-1.4.0.md#cis1.4-2.1.1-remediation)  |  Ensure all S3 buckets employ encryption\-at\-rest  | 
|  [2\.1\.2](securityhub-cis-controls-1.4.0.md#cis1.4-2.1.2-remediation)  |  Ensure S3 bucket policy is set to deny HTTP requests  | 
|  [2\.1\.5\.1](securityhub-cis-controls-1.4.0.md#cis1.4-2.1.5.1-remediation)  |  S3 Block Public Access setting should be enabled  | 
|  [2\.1\.5\.2](securityhub-cis-controls-1.4.0.md#cis1.4-2.1.5.2-remediation)  |  S3 Block Public Access setting should be enabled at the bucket level  | 
|  [2\.2\.1](securityhub-cis-controls-1.4.0.md#cis1.4-2.2.1-remediation)  |  Ensure EBS volume encryption is enabled  | 
|  [2\.3\.1](securityhub-cis-controls-1.4.0.md#cis1.4-2.3.1-remediation)  |  Ensure that encryption is enabled for RDS Instances  | 
|  [5\.1](securityhub-cis-controls-1.4.0.md#cis1.4-5.1-remediation)  |  Ensure no Network ACLs allow ingress from 0\.0\.0\.0/0 to remote server administration ports  | 

## Controls that exist in CIS AWS Foundations Benchmark v1\.2\.0, but not in v1\.4\.0<a name="cis1.2-only"></a>

The following controls exist only in CIS AWS Foundations Benchmark v1\.2\.0\. These controls are *not* included in CIS AWS Foundations Benchmark v1\.4\.0\.


| CISv1\.2\.0 requirement | Control title | Reason not included in v1\.4\.0 | 
| --- | --- | --- | 
|  [1\.1](securityhub-cis-controls.md#cis-1.1-remediation)  |  Avoid the use of the root user  |  See instead, [1\.7 – Eliminate use of the 'root user for administrative and daily tasks](securityhub-cis-controls-1.4.0.md#securityhub-cis1.4-controls-1.7)  | 
|  [1\.3](securityhub-cis-controls.md#cis-1.3-remediation)  |  Ensure credentials unused for 90 days or greater are disabled  |  See instead, [1\.12 – Ensure credentials unused for 45 days or greater are disabled ](securityhub-cis-controls-1.4.0.md#securityhub-cis1.4-controls-1.12)  | 
|  [1\.5](securityhub-cis-controls.md#cis-1.5-remediation)  |  Ensure IAM password policy requires at least one uppercase letter  |  Not a requirement in CISv1\.4\.0  | 
|  [1\.6](securityhub-cis-controls.md#cis-1.6-remediation)  |  Ensure IAM password policy requires at least one lowercase letter  |  Not a requirement in CISv1\.4\.0  | 
|  [1\.7](securityhub-cis-controls.md#cis-1.7-remediation)  |  Ensure IAM password policy requires at least one symbol  |  Not a requirement in CISv1\.4\.0  | 
|  [1\.8](securityhub-cis-controls.md#cis-1.8-remediation)  |  Ensure IAM password policy requires at least one number  |  Not a requirement in CISv1\.4\.0  | 
|  [1\.11](securityhub-cis-controls.md#cis-1.11-remediation)  |  Ensure IAM password policy expires passwords within 90 days or less  |  Not a requirement in CISv1\.4\.0  | 
|  [1\.16](securityhub-cis-controls.md#cis-1.16-remediation)  |  Ensure IAM policies are attached only to groups or roles  |  Automated check that Security Hub doesn't support  | 
|  [3\.1](securityhub-cis-controls.md#cis-3.1-remediation)  |  Ensure a log metric filter and alarm exist for unauthorized API calls  |  Automated check that Security Hub doesn't support  | 
|  [3\.2](securityhub-cis-controls.md#cis-3.2-remediation)  |  Ensure a log metric filter and alarm exist for AWS Management Console sign\-in without MFA  |  Automated check that Security Hub doesn't support  | 
|  [4\.1](securityhub-cis-controls.md#cis-4.1-remediation)  |  Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 22  |  See instead, [5\.1 – Ensure no Network ACLs allow ingress from 0\.0\.0\.0/0 to remote server administration ports](securityhub-cis-controls-1.4.0.md#securityhub-cis1.4-controls-5.1)  | 
|  [4\.2](securityhub-cis-controls.md#cis-4.2-remediation)  |  Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389  |  Automated check that Security Hub doesn't support  | 

## Controls that exist in CIS AWS Foundations Benchmark v1\.2\.0 and v1\.4\.0<a name="cis-controls-all-versions"></a>

The following controls exist in both CIS AWS Foundations Benchmark v1\.2\.0 and v1\.4\.0\. However, the controls IDs and some of the control titles differ in each version\.


| CISv1\.2\.0 requirement | Control title in CISv1\.2\.0 | CISv1\.4\.0 requirement | Control title in CISv1\.4\.0 | 
| --- | --- | --- | --- | 
|  [1\.2](securityhub-cis-controls.md#cis-1.2-remediation)  |  Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password  |  [1\.10](securityhub-cis-controls-1.4.0.md#cis1.4-1.10-remediation)  |  Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password  | 
|  [1\.4](securityhub-cis-controls.md#cis-1.4-remediation)  |  Ensure access keys are rotated every 90 days or less  |  [1\.14](securityhub-cis-controls-1.4.0.md#cis1.4-1.14-remediation)  |  Ensure access keys are rotated every 90 days or less  | 
|  [1\.9](securityhub-cis-controls.md#cis-1.9-remediation)  |  Ensure IAM password policy requires minimum password length of 14 or greater  |  [1\.8](securityhub-cis-controls-1.4.0.md#cis1.4-1.8-remediation)  |  Ensure IAM password policy requires minimum length of 14 or greater  | 
|  [1\.10](securityhub-cis-controls.md#cis-1.10-remediation)  |  Ensure IAM password policy prevents password reuse  |  [1\.9](securityhub-cis-controls-1.4.0.md#cis1.4-1.9-remediation)  |  Ensure IAM password policy prevents password reuse  | 
|  [1\.12](securityhub-cis-controls.md#cis-1.12-remediation)  |  Ensure no root user access key exists  |  [1\.4](securityhub-cis-controls-1.4.0.md#cis1.4-1.4-remediation)  |  Ensure no 'root' user account access key exists  | 
|  [1\.13](securityhub-cis-controls.md#cis-1.13-remediation)  |  Ensure MFA is enabled for the root user  |  [1\.5](securityhub-cis-controls-1.4.0.md#cis1.4-1.5-remediation)  |  Ensure MFA is enabled for the 'root' user account  | 
|  [1\.14](securityhub-cis-controls.md#cis-1.14-remediation)  |  Ensure hardware MFA is enabled for the root user  |  [1\.6](securityhub-cis-controls-1.4.0.md#cis1.4-1.6-remediation)  |  Ensure hardware MFA is enabled for the 'root' user account  | 
|  [1\.20](securityhub-cis-controls.md#cis-1.20-remediation)  |  Ensure a support role has been created to manage incidents with AWS Support  |  [1\.17](securityhub-cis-controls-1.4.0.md#cis1.4-1.17-remediation)  |  Ensure a support role has been created to manage incidents with AWS Support  | 
|  [1\.22](securityhub-cis-controls.md#cis-1.22-remediation)  |  Ensure IAM policies that allow full "\*:\*" administrative privileges are not created  |  [1\.16](securityhub-cis-controls-1.4.0.md#cis1.4-1.16-remediation)  |  Ensure IAM policies that allow full "\*:\*" administrative privileges are not attached  | 
|  [2\.1](securityhub-cis-controls.md#cis-2.1-remediation)  |  Ensure CloudTrail is enabled in all Regions  |  [3\.1](securityhub-cis-controls-1.4.0.md#cis1.4-3.1-remediation)  |  Ensure CloudTrail is enabled in all Regions  | 
|  [2\.2](securityhub-cis-controls.md#cis-2.2-remediation)  |  Ensure CloudTrail log file validation is enabled  |  [3\.2](securityhub-cis-controls-1.4.0.md#cis1.4-3.2-remediation)  |  Ensure CloudTrail log file validation is enabled  | 
|  [2\.3](securityhub-cis-controls.md#cis-2.3-remediation)  |  Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible  |  [3\.3](securityhub-cis-controls-1.4.0.md#cis1.4-3.3-remediation)  |  Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible  | 
|  [2\.4](securityhub-cis-controls.md#cis-2.4-remediation)  |  Ensure CloudTrail trails are integrated with CloudWatch Logs  |  [3\.4](securityhub-cis-controls-1.4.0.md#cis1.4-3.4-remediation)  |  Ensure CloudTrail trails are integrated with CloudWatch Logs  | 
|  [2\.5](securityhub-cis-controls.md#cis-2.5-remediation)  |  Ensure AWS Config is enabled  |  [3\.5](securityhub-cis-controls-1.4.0.md#cis1.4-3.5-remediation)  |  Ensure AWS Config is enabled in all Regions  | 
|  [2\.6](securityhub-cis-controls.md#cis-2.6-remediation)  |  Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket  |  [3\.6](securityhub-cis-controls-1.4.0.md#cis1.4-3.6-remediation)  |  Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket  | 
|  [2\.7](securityhub-cis-controls.md#cis-2.7-remediation)  |  Ensure CloudTrail logs are encrypted at rest using AWS KMS keys  |  [3\.7](securityhub-cis-controls-1.4.0.md#cis1.4-3.7-remediation)  |  Ensure CloudTrail logs are encrypted at rest using AWS KMS keys  | 
|  [2\.8](securityhub-cis-controls.md#cis-2.8-remediation)  |  Ensure rotation for customer\-created KMS keys is enabled  |  [3\.8](securityhub-cis-controls-1.4.0.md#cis1.4-3.8-remediation)  |  Ensure rotation for customer\-created KMS keys is enabled  | 
|  [2\.9](securityhub-cis-controls.md#cis-2.9-remediation)  |  Ensure VPC flow logging is enabled in all VPCs  |  [3\.9](securityhub-cis-controls-1.4.0.md#cis1.4-3.9-remediation)  |  Ensure VPC flow logging is enabled in all VPCs  | 
|  [3\.3](securityhub-cis-controls.md#cis-3.3-remediation)  |  Ensure a log metric filter and alarm exist for usage of root user  |  [1\.7](securityhub-cis-controls-1.4.0.md#cis1.4-1.7-remediation)  |  Eliminate use of the 'root' user for administrative and daily tasks  | 
|  [3\.4](securityhub-cis-controls.md#cis-3.4-remediation)  |  Ensure a log metric filter and alarm exist for IAM policy changes  |  [4\.4](securityhub-cis-controls-1.4.0.md#cis1.4-4.4-remediation)  |  Ensure a log metric filter and alarm exist for IAM policy changes  | 
|  [3\.5](securityhub-cis-controls.md#cis-3.5-remediation)  |  Ensure a log metric filter and alarm exist for CloudTrail configuration change  |  [4\.5](securityhub-cis-controls-1.4.0.md#cis1.4-4.5-remediation)  |  Ensure a log metric filter and alarm exist for CloudTrail configuration change  | 
|  [3\.6](securityhub-cis-controls.md#cis-3.6-remediation)  |  Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  |  [4\.6](securityhub-cis-controls-1.4.0.md#cis1.4-4.6-remediation)  |  Ensure a log metric filter and alarm exist for AWS Management Console authentication failures  | 
|  [3\.7](securityhub-cis-controls.md#cis-3.7-remediation)  |  Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer managed keys  |  [4\.7](securityhub-cis-controls-1.4.0.md#cis1.4-4.7-remediation)  |  Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer managed keys  | 
|  [3\.8](securityhub-cis-controls.md#cis-3.8-remediation)  |  Ensure a log metric filter and alarm exist for S3 bucket policy changes  |  [4\.8](securityhub-cis-controls-1.4.0.md#cis1.4-4.8-remediation)  |  Ensure a log metric filter and alarm exist for S3 bucket policy changes  | 
|  [3\.9](securityhub-cis-controls.md#cis-3.9-remediation)  |  Ensure a log metric filter and alarm exist for AWS Config configuration changes  |  [4\.9](securityhub-cis-controls-1.4.0.md#cis1.4-4.9-remediation)  |  Ensure a log metric filter and alarm exist for AWS Config configuration changes  | 
|  [3\.10](securityhub-cis-controls.md#cis-3.10-remediation)  |  Ensure a log metric filter and alarm exist for security group changes  |  [4\.10](securityhub-cis-controls-1.4.0.md#cis1.4-4.10-remediation)  |  Ensure a log metric filter and alarm exist for security group changes  | 
|  [3\.11](securityhub-cis-controls.md#cis-3.11-remediation)  |  Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  |  [4\.11](securityhub-cis-controls-1.4.0.md#cis1.4-4.11-remediation)  |  Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)  | 
|  [3\.12](securityhub-cis-controls.md#cis-3.12-remediation)  |  Ensure a log metric filter and alarm exist for changes to network gateways  |  [4\.12](securityhub-cis-controls-1.4.0.md#cis1.4-4.12-remediation)  |  Ensure a log metric filter and alarm exist for changes to network gateways  | 
|  [3\.13](securityhub-cis-controls.md#cis-3.13-remediation)  |  Ensure a log metric filter and alarm exist for route table changes  |  [4\.13](securityhub-cis-controls-1.4.0.md#cis1.4-4.13-remediation)  |  Ensure a log metric filter and alarm exist for route table changes  | 
|  [3\.14](securityhub-cis-controls.md#cis-3.14-remediation)  |  Ensure a log metric filter and alarm exist for VPC changes  |  [4\.14](securityhub-cis-controls-1.4.0.md#cis1.4-4.14-remediation)  |  Ensure a log metric filter and alarm exist for VPC changes  | 
|  [4\.3](securityhub-cis-controls.md#cis-4.3-remediation)  |  Ensure the default security group of every VPC restricts all traffic  |  [5\.3](securityhub-cis-controls-1.4.0.md#cis1.4-5.3-remediation)  |  Ensure the default security group of every VPC restricts all traffic  | 

## Finding fields format for CIS AWS Foundations Benchmark v1\.4\.0<a name="cisv1.4.0-finding-fields"></a>

When you enable CIS AWS Foundations Benchmark v1\.4\.0, you'll begin receiving findings in the AWS Security Finding Format \(ASFF\)\. For these findings, standard\-specific fields will reference v1\.4\.0\. For CIS AWS Foundations Benchmark v1\.4\.0, note the following format for [`GeneratorID`](asff-required-attributes.md#GeneratorId) and any ASFF fields that reference the standard Amazon Resource Name \(ARN\)\.
+ **Standard ARN** – `arn:aws::securityhub:region::standards/cis-aws-foundations-benchmark/v/1.4.0`
+ **`GeneratorID`** – `cis-aws-foundations-benchmark/v/1.4.0/control ID`

You can call the [GetEnabledStandards](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html) API operation to find out the ARN of a standard\.

**Note**  
When you enable CIS AWS Foundations Benchmark v1\.4\.0, Security Hub may take up to 18 hours to generate findings for controls that use the same AWS Config service\-linked rule as enabled controls from other enabled standards\. For more information, see [Schedule for running security checks](securityhub-standards-schedule.md)\.

### Sample finding for CIS AWS Foundations Benchmark v1\.4\.0<a name="cisv1.4.0-sample-finding"></a>

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:eu-west-1:123456789012:subscription/cis-aws-foundations-benchmark/v/1.4.0/1.4/finding/aea33149-7039-4138-8e34-00f8fa5026fd",
  "ProductArn": "arn:aws:securityhub:eu-west-1::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "eu-west-1",
  "GeneratorId": "arn:aws:securityhub:::standards/cis-aws-foundations-benchmark/v/1.4.0/1.4",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards/CIS AWS Foundations Benchmark"
  ],
  "FirstObservedAt": "2022-08-16T19:05:32.775Z",
  "LastObservedAt": "2022-08-16T19:05:42.099Z",
  "CreatedAt": "2022-08-16T19:05:32.775Z",
  "UpdatedAt": "2022-08-16T19:05:32.775Z",
  "Severity": {
    "Product": 90,
    "Label": "CRITICAL",
    "Normalized": 90,
    "Original": "CRITICAL"
  },
  "Title": "1.4 Ensure no 'root' user account access key exists",
  "Description": "The root user is the most privileged user in an AWS account. AWS Access Keys provide programmatic access to a given AWS account. It is recommended that all access keys associated with the root user be removed.",
  "Remediation": {
    "Recommendation": {
      "Text": "For directions on how to fix this issue, consult the AWS Security Hub CIS documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/standards-cis-1.4/remediation"
    }
  },
  "ProductFields": {
    "StandardsGuideArn": "arn:aws:securityhub:::standards/cis-aws-foundations-benchmark/v/1.4.0",
    "StandardsGuideSubscriptionArn": "arn:aws:securityhub:eu-west-1:123456789012:subscription/cis-aws-foundations-benchmark/v/1.4.0",
    "RuleId": "1.4",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/standards-cis-1.4/remediation",
    "RelatedAWSResources:0/name": "securityhub-iam-root-access-key-check-53cc262a",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:eu-west-1:123456789012:control/cis-aws-foundations-benchmark/v/1.4.0/1.4",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "Resources:0/Id": "arn:aws:iam::123456789012:root",
    "aws/securityhub/FindingId": "arn:aws:securityhub:eu-west-1::product/aws/securityhub/arn:aws:securityhub:eu-west-1:123456789012:subscription/cis-aws-foundations-benchmark/v/1.4.0/1.4/finding/aea35549-7039-4138-8e34-00f8fa5026fd"
  },
  "Resources": [
    {
      "Type": "AwsAccount",
      "Id": "AWS:::Account:123456789012",
      "Partition": "aws",
      "Region": "eu-west-1"
    }
  ],
  "Compliance": {
    "Status": "FAILED"
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "CRITICAL",
      "Original": "CRITICAL"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards/CIS AWS Foundations Benchmark"
    ]
  }
}
```