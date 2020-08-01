# Enabling new controls automatically<a name="controls-auto-enable"></a>

AWS Security Hub regularly adds new controls to standards\. When you first enable Security Hub, it automatically enables new controls as they are added\. This only applies to enabled standards\. Security Hub does not enable new controls when they are added to a standard that you disabled\.

You can choose whether to automatically enable new controls\. If you do not automatically enable new controls, then you must enable them manually\. See [Disabling and enabling individual controls](securityhub-standards-enable-disable-controls.md)\.

## Choosing whether to automatically enable new controls \(console\)<a name="controls-auto-enable-console"></a>

The **General** tab of the **Settings** page includes a setting to control whether to automatically enable new controls\.

**To choose whether to enable new controls for enabled standards**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**, and then choose the **General** tab\.

1. Under **Auto\-enable new controls**, choose **Edit**\.

1. Toggle **Auto\-enable new controls in standards I have enabled**\.

1. Choose **Save**\.

## Choosing whether to automatically enable new controls \(Security Hub API, AWS CLI\)<a name="controls-auto-enable-api-cli"></a>

To configure whether to automatically enable new controls, you can use an API call or the AWS Command Line Interface\.

**To configure whether to automatically enable new controls \(Security Hub API, AWS CLI\)**
+ **Security Hub** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateSecurityHubConfiguration.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateSecurityHubConfiguration.html) operation\. To automatically enable controls, set `AutoEnableControls` to `true`\. To not automatically enable controls, set `AutoEnableControls` to false\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-security-hub-configuration.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-security-hub-configuration.html) command\. To automatically enable new controls, specify `--auto-enable-controls`\. To not enable new controls, specify `--no-auto-enable-controls`\.

  ```
  aws securityhub update-security-hub-configuration --auto-enable-controls | --no-auto-enable-controls
  ```

  **Example**

  ```
  aws securityhub update-security-hub-configuration --auto-enable-controls
  ```