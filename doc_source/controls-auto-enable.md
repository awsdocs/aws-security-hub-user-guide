# Enabling new controls in enabled standards automatically<a name="controls-auto-enable"></a>

AWS Security Hub regularly adds new controls to standards\. You can choose whether to automatically enable new controls in your enabled standards\. If you do not automatically enable new controls, then you must enable them manually\. See [Enabling and disabling controls in all standards](securityhub-standards-enable-disable-controls.md)\.

Security Hub doesn't enable new controls when they are added to a standard that you disabled\.

Choose your preferred access method, and follow the steps to automatically enable new controls in enabled standards\.

------
#### [ Security Hub console ]

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**, and then choose the **General** tab\.

1. Under **Controls**, choose **Edit**\.

1. Turn on **Auto\-enable new controls in enabled standards**\.

1. Choose **Save**\.

------
#### [ Security Hub API ]

1. Run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateSecurityHubConfiguration.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateSecurityHubConfiguration.html)\.

1. To automatically enable new controls for enabled standards, set `AutoEnableControls` to `true`\. If you don't want to automatically enable new controls, set `AutoEnableControls` to false\.

------
#### [ AWS CLI ]

1. Run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-security-hub-configuration.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/update-security-hub-configuration.html) command\.

1. To automatically enable new controls for enabled standards, specify `--auto-enable-controls`\. If you don't want to automatically enable new controls, specify `--no-auto-enable-controls`\.

   ```
   aws securityhub update-security-hub-configuration --auto-enable-controls | --no-auto-enable-controls
   ```

   **Example command**

   ```
   aws securityhub update-security-hub-configuration --auto-enable-controls
   ```

------