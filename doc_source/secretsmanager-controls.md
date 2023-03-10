# AWS Secrets Manager controls<a name="secretsmanager-controls"></a>

These controls are related to Secrets Manager resources\.

## \[SecretsManager\.1\] Secrets Manager secrets should have automatic rotation enabled<a name="secretsmanager-1"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3\(15\)

**Category:** Protect > Secure development

**Severity:** Medium

**Resource type:** `AWS::SecretsManager::Secret`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-rotation-enabled-check.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-rotation-enabled-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a secret stored in AWS Secrets Manager is configured with automatic rotation\.

Secrets Manager helps you improve the security posture of your organization\. Secrets include database credentials, passwords, and third\-party API keys\. You can use Secrets Manager to store secrets centrally, encrypt secrets automatically, control access to secrets, and rotate secrets safely and automatically\.

Secrets Manager can rotate secrets\. You can use rotation to replace long\-term secrets with short\-term ones\. Rotating your secrets limits how long an unauthorized user can use a compromised secret\. For this reason, you should rotate your secrets frequently\. To learn more about rotation, see [Rotating your AWS Secrets Manager secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html) in the *AWS Secrets Manager User Guide*\.

**Note**  
This control is not supported in the following Regions\.  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
Middle East \(UAE\)

### Remediation<a name="secretsmanager-1-remediation"></a>

To remediate this issue, you enable automatic rotation for your secrets\.

**To enable automatic rotation for secrets**

1. Open the Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

1. To find the secret that requires rotating, enter the secret name in the search field\. 

1. Choose the secret you want to rotate, which displays the secrets details page\. 

1. Under **Rotation configuration**, choose **Edit rotation**\.

1. From **Edit rotation configuration**, choose **Enable automatic rotation**\.

1. For **Select Rotation Interval**, choose a rotation interval\.

1. Choose a Lambda function for rotation\. For information about customizing your Lambda rotation function, see [Understanding and customizing your Lambda rotation function](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets-lambda-function-customizing.html) in the *AWS Secrets Manager User Guide*\.

1. To configure the secret for rotation, choose **Next**\.

To learn more about Secrets Manager rotation, see [Rotating your AWS Secrets Manager secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html) in the *AWS Secrets Manager User Guide*\.

## \[SecretsManager\.2\] Secrets Manager secrets configured with automatic rotation should rotate successfully<a name="secretsmanager-2"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3\(15\)

**Category:** Protect > Secure development

**Severity:** Medium

**Resource type:** `AWS::SecretsManager::Secret`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-scheduled-rotation-success-check.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-scheduled-rotation-success-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS Secrets Manager secret rotated successfully based on the rotation schedule\. The control fails if `RotationOccurringAsScheduled` is `false`\. The control does not evaluate secrets that do not have rotation configured\.

Secrets Manager helps you improve the security posture of your organization\. Secrets include database credentials, passwords, and third\-party API keys\. You can use Secrets Manager to store secrets centrally, encrypt secrets automatically, control access to secrets, and rotate secrets safely and automatically\.

Secrets Manager can rotate secrets\. You can use rotation to replace long\-term secrets with short\-term ones\. Rotating your secrets limits how long an unauthorized user can use a compromised secret\. For this reason, you should rotate your secrets frequently\.

In addition to configuring secrets to rotate automatically, you should ensure that those secrets rotate successfully based on the rotation schedule\.

To learn more about rotation, see [Rotating your AWS Secrets Manager secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html) in the *AWS Secrets Manager User Guide*\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="secretsmanager-2-remediation"></a>

If the automatic rotation fails, then Secrets Manager might have encountered errors with the configuration\. 

To rotate secrets in Secrets Manager, you use a Lambda function that defines how to interact with the database or service that owns the secret\. 

For help on how to diagnose and fix common errors related to secrets rotation, see [Troubleshooting AWS Secrets Manager rotation of secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/troubleshoot_rotation.html) in the *AWS Secrets Manager User Guide*\.

## \[SecretsManager\.3\] Remove unused Secrets Manager secrets<a name="secretsmanager-3"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3\(15\)

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::SecretsManager::Secret`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-unused.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-unused.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether your secrets have been accessed within a specified number of days\. The default value is 90 days\. If a secret was not accessed within the defined number of days, this control fails\.

Deleting unused secrets is as important as rotating secrets\. Unused secrets can be abused by their former users, who no longer need access to these secrets\. Also, as more users get access to a secret, someone might have mishandled and leaked it to an unauthorized entity, which increases the risk of abuse\. Deleting unused secrets helps revoke secret access from users who no longer need it\. It also helps to reduce the cost of using Secrets Manager\. Therefore, it is essential to routinely delete unused secrets\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="secretsmanager-3-remediation"></a>

You can delete inactive secrets from the Secrets Manager console\.

**To delete inactive secrets**

1. Open the Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

1. To locate the secret, enter the secret name in the search box\.

1. Choose the secret to delete\. 

1. Under **Secret details**, from **Actions**, choose **Delete secret**\.

1. Under **Schedule secret deletion**, enter the number of days to wait before the secret is deleted\.

1. Choose **Schedule deletion**\.

## \[SecretsManager\.4\] Secrets Manager secrets should be rotated within a specified number of days<a name="secretsmanager-4"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3\(15\)

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::SecretsManager::Secret`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-periodic-rotation.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-periodic-rotation.html)

**Schedule type:** Periodic

**Parameters:**
+ **Rotation period:** 90 days by default

This control checks whether your secrets have been rotated at least once within 90 days\.

Rotating secrets can help you to reduce the risk of an unauthorized use of your secrets in your AWS account\. Examples include database credentials, passwords, third\-party API keys, and even arbitrary text\. If you do not change your secrets for a long period of time, the secrets are more likely to be compromised\.

As more users get access to a secret, it can become more likely that someone mishandled and leaked it to an unauthorized entity\. Secrets can be leaked through logs and cache data\. They can be shared for debugging purposes and not changed or revoked once the debugging completes\. For all these reasons, secrets should be rotated frequently\.

You can configure your secrets for automatic rotation in AWS Secrets Manager\. With automatic rotation, you can replace long\-term secrets with short\-term ones, significantly reducing the risk of compromise\.

Security Hub recommends that you enable rotation for your Secrets Manager secrets\. To learn more about rotation, see [Rotating your AWS Secrets Manager secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html) in the *AWS Secrets Manager User Guide*\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="secretsmanager-4-remediation"></a>

You can enable automatic secret rotation in the Secrets Manager console\.

**To enable secret rotation**

1. Open the Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

1. To locate the secret, enter the secret name in the search box\.

1. Choose the secret to display\.

1. Under **Rotation configuration**, choose **Edit rotation**\.

1. From **Edit rotation configuration**, choose **Enable automatic rotation**\.

1. From **Select Rotation Interval**, choose the rotation interval\.

1. Choose a Lambda function to use for rotation\.

1. Choose **Next**\.

1. After you configure the secret for automatic rotation, under **Rotation Configuration**, choose** Rotate secret immediately**\.