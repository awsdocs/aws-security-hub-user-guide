# Setting Up AWS Security Hub<a name="securityhub-settingup"></a>

You must have an AWS account to enable AWS Security Hub\. If you don't have an account, use the following procedure to create one\.

**To sign up for AWS**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

## Enabling Security Hub<a name="securityhub-enable"></a>

To use Security Hub, you must first enable it\.

**Permissions required to enable Security Hub**

1. The IAM identity \(user, role, or group\) that you use to enable Security Hub must have the required permissions\. To grant the permissions required to enable Security Hub, attach the following policy to an IAM user, group, or role\.

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

1. Use the credentials of the IAM identity from step 1 to sign in to the Security Hub console\. When you open the Security Hub console for the first time, choose **Get Started** and then choose **Enable Security Hub **\.

When you enable Security Hub, it's assigned a service\-linked role named `AWSServiceRoleForSecurityHub`\. This service\-linked role includes the permissions and trust policy that Security Hub requires to do the following:
+ Detect and aggregate findings from Amazon GuardDuty, Amazon Inspector, and Amazon Macie
+ Configure the requisite AWS Config infrastructure to run supported standards \(in this release, CIS AWS Foundations\) compliance checks

To view the details of `AWSServiceRoleForSecurityHub`, on the **Enable Security Hub** page, choose **View service role permissions**\. For more information, see [Using Service\-Linked Roles for AWS Security Hub](using-service-linked-roles.md)\. For more information about service\-linked roles, see [Using Service\-Linked Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html) in the *IAM User Guide*\.

By enabling Security Hub in a particular account, you also, by default, enable the supported CIS AWS Foundations standard in that account\. For Security Hub to successfully run compliance checks against the rules included in the CIS AWS Foundations standard, you must have AWS Config enabled in the account where you enabled Security Hub\. \(If this is a Security Hub master account, enable AWS Config in each of this account's Security Hub member accounts\.\) Security Hub doesn't manage AWS Config for you\. If you already have AWS Config enabled, you can continue configuring its settings through the AWS Config console or APIs\. If you don't have AWS Config enabled, you can enable it manually or by using the AWS CloudFormation "Enable AWS Config" template in AWS CloudFormation StackSets Sample Templates\.

**Important**  
When you turn on the AWS Config recorder, choose to record all resources supported in a given Region, including global resources\.

For more information, see [Getting Started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.