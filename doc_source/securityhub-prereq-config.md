# Enabling and configuring AWS Config<a name="securityhub-prereq-config"></a>

AWS Security Hub uses service\-linked AWS Config rules to perform most of its security checks for controls\.

To support these controls, AWS Config must be enabled on all accounts – both the administrator account and member accounts – in each Region where Security Hub is enabled\. AWS Config must be configured to record at a minimum the resources that are required for the standards that you have enabled\.
+ [AWS Config resources required for CIS controls](securityhub-standards-cis-config-resources.md)
+ [AWS Config resources required for PCI DSS controls](securityhub-standards-pci-config-resources.md)
+ [AWS Config resources required for AWS Foundational Security Best Practices controls](standards-fsbp-config-resources.md)

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

1. **Console or CLI** – You can manually enable AWS Config using the AWS Config console or CLI\. See [Getting started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.

1. **AWS CloudFormation template** – If you have integrated with AWS Organizations or want to enable AWS Config on a large set of accounts, you can easily enable AWS Config with the CloudFormation template **Enable AWS Config**\. To access this template, see [AWS CloudFormation StackSets sample templates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html) in the *AWS CloudFormation User Guide*\. For more details about using this template, see [Managing AWS Organizations accounts using AWS Config and AWS CloudFormation StackSets](http://aws.amazon.com/blogs/mt/managing-aws-organizations-accounts-using-aws-config-and-aws-cloudformation-stacksets/)\.

1. **Github script** – Security Hub offers a [script in GitHub](https://github.com/awslabs/aws-securityhub-multiaccount-scripts) that allows you to enable multiple accounts across Regions\. This script is useful if you have not integrated with Organizations or if you have accounts that are not part of your organization\. When you use this script to enable Security Hub, it also automatically enables AWS Config for these accounts\.

## Configuring resource recording in AWS Config<a name="config-resource-recording"></a>

When you enable resource recording during AWS Config setup, AWS Config records all supported types of *regional resources* that AWS Config discovers in the region in which it is running\. You can also configure AWS Config to record supported types of *global resources*\. You only need to record global resources in a single Region\.

If you are using CloudFormation StackSets to enable AWS Config, we recommend that you run two different StackSets\. Run one StackSet to record all resources, including global resources, in a single Region\. Run a second StackSet to record all resources except global resources in other Regions\.

You can also use Quick Setup, a capability of AWS Systems Manager, to quickly configure resource recording in AWS Config across your accounts and Regions\. During Quick Setup, you can choose which Region you would like to record global resources in\. For more information, see [AWS Config recording](https://docs.aws.amazon.com/systems-manager/latest/userguide/quick-setup-config.html) in the *AWS Systems Manager User Guide*\.

If you do not record global resources in all Regions, then in the Regions where you do not record global resources, you must disable the control [2\.5 – Ensure AWS Config is enabled](securityhub-cis-controls.md#securityhub-cis-controls-2.5)\. CIS 2\.5 generates failed findings in Regions where global resources are not recorded\. For details about other controls that you may want to disable in Regions where global resources are not recorded, see the following topics\.
+ [CIS AWS Foundations Benchmark controls that you might want to disable](securityhub-standards-cis-to-disable.md)
+ [PCI DSS controls that you might want to disable](securityhub-standards-pcidss-to-disable.md)
+ [AWS Foundational Best Practices controls that you might want to disable](securityhub-standards-fsbp-to-disable.md)

Note that if you use the [multi\-account script](https://github.com/awslabs/aws-securityhub-multiaccount-scripts) to enable Security Hub, it automatically enables resource recording for all resources, including global resources, in all Regions\. It does not limit recording of global resources to a single Region\. You can then update the configuration to only record global resources in a single Region\. See [Selecting which resources AWS Config records](https://docs.aws.amazon.com/config/latest/developerguide/select-resources.html) in the *AWS Config Developer Guide*\.

The following topics list the required resources for each standard\. You can enable recording only for the required resources\. However, Security Hub continues to add new controls and support new resources\.
+ [AWS Config resources required for CIS controls](securityhub-standards-cis-config-resources.md)
+ [AWS Config resources required for PCI DSS controls](securityhub-standards-pci-config-resources.md)
+ [AWS Config resources required for AWS Foundational Security Best Practices controls](standards-fsbp-config-resources.md)

For details about the costs associated with resource recording, see the [AWS Config pricing page](http://aws.amazon.com/config/pricing/)\.