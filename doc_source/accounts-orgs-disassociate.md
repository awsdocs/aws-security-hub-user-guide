# Disassociating member accounts from your organization<a name="accounts-orgs-disassociate"></a>

To stop receiving and viewing findings from an enabled member account, you can disassociate the member account\.

When you disassociate a member account, the status changes to **Not a member**\.

## Disassociating member accounts \(console\)<a name="orgs-accounts-disassociate-console"></a>

**To disassociate member accounts**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**\. Then choose **Accounts**\.

1. In the **Accounts** list, select the accounts to disassociate\. You can only disassociate **Enabled** accounts\.

1. Choose **Actions**, and then choose **Disassociate account**\.

## Disassociating an account \(Security Hub API, AWS CLI\)<a name="accounts-orgs-disassociate-api"></a>

To disassociate member accounts, you can use the Security Hub API or the AWS Command Line Interface\.

**To disassociate member accounts \(Security Hub API, AWS CLI\)**
+ **Security Hub API –** Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisassociateMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisassociateMembers.html) operation\. You must provide the AWS account IDs for the member accounts to disassociate\. To view a list of member accounts, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListMembers.html) operation\.
+ **AWS CLI –** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/disassociate-members.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/disassociate-members.html) command\.

  ```
  aws securityhub disassociate-members --account-ids <accountIds>
  ```

  **Example**

  ```
  aws securityhub disassociate-members --account-ids "123456789111" "123456789222"
  ```