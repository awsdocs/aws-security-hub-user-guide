# Responding to an invitation to be a member account<a name="securityhub-invitation-respond"></a>

You can accept or decline an invitation to be a member account\.

After you accept an invitation, your account becomes an AWS Security Hub member account\. The account that sent the invitation becomes your Security Hub master account\. The master account user can view findings for your member account in Security Hub\.

If you decline the invitation, then your account is marked as **Resigned** on the master account's list of member accounts\.

You can only accept one invitation to be a member account\.

Before you can accept or decline an invitation, you must enable Security Hub\. For information on how to enable Security Hub, see [Enabling Security Hub](securityhub-settingup.md#securityhub-enable)\.

## Accepting an invitation \(console\)<a name="securityhub-accept-invitation-console"></a>

On the **Accounts** page, **Master account** contains the invitation and membership information for an account\.

**To accept an invitation to be a member account**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**, and then choose **Accounts**\.

1. Under **Master account**, toggle **Accept** to the on position, and then choose **Accept invitation**\.

## Accepting an invitation \(Security Hub API, AWS CLI\)<a name="securityhub-accept-invitation-api-cli"></a>

To accept an invitation to be a member account, you can use an API call or the AWS Command Line Interface\. You must use the credentials for the member account that received the invitation\.

**To accept an invitation \(Security Hub API, AWS CLI\)**
+ **Security Hub** API – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AcceptInvitation.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AcceptInvitation.html) operation\. You must provide the invitation identifier and the AWS account ID of the master account\. To retrieve details about the invitation, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListInvitations.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListInvitations.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/accept-invitation.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/accept-invitation.html) command\.

  ```
  aws securityhub accept-invitation --master-id <masterAccountID> --invitation-id <invitationID>
  ```

  **Example**

  ```
  aws securityhub accept-invitation --master-id 123456789012 --invitation-id 7ab938c5d52d7904ad09f9e7c20cc4eb
  ```

## Declining an invitation \(console\)<a name="securityhub-decline-invitation-console"></a>

You can decline an invitation to be a member account\. When you decline an invitation, your account is marked as **Resigned** on the master account's list of member accounts\.

**To decline an invitation to be a member account**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**, and then choose **Accounts**\.

1. Under **Master account**, choose **Decline invitation**\.

## Declining an invitation \(Security Hub API, AWS CLI\)<a name="securityhub-decline-invitation-api-cli"></a>

To decline an invitation, you can use an API call or the AWS Command Line Interface\.

**To decline an invitation \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DeclineInvitations.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DeclineInvitations.html) operation\. You must provide the AWS account ID of the master account that issued the invitation\. To view information about your invitations, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListInvitations.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListInvitations.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/decline-invitations.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/decline-invitations.html) command\.

  ```
  aws securityhub decline-invitations --account-ids "<masterAccountId>"
  ```

  **Example**

  ```
  aws securityhub decline-invitations --account-ids "123456789012"
  ```