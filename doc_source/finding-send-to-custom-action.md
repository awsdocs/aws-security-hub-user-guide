# Sending findings to a custom action<a name="finding-send-to-custom-action"></a>

You can create AWS Security Hub custom actions to automate Security Hub with Amazon CloudWatch Events\. For custom actions, the event type is **Security Hub Findings \- Custom Action**\.

For more information and detailed steps on creating custom actions, see [Automating AWS Security Hub with CloudWatch Events](securityhub-cloudwatch-events.md)\.

After you set up a custom action, you can send findings to it\.

**To send findings to a custom action**

1. In the findings list, select the check box for each finding to send to the custom action\.

   You can send up to 20 findings at a time\.

1. For **Actions**, choose the custom action\.