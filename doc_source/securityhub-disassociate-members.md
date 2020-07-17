# Disassociating member accounts<a name="securityhub-disassociate-members"></a>

To stop receiving and viewing findings from an enabled member account, you can disassociate the member account\. You must disassociate a member account before you can delete it\.

When you disassociate a member account, it remains in your list of member accounts with a status of **Removed \(Disassociated\)**\. Your account is removed from the master account information for the member account\.

To resume receiving findings for the account, you can resend the invitation\. To remove the member account entirely, you can delete the member account\.

## Disassociating member accounts \(console\)<a name="securityhub-disassociate-members-console"></a>

From the **Accounts** page, you can disassociate one or more member accounts\.

**To disassociate member accounts**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**, and then choose **Accounts**\.

1. Under **Member accounts**, select the accounts to disassociate\.

1. Choose **Actions**, and then choose **Disassociate accounts**\.

## Disassociating member accounts \(Security Hub API, AWS CLI\)<a name="securityhub-disassociate-members-api-cli"></a>

To disassociate member accounts, you can use an API call or the AWS Command Line Interface\.

**To disassociate member accounts \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisassociateMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisassociateMembers.html) operation\. You must provide the AWS account IDs for the member accounts to disassociate\. To view a list of member accounts, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListMembers.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/disassociate-members.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/disassociate-members.html) command\.

  ```
  aws securityhub disassociate-members --account-ids <accountIds>
  ```

  **Example**

  ```
  aws securityhub disassociate-members --account-ids "123456789111" "123456789222"
  ```