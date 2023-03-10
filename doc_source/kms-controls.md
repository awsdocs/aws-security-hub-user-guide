# AWS Key Management Service controls<a name="kms-controls"></a>

These controls are related to AWS KMS resources\.

## \[KMS\.1\] IAM customer managed policies should not allow decryption actions on all KMS keys<a name="kms-1"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-5, NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 AC\-6\(3\)

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::IAM::Policy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-customer-policy-blocked-kms-actions.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-customer-policy-blocked-kms-actions.html)

**Schedule type:** Change triggered

**Parameters:** 
+ `blockedActionsPatterns: kms:ReEncryptFrom, kms:Decrypt`
+ `excludePermissionBoundaryPolicy`: `True`

Checks whether the default version of IAM customer managed policies allow principals to use the AWS KMS decryption actions on all resources\. This control uses [Zelkova](http://aws.amazon.com/blogs/security/protect-sensitive-data-in-the-cloud-with-automated-reasoning-zelkova/), an automated reasoning engine, to validate and warn you about policies that may grant broad access to your secrets across AWS accounts\.

This control fails, and flags the policy as `FAILED`, if the policy is open enough to allow `kms:Decrypt` or `kms:ReEncryptFrom` actions on any arbitrary KMS key\.

The control only checks KMS keys in the Resource element and doesn't take into account any conditionals in the Condition element of a policy\. In addition, the control evaluates both attached and unattached customer managed policies\. It doesn't check inline policies or AWS managed policies\.

With AWS KMS, you control who can use your KMS keys and gain access to your encrypted data\. IAM policies define which actions an identity \(user, group, or role\) can perform on which resources\. Following security best practices, AWS recommends that you allow least privilege\. In other words, you should grant to identities only the `kms:Decrypt` or `kms:ReEncryptFrom` permissions and only for the keys that are required to perform a task\. Otherwise, the user might use keys that are not appropriate for your data\.

Instead of granting permissions for all keys, determine the minimum set of keys that users need to access encrypted data\. Then design policies that allow users to use only those keys\. For example, do not allow `kms:Decrypt` permission on all KMS keys\. Instead, allow `kms:Decrypt` only on keys in a particular Region for your account\. By adopting the principle of least privilege, you can reduce the risk of unintended disclosure of your data\.

**Note**  
This control is not supported in the following Regions\.  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
Middle East \(UAE\)

### Remediation<a name="kms-1-remediation"></a>

To remediate this issue, you modify the IAM customer managed policies to restrict access to the keys\.

**To modify an IAM customer managed policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the IAM navigation pane, choose **Policies**\.

1. Choose the arrow next to the policy you want to modify\.

1. Choose **Edit policy**\.

1. Choose the **JSON** tab\.

1. Change the `"Resource"` value to the specific key or keys that you want to allow\.

1. After you modify the policy, choose **Review policy**\.

1. Choose **Save changes**\.

For more information, see [Using IAM policies with AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html) in the *AWS Key Management Service Developer Guide*\.

## \[KMS\.2\] IAM principals should not have IAM inline policies that allow decryption actions on all KMS keys<a name="kms-2"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2, NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-5, NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 AC\-6\(3\)

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:**
+ `AWS::IAM::Role`
+ `AWS::IAM::User`
+ `AWS::IAM::Group`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-inline-policy-blocked-kms-actions.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-inline-policy-blocked-kms-actions.html) 

**Schedule type:** Change triggered

**Parameters:**
+ `blockedActionsPatterns: kms:ReEncryptFrom, kms:Decrypt`

This control checks whether the inline policies that are embedded in your IAM identities \(role, user, or group\) allow the AWS KMS decryption and re\-encryption actions on all KMS keys\. This control uses [Zelkova](http://aws.amazon.com/blogs/security/protect-sensitive-data-in-the-cloud-with-automated-reasoning-zelkova/), an automated reasoning engine, to validate and warn you about policies that may grant broad access to your secrets across AWS accounts\. The control fails if the policy is open enough to allow `kms:Decrypt` or `kms:ReEncryptFrom` actions on any arbitrary KMS key\.

The control only checks KMS keys in the Resource element and doesn't take into account any conditionals in the Condition element of a policy\.

With AWS KMS, you control who can use your KMS keys and gain access to your encrypted data\. IAM policies define which actions an identity \(user, group, or role\) can perform on which resources\. Following security best practices, AWS recommends that you allow least privilege\. In other words, you should grant to identities only the permissions they need and only for keys that are required to perform a task\. Otherwise, the user might use keys that are not appropriate for your data\.

Instead of granting permission for all keys, determine the minimum set of keys that users need to access encrypted data\. Then design policies that allow the users to use only those keys\. For example, do not allow `kms:Decrypt` permission on all KMS keys\. Instead, allow the permission only on specific keys in a specific Region for your account\. By adopting the principle of least privilege, you can reduce the risk of unintended disclosure of your data\.

**Note**  
This control is not supported in the following Regions\.  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
Middle East \(UAE\)

### Remediation<a name="kms-2-remediation"></a>

To remediate this issue, you modify the inline policy to restrict access to the keys\.

**To modify an IAM inline policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the IAM navigation pane, choose **Users**, **Groups**, or **Roles**\. 

1. Choose the name of the user, group or role for which to modify IAM inline policies\. 

1. Choose the arrow next to the policy to modify\.

1. Choose **Edit policy**\.

1. Choose the **JSON** tab\.

1. Change the `"Resource"` value to the specific keys you want to allow\.

1. After you modify the policy, choose **Review policy**\.

1. Choose **Save changes**\.

For more information, see [Using IAM policies with AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html) in the *AWS Key Management Service Developer Guide*\.

## \[KMS\.3\] AWS KMS keys should not be deleted unintentionally<a name="kms-3"></a>

**Related requirements:** NIST\.800\-53\.r5 SC\-12, NIST\.800\-53\.r5 SC\-12\(2\)

**Category:** Protect > Data protection > Data deletion protection

**Severity:** Critical

**Resource type:** `AWS::KMS::Key`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/kms-cmk-not-scheduled-for-deletion.html](https://docs.aws.amazon.com/config/latest/developerguide/kms-cmk-not-scheduled-for-deletion.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether KMS keys are scheduled for deletion\. The control fails if a KMS key is scheduled for deletion\.

KMS keys cannot be recovered once deleted\. Data encrypted under a KMS key is also permanently unrecoverable if the KMS key is deleted\. If meaningful data has been encrypted under a KMS key scheduled for deletion, consider decrypting the data or re\-encrypting the data under a new KMS key unless you are intentionally performing a *cryptographic erasure*\.

When a KMS key is scheduled for deletion, a mandatory waiting period is enforced to allow time to reverse the deletion, if it was scheduled in error\. The default waiting period is 30 days, but it can be reduced to as short as 7 days when the KMS key is scheduled for deletion\. During the waiting period, the scheduled deletion can be canceled and the KMS key will not be deleted\.

For additional information regarding deleting KMS keys, see [Deleting KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/deleting-keys.html) in the *AWS Key Management Service Developer Guide*\.

**Note**  
This control is not supported in the Asia Pacific \(Osaka\) and Europe \(Milan\) Regions\.

### Remediation<a name="kms-3-remediation"></a>

For detailed remediation instructions to cancel a scheduled KMS key deletion, see **To cancel key deletion** under [Scheduling and canceling key deletion \(console\)](https://docs.aws.amazon.com/kms/latest/developerguide/deleting-keys.html#deleting-keys-scheduling-key-deletion) in the AWS Key Management Service Developer Guide\. 

## \[KMS\.4\] AWS KMS key rotation should be enabled<a name="kms-4"></a>

**Related requirements:** PCI DSS v3\.2\.1/3\.6\.4, CIS AWS Foundations Benchmark v1\.2\.0/2\.8, CIS AWS Foundations Benchmark v1\.4\.0/3\.8, NIST\.800\-53\.r5 SC\-12, NIST\.800\-53\.r5 SC\-12\(2\), NIST\.800\-53\.r5 SC\-28\(3\)

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html)

**Schedule type:** Periodic

AWS KMS enables customers to rotate the backing key, which is key material stored in AWS KMS and is tied to the key ID of the KMS key\. It's the backing key that is used to perform cryptographic operations such as encryption and decryption\. Automated key rotation currently retains all previous backing keys so that decryption of encrypted data can take place transparently\.

CIS recommends that you enable KMS key rotation\. Rotating encryption keys helps reduce the potential impact of a compromised key because data encrypted with a new key can't be accessed with a previous key that might have been exposed\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="kms-4-remediation"></a>

**To enable KMS key rotation**

1. Open the AWS KMS console at [https://console\.aws\.amazon\.com/kms](https://console.aws.amazon.com/kms)\.

1. To change the AWS Region, use the Region selector in the upper\-right corner of the page\.

1. Choose **Customer managed keys**\.

1. Choose the alias of the key to update in the **Alias** column\.

1. Choose **Key rotation**\.

1. Select **Automatically rotate this KMS key every year** and then choose **Save**\.