# Amazon EC2 Systems Manager controls<a name="ssm-controls"></a>

These controls are related to SSM resources\.

## \[SSM\.1\] Amazon EC2 instances should be managed by AWS Systems Manager<a name="ssm-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/2\.4, NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\), NIST\.800\-53\.r5 CM\-8, NIST\.800\-53\.r5 CM\-8\(1\), NIST\.800\-53\.r5 CM\-8\(2\), NIST\.800\-53\.r5 CM\-8\(3\), NIST\.800\-53\.r5 SA\-15\(2\), NIST\.800\-53\.r5 SA\-15\(8\), NIST\.800\-53\.r5 SA\-3, NIST\.800\-53\.r5 SI\-2\(3\)

**Category:** Identify > Inventory

**Severity:** Medium

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-managed-by-systems-manager.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-managed-by-systems-manager.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the stopped and running EC2 instances in your account are managed by AWS Systems Manager\. Systems Manager is an AWS service that you can use to view and control your AWS infrastructure\.

To help you to maintain security and compliance, Systems Manager scans your stopped and running managed instances\. A managed instance is a machine that is configured for use with Systems Manager\. Systems Manager then reports or takes corrective action on any policy violations that it detects\. Systems Manager also helps you to configure and maintain your managed instances\.

To learn more, see [https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="ssm-1-remediation"></a>

You can use the Systems Manager console to remediate this issue\.

**To ensure that EC2 instances are managed by Systems Manager**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation menu, choose **Quick setup**\.

1. Choose **Create**\.

1. Under **Configuration type**, choose **Host Management**, then choose **Next**\.

1. On the configuration screen, you can keep the default options\.

   You can optionally make the following changes:

   1. If you use CloudWatch to monitor EC2 instances, select **Install and configure the CloudWatch agent** and **Update the CloudWatch agent once every 30 days**\.

   1. Under **Targets**, choose the management scope to determine the accounts and Regions where this configuration is applied\.

   1. Under **Instance profile options**, select **Add required IAM policies to existing instance profiles attached to your instances**\.

1. Choose **Create**\.

To determine whether your instances support Systems Manager associations, see [Systems Manager prerequisites](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html) in the *AWS Systems Manager User Guide*\.

## \[SSM\.2\] Amazon EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation<a name="ssm-2"></a>

**Related requirements:** PCI DSS v3\.2\.1/6\.2, NIST\.800\-53\.r5 CM\-8\(3\), NIST\.800\-53\.r5 SI\-2, NIST\.800\-53\.r5 SI\-2\(2\), NIST\.800\-53\.r5 SI\-2\(3\), NIST\.800\-53\.r5 SI\-2\(4\), NIST\.800\-53\.r5 SI\-2\(5\)

**Category:** Detect > Detection services 

**Severity:** High

**Resource type:** `AWS::SSM::PatchCompliance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the compliance status of Systems Manager patch compliance is `COMPLIANT` or `NON_COMPLIANT` after the patch installation on the instance\. It only checks instances that are managed by Systems Manager Patch Manager\.

Having your EC2 instances fully patched as required by your organization reduces the attack surface of your AWS accounts\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(Bahrain\)
Middle East \(UAE\)

### Remediation<a name="ssm-2-remediation"></a>

To remediate this issue, install the required patches on your noncompliant instances\.

**To remediate noncompliant patches**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. Under **Node Management**, choose **Run Command** and then choose **Run command**\.

1. Choose the button next to **AWS\-RunPatchBaseline**\.

1. Change the **Operation** to **Install**\.

1. Choose **Choose instances manually** and then choose the noncompliant instances\.

1. At the bottom of the page, choose **Run**\.

1. After the command is complete, to monitor the new compliance status of your patched instances, in the navigation pane, choose **Compliance**\.

For more information about using Systems Manager documents to patch a managed instance, see[ About SSM documents for patching instances](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-ssm-documents.html) and [Running commands using Systems Manager Run command](https://docs.aws.amazon.com/systems-manager/latest/userguide/run-command.html) in the *AWS Systems Manager User Guide*\.

## \[SSM\.3\] Amazon EC2 instances managed by Systems Manager should have an association compliance status of COMPLIANT<a name="ssm-3"></a>

**Related requirements:** PCI DSS v3\.2\.1/2\.4, NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\), NIST\.800\-53\.r5 CM\-8, NIST\.800\-53\.r5 CM\-8\(1\), NIST\.800\-53\.r5 CM\-8\(3\), NIST\.800\-53\.r5 SI\-2\(3\)

**Category:** Detect > Detection services

**Severity:** Low

**Resource type:** `AWS::SSM::AssociationCompliance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-association-compliance-status-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-association-compliance-status-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the status of the AWS Systems Manager association compliance is `COMPLIANT` or `NON_COMPLIANT` after the association is run on an instance\. The control passes if the association compliance status is `COMPLIANT`\.

A State Manager association is a configuration that is assigned to your managed instances\. The configuration defines the state that you want to maintain on your instances\. For example, an association can specify that antivirus software must be installed and running on your instances or that certain ports must be closed\. 

After you create one or more State Manager associations, compliance status information is immediately available to you\. You can view the compliance status in the console or in response to AWS CLI commands or corresponding Systems Manager API actions\. For associations, Configuration Compliance shows the compliance status \(`Compliant` or `Non-compliant`\)\. It also shows the severity level assigned to the association, such as `Critical` or `Medium`\.

To learn more about State Manager association compliance, see [About State Manager association compliance](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-compliance-about.html#sysman-compliance-about-association) in the *AWS Systems Manager User Guide*\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="ssm-3-remediation"></a>

A failed association can be related to different things, including targets and SSM document names\. To remediate this issue, you must first identify and investigate the association\. You can then update the association to correct the specific issue\.

You can edit an association to specify a new name, schedule, severity level, or targets\. After you edit an association, AWS Systems Manager creates a new version\.

**To investigate and update a failed association**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation pane, under **Node Management**, choose **Fleet Manager**\.

1. Choose the instance ID that has an **Association status** of **Failed**\.

1. Choose **View details**\.

1. Choose **Associations**\.

1. Note the name of the association that has an **Association status** of **Failed**\. This is the association that you need to investigate\. You need to use the association name in the next step\.

1. In the navigation pane, under **Node Management**, choose **State Manager**\. Search for the association name, then select the association\.

1. After you determine the issue, edit the failed association to correct the problem\. For information on how to edit an association, see [Edit an association](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-state-assoc-edit.html)\.

For more information on creating and editing State Manager associations, see [Working with associations in Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-associations.html) in the *AWS Systems Manager User Guide*\.

## \[SSM\.4\] SSM documents should not be public<a name="ssm-4"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration > Resources not publicly accessible

**Severity:** Critical

**Resource type:** `AWS::SSM::Document`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ssm-document-not-public.html](https://docs.aws.amazon.com/config/latest/developerguide/ssm-document-not-public.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether AWS Systems Manager documents that are owned by the account are public\. This control fails if SSM documents with the owner `Self` are public\.

SSM documents that are public might allow unintended access to your documents\. A public SSM document can expose valuable information about your account, resources, and internal processes\.

Unless your use case requires public sharing to be enabled, Security Hub recommends that you turn on the block public sharing setting for your Systems Manager documents that are owned by `Self`\.

**Note**  
This control is not supported in the following Regions:  
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ssm-4-remediation"></a>



For more information about disabling public access to SSM documents, see [Modify permissions for a shared SSM document](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-share-modify.html) and [Best practices for shared SSM documents](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-before-you-share.html) in the *AWS Systems Manager User Guide*\.