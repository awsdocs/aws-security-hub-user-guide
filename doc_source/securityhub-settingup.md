# Setting up AWS Security Hub<a name="securityhub-settingup"></a>

You must have an AWS account to enable AWS Security Hub\. If you don't have an account, use the following procedure to create one\.

**To sign up for AWS**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

## Attaching the required IAM policy to the IAM identity<a name="securityhub-enable-attach-policy"></a>

The IAM identity \(user, role, or group\) that you use to enable Security Hub must have the required permissions\.

To grant the permissions required to enable Security Hub, attach the following policy to an IAM user, group, or role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "securityhub:*",
            "Resource": "*"    
        },
        {
            "Effect": "Allow",
            "Action": "iam:CreateServiceLinkedRole",
            "Resource": "*",
            "Condition": {
                "StringLike": {
                    "iam:AWSServiceName": "securityhub.amazonaws.com"
                }
            }
        }
    ]
}
```

## Enabling Security Hub<a name="securityhub-enable"></a>

After you attach the required policy to the IAM identity, you use that identity to enable Security Hub\.

You can enable Security Hub from the AWS Management Console or the API\.

### Enabling Security Hub \(console\)<a name="securityhub-enable-console"></a>

When you enable Security Hub from the console, you also have the option to enable the supported security standards\.

**To enable Security Hub**

1. Use the credentials of the IAM identity to sign in to the Security Hub console\.

1.  When you open the Security Hub console for the first time, choose **Get Started**\.

1. On the welcome page, **Security standards** lists the security standards that Security Hub supports\.

   To enable a standard, select its check box\.

   To disable a standard, clear its check box\.

   You can enable or disable a standard or its individual controls at any time\. For information about the security standards and how to manage them, see [Security standards and controls in AWS Security Hub](securityhub-standards.md)\.

1. Choose **Enable Security Hub**\.

### Enabling Security Hub \(Security Hub API, AWS CLI\)<a name="securityhub-enable-api"></a>

To enable Security Hub, you can use an API call or the AWS Command Line Interface\.

**To enable Security Hub \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableSecurityHub.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableSecurityHub.html) operation\. When you enable Security Hub from the API, it automatically enables these security standards\.
  + CIS AWS Foundations Benchmark
  + AWS Foundational Security Best Practices Standard

  If you do not want to enable these standards, then set `EnableDefaultStandards` to `false`\.

  You can also use the `Tags` parameter to assign tag values to the hub resource\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/enable-security-hub.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/enable-security-hub.html) command\. To enable the default standards, include `--enable-default-standards`\. To not enable the default standards, include `--no-enable-default-standards`\.

  ```
  aws securityhub enable-security-hub [--tags <tag values>] [--enable-default-standards | --no-enable-default-standards]
  ```

  **Example**

  ```
  aws securityhub enable-security-hub --enable-default-standards --tags '{"Department": "Security"}'
  ```

After you enable Security Hub, you can enable or disable standards\. See [Disabling or enabling a security standard](securityhub-standards-enable-disable.md)\.

## Service\-linked role assigned to Security Hub<a name="security-hub-enable-slr"></a>

When you enable Security Hub, it is assigned a service\-linked role named `AWSServiceRoleForSecurityHub`\. This service\-linked role includes the permissions and trust policy that Security Hub requires to do the following:
+ Detect and aggregate findings from Amazon GuardDuty, Amazon Inspector, and Amazon Macie
+ Configure the requisite AWS Config infrastructure to run security checks for the supported standards \(in this release, CIS AWS Foundations\)

To view the details of `AWSServiceRoleForSecurityHub`, on the **Enable Security Hub** page, choose **View service role permissions**\. For more information, see [Using service\-linked roles for AWS Security Hub](using-service-linked-roles.md)\.

For more information about service\-linked roles, see [Using service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html) in the *IAM User Guide*\.

## Enabling AWS Config to support security checks<a name="securityhub-enable-config"></a>

When you enable Security Hub from the console, you also have the option to enable the supported security standards\. When you enable Security Hub from the API, then the CIS AWS Foundations Benchmark standard is enabled automatically\.

Many of the controls for the security standards rely on AWS Config service\-level rules\.

If you have any of the security standards enabled, you must enable AWS Config in the account where you enabled Security Hub\. For a Security Hub master account, you must enable AWS Config in each of this account's Security Hub member accounts\.

Security Hub does not manage AWS Config for you\. If you already have AWS Config enabled, you can continue configuring its settings through the AWS Config console or APIs\.

If you do not have AWS Config enabled, you can enable it manually\. You can also use the AWS CloudFormation "Enable AWS Config" template in AWS CloudFormation StackSets Sample Templates\. If you use the Security Hub [multi\-account, multi\-region enablement script](https://github.com/awslabs/aws-securityhub-multiaccount-scripts), it also enables AWS Config for you\.

**Important**  
When you turn on the AWS Config recorder, choose to record all resources supported in a given Region, including global resources\.

For more information, see [Getting started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.