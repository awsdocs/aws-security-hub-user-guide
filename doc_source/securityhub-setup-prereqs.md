# Prerequisites and recommendations<a name="securityhub-setup-prereqs"></a>

You must have an AWS account to enable AWS Security Hub\. If you don't have an account, use the following procedure to create one\.

**To sign up for AWS**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

Security Hub strongly recommends that you enable AWS Organizations\. Using Organizations to manage your accounts streamlines the process of managing member accounts\.

Security Hub requires that AWS Config is enabled in all accounts that have Security Hub enabled\. Security Hub controls use AWS Config rules to complete security checks\.

**Topics**
+ [Using AWS Organizations to manage accounts](securityhub-prereq-orgs.md)
+ [Enabling and configuring AWS Config](securityhub-prereq-config.md)