# Automatically enabling new organization accounts<a name="accounts-orgs-auto-enable"></a>

The Security Hub administrator account can configure Security Hub to automatically enable new organization accounts as member accounts\.

When new accounts are added to your organization, they are added to the list on the **Accounts** page\. For organization accounts, **Type** is **By organization**\.

By default, the new accounts are not enabled as member accounts\. Their status is **Not a member**\.

When you enable the automatic enablement setting, Security Hub begins to enable new accounts as member accounts when they are added to the organization\. It does not enable existing organization accounts that are not enabled as member accounts\. Security Hub also cannot automatically enable accounts that already belong to another administrator account\.

If the account does not have Security Hub enabled, then Security Hub and the default standards are enabled automatically for that account\.

For organization accounts that already have Security Hub enabled, Security Hub does not make any other changes to the account\. It only enables the membership\.

Remember that all Security Hub accounts must have AWS Config enabled and configured to record all resources\. For details on the requirement for AWS Config, see [Enabling and configuring AWS Config](securityhub-prereq-config.md)\.

## Enabling Security Hub automatically for new accounts \(console\)<a name="accounts-orgs-auto-enable-console"></a>

The **Accounts** page includes a configuration option to automatically add new accounts\.

**To automatically enable new organization accounts as member accounts**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the Security Hub navigation pane, choose **Settings**\.

1. On the **Settings** page, choose **Accounts**\.

1. On the **Accounts** tab, toggle the automatic enablement setting to **Auto\-enable is on**\.

## Enabling Security Hub automatically for new organization accounts \(Security Hub API, AWS CLI\)<a name="accounts-orgs-auto-enable-api"></a>

To determine whether to automatically enable new organization accounts, the administrator account can use the Security Hub API or the AWS Command Line Interface\.

**To automatically enable new organization accounts**
+ **Security Hub API –** Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateOrganizationConfiguration.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateOrganizationConfiguration.html) operation\. To automatically enable new organization accounts, set `autoEnable` to `true`\.
+ **AWS CLI –** At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-organization-configuration.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-organization-configuration.html) command\.

  ```
  aws securityhub update-organization-configuration --auto-enable
  ```