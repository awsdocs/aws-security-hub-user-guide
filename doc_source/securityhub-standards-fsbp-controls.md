# AWS Foundational Security Best Practices controls<a name="securityhub-standards-fsbp-controls"></a>

The AWS Foundational Security Best Practices standard contains the following controls\. For each control, the information includes the following information\.
+ The category and subcategory that the control applies to
+ The severity
+ The applicable resource
+ The required AWS Config rule, and any specific parameter values set by AWS Security Hub
+ Remediation steps

## \[ACM\.1\] Imported ACM certificates should be renewed within 90 days of expiration<a name="fsbp-acm-1"></a>

**Category:** Protect \- Data Protection \- Encryption of data\-in\-transit

**Severity: **Medium

**Resource: **ACM certificate

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/acm-certificate-expiration-check.html](https://docs.aws.amazon.com/config/latest/developerguide/acm-certificate-expiration-check.html)

**Parameters:**
+ `daysToExpiration`: 90

This control checks whether ACM certificates in your account are marked for expiration within 90 days\. Certificates provided by AWS Certificate Manager are automatically renewed\. ACM does not automatically renew certificates that you import\.

If you're using certificates provided by ACM, you do not need to rotate SSL/TLS certificates\. ACM manages certificate renewals for you\. For more information, see [Managed renewal](https://docs.aws.amazon.com/acm/latest/userguide/managed-renewal.html) in the *AWS Certificate Manager User Guide*\. 

### Remediation<a name="acm-1-remediation"></a>

ACM provides managed renewal for your Amazon\-issued SSL/TLS certificates\. This includes both public and private certificates issued by using ACM\. If possible, ACM renews your certificates automatically with no action required from you\. A certificate is eligible for renewal if it is associated with another AWS service, such as Elastic Load Balancing or Amazon CloudFront, or if it has been exported since being issued or last renewed\.

If ACM cannot automatically validate one or more domain names in a certificate, ACM notifies the domain owner that the domain must be validated manually\. A domain can require manual validation for the following reasons\.
+ ACM cannot establish an HTTPS connection with the domain\.
+ The certificate that is returned in the response to the HTTPS requests does not match the one that ACM is renewing\.

When a certificate is 45 days from expiration and one or more domain names in the certificate requires manual validation, ACM notifies the domain owner in the following ways\.

**By email \(for email\-validated certificates\)**  
If the certificate was last validated by email, ACM sends to the domain owner an email for each domain name that requires manual validation\. To ensure that this email can be received, the domain owner must correctly configure email for each domain\.  
For more information, see [\(Optional\) Configure email for your domain](https://docs.aws.amazon.com/acm/latest/userguide/setup-email.html)\. The email contains a link that performs the validation\. This link expires after 72 hours\. If necessary, you can use the ACM console,AWS CLI, or API to request that ACM resend the domain validation email\. For more information, see [Request a domain validation email for certificate renewal](https://docs.aws.amazon.com/acm/latest/userguide/request-domain-validation-email-for-renewal.html)\.  
Email\-validated certificates are automatically renewed up to 825 days after their last manual validation date\. After 825 days, to proceed with the renewal, the domain owner or an authorized representative must manually re\-validate ownership of the domain\. To avoid this issue, Security Hub recommends that you create a new certificate and use DNS validation if possible\. If they are properly configured, DNS\-validated certificates are re\-validated indefinitely\.

**By notification in your AWS Personal Health Dashboard**  
ACM sends notifications to your Personal Health Dashboard to notify you that one or more domain names in the certificate require validation before the certificate can be renewed\. ACM sends these notifications when your certificate is 45 days, 30 days, 15 days, 7 days, 3 days, and 1 day from expiration\. These notifications are informational only\.

## \[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail<a name="fsbp-cloudtrail-1"></a>

**Category:** Identify \- Logging

**Severity:** High

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloud-trail-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloud-trail-enabled.html)

**Parameters: **
+ `readWriteType`: `ALL`

This control checks that there is at least one multi\-Region CloudTrail trail\.

AWS CloudTrail records AWS API calls for your account and delivers log files to you\. The recorded information includes the following information\.
+ Identity of the API caller
+ Time of the API call
+ Source IP address of the API caller
+ Request parameters
+ Response elements returned by the AWS service\.

CloudTrail provides a history of AWS API calls for an account, including API calls made via the AWS Management Console, AWS SDKs, command\-line tools, and higher\-level AWS services such as AWS CloudFormation\.

The AWS API call history produced by CloudTrail enables security analysis, resource change tracking, and compliance auditing\. Multi\-Region trails also provide the following benefits\.
+ multi\-Region trail helps to detect unexpected activity occurring in otherwise unused Regions
+ A multi\-Region trail ensures that Global Service Logging is enabled for a trail by default\. Global Service Logging records events generated by AWS global services\.
+ For a multi\-Region trail, management events for all read and write operations ensure that CloudTrail records management operations on all of an AWS account’s resources\.

### Remediation<a name="cloudtrail-1-remediation"></a>

**To create a new trail in CloudTrail**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. If you haven't used CloudTrail before, choose **Get Started Now**\.

1. Choose **Trails** and then choose **Create trail**\.

1. Enter a name for the trail\.

1. For **Apply trail to all regions**, choose **Yes**\.

1. Under **Storage location**, do one of the following:

   1. To create a new S3 bucket for CloudTrail logs, for **Create a new S3 bucket**, choose **Yes**, then enter a name for the new S3 bucket\.

   1. To use an existing S3 bucket, for **Create a new S3 bucket**, choose **No**, then select the S3 bucket to use\.

1. Choose **Advanced**\. For **Enable log file validation**, choose **Yes**\.

1. Choose **Create**\.

**To update an existing trail in CloudTrail**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. In the **Name** column, choose the name of the trail\.

1. For **Trail settings**, choose the pencil icon\.

1. For **Apply trail to all regions**, choose **Yes**, then choose **Save**\.

1. For **Management events**, choose the pencil icon\.

1. For **Read/Write events**, choose **All**, then choose **Save**\.

1. For **Storage location**, choose the pencil icon\.

1. For **Enable log file validation**, choose **Yes**, then choose **Save**\.

## \[CloudTrail\.2\] CloudTrail should have encryption at\-rest enabled<a name="fsbp-cloudtrail-2"></a>

**Category:** Protect \- Data Protection \- Encryption of data\-at\-rest

**Severity:** Medium

**Resource:** CloudTrail trail

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html)

**Parameters:** None

This control checks whether CloudTrail is configured to use the server\-side encryption \(SSE\) AWS Key Management Service customer master key \(CMK\) encryption\. The check passes if the `KmsKeyId` is defined\.

For an added layer of security for your sensitive CloudTrail log files, you should use [server\-side encryption with AWS KMS–managed keys \(SSE\-KMS\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html) for your CloudTrail log files for encryption at\-rest\. Note that by default, the log files delivered by CloudTrail to your buckets are encrypted by [Amazon server\-side encryption with Amazon S3\-managed encryption keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)\. 

### Remediation<a name="cloudtrail-2-remediation"></a>

**To enable encryption for CloudTrail logs**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the trail to update\.

1. Under **Storage location**, choose the pencil icon to edit the settings\.

1. For **Encrypt log files with SSE\-KMS**, choose **Yes**\.

1. For **Create a new KMS key**, do one of the following:
   + To create a key, choose **Yes** and then enter an alias for the key in the **KMS key **field\. The key is created in the same Region as the bucket\.
   + To use an existing key, choose **No** and then select the key from the KMS key list\.
**Note**  
The AWS KMS key and S3 bucket must be in the same Region\.

1. Choose **Save**\.

   You might need to modify the policy for CloudTrail to successfully interact with your CMK\. For more information, see [Encrypting CloudTrail log files with AWS KMS–managed keys \(SSE\-KMS\)](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html) in the *AWS CloudTrail User Guide*\.

## \[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth<a name="fsbp-codebuild-1"></a>

**Note**  
This control is not supported in AWS GovCloud \(US\-West\)\.

**Category: **Protect \- Secure Development

**Severity:** Critical

**Resource:** CodeBuild project

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-source-repo-url-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-source-repo-url-check.html)

**Parameters:** None

This control checks whether the GitHub or Bitbucket source repository URL contains either personal access tokens or a user name and password\.

Authentication credentials should never be stored or transmitted in clear text or appear in the repository URL\. Instead of personal access tokens or user name and password, you should use OAuth to grant authorization for accessing GitHub or Bitbucket repositories\. Using personal access tokens or a user name and password could expose your credentials to unintended data exposure and unauthorized access\.

### Remediation<a name="codebuild-1-remediation"></a>

**To remove basic authentication / \(GitHub\) Personal Access Token from CodeBuild project source**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Choose the build project that contains personal access tokens or a user name and password\.

1. From **Edit**, choose **Source**\.

1. Choose **Disconnect from GitHub / Bitbucket**\.

1. Choose **Connect using OAuth**, then choose **Connect to GitHub / Bitbucket**\.

1. When prompted, choose **authorize as appropriate**\.

1. Reconfigure your repository URL and additional configuration settings, as needed\.

1. Choose **Update source**\.

For more information, refer to [CodeBuild use case\-based samples](https://docs.aws.amazon.com/codebuild/latest/userguide/use-case-based-samples.html) in the *AWS CodeBuild User Guide*\.

## \[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials<a name="fsbp-codebuild-2"></a>

**Note**  
This control is not supported in AWS GovCloud \(US\-West\)\.

**Category: **Protect \- Secure Development

**Severity: **Critical

**Resource:** CodeBuild project

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-envvar-awscred-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-envvar-awscred-check.html)

**Parameters:** None

This control checks whether the project contains the environment variables `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`\.

Authentication credentials `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` should never be stored in clear text, as this could lead to unintended data exposure and unauthorized access\.

### Remediation<a name="codebuild-2-remediation"></a>

**To remove your environmental variable**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Expand **Build**\.

1. Choose **Build project**, and then choose the build project that contains plaintext credentials\.

1. From **Edit**, choose **Environment**\.

1. Expand **Additional configuration**\.

1. Choose **Remove** next to the environment variables\.

1. Choose **Update environment**\.

**To store sensitive values in the Amazon EC2 Systems Manager Parameter Store and then retrieve them from your build spec**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Expand **Build**\.

1. Choose** Build project**, and then choose the build project that contains plaintext credentials\.

1. From **Edit**, choose **Environment**\.

1. Expand **Additional configuration** and scroll to **Environment variables**\.

1. Follow [this tutorial](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-paramstore-console.html) to create a Systems Manager parameter that contains your sensitive data\.

1. After you create the parameter, copy the parameter name\.

1. Back in the CodeBuild Console, choose **Create environmental variable**\.

1. Enter the name of your variable as it appears in your build spec\.

1. For **Value**, paste the name of your parameter\.

1. For **Type**, choose **Parameter**\.

1. To remove your non\-compliant environmental variable that contains plaintext credentials, choose **Remove**\.

1. Choose **Update environment**\.

For more information, see [Environment variables in build environments](https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-env-vars.html) in the *AWS CodeBuild User Guide*\.

## \[Config\.1\] AWS Config should be enabled<a name="fsbp-config-1"></a>

**Category:** Identify \- Inventory

**Severity:** Medium

**Resource:** Account

**AWS Config rule:** None

**Parameters:** None

This control checks whether AWS Config is enabled in the account for the local region and is recording all resources\.

The AWS Config service performs configuration management of supported AWS resources in your account and delivers log files to you\. The recorded information includes the configuration item \(AWS resource\), relationships between configuration items, and any configuration changes between resources\. 

Security Hub recommends that you enable AWS Config in all Regions\. The AWS configuration item history that AWS Config captures enables security analysis, resource change tracking, and compliance auditing\. 

**Note**  
Because Security Hub is a regional service, the check performed for this control checks only the current Region for the account\. It does not check all Regions\.   
To allow security checks against global resources in each Region, you also must record global resources\. 

To learn more, see [Getting started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.

### Remediation<a name="config-1-remediation"></a>

**To configure AWS Config settings**

1. Open the AWS Config console at [https://console\.aws\.amazon\.com/config/](https://console.aws.amazon.com/config/)\.

1. Choose the Region to configure AWS Config in\.

1. If you have not used AWS Config before, choose **Get started**\.

1. On the **Settings** page, do the following:

   1. Under **Resource types to record**, choose** Record all resources supported in this region** and Include global resources \(for example, IAM resources\)\. 

   1. Under **Amazon S3 bucket**, specify the bucket to use or create a bucket and optionally include a prefix\. 

   1. Under **Amazon SNS topic**, choose an Amazon SNS topic from your account or create one\. For more information about Amazon SNS, see the [https://docs.aws.amazon.com/sns/latest/gsg/](https://docs.aws.amazon.com/sns/latest/gsg/)\. 

   1. Under **AWS Config role**, either choose **Create AWS Config service\-linked role** or **Choose a role from your account** and then choose the role to use\.

1. Choose **Next**\.

1. On the **AWS Config rules** page, choose **Skip**\. 

1. Choose **Confirm**\.

For more information about using AWS Config from the AWS CLI, see [Turning on AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/gs-cli-subscribe.html) in the *AWS Config Developer Guide*\. 

You can also use an AWS CloudFormation template to automate this process\. For more information, see the [AWS CloudFormation StackSets sample template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html) in the *AWS CloudFormation User Guide*\. 

## \[EC2\.1\] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone<a name="fsbp-ec2-1"></a>

**Category:** Protect \- Secure Network Configuration

**Severity:** Critical 

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html)

Parameters: None

This control checks that Amazon Elastic Block Store snapshots are not public, determined by the ability to be restorable by anyone\.

EBS snapshots are used to back up the data on your EBS volumes to Amazon S3 at a specific point in time, and can be used to restore previous states of EBS volumes\. EBS snapshots should not be publicly restorable by everyone unless you explicitly allow it\.

### Remediation<a name="ec2-1-remediation"></a>

**To make a public EBS snapshot private**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the navigation pane, choose **Snapshots** menu and then choose your public snapshot\.

1. From **Actions**, choose **Modify permissions**\.

1. Choose **Private**\.

1. Optionally, add the AWS account numbers of the authorized accounts to share your snapshot with

1. Choose **Save**\.

## \[EC2\.2\] The VPC default security group should not allow inbound and outbound traffic<a name="fsbp-ec2-2"></a>

**Category:** Protect \- Secure Network Configuration

**Severity:** Medium 

**Resource:** EC2 security group

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html)

**Parameters:** None

This control checks that the default security group of a VPC does not allow inbound or outbound traffic\.

The rules for the [default security group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#DefaultSecurityGroup) allow all outbound and inbound traffic from network interfaces \(and their associated instances\) that are assigned to the same security group\.

We do not recommend using the default security group\. Because the default security group cannot be deleted, you should change the default security group rules setting to restrict inbound and outbound traffic\. This prevents unintended traffic if the default security group is accidentally configured for resources such as EC2 instances\.

### Remediation<a name="ec2-2-remediation"></a>

**To update the default security group to restrict all access**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. View the default security groups details to see the resources that are assigned to them\. 

1. Create a set of least\-privilege security groups for the resources\.

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the Amazon EC2 console, change the security group for the resources that use the default security groups to the least\-privilege security group you created\. 

1. For each default security group, choose the **Inbound** tab and then delete all inbound rules\. 

1. For each default security group, choose the **Outbound** tab and then delete all outbound rules\. 

For more information, see [Working with security groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the *Amazon VPC User Guide*\.

## \[EC2\.3\] Attached EBS volumes should be encrypted at\-rest<a name="fsbp-ec2-3"></a>

**Category:** Protect \- Data Protection \- Encryption of data\-at\-rest

**Severity:** Medium

**Resource:** EC2 volume

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/encrypted-volumes.html](https://docs.aws.amazon.com/config/latest/developerguide/encrypted-volumes.html)

**Parameters:** None

This control checks whether the EBS volumes that are in an attached state are encrypted\. To pass this check, EBS volumes must be in\-use state and encrypted\. If the EBS volume is not attached, then it is not in scope for this check\.

For an added layer of security of your sensitive data in EBS volumes, you should enable EBS encryption at rest\. Amazon EBS encryption offers a straightforward encryption solution for your EBS resources that doesn't require you to build, maintain, and secure your own key management infrastructure\. It uses AWS KMS customer master keys \(CMK\) when creating encrypted volumes and snapshots\.

To learn more about Amazon EBS encryption, see [Amazon EBS encryption](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html) in the *Amazon EC2 User Guide for Linux Instances*\.

### Remediation<a name="ec2-3-remediation"></a>

There is no direct way to encrypt an existing unencrypted volume or snapshot\. You can only encrypt a new volume or snapshot when you create it\.

If you enabled encryption by default, Amazon EBS encrypts the resulting new volume or snapshot using your default key for Amazon EBS encryption\. Even if you have not enabled encryption by default, you can enable encryption when you create an individual volume or snapshot\. In both cases, you can override the default key for Amazon EBS encryption and choose a symmetric customer managed CMK\.

For more information, see [Creating an Amazon EBS volume](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-creating-volume.html) and [Copying an Amazon EBS snapshot](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-copy-snapshot.html) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EFS\.1\] Amazon EFS should be configured to encrypt file data at\-rest using AWS KMS<a name="fsbp-efs-1"></a>

**Category:** Protect \- Data Protection \- Encryption of data\-at\-rest

**Severity:** Medium

**Resource:** EFS file system

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html)

**Parameters:** None

This control checks whether Amazon Elastic File System is configured to encrypt the file data using AWS KMS\. The check fails in the following cases\.
+ `Encrypted` is set to `false` in the [https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html](https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html) response\.
+ The `KmsKeyId` key in the [https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html](https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html) response does not match the `KmsKeyId` parameter for [https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html)\.

Note that this control does not use the `KmsKeyId` parameter for [https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html)\. It only checks the value of `Encrypted`\.

For an added layer of security for your sensitive data in Amazon EFS, you should create encrypted file systems\. Amazon EFS supports encryption for file systems at\-rest\. You can enable encryption of data at\-rest when you create an Amazon EFS file system\. To learn more about Amazon EFS encryption, see[ Data encryption in Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/encryption.html) in the *Amazon Elastic File System User Guide*\.

### Remediation<a name="efs-1-remediation"></a>

For details on how to encrypt a new Amazon EFS file system, see [Encrypting data at rest](https://docs.aws.amazon.com/efs/latest/ug/encryption-at-rest.html) in the *Amazon Elastic File System User Guide*\.

## \[ELBv2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS<a name="fsbp-elbv2-1"></a>

**Category:** Protect \- Data Protection \- Encryption of data\-in\-transit

**Severity:** Medium

**Resource:** Elbv2 load balancer

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html](https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html)

**Parameters:** None

This control checks whether HTTP to HTTPS redirection is configured on all HTTP listeners of Application Load Balancers\. The check fails if one or more HTTP listeners of Application Load Balancers do not have HTTP to HTTPS redirection configured\.

Before you start to use your Application Load Balancer, you must add one or more listeners\. A listener is a process that uses the configured protocol and port to check for connection requests\. Listeners support the both HTTP and HTTPS protocols\. You can use an HTTPS listener to offload the work of encryption and decryption to your Application Load Balancer\. You should use redirect actions with Application Load Balancer to redirect client HTTP request to an HTTPS request on port 443 to enforce encryption in\-transit\.

To learn more, see [Listeners for your Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-listeners.html) in *User Guide for Application Load Balancers*\.

### Remediation<a name="elbv2-1-remediation"></a>

**To redirect HTTP requests to HTTPS on an Application Load Balancer**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Load balancers**\.

1. Choose an Application Load Balancer\.

1. Choose the **Listeners** tab\.

1. Choose a HTTP listener \(port 80 TCP\) and then choose **Edit**\.

1. If there is an existing rule, you must delete it\. Otherwise, choose **Add action** and then choose** Redirect to\.\.\.**

1. Choose **HTTPS** and then enter **443**\.

1. Choose the check mark in a circle symbol and then choose **Update**\.

## \[ES\.1\] Elasticsearch domains should have encryption at\-rest enabled<a name="fsbp-es-1"></a>

**Category:** Protect \- Data Protection \- Encryption of data\-at\-rest

**Severity:** Medium

**Resource:** Elasticsearch domain

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-encrypted-at-rest.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-encrypted-at-rest.html)

**Parameters:** None

This control checks whether Amazon Elasticsearch Service \(Amazon ES\) domains have encryption at rest configuration enabled\. The check fails if the EncryptionAtRestOptions field is not enabled\.

For an added layer of security for your sensitive data in Elasticsearch, you should configure your Elasticsearch to be encrypted at rest\. Elasticsearch domains offer encryption of data at rest\. The feature uses AWS KMS to store and manage your encryption keys\. To perform the encryption, it uses the Advanced Encryption Standard algorithm with 256\-bit keys \(AES\-256\)\.

To learn more about Elasticsearch encryption at\-rest, see [Encryption of data at rest for Amazon Elasticsearch Service](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/encryption-at-rest.html) in the *Amazon Elasticsearch Service Developer Guide*\.

**Note**  
Certain instance types, such as t\.small and t\.medium, do not support encryption of data at rest\. For details, see [Supported instance types](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/aes-supported-instance-types.html) in the *Amazon Elasticsearch Service Developer Guide*\.

### Remediation<a name="es-1-remediation"></a>

By default, domains do not encrypt data at rest, and you cannot configure existing domains to use the feature\.

To enable the feature, you must create another domain and migrate your data\. For information about creating domains, see the [https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createupdatedomains.html#es-createdomains](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createupdatedomains.html#es-createdomains)\.

Encryption of data at rest requires Amazon ES 5\.1 or later\. For more information about encrypting data at rest for Amazon ES, see the [https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/encryption-at-rest.html](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/encryption-at-rest.html)\.

## \[GuardDuty\.1\] GuardDuty should be enabled<a name="fsbp-guardduty-1"></a>

**Note**  
This control is not supported in AWS GovCloud \(US\-West\)\.

**Category:** Detect \- Detection Services 

**Severity:** Medium

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html](https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html)

**Parameters:** None

This control checks whether Amazon GuardDuty is enabled in your GuardDuty account and Region\.

It is highly recommended that you enable GuardDuty in all supported AWS regions\. This allows GuardDuty to generate findings about unauthorized or unusual activity, even in regions that you do not actively use\. This also allows GuardDuty to monitor CloudTrail events for global AWS services such as IAM\.

### Remediation<a name="guardduty-1-remediation"></a>

**To enable GuardDuty**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Get Started**\.

1. Choose **Enable GuardDuty**\.

## \[IAM\.1\] IAM policies should not allow full "\*" administrative privileges<a name="fsbp-iam-1"></a>

**Category:** Protect \- Secure Access Management

**Severity:** High

**Resource:** IAM policy

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html)

**Parameters:** None

This control checks whether the default version of IAM policies \(also known as customer managed policies\) has administrator access that includes a statement with "Effect": "Allow" with "Action": "\*" over "Resource": "\*"\.

The control only checks the customer managed policies that you create\. It does not check inline and AWS managed policies\.

IAM policies define a set of privileges granted to users, groups, or roles\. It is recommended and considered a standard security advice to grant least privilege, which means to grant only the permissions required to perform a task\. When you provide full administrative privileges instead of the minimum set of permissions that the user needs, you expose the resources to potentially unwanted actions\.

Instead of allowing full administrative privileges, determine what users need to do and then craft policies that let the users perform only those tasks\. It is more secure to start with a minimum set of permissions and grant additional permissions as necessary\. Do not start with permissions that are too lenient and then try to tighten them later\.

You should remove IAM policies that have a statement with `"Effect": "Allow" `with `"Action": "*"` over `"Resource": "*"`\.

### Remediation<a name="iam-1-remediation"></a>

**To modify an IAM policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Policies**\.

1. Choose the radio button next to the policy to remove\.

1. From **Policy actions**, choose **Detach**\.

1. For each user to detach the policy from, choose the radio button next to the user, then choose **Detach policy**\.

Confirm that the user that you detached the policy from can still access AWS services and resources as expected\.

## \[IAM\.2\] IAM users should not have IAM policies attached<a name="fsbp-iam-2"></a>

**Category:** Protect \- Secure Access Management

**Severity:** Low

**Resource:** IAM user

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html)

**Parameters:** None

This control checks that none of your IAM users have policies attached\. Instead, IAM users must inherit permissions from IAM groups or roles\.

By default, IAM users, groups, and roles have no access to AWS resources\. IAM policies grant privileges to users, groups, or roles\. We recommend that you apply IAM policies directly to groups and roles but not to users\. Assigning privileges at the group or role level reduces the complexity of access management as the number of users grows\. Reducing access management complexity might in turn reduce the opportunity for a principal to inadvertently receive or retain excessive privileges\. 

### Remediation<a name="iam-2-remediation"></a>

To resolve this issue, create an IAM group, assign the policy to the group, and then add the users to the group\. The policy is applied to each user in the group\.

**To create an IAM group**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Groups** and then choose **Create New Group**\.

1. Enter a name for the group to create and then choose **Next Step**\.

1. Select each policy to assign to the group and then choose **Next Step**\. The policies that you choose should include any policies currently attached directly to a user account\.

1. Add users to a group and then assign the policies to that group\. Each user in the group is then assigned the policies that are assigned to the group\.

1. Confirm the details on the Review page and then choose **Create Group**\.

For more information about creating groups, see [Creating IAM groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_create.html) in the *IAM User Guide*\.

**To add users to an IAM group**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Groups**\.

1. Choose **Group Actions** and then choose **Add Users to Group**\.

1. Select the users to add to the group and then choose **Add Users**\.

For more information about adding users to groups, see [Adding and removing users in an IAM group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_manage_add-remove-users.html) in the *IAM User Guide*\.

**To remove a policy attached directly to a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. For the user to detach a policy from, choose the name in the **User name** column\.

1. For each policy listed under **Attached directly**, choose the **X** on the right side of the page to remove the policy from the user and then choose **Remove**\.

1. Confirm that the user can still use AWS services as expected\.

## \[IAM\.3\] IAM users access keys should be rotated every 90 days or less<a name="fsbp-iam-3"></a>

**Category:** Protect \- Secure Access Management

**Severity:** Medium 

**Resource:** IAM user

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html](https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html)

**Parameters:**
+ `maxAccessKeyAge`: 90

This control checks whether the active access keys are rotated within 90 days\.

We highly recommend that you do not generate and remove all access keys in your account\. Instead, the recommended best practice is to either create one or more IAM roles, or to use [federation](https://aws.amazon.com/identity/federation/) to allow your users to use their existing corporate credentials to log into the AWS console and AWS CLI\.

Each approach has its use cases\. Federation is generally better for enterprises that have an existing central directory or plan to need more than the current limit IAM users\. Applications running outside of an AWS environment need access keys for programmatic access to AWS resources\.

However, if the resources that need programmatic access run inside AWS, the best practice is to use IAM roles\. Roles allow you to grant a resource access without hardcoding an access key ID and secret access key into the configuration\.

To learn more about protecting your access keys and account, see [Best practices for managing AWS access keys](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html) in the *AWS General Reference*\. Also see the blog post [Guidelines for protecting your AWS account while using programmatic access](http://aws.amazon.com/blogs/security/guidelines-for-protecting-your-aws-account-while-using-programmatic-access/)\.

If you already have an access key, Security Hub recommends that you rotate the access keys every 90 days\. Rotating access keys reduces the chance that an access key that is associated with a compromised or terminated account is used\. It also ensures that data cannot be accessed with an old key that might have been lost, cracked, or stolen\. Always update your applications after you rotate access keys\. 

Access keys consist of an access key ID and a secret access key\. They are used to sign programmatic requests that you make to AWS\. AWS users need their own access keys to make programmatic calls to AWS from the AWS CLI, Tools for Windows PowerShell, the AWS SDKs, or direct HTTP calls using the APIs for individual AWS services\.

If your organization uses AWS Single Sign\-On \(AWS SSO\), your users can sign in to Active Directory, a built\-in AWS SSO directory, or [another iDP connected to AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-idp.html)\. They can then be mapped to an IAM role that enables them to run AWS CLI commands or call AWS APIs without the need for IAM user access keys\. To learn more, see [Configuring the AWS CLI to use AWS Single Sign\-On](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html) in the *AWS Command Line Interface User Guide*\.

### Remediation<a name="iam-3-remediation"></a>

**To ensure that access keys aren't more than 90 days old**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. For each user that shows an **Access key age** that is greater than 90 days, choose the **User name** to open the settings for that user\.

1. Choose **Security credentials**\.

1. To create a new key for the user:

   1. Choose **Create access key**\.

   1. To save the key content, either download the secret access key, or choose **Show** and then copy it from the page\.

   1. Store the key in a secure location to provide to the user\.

   1. Choose **Close**\.

1. Update all applications that were using the previous key to use the new key\.

1. For the previous key, choose **Make inactive** to make the access key inactive\. The user now cannot use that key to make requests\.

1. Confirm that all applications work as expected with the new key\.

1. After confirming that all applications work with the new key, delete the previous key\. After you delete the access key, you cannot recover it\.

   To delete the previous key, choose the **X** at the end of the row and then choose **Delete**\.

## \[IAM\.4\] IAM root user access key should not exist<a name="fsbp-iam-4"></a>

**Category:** Protect \- Secure Access Management

**Severity:** Critical 

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html)

**Parameters:** None

This control checks whether the root user access key is available\. 

The root account is the most privileged user in an AWS account\. AWS access keys provide programmatic access to a given account\.

Security Hub recommends that you remove all access keys that are associated with the root account\. This limits that vectors that can be used to compromise the account\. It also encourages the creation and use of role\-based accounts that are least privileged\. 

### Remediation<a name="iam-4-remediation"></a>

**To deactivate or delete access keys**

1. Log in to your account using the root credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\. 

1. Choose **Access keys \(access key ID and secret access key\)**\. 

1. For any existing keys, do one of the following:
   + To prevent the key from being used to authenticate the account, choose **Make Inactive**\.
   + To permanently delete the key, choose **Delete** and then choose **Yes**\. You cannot recover deleted keys\.

## \[IAM\.5\] MFA should be enabled for all IAM users that have a console password<a name="fsbp-iam-5"></a>

**Category:** Protect \- Secure Access Management

**Severity:** Medium

**Resource:** IAM user

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html](https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html)

**Parameters:** None

This control checks whether AWS Multi\-Factor Authentication \(MFA\) is enabled for all IAM users that use a console password\.

Multi\-factor authentication \(MFA\) adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they are prompted for their user name and password as well as for an authentication code from their AWS MFA device\.

We recommend that you enable MFA for all accounts that have a console password\. MFA is designed to provide increased security for console access\. The authenticating principal must possess a device that emits a time\-sensitive key and must have knowledge of a credential\. 

### Remediation<a name="iam-5-remediation"></a>

**To configure MFA for a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the **User name** of the user to configure MFA for\.

1. Choose **Security credentials**\.

1. Next to **Assigned MFA Device**, choose **Manage**\.

1. Follow the **Manage MFA Device** wizard to assign the type of device appropriate for your environment\. 

To learn how to delegate MFA setup to users, see the blog post [How to delegate management of multi\-factor authentication to AWS IAM users](http://aws.amazon.com/blogs/security/how-to-delegate-management-of-multi-factor-authentication-to-aws-iam-users/)\.

## \[IAM\.6\] Hardware MFA should be enabled for the root user<a name="fsbp-iam-6"></a>

**Note**  
This control is not supported in AWS GovCloud \(US\-West\)\.

**Category:** Protect \- Secure Access Management

**Severity:** Critical

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html)

**Parameters:** None

This control checks whether your AWS account is enabled to use a hardware multi\-factor authentication \(MFA\) device to sign in with root credentials\.

Virtual MFA might not provide the same level of security as hardware MFA devices\. We recommend that you only use a virtual MFA device while you wait for hardware purchase approval or for your hardware to arrive\. To learn more, see[ Enabling a virtual multi\-factor authentication \(MFA\) device \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html) in the *IAM User Guide*\.

### Remediation<a name="iam-6-remediation"></a>

**To enable hardware\-based MFA for the root account**

1. Log in to your account using the root credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Multi\-Factor Authentication \(MFA\)**\.

1. Choose **Activate MFA**\.

1. Choose a hardware\-based \(not virtual\) device to use for MFA and then choose **Continue**\.

1. Complete the steps to configure the device type appropriate to your selection\.

## \[IAM\.7\] Password policies for IAM users should have strong configurations<a name="fsbp-iam-7"></a>

**Category:** Protect \- Secure Access Management

**Severity:** Medium

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Parameters:**
+ `RequireUppercaseCharacters`: `true`
+ `RequireLowercaseCharacters`: `true`
+ `RequireSymbols`: `true`
+ `RequireNumbers`: `true`
+ `MinimumPasswordLength`: 14 or greater
+ `PasswordReusePrevention`: 24
+ `MaxPasswordAge`: 90

This control checks whether the account password policy for IAM users uses the following recommended configurations\.
+ `RequireUppercaseCharacters`: `true`
+ `RequireLowercaseCharacters`: `true`
+ `RequireSymbols`: `true`
+ `RequireNumbers`: `true`
+ `MinimumPasswordLength`: 14 or greater
+ `PasswordReusePrevention`: 24
+ `MaxPasswordAge`: 90

We highly recommend that you do not generate and remove all access keys in your account\. Instead, the recommended best practice is to either create one or more IAM roles, or to use federation to allow your users to use their existing corporate credentials to log into the AWS console and AWS CLI\.

Each approach has its use cases\. Federation is generally better for enterprises that have an existing central directory or plan to need more than the current limit IAM users\. Applications running outside of an AWS environment need access keys for programmatic access to AWS resources\.

However, if the resources that need programmatic access run inside AWS, the best practice is to use IAM roles\. Roles allow you to grant a resource access without hardcoding an access key ID and secret access key into the configuration\.

To learn more about protecting your access keys and account, see [Best practices for managing AWS access keys](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html) in the *AWS General Reference*\. Also see the blog post[ Guidelines for protecting your AWS account while using programmatic access](http://aws.amazon.com/blogs/security/guidelines-for-protecting-your-aws-account-while-using-programmatic-access/)\.

If you already have an access key, Security Hub recommends that you enforce the creation of strong user passwords\. When you create or change a password policy, the change is enforced immediately for new users\. It does not require existing users to change their passwords\.

### Remediation<a name="iam-7-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Prevent password reuse**\. For **Number of passwords to remember**, enter **24**\.

1. Select **Requires at least one uppercase letter**\.

1. Select **Requires at least one lowercase letter**\.

1. Select **Requires at least one non\-alphanumeric character**\.

1. Select **Requires at least one number**\.

1. For **Minimum password length**, enter **14**\.

1. Choose **Enable password expiration**\. For **Password expiration period \(in days\)**, enter **90**\. 

1. Choose **Apply password policy**\.

## \[Lambda\.1\] Lambda functions should prohibit public access by other accounts<a name="fsbp-lambda-1"></a>

**Category:** Protect \- Secure Network Configuration

**Severity:** Critical

**Resource:** Lambda function

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-public-access-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-public-access-prohibited.html)

**Parameters:** None

This control checks whether the Lambda function resource\-based policy prohibits public access outside of your account\.

The Lambda function should not be publicly accessible, as this may allow unintended access to your code stored in the function\.

### Remediation<a name="lambda-1-remediation"></a>

You can only update resource\-based policies for Lambda resources within the scope of the [https://docs.aws.amazon.com/lambda/latest/dg/API_AddPermission.html](https://docs.aws.amazon.com/lambda/latest/dg/API_AddPermission.html) and [https://docs.aws.amazon.com/lambda/latest/dg/API_AddLayerVersionPermission.html](https://docs.aws.amazon.com/lambda/latest/dg/API_AddLayerVersionPermission.html) API actions\. You cannot author policies for your Lambda resources in JSON, or use conditions that don't map to parameters for those actions using the AWS CLI or the SDK\. We will use the AWS CLI\.

**To create a private Lambda function**

1. Get the ID of the statement from the output of `GetPolicy`\.

   1. From the AWS CLI, run `aws lambda get-policy —function-name yourfunctionname`\. This command returns the Lambda resource\-based policy string associated with the publicly accessible Lambda\.

   1. Copy the string value of the **Sid** field in the policy statement\.

1. From the AWS CLI, run `aws lambda remove-permission --function-name yourfunctionname —statement-id youridvalue`

## \[Lambda\.2\] Lambda functions should use latest runtimes<a name="fsbp-lambda-2"></a>

**Category:** Protect \- Secure Development

**Severity:** Medium

**Resource:** Lambda function

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-settings-check.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-settings-check.html)

**Parameters:** 
+ `runtime`: `nodejs12.x, nodejs10.x, python3.8, python3.7, python3.6, python2.7, ruby2.5, java11, java8,go1.x, dotnetcore2.1`

This control checks that the Lambda function settings for runtimes match the expected values set for the latest runtimes for each supported language\. This control checks for the following runtimes: `nodejs12.x`, `nodejs10.x`, `python3.8`, `python3.7`, `python3.6`, `ruby2.5`, `java11`, `java8`, `go1.x`, `dotnetcore2.1`

[Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) are built around a combination of operating system, programming language, and software libraries that are subject to maintenance and security updates\. When a runtime component is no longer supported for security updates, Lambda deprecates the runtime\. Even though you cannot create functions that use the deprecated runtime, the function is still available to process invocation events\. Make sure that your Lambda functions are current and do not use out\-of\-date runtimes environments\.

To learn more about the latest runtimes this control checks for all supported languages, see [AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) in the *AWS Lambda Developer Guide*\.

### Remediation<a name="lambda-2-remediation"></a>

For more information on supported runtimes and deprecation schedules, see the [Runtime support policy](https://docs.aws.amazon.com/lambda/latest/dg/runtime-support-policy.html) section of the *AWS Lambda Developer Guide*\. When you migrate your runtimes to the latest version, follow the syntax and guidance from the publishers of the language\.

## \[RDS\.1\] RDS snapshots should be private<a name="fsbp-rds-1"></a>

**Category:** Protect \- Secure Network Configuration

**Severity:** Critical

**Resource:** RDS DB snapshot

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html)

**Parameters:** None

This control checks whether RDS snapshots are public\.

RDS snapshots are used to back up the data on your RDS instances at a specific point in time\. They can be used to restore previous states of RDS instances\.

An RDS snapshot must not be public unless intended\. If you share an unencrypted manual snapshot as public, this makes the snapshot available to all AWS accounts\. This may result in unintended data exposure from your RDS instance\.

Note that if the configuration is changed to allow public access, the AWS Config rule may not be able to detect the change for up to 12 hours\. Until the AWS Config rule detects the change, the check passes even though the configuration violates the rule\.

To learn more about sharing a DB snapshot, see [Sharing a DB snapshot](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-1-remediation"></a>

**To remove public access for RDS snapshots**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Navigate to **Snapshots** and then choose the public snapshot you want to modify\.

1. From **Actions**, choose **Share Snapshots**\.

1. From **DB snapshot visibility**, choose **Private**\.

1. Under **DB snapshot visibility**, choose **all**\.

1. Choose **Save**\.

## \[RDS\.2\] RDS DB instances should prohibit public access, determined by the PubliclyAccessible configuration<a name="fsbp-rds-2"></a>

**Category:** Protect \- Secure Network Configuration

**Severity:** Critical

**Resource:** RDS DB instance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html)

**Parameters:** None

This control checks whether RDS instances are publicly accessible by evaluating the `PubliclyAccessible` field in the instance configuration item\.

The `PubliclyAccessible` value in the RDS instance configuration indicates whether the DB instance is publicly accessible\. When the DB instance is configured with `PubliclyAccessible`, it is an Internet\-facing instance with a publicly resolvable DNS name, which resolves to a public IP address\. When the DB instance isn't publicly accessible, it is an internal instance with a DNS name that resolves to a private IP address\.

Unless you intend for your RDS instance to be publicly accessible, the RDS instance should not be configured with `PubliclyAccessible` value, as this may allow necessary traffic to your database instance\.

### Remediation<a name="rds-2-remediation"></a>

**To remove public access from RDS DB instances**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Navigate to **Databases** and then choose your public database\.

1. Choose **Modify**\.

1. Under **Network & Security**, choose **No** for **Public accessibility**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications** choose **Apply immediately**\.

1. Choose **Modify DB Instance**\.

For more information, see [Working with a DB instance in a VPC](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html) in the *Amazon RDS User Guide*\.

## \[RDS\.3\] RDS DB instances should have encryption at\-rest enabled<a name="fsbp-rds-3"></a>

**Category:** Protect \- Data Protection \- Encryption of data\-at\-rest

**Severity:** Medium

**Resource:** RDS DB instance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html)

**Parameters:** None

This control checks whether storage encryption is enabled for your RDS DB instances\.

For an added layer of security for your sensitive data in RDS DB instances, you should configure your RDS DB instances to be encrypted at rest\. To encrypt your Amazon RDS DB instances and snapshots at rest, enable the encryption option for your RDS DB instances\. Data that is encrypted at rest includes the underlying storage for DB instances, its automated backups, Read Replicas, and snapshots\. 

RDS encrypted DB instances use the industry standard AES\-256 encryption algorithm to encrypt your data on the server that hosts your RDS DB instances\. After your data is encrypted, Amazon RDS handles authentication of access and decryption of your data transparently with a minimal impact on performance\. You do not need to modify your database client applications to use encryption\. 

Amazon RDS encryption is currently available for all database engines and storage types\. Amazon RDS encryption is available for most DB instance classes\. To learn about DB instance classes that do not support Amazon RDS encryption, see [Encrypting Amazon RDS resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-3-remediation"></a>

For information about encrypting DB instances in Amazon RDS, see [Encrypting Amazon RDS resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html) in the *Amazon RDS User Guide*\.

## \[S3\.1\] S3 Block Public Access setting should be enabled<a name="fsbp-s3-1"></a>

**Category:** Protect \- Secure Network Configuration

**Severity:** Medium

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks.html) 

**Parameters:** 
+ `ignorePublicAcls`: `true`
+ `blockPublicPolicy`: `true`
+ `blockPublicAcls`: `true`
+ `restrictPublicBuckets`: `true`

This control checks whether the following public access block settings are configured at the account level:
+ `ignorePublicAcls`: `true`
+ `blockPublicPolicy`: `true`
+ `blockPublicAcls`: `true`
+ `restrictPublicBuckets`: `true`

S3 Block Public Access is designed to provide controls across an entire AWS account or at the individual S3 bucket level to ensure that objects never have public access\. Public access is granted to buckets and objects through access control lists \(ACLs\), bucket policies, or both\.

Unless you intend to have your S3 buckets be publicly accessible, you should configure the account level S3 block public access feature\.

To learn more, see [Using Amazon S3 Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service Developer Guide*\.

### Remediation<a name="s3-1-remediation"></a>

**To enable Amazon S3 Block Public Access**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Block public access \(account settings\)**\.

1. Select **Block all public access**\.

1. Choose **Save changes**\.

For more information, see [Using Amazon S3 Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service Developer Guide*\.

## \[S3\.2\] S3 buckets should prohibit public read access<a name="fsbp-s3-2"></a>

**Category:** Protect \- Secure Network Configuration

**Severity:** Critical

**Resource:** S3 bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited)

**Parameters:** None

This control checks whether your S3 buckets allow public read access\. It evaluates the Block Public Access settings, the bucket policy, and the bucket access control list \(ACL\)\.

There are select use cases that require everyone on the internet to read from your S3 bucket\. However, those situations are extremely rare\. To ensure the integrity and security of your data, your S3 bucket should not be publicly readable\.

### Remediation<a name="s3-2-remediation"></a>

**To remove public access for an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the name of the bucket where your CloudTrail logs are stored\.

1. Choose **Permissions** and then choose **Public access settings**\. 

1. Choose **Edit**\.

1. Select all four options and then choose **Save**\.

1. If prompted, enter confirm and then choose **Confirm**\.

## \[S3\.3\] S3 buckets should prohibit public write access<a name="fsbp-s3-3"></a>

**Category:** Protect \- Secure Network Configuration

**Severity:** Critical

**Resource:** S3 bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html) 

**Parameters:** None

This control checks whether your S3 buckets allow public write access\. It evaluates the Block Public Access settings, the bucket policy, and the bucket access control list \(ACL\)\.

There are select use cases that require everyone on the internet to write to your S3 bucket\. However, those situations are extremely rare\. To ensure the integrity and security of your data, your S3 bucket should not be publicly writable\.

### Remediation<a name="s3-3-remediation"></a>

**To remove public access for an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the name of the bucket where your CloudTrail logs are stored\.

1. Choose **Permissions** and then choose **Public access settings**\.

1. Choose **Edit**\.

1. Select all four options and then choose **Save**\.

1. If prompted, enter confirm and then choose **Confirm**\.

## \[S3\.4\] S3 buckets should have server\-side encryption enabled<a name="fsbp-s3-4"></a>

**Category:** Protect \- Data Protection \- Encryption of data\-at\-rest

**Severity:** Medium

**Resource:** S3 bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html)

**Parameters:** None

This control checks that your S3 bucket either has Amazon S3 default encryption enabled or that the S3 bucket policy explicitly denies put\-object requests without server side encryption\.

For an added layer of security for your sensitive data in S3 buckets, you should configure your buckets with server\-side encryption to protect your data at rest\. Amazon S3 encrypts each object with a unique key\. As an additional safeguard, it encrypts the key itself with a master key that it rotates regularly\. Amazon S3 server\-side encryption uses one of the strongest block ciphers available to encrypt your data, 256\-bit Advanced Encryption Standard \(AES\-256\)\.

To learn more, see [Protecting data using server\-side encryption with Amazon S3\-managed encryption keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html) in the *Amazon Simple Storage Service Developer Guide*\.

### Remediation<a name="s3-4-remediation"></a>

**To enable default encryption on an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the bucket from the list\.

1. Choose **Properties**\.

1. Choose **Default encryption**\.

1. For the encryption, choose either **AES\-256** or **AWS\-KMS**\.
   + To use keys that are managed by Amazon S3 for default encryption, choose **AES\-256**\. For more information about using Amazon S3 server\-side encryption to encrypt your data, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)\.
   + To use keys that are managed by AWS KMS for default encryption, choose **AWS\-KMS**, and then choose a master key from the list of the AWS KMS master keys that you have created\.

     Type the Amazon Resource Name \(ARN\) of the AWS KMS key to use\. You can find the ARN for your AWS KMS key in the IAM console, under **Encryption keys**\. Or, you can choose a key name from the drop\-down list\.
**Important**  
If you use the AWS KMS option for your default encryption configuration, you are subject to the RPS \(requests per second\) quotas of AWS KMS\. For more information about AWS KMS quotas and how to request a quota increase, see the [https://docs.aws.amazon.com/kms/latest/developerguide/limits.html](https://docs.aws.amazon.com/kms/latest/developerguide/limits.html)\.

     For more information about creating an AWS KMS key, see the [https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html)\.

     For more information about using AWS KMS with Amazon S3, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html)\.

   When enabling default encryption, you might need to update your bucket policy\. For more information about moving from bucket policies to default encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy)\.

1. Choose **Save**\.

For more information about default S3 bucket encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html)\.

## \[SSM\.1\] EC2 instances should be managed by AWS Systems Manager<a name="fsbp-ssm-1"></a>

**Category:** Identify \- Inventory

**Severity:** Medium

**Resource:** EC2 instance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-managed-by-ssm.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-managed-by-ssm.html)

**Parameters:** None

This control checks whether the EC2 instances in your account are managed by AWS Systems Manager\. Systems Manager is an AWS service that you can use to view and control your AWS infrastructure\.

To help you to maintain security and compliance, Systems Manager scans your managed instances\. A managed instance is a machine that is configured for use with Systems Manager\. Systems Manager then reports or takes corrective action on any policy violations that it detects\. Systems Manager also helps you to configure and maintain your managed instances\.

To learn more, see [https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)\.

### Remediation<a name="ssm-1-remediation"></a>

**To ensure EC2 instances are managed by Systems Manager**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. Choose **Quick setup**\.

1. On the configuration screen, keep the default options\.

1. Choose** Set up Systems Manager**\.

To determine whether your instances support Systems Manager associations, see [Systems Manager prerequisites](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html) in the *AWS Systems Manager User Guide*\.

## \[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements<a name="fsbp-ssm-2"></a>

**Category:** Detect \- Detection Services 

**Severity:** Medium

**Resource:** SSM patch compliance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html)

**Parameters:** None

This control checks whether the compliance status of the Amazon EC2 Systems Manager patch compliance is `COMPLIANT` or `NON_COMPLIANT` after the patch installation on the instance\. It only checks instances that are managed by Systems Manager Patch Manager\.

Having your EC2 instances fully patched as required by your organization reduces the attack surface of your AWS accounts\. 

### Remediation<a name="ssm-2-remediation"></a>

**To remediate non\-compliant patches**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. Under **Instances & Nodes**, choose **Run Command** and then choose **Run command**\.

1. Choose the radio button next to **AWS\-RunPatchBaseline**\.

1. Change the **Operation** to **Install**\.

1. Choose **Choose instances manually** and then choose the non\-compliant instances\.

1. At the bottom of the page, choose **Run**\.

1. After the command completes, to monitor the new compliance status of your patched instances, in the navigation pane, choose **Compliance**\.

For more information about using Systems Manager Documents to patch a managed instance, see[ About SSM socuments for patching instances](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-ssm-documents.html) and [Running commands using Systems Manager Run command](https://docs.aws.amazon.com/systems-manager/latest/userguide/run-command.html) in the *AWS Systems Manager User Guide*\.