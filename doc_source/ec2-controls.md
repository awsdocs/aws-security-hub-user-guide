# Amazon Elastic Compute Cloud controls<a name="ec2-controls"></a>

These controls are related to Amazon EC2\.

## \[EC2\.1\] Amazon EBS snapshots should not be publicly restorable<a name="ec2-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1,PCI DSS v3\.2\.1/1\.3\.1,PCI DSS v3\.2\.1/1\.3\.4,PCI DSS v3\.2\.1/7\.2\.1, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration

**Severity:** Critical 

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether Amazon Elastic Block Store snapshots are not public\. The control fails if Amazon EBS snapshots are restorable by anyone\.

EBS snapshots are used to back up the data on your EBS volumes to Amazon S3 at a specific point in time\. You can use the snapshots to restore previous states of EBS volumes\. It is rarely acceptable to share a snapshot with the public\. Typically the decision to share a snapshot publicly was made in error or without a complete understanding of the implications\. This check helps ensure that all such sharing was fully planned and intentional\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="ec2-1-remediation"></a>

To remediate this issue, update your EBS snapshot to make it private instead of public\.

**To make a public EBS snapshot private**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Elastic Block Store**, choose **Snapshots** menu and then choose your public snapshot\.

1. From **Actions**, choose **Modify permissions**\.

1. Choose **Private**\.

1. \(Optional\) Add the AWS account numbers of the authorized accounts to share your snapshot with and choose **Add Permission**\.

1. Choose **Save**\.

## \[EC2\.2\] The VPC default security group should not allow inbound and outbound traffic<a name="ec2-2"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1,PCI DSS v3\.2\.1/1\.3\.4,PCI DSS v3\.2\.1/2\.1, CIS AWS Foundations Benchmark v1\.2\.0/4\.3, CIS AWS Foundations Benchmark v1\.4\.0/5\.3, NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(5\)

**Category:** Protect > Secure network configuration

**Severity:** High 

**Resource type:** `AWS::EC2::SecurityGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks that the default security group of a VPC does not allow inbound or outbound traffic\.

The rules for the [default security group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#DefaultSecurityGroup) allow all outbound and inbound traffic from network interfaces \(and their associated instances\) that are assigned to the same security group\.

We do not recommend using the default security group\. Because the default security group cannot be deleted, you should change the default security group rules setting to restrict inbound and outbound traffic\. This prevents unintended traffic if the default security group is accidentally configured for resources such as EC2 instances\.

### Remediation<a name="ec2-2-remediation"></a>

To remediate this issue, create new security groups and assign those security groups to your resources\. To prevent the default security groups from being used, remove their inbound and outbound rules\.

**To create new security groups and assign them to your resources**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Security groups**\. View the default security groups details to see the resources that are assigned to them\.

1. Create a set of least\-privilege security groups for the resources\. For details on how to create security groups, see [Creating a security group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#CreatingSecurityGroups) in the *Amazon VPC User Guide*\.

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the Amazon EC2 console, change the security group for the resources that use the default security groups to the least\-privilege security group you created\. See [Changing an instance's security groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#SG_Changing_Group_Membership) in the *Amazon VPC User Guide*\.

After you assign the new security groups to the resources, remove the inbound and outbound rules from the default security groups\. This ensures that the default security groups are not used\.

**To remove the rules from the default security group**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Security groups**\.

1. Select a default security group and choose the **Inbound rules** tab\. Choose **Edit inbound rules**\. Then delete all inbound rules\. Choose **Save rules**\.

1. Repeat the previous step for each default security group\.

1. Select a default security group and choose the **Outbound rule** tab\. Choose **Edit outbound rules**\. Then delete all outbound rules\. Choose **Save rules**\.

1. Repeat the previous step for each default security group\.

For more information, see [Working with security groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the *Amazon VPC User Guide*\.

## \[EC2\.3\] Attached Amazon EBS volumes should be encrypted at\-rest<a name="ec2-3"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::EC2::Volume`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/encrypted-volumes.html](https://docs.aws.amazon.com/config/latest/developerguide/encrypted-volumes.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the EBS volumes that are in an attached state are encrypted\. To pass this check, EBS volumes must be in use and encrypted\. If the EBS volume is not attached, then it is not subject to this check\.

For an added layer of security of your sensitive data in EBS volumes, you should enable EBS encryption at rest\. Amazon EBS encryption offers a straightforward encryption solution for your EBS resources that doesn't require you to build, maintain, and secure your own key management infrastructure\. It uses KMS keys when creating encrypted volumes and snapshots\.

To learn more about Amazon EBS encryption, see [Amazon EBS encryption](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html) in the *Amazon EC2 User Guide for Linux Instances*\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="ec2-3-remediation"></a>

There is no direct way to encrypt an existing unencrypted volume or snapshot\. You can only encrypt a new volume or snapshot when you create it\.

If you enabled encryption by default, Amazon EBS encrypts the resulting new volume or snapshot using your default key for Amazon EBS encryption\. Even if you have not enabled encryption by default, you can enable encryption when you create an individual volume or snapshot\. In both cases, you can override the default key for Amazon EBS encryption and choose a symmetric customer managed key\.

For more information, see [Creating an Amazon EBS volume](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-creating-volume.html) and [Copying an Amazon EBS snapshot](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-copy-snapshot.html) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.4\] Stopped Amazon EC2 instances should be removed after a specified time period<a name="ec2-4"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\)

**Category:** Identify > Inventory

**Severity:** Medium

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-stopped-instance.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-stopped-instance.html)

**Schedule type:** Periodic

**Parameters:**
+ `allowedDays`: 30

This control checks whether any EC2 instances have been stopped for more than the allowed number of days\. An EC2 instance fails this check if it is stopped for longer than the maximum allowed time period, which by default is 30 days\.

A failed finding indicates that an EC2 instance has not run for a significant period of time\. This creates a security risk because the EC2 instance is not being actively maintained \(analyzed, patched, updated\)\. If it is later launched, the lack of proper maintenance could result in unexpected issues in your AWS environment\. To safely maintain an EC2 instance over time in a nonrunning state, start it periodically for maintenance and then stop it after maintenance\. Ideally this is an automated process\. 

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="ec2-4-remediation"></a>

You can terminate an EC2 instance using either the console or the command line\.

Before you terminate the EC2 instance, verify that you won't lose any data:
+ Check that your Amazon EBS volumes will not be deleted on termination\.
+ Copy any data that you need from your EC2 instance store volumes to Amazon EBS or Amazon S3\. 

**To terminate an EC2 instance \(console\)**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Instances**, choose **Instances**\.

1. Select the instance, and then choose **Actions**, **Instance State**, **Terminate**\. 

1. When prompted for confirmation, choose **Yes, Terminate**\. 

**To terminate an EC2 instance \(AWS CLI, Tools for Windows PowerShell\)**  
Use one of the following commands\. For more information about the command line interface, see [Accessing Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html#access-ec2) in the *Amazon EC2 User Guide for Linux Instances*\.
+ From the AWS CLI, use [https://docs.aws.amazon.com/cli/latest/reference/ec2/terminate-instances.html](https://docs.aws.amazon.com/cli/latest/reference/ec2/terminate-instances.html)
+ From the Tools for Windows PowerShell, use [https://docs.aws.amazon.com/powershell/latest/reference/items/Stop-EC2Instance.html](https://docs.aws.amazon.com/powershell/latest/reference/items/Stop-EC2Instance.html)\.

To learn more about terminating instances, see [Terminating an instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/terminating-instances.html#terminating-instances-console) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.6\] VPC flow logging should be enabled in all VPCs<a name="ec2-6"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/2\.9, PCI DSS v3\.2\.1/10\.3\.3,PCI DSS v3\.2\.1/10\.3\.4,PCI DSS v3\.2\.1/10\.3\.5,PCI DSS v3\.2\.1/10\.3\.6, CIS AWS Foundations Benchmark v1\.4\.0/3\.9, NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SI\-7\(8\)

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::EC2::VPC`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html)

**Schedule type:** Periodic

**Parameters:**
+ `trafficType`: `REJECT`

This control checks whether Amazon VPC Flow Logs are found and enabled for VPCs\. The traffic type is set to `Reject`\. 

With the VPC Flow Logs feature, you can capture information about the IP address traffic going to and from network interfaces in your VPC\. After you create a flow log, you can view and retrieve its data in CloudWatch Logs\. To reduce cost, you can also send your flow logs to Amazon S3\. 

Security Hub recommends that you enable flow logging for packet rejects for VPCs\. Flow logs provide visibility into network traffic that traverses the VPC and can detect anomalous traffic or provide insight during security workflows\.

By default, the record includes values for the different components of the IP address flow, including the source, destination, and protocol\. For more information and descriptions of the log fields, see [VPC Flow Logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html) in the *Amazon VPC User Guide*\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="ec2-6-remediation"></a>

To remediate this issue, enable VPC flow logging\.

**To enable VPC flow logging**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Under **Virtual Private Cloud**, choose **Your VPCs**\.

1. Select a VPC to update\.

1. At the bottom of the page, choose **Flow Logs**\.

1. Choose **Create flow log**\.

1. For **Filter**, choose **Reject**\.

1. For **Destination log group**, choose the log group to use\.

1. For **IAM role**, choose the IAM role to use\.

1. Choose **Create**\.

## \[EC2\.7\] Amazon EBS default encryption should be enabled<a name="ec2-7"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.4\.0/2\.2\.1, NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest 

**Severity:** Medium

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-ebs-encryption-by-default.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-ebs-encryption-by-default.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether account\-level encryption is enabled by default for Amazon Elastic Block Store\(Amazon EBS\)\. The control fails if the account level encryption is not enabled\. 

When encryption is enabled for your account, Amazon EBS volumes and snapshot copies are encrypted at rest\. This adds an additional layer of protection for your data\. For more information, see [Encryption by default](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html#encryption-by-default) in the *Amazon EC2 User Guide for Linux Instances*\.

Note that following instance types do not support encryption: R1, C1, and M1\.

**Note**  
This control is not supported in the following Regions\.  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
Middle East \(UAE\)

### Remediation<a name="ec2-7-remediation"></a>

You can use the Amazon EC2 console to enable default encryption for Amazon EBS volumes\.

**To configure the default encryption for Amazon EBS encryption for a Region**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the navigation pane, select **EC2 Dashboard**\.

1. In the upper\-right corner of the page, choose **Account Attributes, EBS encryption**\.

1. Choose **Manage**\.

1. Select **Enable**\. You can keep the AWS managed key with the alias `alias/aws/ebs` created on your behalf as the default encryption key, or choose a symmetric customer managed key\.

1. Choose **Update EBS encryption**\.

## \[EC2\.8\] Amazon EC2 instances should use Instance Metadata Service Version 2 \(IMDSv2\)<a name="ec2-8"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-6

**Category:** Protect > Network security

**Severity:** High

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-imdsv2-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-imdsv2-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether your EC2 instance metadata version is configured with Instance Metadata Service Version 2 \(IMDSv2\)\. The control passes if `HttpTokens` is set to required for IMDSv2\. The control fails if `HttpTokens` is set to `optional`\.

You use instance metadata to configure or manage the running instance\. The IMDS provides access to temporary, frequently rotated credentials\. These credentials remove the need to hard code or distribute sensitive credentials to instances manually or programmatically\. The IMDS is attached locally to every EC2 instance\. It runs on a special "link local" IP address of 169\.254\.169\.254\. This IP address is only accessible by software that runs on the instance\.

Version 2 of the IMDS adds new protections for the following types of vulnerabilities\. These vulnerabilities could be used to try to access the IMDS\.
+ Open website application firewalls
+ Open reverse proxies
+ Server\-side request forgery \(SSRF\) vulnerabilities
+ Open Layer 3 firewalls and network address translation \(NAT\)

Security Hub recommends that you configure your EC2 instances with IMDSv2\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="ec2-8-remediation"></a>

To remediate an EC2 instance that is not configured with IMDSv2, you can require the use of IMDSv2\.

To require IMDSv2 on an existing instance, when you request instance metadata, modify the Amazon EC2 metadata options\. Follow the instructions in [Configuring instance metadata options for existing instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html) in the *Amazon EC2 User Guide for Linux Instances*\.

To require the use of IMDSv2 on a new instance when you launch it, follow the instructions in [Configuring instance metadata options for new instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html) in the *Amazon EC2 User Guide for Linux Instances*\.

**To configure your new EC2 instance with IMDSv2 from the console**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. Choose **Launch instance**, and then choose **Launch instance**\.

1. Under **Advanced details**, for **Metadata version**, choose **V2 only \(token required\)**\.

1. In the Summary panel, review your changes, and then choose **Launch instance**\.

If your software uses IMDSv1, you can reconfigure your software to use IMDSv2\. For details, see [Transitioning to using Instance Metadata Service Version 2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html#instance-metadata-transition-to-version-2) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.9\] Amazon EC2 instances should not have a public IPv4 address<a name="ec2-9"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration > Public IP addresses

**Severity:** High

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-no-public-ip.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-no-public-ip.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether EC2 instances have a public IP address\. The control fails if the `publicIp` field is present in the EC2 instance configuration item\. This control applies to IPv4 addresses only\. 

A public IPv4 address is an IP address that is reachable from the internet\. If you launch your instance with a public IP address, then your EC2 instance is reachable from the internet\. A private IPv4 address is an IP address that is not reachable from the internet\. You can use private IPv4 addresses for communication between EC2 instances in the same VPC or in your connected private network\.

IPv6 addresses are globally unique, and therefore are reachable from the internet\. However, by default all subnets have the IPv6 addressing attribute set to false\. For more information about IPv6, see [IP addressing in your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-ip-addressing.html) in the *Amazon VPC User Guide*\.

If you have a legitimate use case to maintain EC2 instances with public IP addresses, then you can suppress the findings from this control\. For more information about front\-end architecture options, see the [AWS Architecture Blog](http://aws.amazon.com/blogs/architecture/) or the [This Is My Architecture series](http://aws.amazon.com/this-is-my-architecture/?tma.sort-by=item.additionalFields.airDate&tma.sort-order=desc&awsf.category=categories%23mobile)\.

### Remediation<a name="ec2-9-remediation"></a>

Use a non\-default VPC so that your instance is not assigned a public IP address by default\.

When you launch an EC2 instance into a default VPC, it is assigned a public IP address\. When you launch an EC2 instance into a non\-default VPC, the subnet configuration determines whether it receives a public IP address\. The subnet has an attribute to determine if new EC2 instances in the subnet receive a public IP address from the public IPv4 address pool\.

You cannot manually associate or disassociate an automatically\-assigned public IP address from your EC2 instance\. To control whether your EC2 instance receives a public IP address, do one of the following:
+ Modify the public IP addressing attribute of your subnet\. For more information, see [Modifying the public IPv4 addressing attribute for your subnet](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-ip-addressing.html#subnet-public-ip) in the *Amazon VPC User Guide*\. 
+ Enable or disable the public IP addressing feature during launch\. This overrides the subnet's public IP addressing attribute\. For more information, see[ Assign a public IPv4 address during instance launch](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html#public-ip-addresses) in the *Amazon EC2 User Guide for Linux Instances*\.

For more information, see [Public IPv4 addresses and external DNS hostnames](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html#concepts-public-addresses) in the *Amazon EC2 User Guide for Linux Instances*\.

If your EC2 instance is associated with an Elastic IP address, then your EC2 instance is reachable from the internet\. You can disassociate an Elastic IP address from an instance or network interface at any time\.

**To disassociate an Elastic IP address**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Elastic IPs**\.

1. Select the Elastic IP address to disassociate\.

1. From **Actions**, choose **Disassociate Elastic IP address**\.

1. Choose **Disassociate**\.

## \[EC2\.10\] Amazon EC2 should be configured to use VPC endpoints that are created for the Amazon EC2 service<a name="ec2-10"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\)

**Category:** Protect > Secure network configuration > API private access

**Severity:** Medium

**Resource type:** `AWS::EC2::VPC`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/service-vpc-endpoint-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/service-vpc-endpoint-enabled.html)

**Schedule type:** Periodic

**Parameters:** 
+ `serviceName`: `ec2`

This control checks whether a service endpoint for Amazon EC2 is created for each VPC\. The control fails if a VPC does not have a VPC endpoint created for the Amazon EC2 service\. 

This control evaluates resources in single account\. It cannot describe resources that are outside of the account\. Because AWS Config and Security Hub do not conduct cross\-account checks, you will see `FAILED` findings for VPCs that are shared across accounts\. Security Hub recommends that you suppress these `FAILED` findings\.

To improve the security posture of your VPC, you can configure Amazon EC2 to use an interface VPC endpoint\. Interface endpoints are powered by AWS PrivateLink, a technology that enables you to access Amazon EC2 API operations privately\. It restricts all network traffic between your VPC and Amazon EC2 to the Amazon network\. Because endpoints are supported within the same Region only, you cannot create an endpoint between a VPC and a service in a different Region\. This prevents unintended Amazon EC2 API calls to other Regions\. 

To learn more about creating VPC endpoints for Amazon EC2, see [Amazon EC2 and interface VPC endpoints ](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/interface-vpc-endpoints.html)in the *Amazon EC2 User Guide for Linux Instances*\.

### Remediation<a name="ec2-10-remediation"></a>

To remediate this issue, you can create an interface VPC endpoint to Amazon EC2\.

**To create an interface endpoint to Amazon EC2 from the Amazon VPC console**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Endpoints**\.

1. Choose **Create Endpoint**\. 

1. For **Service category**, choose **AWS services**\. 

1. For **Service Name**, choose **com\.amazonaws\.<region>\.ec2**\.

1. For **Type**, choose **Interface**\. 

1. Complete the following information\. 

   1. For **VPC**, select a VPC in which to create the endpoint\. 

   1. For **Subnets**, select the subnets \(Availability Zones\) in which to create the endpoint network interfaces\. Not all Availability Zones are supported for all AWS services\. 

   1. To enable private DNS for the interface endpoint, select the check box for **Enable DNS Name**\. This option is enabled by default\.

      To use the private DNS option, the following attributes of your VPC must be set to true:
      + `enableDnsHostnames`
      + `enableDnsSupport`

      For more information, see [Viewing and updating DNS support for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-dns-updating) in the *Amazon VPC User Guide*\. 

   1. For **Security group**, select the security groups to associate with the endpoint network interfaces\. 

   1. \(Optional\) Add or remove a tag\. To add a tag, choose **Add tag** and do the following: 
      + For **Key**, enter the tag name\. 
      + For **Value**, enter the tag value\.

   1. To remove a tag, choose the delete button \(**x**\) to the right of the tag **Key** and **Value**\. 

1. Choose **Create endpoint**\.

**To create an interface VPC endpoint policy**

You can attach a policy to your VPC endpoint to control access to the Amazon EC2 API\. The policy specifies the following: 
+ The principal that can perform actions
+ The actions that can be performed
+ The resource on which the actions can be performed

For more details on creating a VPC endpoint policy, see [Amazon EC2 and interface VPC endpoints](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/interface-vpc-endpoints.html) In the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.12\] Unused Amazon EC2 EIPs should be removed<a name="ec2-12"></a>

**Related requirements:** PCI DSS v3\.2\.1/2\.4, NIST\.800\-53\.r5 CM\-8\(1\)

**Category:** Protect > Secure network configuration

**Severity:** Low

**Resource type:** `AWS::EC2::EIP`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/eip-attached.html](https://docs.aws.amazon.com/config/latest/developerguide/eip-attached.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Elastic IP \(EIP\) addresses that are allocated to a VPC are attached to EC2 instances or in\-use elastic network interfaces \(ENIs\)\.

A failed finding indicates you may have unused EC2 EIPs\.

This will help you maintain an accurate asset inventory of EIPs in your cardholder data environment \(CDE\)\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="ec2-12-remediation"></a>

If you no longer need an Elastic IP address, Security Hub recommends that you release it \(the address must not be associated with an instance\)\. 

**To release an Elastic IP address using the console**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Network & Security**, choose **Elastic IPs**\. 

1. Choose the Elastic IP address, choose **Actions**, and then choose **Release Elastic IP address**\.

1. When prompted, choose **Release**\. 

For more information, see the information on releasing Elastic IP addresses in the [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-eips-releasing](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-eips-releasing)\.

## \[EC2\.13\] Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22<a name="ec2-13"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/4\.1, PCI DSS v3\.2\.1/1\.2\.1,PCI DSS v3\.2\.1/1\.3\.1,PCI DSS v3\.2\.1/2\.2\.2, NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 CM\-7, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(5\)

**Category:** Protect > Secure network configuration

**Severity:** High

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/restricted-ssh.html](https://docs.aws.amazon.com/config/latest/developerguide/restricted-ssh.html)

**Schedule type:** Change triggered

Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\.

CIS recommends that no security group allow unrestricted ingress access to port 22\. Removing unfettered connectivity to remote console services, such as SSH, reduces a server's exposure to risk\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="ec2-13-remediation"></a>

Perform the following steps for each security group associated with a VPC\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the left pane, choose **Security groups**\.

1. Select a security group\.

1. In the bottom section of the page, choose the **Inbound Rules** tab\.

1. Choose **Edit rules**\.

1. Identify the rule that allows access through port 22 and then choose the **X** to remove it\.

1. Choose **Save rules**\.

## \[EC2\.14\] Ensure no security groups allow ingress from 0\.0\.0\.0/0 to port 3389<a name="ec2-14"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/4\.2

**Category:** Protect > Secure network configuration

**Severity:** High

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/restricted-common-ports.html](https://docs.aws.amazon.com/config/latest/developerguide/restricted-common-ports.html)

**Schedule type:** Change triggered

The name of the associated AWS Config managed rule is` restricted-common-ports`\. However, the rule that is created uses the name `restricted-rdp`\.

Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\.

CIS recommends that no security group allow unrestricted ingress access to port 3389\. Removing unfettered connectivity to remote console services, such as RDP, reduces a server's exposure to risk\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="ec2-14-remediation"></a>

Perform the following steps for each security group associated with a VPC\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the left pane, choose **Security groups**\.

1. Select a security group\.

1. In the bottom section of the page, choose the **Inbound Rules** tab\.

1. Choose **Edit rules**\.

1. Identify the rule that allows access through port 3389 and then choose the **X** to remove it\.

1. Choose **Save rules**\.

## \[EC2\.15\] Amazon EC2 subnets should not automatically assign public IP addresses<a name="ec2-15"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Network security

**Severity:** Medium

**Resource type:** `AWS::EC2::Subnet`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/subnet-auto-assign-public-ip-disabled.html](https://docs.aws.amazon.com/config/latest/developerguide/subnet-auto-assign-public-ip-disabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the assignment of public IPs in Amazon Virtual Private Cloud \(Amazon VPC\) subnets have `MapPublicIpOnLaunch` set to `FALSE`\. The control passes if the flag is set to `FALSE`\. 

All subnets have an attribute that determines whether a network interface created in the subnet automatically receives a public IPv4 address\. Instances that are launched into subnets that have this attribute enabled have a public IP address assigned to their primary network interface\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-15-remediation"></a>

You can configure a subnet from the Amazon VPC console\.

**To configure a subnet to not assign public IP addresses**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Subnets**\.

1. Select your subnet and then choose **Subnet Actions**, **Modify auto\-assign IP settings**\.

1. Clear the **Enable auto\-assign public IPv4 address** check box and then choose **Save**\.

## \[EC2\.16\] Unused Network Access Control Lists should be removed<a name="ec2-16"></a>

**Related requirements:** NIST\.800\-53\.r5 CM\-8\(1\)

**Category:** Prevent > Network security 

**Severity:** Low

**Resource type:** `AWS::EC2::NetworkAcl`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-network-acl-unused-check.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-network-acl-unused-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether there are any unused network access control lists \(ACLs\)\.

The control checks the item configuration of the resource `AWS::EC2::NetworkAcl` and determines the relationships of the network ACL\.

If the only relationship is the VPC of the network ACL, then the control fails\.

If other relationships are listed, then the control passes\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-16-remediation"></a>

For instructions on how to delete an unused network ACL, see [Deleting a network ACL](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html#DeleteNetworkACL) in the *Amazon VPC User Guide*\. You cannot delete the default network ACL or an ACL that is associated with subnets\.

## \[EC2\.17\] Amazon EC2 instances should not use multiple ENIs<a name="ec2-17"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(21\)

**Category:** Network security

**Severity:** Low

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-multiple-eni-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-multiple-eni-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `Adapterids` \(Optional\) – A list of network interface IDs that are attached to EC2 instances

This control checks whether an EC2 instance uses multiple Elastic Network Interfaces \(ENIs\) or Elastic Fabric Adapters \(EFAs\)\. This control passes if a single network adapter is used\. The control includes an optional parameter list to identify the allowed ENIs\.

Multiple ENIs can cause dual\-homed instances, meaning instances that have multiple subnets\. This can add network security complexity and introduce unintended network paths and access\.

This control also fails if an Amazon EKS cluster that belongs to an Amazon EKS cluster has more than one ENI\. If you need to use EC2 instances that have multiple ENIs as part of an Amazon EKS cluster, you can suppress those findings\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-17-remediation"></a>

To remediate this issue, detach the additional ENIs\.

**To detach a network interface**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. Under **Network & Security**, choose **Network Interfaces**\.

1. Filter the list by the noncompliant instance IDs to see the associated ENIs\.

1. Select the ENIs that you want to remove\.

1. From the **Actions** menu, choose **Detach**\.

1. If you see the prompt **Are you sure that you want to detach the following network interface?**, choose **Detach**\.

## \[EC2\.18\] Security groups should only allow unrestricted incoming traffic for authorized ports<a name="ec2-18"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(5\)

**Category:** Protect > Secure network configuration > Security group configuration

**Severity:** High

**Resource type:** `AWS::EC2::SecurityGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-sg-open-only-to-authorized-ports.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-sg-open-only-to-authorized-ports.html)

**Schedule type:** Change triggered

**Parameters:**
+ `authorizedTcpPorts` \(Optional\) – Comma\-separated list of ports to which to allow unrestricted access\. For example: `'80, 443'`\. For this rule, the default values for `authorizedTcpPorts` are 80 and 443\.

This control checks whether the security groups that are in use allow unrestricted incoming traffic\. Optionally the rule checks whether the port numbers are listed in the `authorizedTcpPorts` parameter\.
+ If the security group rule port number allows unrestricted incoming traffic, but the port number is specified in `authorizedTcpPorts`, then the control passes\. The default value for `authorizedTcpPorts` is `80, 443`\.
+ If the security group rule port number allows unrestricted incoming traffic, but the port number is not specified in `authorizedTcpPorts` input parameter, then the control fails\.
+ If the parameter is not used, then the control fails for any security group that has an unrestricted inbound rule\.

Security groups provide stateful filtering of ingress and egress network traffic to AWS\. Security group rules should follow the principal of least privileged access\. Unrestricted access \(IP address with a /0 suffix\) increases the opportunity for malicious activity such as hacking, denial\-of\-service attacks, and loss of data\.

Unless a port is specifically allowed, the port should deny unrestricted access\.

**Note**  
This control is not supported in Asia Pacific \(Osaka\)\.

### Remediation<a name="ec2-18-remediation"></a>

For information on how to modify a security group, see [Add, remove, or update rules](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#AddRemoveRules) in the *Amazon VPC User Guide*\.

## \[EC2\.19\] Security groups should not allow unrestricted access to ports with high risk<a name="ec2-19"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\), NIST\.800\-53\.r5 CM\-7, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(5\)

**Category:** Protect > Restricted network access

**Severity:** Critical

**Resource type:** `AWS::EC2::SecurityGroup`

**AWS Config rule:** `vpc-sg-restricted-common-ports` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether unrestricted incoming traffic for the security groups is accessible to the specified ports that have the highest risk\. This control fails if any of the rules in a security group allow ingress traffic from '0\.0\.0\.0/0' or '::/0' for those ports\.

Unrestricted access \(0\.0\.0\.0/0\) increases opportunities for malicious activity, such as hacking, denial\-of\-service attacks, and loss of data\.

Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\. No security group should allow unrestricted ingress access to the following ports:
+ 20, 21 \(FTP\)
+ 22 \(SSH\)
+ 23 \(Telnet\)
+ 25 \(SMTP\)
+ 110 \(POP3\)
+ 135 \(RPC\)
+ 143 \(IMAP\)
+ 445 \(CIFS\)
+ 1433, 1434 \(MSSQL\)
+ 3000 \(Go, Node\.js, and Ruby web development frameworks\)
+ 3306 \(mySQL\)
+ 3389 \(RDP\)
+ 4333 \(ahsp\)
+ 5000 \(Python web development frameworks\)
+ 5432 \(postgresql\)
+ 5500 \(fcp\-addr\-srvr1\) 
+ 5601 \(OpenSearch Dashboards\)
+ 8080 \(proxy\)
+ 8088 \(legacy HTTP port\)
+ 8888 \(alternative HTTP port\)
+ 9200 or 9300 \(OpenSearch\)

### Remediation<a name="ec2-19-remediation"></a>

For information on how to delete rules from a security group, see [Delete rules from a security group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-security-groups.html#deleting-security-group-rule) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.20\] Both VPN tunnels for an AWS Site\-to\-Site VPN connection should be up<a name="ec2-20"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Resilience > Recover > High availability

**Severity:** Medium 

**Resource type:**`AWS::EC2::VPNConnection`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-vpn-2-tunnels-up.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-vpn-2-tunnels-up.html)

**Schedule type:** Change triggered

**Parameters:** None

A VPN tunnel is an encrypted link where data can pass from the customer network to or from AWS within an AWS Site\-to\-Site VPN connection\. Each VPN connection includes two VPN tunnels which you can simultaneously use for high availability\. Ensuring that both VPN tunnels are up for a VPN connection is important for confirming a secure and highly available connection between an AWS VPC and your remote network\.

This control checks that both VPN tunnels provided by AWS Site\-to\-Site VPN are in UP status\. The control fails if one or both tunnels are in DOWN status\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)

### Remediation<a name="ec2-20-remediation"></a>

To modify VPN tunnel options, see [Modifying Site\-to\-Site VPN tunnel options](https://docs.aws.amazon.com/vpn/latest/s2svpn/modify-vpn-tunnel-options.html) in the AWS Site\-to\-Site VPN User Guide\.

## \[EC2\.21\] Network ACLs should not allow ingress from 0\.0\.0\.0/0 to port 22 or port 3389<a name="ec2-21"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.4\.0/5\.1, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\), NIST\.800\-53\.r5 CM\-7, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(5\)

**Category:** Protect > Secure Network Configuration

**Severity:** Medium 

**Resource type:**`AWS::EC2::NetworkAcl`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/nacl-no-unrestricted-ssh-rdp.html](https://docs.aws.amazon.com/config/latest/developerguide/nacl-no-unrestricted-ssh-rdp.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a network access control list \(NACL\) allows unrestricted access to the default TCP ports for SSH/RDP ingress traffic\. The rule fails if a NACL inbound entry allows a source CIDR block of '0\.0\.0\.0/0' or '::/0' for TCP ports 22 or 3389\.

Access to remote server administration ports, such as port 22 \(SSH\) and port 3389 \(RDP\), should not be publicly accessible, as this may allow unintended access to resources within your VPC\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-21-remediation"></a>

For more information about NACLs, see [Network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html) in the VPC User Guide\.

## \[EC2\.22\] Unused Amazon EC2 security groups should be removed<a name="ec2-22"></a>

**Related requirements:** NIST\.800\-53\.r5 CM\-8\(1\)

**Category:** Identify > Inventory

**Severity:** Medium 

**Resource type:**`AWS::EC2::SecurityGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-security-group-attached-to-eni-periodic.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-security-group-attached-to-eni-periodic.html)

**Schedule type:** Periodic

**Parameters:** None

This AWS control checks that security groups are attached to Amazon Elastic Compute Cloud \(Amazon EC2\) instances or to an elastic network interface\. The control will fail if the security group is not associated with an Amazon EC2 instance or an elastic network interface\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="ec2-22-remediation"></a>

To create, assign and delete security groups, see [Security groups](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/working-with-security-groups.html#deleting-security-group) in Amazon EC2 user guide\.

## \[EC2\.23\] Amazon EC2 Transit Gateways should not automatically accept VPC attachment requests<a name="ec2-23"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure network configuration

**Severity:** High 

**Resource type:**`AWS::EC2::TransitGateway`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-transit-gateway-auto-vpc-attach-disabled.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-transit-gateway-auto-vpc-attach-disabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if EC2 Transit Gateways are automatically accepting shared VPC attachments\. This control fails for a Transit Gateway that automatically accepts shared VPC attachment requests\.

Turning on `AutoAcceptSharedAttachments` configures a Transit Gateway to automatically accept any cross\-account VPC attachment requests without verifying the request or the account the attachment is originating from\. To follow the best practices of authorization and authentication, we recommended turning off this feature to ensure that only authorized VPC attachment requests are accepted\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Hong Kong\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-23-remediation"></a>

For information about how to modify a Transit Gateway, see [Modify a transit gateway](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-transit-gateways.html#tgw-modifying) in the Amazon VPC Developer Guide\.

## \[EC2\.24\] Amazon EC2 paravirtual instance types should not be used<a name="ec2-24"></a>

**Related requirements:** NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\)

**Category:** Identify > Vulnerability, patch, and version management

**Severity:** Medium 

**Resource type:**`AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-paravirtual-instance-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-paravirtual-instance-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the virtualization type of an EC2 instance is paravirtual\. The control fails if the `virtualizationType` of the EC2 instance is set to `paravirtual`\.

Linux Amazon Machine Images \(AMIs\) use one of two types of virtualization: paravirtual \(PV\) or hardware virtual machine \(HVM\)\. The main differences between PV and HVM AMIs are the way in which they boot and whether they can take advantage of special hardware extensions \(CPU, network, and storage\) for better performance\.

Historically, PV guests had better performance than HVM guests in many cases, but because of enhancements in HVM virtualization and the availability of PV drivers for HVM AMIs, this is no longer true\. For more information, see [Linux AMI virtualization types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/virtualization_types.html) in the Amazon EC2 User Guide for Linux Instances\.

**Note**  
This control is not supported in the following Regions:  
US East \(Ohio\)
Africa \(Cape Town\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Jakarta\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Osaka\)
Asia Pacific \(Seoul\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-24-remediation"></a>

For information about how to update an EC2 instance to a new instance type, see [Change the instance type](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-resize.html) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.25\] Amazon EC2 launch templates should not assign public IPs to network interfaces<a name="ec2-25"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration > Resources not publicly accessible

**Severity:** High 

**Resource type:**`AWS::EC2::LaunchTemplate`

**AWS Config rule:** `ec2-launch-template-public-ip-disabled`

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon EC2 launch templates are configured to assign public IP addresses to network interfaces upon launch\. The control fails if an EC2 launch template is configured to assign a public IP address to network interfaces or if there is at least one network interface that has a public IP address\.

A public IP address is one that is reachable from the internet\. If you configure your network interfaces with a public IP address, then the resources associated with those network interfaces may be reachable from the internet\. EC2 resources shouldn't be publicly accessible because this may permit unintended access to your workloads\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-25-remediation"></a>

To update an EC2 launch template, see [Change the default network interface settings](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-launch-template.html#change-network-interface) in the *Amazon EC2 Auto Scaling User Guide*\.

## \[EC2\.28\] EBS volumes should be covered by a backup plan<a name="ec2-28"></a>

**Category:** Recover > Resilience > Backups enabled

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6, NIST\.800\-53\.r5 CP\-6\(1\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-12, NIST\.800\-53\.r5 SI\-13\(5\)

**Severity:** Low

**Resource type:** `AWS::EC2::Volume`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ebs-resources-protected-by-backup-plan.html](https://docs.aws.amazon.com/config/latest/developerguide/ebs-resources-protected-by-backup-plan.html) ``

**Schedule type:** Periodic

**Parameters:** None

This control evaluates if Amazon EBS volumes are covered by backup plans\. The control fails if an Amazon EBS volume isn't covered by a backup plan\. This control only evaluates Amazon EBS volumes that are in the `in-use` state\.

Backups help you recover more quickly from a security incident\. They also strengthen the resilience of your systems\. Including Amazon EBS volumes in a backup plan helps you protect your data from unintended loss or deletion\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-28-remediation"></a>

To add an Amazon EBS volume to an AWS Backup backup plan, see [Assigning resources to a backup plan](https://docs.aws.amazon.com/aws-backup/latest/devguide/assigning-resources.html) in the *AWS Backup Developer Guide*\.

## \[EC2\.29\] EC2 instances should be launched in a VPC<a name="ec2-29"></a>

**Category:** Protect > Secure network configuration > Resources within VPC

**Related requirements:** NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Severity:** High

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instances-in-vpc.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instances-in-vpc.html) ``

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon EC2 instances are launched in a virtual private cloud \(VPC\)\. This control fails if an EC2 instance is launched in the EC2\-Classic network\.

The EC2\-Classic network retired on August 15, 2022\. The EC2\-Classic network model was flat, with public IP addresses assigned at launch time\. The EC2\-VPC network offers more scalability and security features and should be the default for launching EC2 instances\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-29-remediation"></a>

To migrate instances to the EC2\-VPC network, see [Migrate from EC2\-Classic to a VPC](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/vpc-migrate.html) in the *Amazon EC2 User Guide for Linux Instances*\.