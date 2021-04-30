# Disassociating from your administrator account<a name="securityhub-disassociate-from-admin"></a>

Member accounts that were added by invitation can disassociate themselves from the administrator account\. Member accounts that are managed using Organizations cannot disassociate their accounts from the administrator account\.

When you disassociate from your administrator account, your account remains in the administrator account's member list with a status of **Resigned**\. However, the administrator account does not receive any findings for your account\.

After you disassociate yourself from the administrator account, you can accept the invitation again\.

## Disassociating from an administrator account \(console\)<a name="securityhub-disassociate-from-admin-console"></a>

You can decline an invitation to be a member account\. To do this, you update the **Accept** option for the administrator account\.

**To disassociate from your administrator account**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**, and then choose **Accounts**\.

1. Under **Administrator account**, toggle **Accept** to the off position, and then choose **Update**\.

## Disassociating from an administrator account \(Security Hub API, AWS CLI\)<a name="securityhub-disassociate-from-admin-api-cli"></a>

To disassociate your account from your administrator account, you can use an API call or the AWS Command Line Interface\.

**To disassociate from your administrator account \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisassociateFromAdministratorAccount.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisassociateFromAdministratorAccount.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/disassociate-from-administrator-account.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/disassociate-from-administrator-account.html) command\.

  ```
  aws securityhub disassociate-from-administrator-account
  ```

**Note**  
The Security Hub console continues to use `DisassociateFromMasterAccount`\. It will eventually change to use `DisassociateFromAdministratorAccount`\. Any IAM policies that specifically control access to this function must continue to use `DisassociateFromMasterAccount`\. You should also add `DisassociateFromAdministratorAccount` to your policies to ensure that the correct permissions are in place after the console begins to use `DisassociateFromAdministratorAccount`\.