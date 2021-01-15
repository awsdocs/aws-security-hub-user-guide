# Enabling Security Hub manually<a name="securityhub-enable"></a>

After you attach the required policy to the IAM identity, you use that identity to enable Security Hub\. You can enable Security Hub from the AWS Management Console or the API\.

Security Hub also provides a script in GitHub that allows you to enable multiple accounts across Regions\.

## Attaching the required IAM policy to the IAM identity<a name="securityhub-enable-attach-policy"></a>

The IAM identity \(user, role, or group\) that you use to enable Security Hub must have the required permissions\.

If you enable the integration with AWS Organizations, then accounts in your organization have Security Hub enabled automatically\. The required permissions also are handled automatically\.

Accounts that are not managed using Organizations must enable Security Hub manually\. The IAM identity \(user, role, or group\) that you use to enable Security Hub must have the required permissions\.

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

## Enabling Security Hub \(console\)<a name="securityhub-enable-console"></a>

When you enable Security Hub from the console, you also have the option to enable the supported security standards\.

**To enable Security Hub**

1. Use the credentials of the IAM identity to sign in to the Security Hub console\.

1.  When you open the Security Hub console for the first time, choose **Get Started**\.

1. On the welcome page, **Security standards** lists the security standards that Security Hub supports\.

   To enable a standard, select its check box\.

   To disable a standard, clear its check box\.

   You can enable or disable a standard or its individual controls at any time\. For information about the security standards and how to manage them, see [Security standards and controls in AWS Security Hub](securityhub-standards.md)\.

1. Choose **Enable Security Hub**\.

## Enabling Security Hub \(Security Hub API, AWS CLI\)<a name="securityhub-enable-api"></a>

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

## Enabling Security Hub \(Multi\-account script\)<a name="securityhub-enable-multiaccount-script"></a>

The [Security Hub multi\-account enablement script in GitHub](https://github.com/awslabs/aws-securityhub-multiaccount-scripts) allows you to enable Security Hub across accounts and Regions\. The script also automates the process of sending invitations to member accounts and enabling AWS Config\.

The script automatically enables resource recording for all resources, including global resources, in all Regions\. It does not limit recording of global resources to a single Region\.

There is a corresponding script to disable Security Hub across accounts and Regions\.

The readme file provides details on how to use the script\. It includes the following information:
+ How to add the required IAM policy to the accounts
+ How to configure the execution environment
+ How to execute the script