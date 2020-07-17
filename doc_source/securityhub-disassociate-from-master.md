# Disassociating from your master account<a name="securityhub-disassociate-from-master"></a>

Member accounts can disassociate themselves from the master account\. If you disassociate from your master account, your account remains in the master account's member account in the list with a status of **Resigned**\. However, the master account does not receive any findings for your account\.

After you disassociate yourself from the master account, you can accept the invitation again\.

## Disassociating from a master account \(console\)<a name="securityhub-disassociate-from-master-console"></a>

You can decline an invitation to be a member account\. To do this, you update the **Accept** option for the master account\.

**To disassociate from your master account**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**, and then choose **Accounts**\.

1. Under **Master account**, toggle **Accept** to the off position, and then choose **Update**\.

## Disassociating from a master account \(Security Hub API, AWS CLI\)<a name="securityhub-disassociate-from-master-api-cli"></a>

To disassociate your account from your master account, you can use an API call or the AWS Command Line Interface\.

**To disassociate from your master account \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisassociateFromMasterAccount.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisassociateFromMasterAccount.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/disassociate-from-master-account.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/disassociate-from-master-account.html) command\.

  ```
  aws securityhub disassociate-from-master-account
  ```