# Sending findings to a custom action<a name="finding-send-to-custom-action"></a>

You can create AWS Security Hub custom actions to automate Security Hub with Amazon CloudWatch Events\. For custom actions, the event type is **Security Hub Findings \- Custom Action**\.

For more information and detailed steps on creating custom actions, see [Automated response and remediation](securityhub-cloudwatch-events.md)\.

After you set up a custom action, you can send findings to it\.

**To send findings to a custom action**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. To display a finding list, do one of the following:
   + In the Security Hub navigation pane, choose **Findings**\.
   + In the Security Hub navigation pane, choose **Insights**\. Choose an insight\. Then on the results list, choose an insight result\.
   + In the Security Hub navigation pane, choose **Integrations**\. Choose **See findings** for an integration\.
   + In the Security Hub navigation pane, choose **Security standards**\. Choose **View results** to display a list of controls\. Then choose the control name\.

1. In the finding list, select the check box for each finding to send to the custom action\.

   You can send up to 20 findings at a time\.

1. For **Actions**, choose the custom action\.