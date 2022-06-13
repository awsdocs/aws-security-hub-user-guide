# Enabling member accounts from your organization<a name="orgs-accounts-enable"></a>

If you do not automatically enable new organization accounts as member accounts, then you can enable those accounts manually\. You must also manually enable accounts that you disassociated\.

You cannot enable an account if it is already a member account for a different administrator account\.

You also cannot enable an account that is currently suspended\. If you try to enable a suspended account, the account status changes to **Account Suspended**\.

When you enable an organization account as a member account, the following occurs:
+ If the account does not have Security Hub enabled, Security Hub is enabled for that account\. The AWS Foundational Security Best Practices and CIS AWS Foundations Benchmark standards also are enabled for the account\. The account does not receive an invitation\.

  The exception to this is the organization management account\. Security Hub cannot be enabled automatically for the organization management account\. The organization management account must enable Security Hub before you enable the organization management account as a member account\.
+ If the account already has Security Hub enabled, Security Hub does not make any other changes to the account\. It only enables the membership\.

Remember that all Security Hub accounts must have AWS Config enabled and configured to record all resources\. For details on the requirement for AWS Config, see [Enabling and configuring AWS Config](securityhub-prereq-config.md)\.

## Enabling an organization account as a member account \(console\)<a name="orgs-account-enable-console"></a>

In the **Accounts** list, an organization account that was either never enabled or that was disassociated from the Security Hub administrator account has a status of **Not a member**\.

**To enable an organization account as a member account**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Settings**\. Then choose **Accounts**\.

1. In the **Accounts** list, select the check box for each organization account that you want to enable\.

1. Choose **Actions**, then choose **Add member**\.

## Enabling an organization account as a member account \(Security Hub API, AWS CLI\)<a name="accounts-orgs-enable-api"></a>

The Security Hub administrator account can use the Security Hub API or AWS Command Line Interface to enable organization accounts\. Unlike the manual invitation process, when you use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateMembers.html) to enable an organization account, you do not need to send an invitation\.

**To enable organization accounts as member accounts**
+ **Security Hub API –** Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateMembers.html) operation\. For each account to enable, you provide the account ID\.
+ **AWS CLI –** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/create-members.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/create-members.html) command\.

  ```
  aws securityhub create-members --account-details '[{"AccountId": "<account ID>"}]'
  ```

  **Example**

  ```
  aws securityhub create-members --account-details '[{"AccountId": "123456789111"}, {"AccountId": "123456789222"}]'
  ```
