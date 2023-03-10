# Amazon SageMaker controls<a name="sagemaker-controls"></a>

These controls are related to SageMaker resources\.

## \[SageMaker\.1\] Amazon SageMaker notebook instances should not have direct internet access<a name="sagemaker-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.2, PCI DSS v3\.2\.1/1\.3\.4, PCI DSS v3\.2\.1/1\.3\.6, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::SageMaker::NotebookInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/sagemaker-notebook-no-direct-internet-access.html](https://docs.aws.amazon.com/config/latest/developerguide/sagemaker-notebook-no-direct-internet-access.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether direct internet access is disabled for an SageMaker notebook instance\. To do this, it checks whether the `DirectInternetAccess` field is disabled for the notebook instance\. 

If you configure your SageMaker instance without a VPC, then by default direct internet access is enabled on your instance\. You should configure your instance with a VPC and change the default setting to **Disable—Access the internet through a VPC**\.

To train or host models from a notebook, you need internet access\. To enable internet access, make sure that your VPC has a NAT gateway and your security group allows outbound connections\. To learn more about how to connect a notebook instance to resources in a VPC, see [Connect a notebook instance to resources in a VPC](https://docs.aws.amazon.com/sagemaker/latest/dg/appendix-notebook-and-internet-access.html) in the *Amazon SageMaker Developer Guide*\.

You should also ensure that access to your SageMaker configuration is limited to only authorized users\. Restrict users' IAM permissions to modify SageMaker settings and resources\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
Middle East \(UAE\)
 AWS GovCloud \(US\-East\)

### Remediation<a name="sagemaker-1-remediation"></a>

Note that you cannot change the internet access setting after a notebook instance is created\. It must be stopped, deleted, and recreated\.

**To configure an SageMaker notebook instance to deny direct internet access**

1. Open the SageMaker console at [https://console.aws.amazon.com/sagemaker/](https://console.aws.amazon.com/sagemaker/)

1. Navigate to **Notebook instances**\.

1. Delete the instance that has direct internet access enabled\. Choose the instance, choose **Actions**, then choose stop\.

   After the instance is stopped, choose **Actions**, then choose **delete**\.

1. Choose **Create notebook instance**\. Provide the configuration details\.

1. Expand the network section, then choose a VPC, subnet, and security group\. Under **Direct internet access**, choose **Disable—Access the internet through a VPC**\.

1. Choose **Create notebook instance**\.

For more information, see [Connect a notebook instance to resources in a VPC](https://docs.aws.amazon.com/sagemaker/latest/dg/appendix-notebook-and-internet-access.html) in the *Amazon SageMaker Developer Guide*\.

## \[SageMaker\.2\] SageMaker notebook instances should be launched in a custom VPC<a name="sagemaker-2"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration > Resources within VPC

**Severity:** High

**Resource type:** `AWS::SageMaker::NotebookInstance`

**AWS Config rule:** `sagemaker-notebook-instance-inside-vpc`

**Schedule type:** Change triggered

**Parameters:** None

This control checks if an Amazon SageMaker notebook instance is launched within a custom virtual private cloud \(VPC\)\. This control fails if a SageMaker notebook instance is not launched within a custom VPC or if it is launched in the SageMaker service VPC\.

Subnets are a range of IP addresses within a VPC\. We recommend keeping your resources inside a custom VPC whenever possible to ensure secure network protection of your infrastructure\. An Amazon VPC is a virtual network dedicated to your AWS account\. With an Amazon VPC, you can control the network access and internet connectivity of your SageMaker Studio and notebook instances\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="sagemaker-2-remediation"></a>

You can't change the VPC setting after creating a notebook instance\. Instead, you can delete and recreate the instance\. For instructions on deleting and creating a notebook instance, see [Get started with Amazon SageMaker notebook instances](https://docs.aws.amazon.com/sagemaker/latest/dg/gs-console.html) in the *Amazon SageMaker Developer Guide*\.

## \[SageMaker\.3\] Users should not have root access to SageMaker notebook instances<a name="sagemaker-3"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 AC\-6\(10\), NIST\.800\-53\.r5 AC\-6\(2\)

**Category:** Protect > Secure access management > Root user access restrictions

**Severity:** High

**Resource type:** `AWS::SageMaker::NotebookInstance`

**AWS Config rule:** `sagemaker-notebook-instance-root-access-check`

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether root access is turned on for an Amazon SageMaker notebook instance\. The control fails if root access is turned on for a SageMaker notebook instance\.

In adherence to the principal of least privilege, it is a recommended security best practice to restrict root access to instance resources to avoid unintentionally over provisioning permissions\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="sagemaker-3-remediation"></a>

To restrict root access to SageMaker notebook instances, see [Control root access to a SageMaker notebook instance](https://docs.aws.amazon.com/sagemaker/latest/dg/nbi-root-access.html) in the *Amazon SageMaker Developer Guide*\.