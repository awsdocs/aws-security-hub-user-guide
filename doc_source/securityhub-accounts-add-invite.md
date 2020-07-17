# Adding and inviting member accounts<a name="securityhub-accounts-add-invite"></a>

Your account becomes an AWS Security Hub master account when an account that you invite accepts your invitation\.

When you accept an invitation from another account, your account becomes a member account\.

If your account is a master account, you cannot accept an invitation to become a member account\.

Adding a member account consists of the following steps:

1. The master account adds the member account to their list of member accounts\.

1. The master account sends an invitation to the member account\.

1. The member account accepts the invitation\. 

## Adding member accounts \(console\)<a name="securityhub-add-accounts-console"></a>

From the Security Hub console, you can add accounts to your list of member accounts\. You can select accounts individually, or upload a `.csv` file that contains the account information\.

**To add accounts to your list of member accounts**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the left pane, choose **Settings**\.

1. On the **Settings** page, choose **Accounts** and then choose **Add accounts**\. You can then either add accounts individually or upload a `.csv` file containing the list of accounts\.

1. To select the accounts, do one of the following:
   + To add the accounts individually, under **Enter accounts**, enter the account ID of the account to add, and then choose **Add**\.

     To add more accounts, enter the account ID and then choose **Add** for each account\.
   + To use a comma\-separated values \(\.csv\) file to add multiple accounts, first create the file\. The file must contain the account ID and email address for each account to add\.
**Important**  
In your `.csv` list, accounts must appear one per line\. The first line of the `.csv` file must contain the header\. In the header, the first column is **Account ID** and the second column is **Email**\.  
Each subsequent line must contain a valid account ID and email address for the account to add\.  
Here is an example of a `.csv` file when viewed in a text editor\.  

     ```
     Account ID,Email
     111111111111,user@example.com
     ```
In a spreadsheet program, the fields appear in separate columns\. The underlying format is still comma\-separated\.

     To select the file, on the console, choose **Upload list \(\.csv\)**\.

1. After you finish adding accounts, choose **Add**\. Then, under **Accounts to be added**, choose **Next**\.

## Inviting member accounts \(console\)<a name="securityhub-invite-accounts-console"></a>

After you add the member account, you send an invitation to the member account\. You can also resend an invitation to an account that you disassociated\.

**To send an invitation to a new account**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**, and then choose **Accounts**\. 

1. For the account to invite, choose **Invite** in the **Status** column\.

1. When prompted to confirm, choose **Invite**\.

**To resend an invitation to accounts that you disassociated**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**, and then choose **Accounts**\. 

1. Select each disassociated account that you want to resend an invitation to\.

1. From **Actions**, choose **Resend invitation**\.

## Adding member accounts \(Security Hub API, AWS CLI\)<a name="securityhub-add-accounts-api-cli"></a>

To add member accounts, you can use an API call or the AWS Command Line Interface\. You must use the master account credentials\.

**To add member accounts \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateMembers.html) operation\. For each member account to add, you must provide the AWS account ID\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/create-members.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/create-members.html) command\.

  ```
  aws securityhub create-members --account-details [{"AccountId": <accountID1>"}]
  ```

  **Example**

  ```
  aws securityhub create-members --account-details '[{"AccountId": "123456789111"}, {"AccountId": "123456789222"}]'
  ```

## Inviting member accounts \(Security Hub API, AWS CLI\)<a name="securityhub-invite-accounts-api-cli"></a>

To invite accounts that you added, you can use an API call or the AWS Command Line Interface\. You use the same API operation or AWS CLI command to resend invitations to member accounts that you disassociated\. You must use the master account credentials\.

**To invite member accounts \(Security Hub API, AWS CLI\)**
+ **Security Hub API **– Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_InviteMembers.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_InviteMembers.html) operation\. For each account to invite, you must provide the AWS account ID\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/invite-members.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/invite-members.html) command\.

  ```
  aws securityhub invite-members --account-ids <accountIDs>
  ```

  **Example**

  ```
  aws securityhub invite-members --account-ids "123456789111" "123456789222"
  ```