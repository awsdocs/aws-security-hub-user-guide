# Designating a Security Hub administrator account<a name="designate-orgs-admin-account"></a>

The AWS Security Hub administrator account manages Security Hub membership for an organization\.

The organization management account designates the Security Hub administrator account for the organization\. The organization management account can designate any account in the organization, including itself\.

If you have a master account in place from the manual invitation process, then Security Hub recommends that you designate that account as the Security Hub administrator account for your organization\. Member accounts can only be associated with a single master account\. The Security Hub administrator account cannot enable member accounts that belong to another master account\.

The Security Hub administrator account must be the same in each Region\. However, the organization management account must designate that same Security Hub administrator account separately in each Region\.

The organization management account can also remove the currently designated Security Hub administrator account\. When the organization management account uses the console to remove the Security Hub administrator account in one Region, it is automatically removed in all Regions\. The Security Hub API only removes the Security Hub administrator account from the Region where the API call or command is issued\. To remove the Security Hub administrator account from all Regions, you can use the Organizations API\.

Security Hub administrator account is the master account, and it selects the member accounts\. See [Managing member accounts that belong to an organization](securityhub-accounts-orgs.md) and [Managing member accounts that are not in an organization](account-management-manual.md)\.

Remember that all Security Hub accounts must have AWS Config enabled and configured to record all resources\. For details on the requirement for AWS Config, see [Enabling and configuring AWS Config](securityhub-prereq-config.md)\.

## Required permissions to designate a Security Hub administrator account<a name="designate-admin-permissions"></a>

To designate a Security Hub administrator account, the organization management account must have permission for the `EnableOrganizationAdminAccount` action in Security Hub, and for the following actions in Organizations:
+ `EnableAWSServiceAccess`
+ `RegisterDelegatedAdministrator`
+ `DescribeOrganization`

To grant these permissions, add the following to the relevant IAM policy:

```
{
    "Sid": "Permissions to designate a Security Hub administrator account",
    "Effect": "Allow",
    "Action": [
        "securityhub:EnableOrganizationAdminAccount",
        "organizations:EnableAWSServiceAccess",
        "organizations:RegisterDelegatedAdministrator",
        "organizations:DescribeOrganization"
    ],
    "Resource": "*"
}
```

## Designating a Security Hub administrator account \(console\)<a name="designate-admin-console"></a>

The organization management account can use the Security Hub console to designate the Security Hub administrator account\.

The organization management account does not have to enable Security Hub in order to manage the Security Hub administrator account\.

**To designate a Security Hub administrator account from the **Welcome to Security Hub** page**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Choose **Go to Security Hub**\.

1. If a Security Hub administrator account is currently assigned, then you must remove the current account before you can designate a new account\.

   To remove the current account, under **Delegated Administrator**, choose **Remove**\.

1. Under **Delegated Administrator**, enter the account ID of the account to designate as the **Security Hub** administrator account\.

   You must designate the same Security Hub administrator account in all Regions\. If you designate an account that is different from the account designated in other Regions, Security Hub returns an error\.

1. Choose **Delegate**\.

You can also designate the Security Hub administrator account from the **Settings** page\. The organization management account uses this option if they are designated as the Security Hub administrator or enabled as a member account\.

**To designate a Security Hub administrator account from the **Settings** page**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Settings**\. Then choose **General**\.

1. If a Security Hub is currently assigned, then before you can designate a new account, you must remove the current account\.

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

The organization management account can remove the current Security Hub administrator account\. When the organization management account uses the console to remove the Security Hub administrator account, the Security Hub administrator account is removed in all Regions\.

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

When you use the API or AWS CLI to remove the Security Hub administrator account, it is only removed in the Region where the API call or command was issued\.

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

## Removing a Security Hub administrator account \(Organizations API, AWS CLI\)<a name="remove-admin-orgs-api"></a>

When you use the Security Hub API to remove the Security Hub administrator account, it is only removed in the Region where the API call or command was issued\.

The Organizations API allows you to remove the Security Hub administrator account from all Regions at once\.

To remove the Security Hub administrator account \(Organizations API, AWS CLI\)
+ **Organizations API –** Use the [https://docs.aws.amazon.com/organizations/latest/APIReference/API_DeregisterDelegatedAdministrator.html](https://docs.aws.amazon.com/organizations/latest/APIReference/API_DeregisterDelegatedAdministrator.html) operation\. You must provide the account ID of the Security Hub administrator account, and the service principal for Security Hub, which is `securityhub.amazonaws.com`\.
+ **AWS CLI –** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/organizations/deregister-delegated-administrator.html](https://docs.aws.amazon.com/cli/latest/reference/organizations/deregister-delegated-administrator.html) command\.

  ```
  aws organizations deregister-delegated-administrator --account-id <admin account ID> --service-principal <Security Hub service principal>
  ```

  **Example**

  ```
  aws organizations deregister-delegated-administrator --account-id 777788889999 --service-principal securityhub.amazonaws.com
  ```