# AWS Config controls<a name="config-controls"></a>

These controls are related to AWS Config resources\.

## \[Config\.1\] AWS Config should be enabled<a name="config-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/10\.5\.2,PCI DSS v3\.2\.1/11\.5, CIS AWS Foundations Benchmark v1\.2\.0/2\.5, CIS AWS Foundations Benchmark v1\.4\.0/3\.5, NIST\.800\-53\.r5 CM\-3, NIST\.800\-53\.r5 CM\-6\(1\), NIST\.800\-53\.r5 CM\-8, NIST\.800\-53\.r5 CM\-8\(2\)

**Category:** Identify > Inventory

**Severity:** Medium

**Resource type:** AWS account

**AWS Config rule:** None

**Schedule type:** Periodic

**Parameters:** None

This control checks whether AWS Config is enabled in the account for the local Region and is recording all resources\.

The AWS Config service performs configuration management of supported AWS resources in your account and delivers log files to you\. The recorded information includes the configuration item \(AWS resource\), relationships between configuration items, and any configuration changes between resources\. 

Security Hub recommends that you enable AWS Config in all Regions\. The AWS configuration item history that AWS Config captures enables security analysis, resource change tracking, and compliance auditing\. 

**Note**  
Config\.1 requires that AWS Config is enabled in all Regions in which you use Security Hub\.  
Because Security Hub is a Regional service, the check performed for this control checks only the current Region for the account\. It does not check all Regions\.   
To allow security checks against global resources in each Region, you also must record global resources\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.  
You may also consider disabling IAM\.1, IAM\.2, IAM\.3, IAM\.5, IAM\.8, and IAM\.21 in Regions in which global resource recording not enabled\. Since IAM is a global service, IAM resources will only be recorded in the Region in which global resource recording is enabled\.

To learn more, see [Getting started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.

### Remediation<a name="config-1-remediation"></a>

After you enable AWS Config, configure it to record all resources\.

**To configure AWS Config settings**

1. Open the AWS Config console at [https://console\.aws\.amazon\.com/config/](https://console.aws.amazon.com/config/)\.

1. Select the Region to configure AWS Config in\.

1. If you haven't used AWS Config before, see [Getting Started](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.

1. Navigate to the Settings page from the menu, and do the following:
   + Choose **Edit**\.
   + Under **Resource types to record**, select **Record all resources supported in this region** and **Include global resources \(e\.g\., AWS IAM resources\)**\.
   + Under **Data retention period**, choose the default retention period for AWS Config data, or specify a custom retention period\.
   + Under **AWS Config role**, either choose **Create AWS Config service\-linked role** or choose **Choose a role from your account** and then select the role to use\.
   + Under **Amazon S3 bucket**, specify the bucket to use or create a bucket and optionally include a prefix\.
   + Under **Amazon SNS topic**, select an Amazon SNS topic from your account or create one\. For more information about Amazon SNS, see the [https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html)\.

1. Choose **Save**\.

For more information about using AWS Config from the AWS CLI, see [Turning on AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/gs-cli-subscribe.html) in the *AWS Config Developer Guide*\. 

You can also use an AWS CloudFormation template to automate this process\. For more information, see the [AWS CloudFormation StackSets sample template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html) in the *AWS CloudFormation User Guide*\. 