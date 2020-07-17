# Deleting member accounts<a name="securityhub-delete-member-accounts"></a>

As a master account, you can delete your member accounts\. You cannot delete enabled accounts\. Before you can delete an enabled account, you must disassociate it\.

When you delete a member account, it is completely removed from the list\. To restore the account's membership, you must add it and invite it as if it were a completely new member account\.

## Deleting member accounts \(console\)<a name="securityhub-delete-members-console"></a>

From the Security Hub console, you can delete one or more accounts\.

**To delete member accounts**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**, and then choose **Accounts**\.

1. Under **Member accounts**, select the accounts to delete\.

1. Choose **Actions**, and then choose **Delete accounts**\.

## Deleting member accounts \(Security Hub API, AWS CLI\)<a name="securityhub-delete-members-api-cli"></a>

To delete member accounts, you can use an API call or the AWS Command Line Interface\.

**To delete member accounts \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DeleteMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DeleteMembers.html) operation\. You must provide the AWS account IDs of the member accounts to delete\. To retrieve the list of member accounts, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListMembers.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/delete-members.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/delete-members.html) command\.

  ```
  aws securityhub delete-members --account-ids <memberAccountIDs>
  ```

  **Example**

  ```
  aws securityhub delete-members --account-ids "123456789111" "123456789222"
  ```