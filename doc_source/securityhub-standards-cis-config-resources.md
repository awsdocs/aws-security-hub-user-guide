# AWS Config resources required for CIS controls<a name="securityhub-standards-cis-config-resources"></a>

To run security checks for the enabled controls on your environment's resources, Security Hub either runs through the exact audit steps prescribed for the checks in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/) or uses specific AWS Config managed rules\.

Security Hub accurately reports findings for CIS controls only if you're recording resources in AWS Config\. If you aren't recording changes for all required resources in AWS Config, Security Hub generates a finding for controls [2\.5 – Ensure AWS Config is enabled](securityhub-cis-controls.md#securityhub-cis-controls-2.5) \(CIS v1\.2\.0\) and [3\.5 – Ensure AWS Config is enabled in all Regions](securityhub-cis-controls-1.4.0.md#securityhub-cis1.4-controls-3.5) \(CIS v1\.4\.0\)\. You can record resources by following the instructions for [Selecting Resources](https://docs.aws.amazon.com/config/latest/developerguide/select-resources.html) in the *AWS Config Developer Guide*\. If you choose to record all resources supported in the current Region, ensure that you include global resources for all CIS controls to produce findings\. Alternatively, you can record the following specific resources:
+ AWS account
+ `AWS::CloudTrail::Trail`
+ `AWS::EC2::NetworkAcl`
+ `AWS::EC2::SecurityGroup`
+ `AWS::EC2::Volume`
+ `AWS::EC2::VPC`
+ `AWS::IAM::Policy`
+ `AWS::IAM::User`
+ `AWS::KMS::Key`
+ `AWS::RDS::DBInstance`
+ `AWS::S3::Bucket`

When Security Hub runs a security check and generates a finding based on an AWS Config rule, the finding details include a **Rules** link to open the associated AWS Config rule\. To navigate to the AWS Config rule, your account must have IAM permissions to navigate to AWS Config\.