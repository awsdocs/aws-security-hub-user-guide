# Designating a Security Hub administrator account<a name="designate-orgs-admin-account"></a>

The Security Hub administrator account manages Security Hub membership for an organization\.

## How the Security Hub administrator account is managed<a name="designate-admin-overview"></a>

The organization management account designates the Security Hub administrator account in each Region\.

The Security Hub administrator account then enables organization accounts as member accounts\. They can also invite other accounts to be member accounts\. See [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md) and [Managing member accounts by invitation](account-management-manual.md)\.

![\[Diagram that shows how the organization management account designates an organization account as the delegated administrator for Security Hub. The delegated administrator becomes a Security Hub administrator account.\]](http://docs.aws.amazon.com/securityhub/latest/userguide/images/diagram_account_delegation.png)

Member accounts can only be associated with a single administrator account\. The Security Hub administrator account cannot enable member accounts that belong to another administrator account\.

All Security Hub accounts must have AWS Config enabled and configured to record all resources\. For details on the requirement for AWS Config, see [Enabling and configuring AWS Config](securityhub-prereq-config.md)\.

### Setting the Security Hub administrator account as the delegated administrator account<a name="designate-admin-delegated-admin"></a>

When you first choose a Security Hub administrator account, Security Hub calls Organizations to make that account the delegated administrator account for Security Hub\.

Once you have a delegated administrator account in Organizations, then you can choose either that account or the organization management account as the Security Hub administrator account in all Regions\. We recommend choosing the same delegated administrator account in all Regions\.

To choose a different account, you must remove the current Security Hub administrator account in all Regions\.

### Recommendations for choosing the Security Hub administrator account<a name="designate-admin-recommendations"></a>

If you have an administrator account in place from the manual invitation process, then Security Hub recommends that you designate that account as the Security Hub administrator account\.

We also recommend that you do not designate the organization management account itself as the Security Hub administrator account\. This is because the users who have access to the organization management account to manage billing are likely to be different from the users who need access to Security Hub for security management\.

The organization management account also cannot be the delegated administrator account for a service in Organizations\.

### Removing the Security Hub administrator account<a name="designate-admin-overview-remove"></a>

The organization management account can remove the Security Hub administrator account\.

When the organization management account uses the console to remove the Security Hub administrator account in one Region, it is automatically removed in all Regions\. Security Hub also calls Organizations to remove the delegated administrator account\.

The Security Hub API only removes the Security Hub administrator account from the Region where the API call or command is issued\. It does not update other Regions, and it does not remove the delegated administrator account in Organizations\.

When you use the Organizations API to remove the delegated administrator account for Security Hub, Security Hub also removes the Security Hub administrator account in all Regions\.

## Required permissions to configure the Security Hub administrator account<a name="designate-admin-permissions"></a>

To designate and remove a Security Hub administrator account, the organization management account must have permissions for the `EnableOrganizationAdminAccount` and `DisableOrganizationAdminAccount` actions in Security Hub\. The organization management account must also have administrative permissions for Organizations\.

To grant all of the required permissions, attach the following Security Hub managed policies to the IAM principal for the organization management account:
+ [`AWSSecurityHubFullAccess`](security-iam-awsmanpol.md#security-iam-awsmanpol-awssecurityhubfullaccess)
+ [`AWSSecurityHubOrganizationsAccess`](security-iam-awsmanpol.md#security-iam-awsmanpol-awssecurityhuborganizationsaccess)

## Designating a Security Hub administrator account \(console\)<a name="designate-admin-console"></a>

The organization management account can use the Security Hub console to designate the Security Hub administrator account\.

The organization management account does not have to enable Security Hub in order to manage the Security Hub administrator account\.

 Security Hub recommends that the organization management account is not the Security Hub administrator account\. However, if the organization management account does choose itself as the Security Hub administrator account, it must have Security Hub enabled\. If it does not have Security Hub enabled, it must enable Security Hub manually\. Security Hub cannot be enabled automatically for the organization management account\.

**To designate a Security Hub administrator account from the **Welcome to Security Hub** page**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Choose **Go to Security Hub**\.

1. If a Security Hub administrator account is currently assigned, then you must remove the current account before you can designate a new account\.

   To remove the current account, under **Delegated Administrator**, choose **Remove**\.

1. Under **Delegated Administrator**, enter the account ID of the account to designate as the **Security Hub** administrator account\.

   You must designate the same Security Hub administrator account in all Regions\. If you designate an account that is different from the account designated in other Regions, Security Hub returns an error\.

1. Choose **Delegate**\.

If you have Security Hub enabled, then you can also designate the Security Hub administrator account from the **Settings** page\.

**To designate a Security Hub administrator account from the **Settings** page**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Settings**\. Then choose **General**\.

1. If a Security Hub administrator account is currently assigned, then before you can designate a new account, you must remove the current account\.

   Under **Delegated Administrator**, to remove the current account, choose **Remove**\.

1. Enter the account ID of the account you want to designate as the **Security Hub** administrator account\.

   You must designate the same Security Hub administrator account in all Regions\. If you designate an account that is different from the account designated in other Regions, Security Hub returns an error\.

1. Choose **Delegate**\.

## Designating a Security Hub administrator account \(Security Hub API, AWS CLI\)<a name="designate-admin-api"></a>

To designate the Security Hub administrator account, you can use an API call or the AWS Command Line Interface\. You must use the organization management account credentials\.

To designate the **Security Hub** administrator account \(Security Hub API, AWS CLI\)
+ **Security Hub API –** Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableOrganizationAdminAccount.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_EnableOrganizationAdminAccount.html) operation\. You must provide the AWS account ID of the Security Hub administrator account\.
+ **AWS CLI –** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/enable-organization-admin-account.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/enable-organization-admin-account.html) command\.

  ```
  aws securityhub enable-organization-admin-account --admin-account-id <admin account ID>
  ```

  **Example**

  ```
  aws securityhub enable-organization-admin-account --admin-account-id 777788889999
  ```

## Removing a Security Hub administrator account \(console\)<a name="remove-admin-console"></a>

The organization management account can remove the current Security Hub administrator account\. When you use the console to remove the Security Hub administrator account, the Security Hub administrator account is removed in all Regions\. Security Hub also calls Organizations to remove the delegated administrator account for Security Hub\.

When the Security Hub administrator account is removed, the member accounts are disassociated from the removed Security Hub administrator account\.

The enabled member accounts still have Security Hub enabled\. They become standalone accounts until a new Security Hub administrator enables them as member accounts\.

If the organization management account is not an enabled account in Security Hub, then use the option on the **Welcome to Security Hub** page\.

**To remove the Security Hub administrator account from the **Welcome to Security Hub** page**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Choose **Go to Security Hub**\.

1. Under **Delegated Administrator**, choose **Remove**\.

If the organization management account is an enabled account in **Security Hub**, then use the option on the **General** tab of the **Settings** page\.

**To remove the Security Hub administrator account from the **Settings** page**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Settings**\. Then choose **General**\.

1. Under **Delegated Administrator**, choose **Remove**\.

## Removing a Security Hub administrator account \(Security Hub API, AWS CLI\)<a name="remove-admin-api"></a>

To remove the Security Hub administrator account, you can use an API call or the AWS Command Line Interface\. You must use the organization management account credentials\.

When you use the API or AWS CLI to remove the Security Hub administrator account, it is only removed in the Region where the API call or command was issued\. Security Hub does not update other Regions, and it does not remove the delegated administrator account in Organizations\.

To remove the Security Hub administrator account \(Security Hub API, AWS CLI\)
+ **Security Hub API –** Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableOrganizationAdminAccount.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableOrganizationAdminAccount.html) operation\. You must provide the account ID of the Security Hub administrator account\.
+ **AWS CLI –** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/disable-organization-admin-acccount.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/disable-organization-admin-acccount.html) command\.

  ```
  aws securityhub disable-organization-admin-account --admin-account-id <admin account ID>
  ```

  **Example**

  ```
  aws securityhub disable-organization-admin-account --admin-account-id 777788889999
  ```

## Removing the delegated administrator account \(Organizations API, AWS CLI\)<a name="remove-admin-orgs-api"></a>

When you use the Security Hub API to remove the Security Hub administrator account, it is only removed in the Region where the API call or command was issued\. Security Hub does not update other Regions, and does not remove the delegated administrator account in Organizations\.

The Organizations API allows you to remove the delegated administrator account\. When you remove the delegated administrator account for Security Hub, Security Hub also removes the Security Hub administrator account from all Regions\.

To remove the delegated administrator account \(Organizations API, AWS CLI\)
+ **Organizations API –** Use the [https://docs.aws.amazon.com/organizations/latest/APIReference/API_DeregisterDelegatedAdministrator.html](https://docs.aws.amazon.com/organizations/latest/APIReference/API_DeregisterDelegatedAdministrator.html) operation\. You must provide the account ID of the delegated administrator account, and the service principal for Security Hub, which is `securityhub.amazonaws.com`\.
+ **AWS CLI –** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/organizations/deregister-delegated-administrator.html](https://docs.aws.amazon.com/cli/latest/reference/organizations/deregister-delegated-administrator.html) command\.

  ```
  aws organizations deregister-delegated-administrator --account-id <admin account ID> --service-principal <Security Hub service principal>
  ```

  **Example**

  ```
  aws organizations deregister-delegated-administrator --account-id 777788889999 --service-principal securityhub.amazonaws.com
  ```