# Amazon Simple Storage Service controls<a name="s3-controls"></a>

These controls are related to Amazon S3 resources\.

## \[S3\.1\] S3 Block Public Access setting should be enabled<a name="s3-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.2, PCI DSS v3\.2\.1/1\.3\.4, PCI DSS v3\.2\.1/1\.3\.6, CIS AWS Foundations Benchmark v1\.4\.0/2\.1\.5, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::S3::Account`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks-periodic.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks-periodic.html) 

**Schedule type:** Periodic

**Parameters:** 
+ `ignorePublicAcls`: `true`
+ `blockPublicPolicy`: `true`
+ `blockPublicAcls`: `true`
+ `restrictPublicBuckets`: `true`

This control checks whether the following Amazon S3 public access block settings are configured at the account level:
+ `ignorePublicAcls`: `true`
+ `blockPublicPolicy`: `true`
+ `blockPublicAcls`: `true`
+ `restrictPublicBuckets`: `true`

The control passes if all of the public access block settings are set to `true`\.

The control fails if any of the settings are set to `false`, or if any of the settings are not configured\.

Amazon S3 public access block is designed to provide controls across an entire AWS account or at the individual S3 bucket level to ensure that objects never have public access\. Public access is granted to buckets and objects through access control lists \(ACLs\), bucket policies, or both\.

Unless you intend to have your S3 buckets be publicly accessible, you should configure the account level Amazon S3 Block Public Access feature\.

To learn more, see [Using Amazon S3 Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service User Guide*\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-1-remediation"></a>

To remediate this issue, enable Amazon S3 Block Public Access\.

**To enable Amazon S3 Block Public Access**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Block public access \(account settings\)**\.

1. Choose **Edit**\.

1. Select **Block *all* public access**\.

1. Choose **Save changes**\.

For more information, see [Using Amazon S3 block public access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service User Guide*\.

## \[S3\.2\] S3 buckets should prohibit public read access<a name="s3-2"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.2, PCI DSS v3\.2\.1/1\.3\.6, PCI DSS v3\.2\.1/7\.2\.1, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited)

**Schedule type:** Periodic and change triggered

**Parameters:** None

This control checks whether your S3 buckets allow public read access\. It evaluates the Block Public Access settings, the bucket policy, and the bucket access control list \(ACL\)\.

Some use cases require that everyone on the internet be able to read from your S3 bucket\. However, those situations are rare\. To ensure the integrity and security of your data, your S3 bucket should not be publicly readable\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="s3-2-remediation"></a>

To remediate this issue, update your S3 bucket to remove public access\.

**To remove public access from an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the left navigation pane, choose **Buckets**\.

1. Choose the name of the S3 bucket to update\.

1. Choose **Permissions** and then choose **Block public access**\. 

1. Choose **Edit**\.

1. Select **Block *all* public access**\. Then choose **Save**\.

1. If prompted, enter **confirm** and then choose **Confirm**\.

## \[S3\.3\] S3 buckets should prohibit public write access<a name="s3-3"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.2, PCI DSS v3\.2\.1/1\.3\.4, PCI DSS v3\.2\.1/1\.3\.6, PCI DSS v3\.2\.1/7\.2\.1, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html) 

**Schedule type:** Periodic and change triggered

**Parameters:** None

This control checks whether your S3 buckets allow public write access\. It evaluates the block public access settings, the bucket policy, and the bucket access control list \(ACL\)\.

Some use cases require that everyone on the internet be able to write to your S3 bucket\. However, those situations are rare\. To ensure the integrity and security of your data, your S3 bucket should not be publicly writable\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="s3-3-remediation"></a>

To remediate this issue, update your S3 bucket to remove public access\.

**To remove public access for an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the left navigation pane, choose **Buckets**\.

1. Choose the name of the S3 bucket to update\.

1. Choose **Permissions** and then choose **Block public access**\.

1. Choose **Edit**\.

1. Select **Block *all* public access**\. Then choose **Save**\.

1. If prompted, enter **confirm** and then choose **Confirm**\.

## \[S3\.4\] S3 buckets should have server\-side encryption enabled<a name="s3-4"></a>

**Related requirements:** PCI DSS v3\.2\.1/3\.4, CIS AWS Foundations Benchmark v1\.4\.0/2\.1\.1, NIST\.800\-53\.r5 AU\-9, NIST\.800\-53\.r5 AU\-9\(2\), NIST\.800\-53\.r5 AU\-9\(7\), NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks that your S3 bucket either has Amazon S3 default encryption enabled or that the S3 bucket policy explicitly denies put\-object requests without server\-side encryption\.

For an added layer of security for your sensitive data in S3 buckets, you should configure your buckets with server\-side encryption to protect your data at rest\. Amazon S3 encrypts each object with a unique key\. As an additional safeguard, Amazon S3 encrypts the key itself with a root key that it rotates regularly\. Amazon S3 server\-side encryption uses one of the strongest block ciphers available to encrypt your data, 256\-bit Advanced Encryption Standard \(AES\-256\)\.

To learn more, see [Protecting data using server\-side encryption with Amazon S3\-managed encryption keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html) in the *Amazon Simple Storage Service User Guide*\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="s3-4-remediation"></a>

To remediate this issue, update your S3 bucket to enable default encryption\.

**To enable default encryption on an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the left navigation pane, choose **Buckets**\.

1. Choose the S3 bucket from the list\.

1. Choose **Properties**\.

1. Choose **Default encryption**\.

1. For the encryption, choose either **AES\-256** or **AWS\-KMS**\.
   + Choose **AES\-256** to use keys that are managed by Amazon S3 for default encryption\. For more information about using Amazon S3 server\-side encryption to encrypt your data, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)\.
   + Choose **AWS\-KMS** to use keys that are managed by AWS KMS for default encryption\. Then choose a root key from the list of the AWS KMS root keys that you have created\.

     Type the Amazon Resource Name \(ARN\) of the AWS KMS key to use\. You can find the ARN for your AWS KMS key in the IAM console, under **Encryption keys**\. Or, you can choose a key name from the drop\-down list\.
**Important**  
If you use the AWS KMS option for your default encryption configuration, you are subject to the RPS \(requests per second\) quotas of AWS KMS\. For more information about AWS KMS quotas and how to request a quota increase, see the [https://docs.aws.amazon.com/kms/latest/developerguide/limits.html](https://docs.aws.amazon.com/kms/latest/developerguide/limits.html)\.

     For more information about creating an AWS KMS key, see the [https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html)\.

     For more information about using AWS KMS with Amazon S3, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html)\.

   When enabling default encryption, you might need to update your bucket policy\. For more information about moving from bucket policies to default encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy)\.

1. Choose **Save**\.

For more information about default S3 bucket encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html)\.

## \[S3\.5\] S3 buckets should require requests to use Secure Socket Layer<a name="s3-5"></a>

**Related requirements:** PCI DSS v3\.2\.1/4\.1, CIS AWS Foundations Benchmark v1\.4\.0/2\.1\.2, NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-ssl-requests-only.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-ssl-requests-only.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether S3 buckets have policies that require requests to use Secure Socket Layer \(SSL\)\. 

S3 buckets should have policies that require all requests \(`Action: S3:*`\) to only accept transmission of data over HTTPS in the S3 resource policy, indicated by the condition key `aws:SecureTransport`\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="s3-5-remediation"></a>

To remediate this issue, update the permissions policy of the S3 bucket\.

**To configure an S3 bucket to deny nonsecure transport**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Navigate to the noncompliant bucket, then choose the bucket name\.

1. Choose **Permissions**, and then choose **Bucket Policy**\.

1. Add a similar policy statement to that in the policy below\. Replace `awsexamplebucket` with the name of the bucket you are modifying\.

   ```
   {
       "Id": "ExamplePolicy",
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "AllowSSLRequestsOnly",
               "Action": "s3:*",
               "Effect": "Deny",
               "Resource": [
                   "arn:aws:s3:::awsexamplebucket",
                   "arn:aws:s3:::awsexamplebucket/*"
               ],
               "Condition": {
                   "Bool": {
                        "aws:SecureTransport": "false"
                   }
               },
              "Principal": "*"
           }
       ]
   }
   ```

1. Choose **Save**\.

For more information, see the knowledge center article [What S3 bucket policy should I use to comply with the AWS Config rule s3\-bucket\-ssl\-requests\-only?](http://aws.amazon.com/premiumsupport/knowledge-center/s3-bucket-policy-for-config-rule/)\.

## \[S3\.6\] S3 permissions granted to other AWS accounts in bucket policies should be restricted<a name="s3-6"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure access management > Sensitive API operations actions restricted 

**Severity:** High

**Resource type:** `AWS::S3::Bucket`

**AWS Config** rule: [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-blacklisted-actions-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-blacklisted-actions-prohibited.html)

**Schedule type:** Change triggered

**Parameters:**
+ `blacklistedactionpatterns`: `s3:DeleteBucketPolicy, s3:PutBucketAcl, s3:PutBucketPolicy, s3:PutEncryptionConfiguration, s3:PutObjectAcl`

This control checks whether the S3 bucket policy prevents principals from other AWS accounts from performing denied actions on resources in the S3 bucket\. The control fails if the S3 bucket policy allows any of the following actions for a principal in another AWS account:
+ `s3:DeleteBucketPolicy`
+ `s3:PutBucketAcl`
+ `s3:PutBucketPolicy`
+ `s3:PutEncryptionConfiguration`
+ `s3:PutObjectAcl`

This control only checks entities in the Principal element and doesn't take into account any conditionals under the Condition element of a policy\.

Implementing least privilege access is fundamental to reducing security risk and the impact of errors or malicious intent\. If an S3 bucket policy allows access from external accounts, it could result in data exfiltration by an insider threat or an attacker\.

The `blacklistedactionpatterns` parameter allows for successful evaluation of the rule for S3 buckets\. The parameter grants access to external accounts for action patterns that are not included in the `blacklistedactionpatterns` list\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="s3-6-remediation"></a>

To remediate this issue, edit the S3 bucket policy to remove the permissions\.

**To edit an S3 bucket policy**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the **Bucket name** list, choose the name of the S3 bucket for which you want to edit the policy\. 

1. Choose **Permissions**, and then choose **Bucket Policy**\.

1. In the **Bucket policy editor** text box, do one of the following:
   + Remove the statements that grant access to denied actions to other AWS accounts
   + Remove the permitted denied actions from the statements

1. Choose **Save**\.

## \[S3\.7\] S3 buckets should have cross\-Region replication enabled<a name="s3-7"></a>

**Related requirements:** PCI DSS v3\.2\.1/2\.2, NIST\.800\-53\.r5 AU\-9\(2\), NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6, NIST\.800\-53\.r5 CP\-6\(1\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-36\(2\), NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Protect > Secure access management

**Severity: ** Low

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule: ** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-replication-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-replication-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether S3 buckets have cross\-region replication enabled\.

PCI DSS does not require data replication or highly available configurations\. However, this check aligns with AWS best practices for this control\.

In addition to availability, you should consider other systems hardening settings\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="s3-7-remediation"></a>

**To enable S3 bucket replication**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the S3 bucket that does not have cross\-region replication enabled\.

1. Choose **Management**, then choose **Replication**\.

1. Choose **Add rule**\. If versioning is not already enabled, you are prompted to enable it\.

1. Choose your source bucket \- **Entire bucket**\.

1. Choose your destination bucket\. If versioning is not already enabled on the destination bucket for your account, you are prompted to enable it\.

1. Choose an IAM role\. For more information on setting up permissions for replication, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/setting-repl-config-perm-overview.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/setting-repl-config-perm-overview.html)\.

1. Enter a rule name, choose **Enabled** for the status, then choose **Next**\.

1. Choose **Save**\.

For more information about replication, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html)\.

## \[S3\.8\] S3 Block Public Access setting should be enabled at the bucket\-level<a name="s3-8"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.4\.0/2\.1\.5, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure access management > Access control

**Severity:** High

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-level-public-access-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-level-public-access-prohibited.html)

**Schedule type:** Change triggered

**Parameters:**
+ `excludedPublicBuckets` \(Optional\) – A comma\-separated list of known allowed public S3 bucket names\.

This control checks whether S3 buckets have bucket\-level public access blocks applied\. This control fails is if any of the following settings are set to `false`:
+ `ignorePublicAcls`
+ `blockPublicPolicy`
+ `blockPublicAcls`
+ `restrictPublicBuckets`

Block Public Access at the S3 bucket level provides controls to ensure that objects never have public access\. Public access is granted to buckets and objects through access control lists \(ACLs\), bucket policies, or both\.

Unless you intend to have your S3 buckets publicly accessible, you should configure the bucket level Amazon S3 Block Public Access feature\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-8-remediation"></a>

For information on how to remove public access at a bucket level, see [Blocking public access to your Amazon S3 storage](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon S3 User Guide*\.

## \[S3\.9\] S3 bucket server access logging should be enabled<a name="s3-9"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(4\), NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AC\-6\(9\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4\(20\), NIST\.800\-53\.r5 SI\-7\(8\)

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-logging-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether server access logging is enabled for S3 buckets\. When logging is enabled, Amazon S3 delivers access logs for a source bucket to a chosen target bucket\. The target bucket must be in the same AWS Region as the source bucket and must not have a default retention period configuration\. This control passes if server access logging is enabled\. The target logging bucket does not need to have server access logging enabled, and you should suppress findings for this bucket\. 

Server access logging provides detailed records of requests made to a bucket\. Server access logs can assist in security and access audits\. For more information, see [Security Best Practices for Amazon S3: Enable Amazon S3 server access logging](https://docs.aws.amazon.com/AmazonS3/latest/dev/security-best-practices.html)\.

### Remediation<a name="s3-9-remediation"></a>

**To enable S3 bucket access logging**

1. Sign in to the AWS Management Console and open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Select the bucket from the list\.

1. Choose **Properties**\.

1. Under **Server access logging**, choose **Edit**\.

1. Under **Server access logging**, choose **Enable**\. Then, choose **Save changes**\. 

## \[S3\.10\] S3 buckets with versioning enabled should have lifecycle policies configured<a name="s3-10"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-version-lifecycle-policy-check.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-version-lifecycle-policy-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon Simple Storage Service \(Amazon S3\) version enabled buckets have lifecycle policy configured\. This rule fails if Amazon S3 lifecycle policy is not enabled\.

It is recommended to configure lifecycle rules on your Amazon S3 bucket as these rules help you define actions that you want Amazon S3 to take during an object's lifetime\. 

### Remediation<a name="s3-10-remediation"></a>

For more information on configuring lifecycle on an Amazon S3 bucket, see [Setting lifecycle configuration on a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-set-lifecycle-configuration-intro.html) and [Managing your storage lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html)\.

## \[S3\.11\] S3 buckets should have event notifications enabled<a name="s3-11"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4, NIST\.800\-53\.r5 SI\-4\(4\)

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-event-notifications-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-event-notifications-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether S3 Event Notifications are enabled on an Amazon S3 bucket\. This control fails if S3 Event Notifications are not enabled on a bucket\.

By enabling Event Notifications, you receive alerts on your Amazon S3 buckets when specific events occur\. For example, you can be notified of object creation, object removal, and object restoration\. These notifications can alert relevant teams to accidental or intentional modifications that may lead to unauthorized data access\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-11-remediation"></a>

For information about detecting changes to S3 buckets and objects, see [Amazon S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/NotificationHowTo.html) in the *Amazon S3 User Guide*\.

## \[S3\.12\] S3 access control lists \(ACLs\) should not be used to manage user access to buckets<a name="s3-12"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-6

**Category:** Protect > Secure access management > Access control

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-acl-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-acl-prohibited.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon S3 buckets provide user permissions via ACLs\. The control fails if ACLs are configured for managing user access on S3 buckets\.

ACLs are legacy access control mechanisms that predate IAM\. Instead of ACLs, we recommend using IAM policies or S3 bucket policies to more easily manage access to your S3 buckets\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-12-remediation"></a>

For more information on managing access to S3 buckets, see [Bucket policies and user policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-iam-policies.html)in the *Amazon S3 User Guide*\. For details on how to review your current ACL permissions, see [Access control list \(ACL\) overview](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html) in the *Amazon S3 User Guide*\.

## \[S3\.13\] S3 buckets should have lifecycle policies configured<a name="s3-13"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Protect > Data protection 

**Severity:** Low

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-lifecycle-policy-check.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-lifecycle-policy-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if a lifecycle policy is configured for an Amazon S3 bucket\. This control fails if a lifecycle policy is not configured for an S3 bucket\.

Configuring lifecycle rules on your S3 bucket defines actions that you want S3 to take during an object's lifetime\. For example, you can transition objects to another storage class, archive them, or delete them after a specified period of time\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-13-remediation"></a>

For information about configuring lifecycle policies on an Amazon S3 bucket, see [Setting lifecycle configuration on a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-set-lifecycle-configuration-intro.html) and see [Managing your storage lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html)in the *Amazon S3 User Guide*\.

## \[S3\.14\] S3 buckets should use versioning<a name="s3-14"></a>

**Category:** Protect > Data protection > Data deletion protection

**Related requirements:** NIST\.800\-53\.r5 AU\-9\(2\), NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6, NIST\.800\-53\.r5 CP\-6\(1\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 CP\-9, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-12, NIST\.800\-53\.r5 SI\-13\(5\)

**Severity:** Low

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-versioning-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-versioning-enabled.html) ``

**Schedule type:** Change triggered

**Parameters:** None

This control checks if your Amazon S3 buckets use versioning\. The control fails if versioning is suspended for an S3 bucket\.

Versioning keeps multiple variants of an object in the same S3 bucket\. You can use versioning to preserve, retrieve, and restore every version of every object stored in your S3 bucket\. With versioning, you can easily recover from both unintended user actions and application failures\.

**Tip**  
As the number of objects increases in a bucket because of versioning, you can set up lifecycle policies to automatically archive or delete versioned objects based on rules\. For more information, see [Amazon S3 Lifecycle Management for Versioned Objects](https://docs.aws.amazon.com/blogs/aws/amazon-s3-lifecycle-management-update/)\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-14-remediation"></a>

To use versioning on an S3 bucket, see [Enabling versioning on buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/manage-versioning-examples.html) in the *Amazon S3 User Guide*\.