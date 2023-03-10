# Enabling and configuring AWS Config<a name="securityhub-prereq-config"></a>

AWS Security Hub uses service\-linked AWS Config rules to perform most of its security checks for controls\.

To support these controls, AWS Config must be enabled on all accounts—both the administrator account and member accounts—in each AWS Region where Security Hub is enabled\. At a minimum, AWS Config must be configured to record resources that are required for the controls that you have enabled in each enabled standard\. For a listing of required resources in each standard, see [AWS Config resources required to generate control findings](controls-config-resources.md)\.

Security Hub recommends that you enable resource recording in AWS Config before you enable Security Hub standards\. If Security Hub tries to run security checks when resource recording is not enabled, the checks return errors\.

Security Hub does not manage AWS Config for you\. If you already have AWS Config enabled, you can continue to configure its settings through the AWS Config console or APIs\.

If you enable AWS Config after you enable a standard, Security Hub still creates the AWS Config rules, but only if you enable AWS Config within 31 days after you enable the standard\. If you do not enable AWS Config within 31 days, then you must disable and re\-enable the standard after you enable AWS Config\.

After you enable a standard, Security Hub tries to create the AWS Config rules up to six times during the 31 days\.
+ On the day you enable the standard
+ The day after you enable the standard
+ Three days after you enable the standard
+ Seven days after you enable the standard
+ 15 days after you enable the standard
+ 31 days after you enable the standard

## How to enable AWS Config<a name="config-how-to-enable"></a>

If you have not set up AWS Config already, you can set it up in one of the following ways:
+ **Console or CLI** – You can manually enable AWS Config using the AWS Config console or CLI\. See [Getting started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.
+ **AWS CloudFormation template** – If you have integrated with AWS Organizations or want to enable AWS Config on a large set of accounts, you can easily enable AWS Config with the CloudFormation template **Enable AWS Config**\. To access this template, see [AWS CloudFormation StackSets sample templates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html) in the *AWS CloudFormation User Guide*\. For more details about using this template, see [Managing AWS Organizations accounts using AWS Config and AWS CloudFormation StackSets](http://aws.amazon.com/blogs/mt/managing-aws-organizations-accounts-using-aws-config-and-aws-cloudformation-stacksets/)\.
+ **Github script** – Security Hub offers a [script in GitHub](https://github.com/awslabs/aws-securityhub-multiaccount-scripts) that allows you to enable multiple accounts across Regions\. This script is useful if you have not integrated with Organizations or if you have accounts that are not part of your organization\. When you use this script to enable Security Hub, it also automatically enables AWS Config for these accounts\.

## Configuring resource recording in AWS Config<a name="config-resource-recording"></a>

When you enable resource recording during AWS Config setup, AWS Config records all supported types of *regional resources* that AWS Config discovers in the region in which it is running\. You can also configure AWS Config to record supported types of *global resources*\. You only need to record global resources in a single Region\.

If you are using CloudFormation StackSets to enable AWS Config, we recommend that you run two different StackSets\. Run one StackSet to record all resources, including global resources, in a single Region\. Run a second StackSet to record all resources except global resources in other Regions\.

You can also use Quick Setup, a capability of AWS Systems Manager, to quickly configure resource recording in AWS Config across your accounts and Regions\. During Quick Setup, you can choose which Region you would like to record global resources in\. For more information, see [AWS Config recording](https://docs.aws.amazon.com/systems-manager/latest/userguide/quick-setup-config.html) in the *AWS Systems Manager User Guide*\.

If you do not record global resources in all Regions, then in the Regions where you do not record global resources, you must disable the control CIS 2\.5\. This control generates failed findings in Regions where global resources are not recorded\. For details about other controls that you may want to disable in Regions where global resources are not recorded, see [Security Hub controls that you might want to disable](controls-to-disable.md)

Note that if you use the [multi\-account script](https://github.com/awslabs/aws-securityhub-multiaccount-scripts) to enable Security Hub, it automatically enables resource recording for all resources, including global resources, in all Regions\. It does not limit recording of global resources to a single Region\. You can then update the configuration to only record global resources in a single Region\. See [Selecting which resources AWS Config records](https://docs.aws.amazon.com/config/latest/developerguide/select-resources.html) in the *AWS Config Developer Guide*\.

For Security Hub to accurately report findings for all controls, you must enable recording for certain resources in AWS Config\. See [AWS Config resources required to generate control findings](controls-config-resources.md)\.

**Note**  
To generate new findings after security checks and avoid stale findings, you must have sufficient permissions for the IAM role that is attached to the configuration recorder to evaluate the underlying resources\.

For details about the costs associated with resource recording, see [AWS Security Hub pricing](http://aws.amazon.com/security-hub/pricing/) and [AWS Config pricing](http://aws.amazon.com/config/pricing/)\.

Security Hub may impact your AWS Config configuration recorder costs by updating the `AWS::Config::ResourceCompliance` configuration item\. Updates may occur each time an AWS Config rule associated with a Security Hub control changes compliance state or is turned on or off\. If you use the AWS Config configuration recorder only for Security Hub, and don't use this configuration item for other purposes, we recommend turning off recording for it in the AWS Config console or AWS CLI\. This can reduce your AWS Config costs\. For instructions, see [Selecting which resources AWS Config records](https://docs.aws.amazon.com/config/latest/developerguide/select-resources.html) in the *AWS Config Developer Guide*\. You don't need to record `AWS::Config::ResourceCompliance` for security checks to work in Security Hub\. Security Hub only requires recording for the resources listed in [AWS Config resources required to generate control findings](controls-config-resources.md)\.