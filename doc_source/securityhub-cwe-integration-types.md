# Types of Security Hub integration with CloudWatch Events<a name="securityhub-cwe-integration-types"></a>

Security Hub uses the following CloudWatch event types to support the following types of integration with CloudWatch Events\.

On the CloudWatch Events dashboard for Security Hub, **All Events** includes all of these event types\.

## All findings \(Security Hub Findings \- Imported\)<a name="securityhub-cwe-integration-types-all-findings"></a>

 Security Hub automatically sends all findings to CloudWatch Events as **Security Hub Findings \- Imported** events\. **Security Hub Findings \- Imported** events are triggered by updates from both [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) and [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

You can define rules in CloudWatch Events that automatically route findings to an Amazon S3 bucket, a remediation workflow, or a third\-party tool\.

Use this method to automatically send all findings, or all findings with specific characteristics, to a response or remediation workflow\.

See [Configuring a CloudWatch Events rule for automatically sent findings](securityhub-cwe-all-findings.md)\.

## Findings for custom actions \(Security Hub Findings \- Custom Action\)<a name="securityhub-cwe-integration-types-finding-custom-action"></a>

Security Hub also sends findings associated with custom actions to CloudWatch Events as **Security Hub Findings \- Custom Action** events\.

This is useful for analysts working with the Security Hub console who want to send a specific finding, or a small set of findings, to a response or remediation workflow\. You can select a custom action for up to 20 findings at a time\. The set of findings is sent to CloudWatch as a single CloudWatch event\.

When you create a custom action, you specify a custom action ID for the custom action\. You can use this ID to create a CloudWatch Events rule that takes a specified action after receiving a finding that is associated with the custom action ID\.

See [Creating a custom action \(console\)](securityhub-cwe-custom-actions.md#securityhub-cwe-configure)\.

For example, you can create a custom action in Security Hub called `send_to_ticketing`\. Then in CloudWatch Events, you create a rule that is triggered when CloudWatch Events receives a finding that includes the `send_to_ticketing` custom action ID\. The rule includes logic to send the finding to your ticketing system\. You can then select findings within Security Hub and use the custom action in Security Hub to manually send findings to your ticketing system\.

For examples of how to send Security Hub findings to CloudWatch Events for further processing, see [How to Integrate AWS Security Hub Custom Actions with PagerDuty](http://aws.amazon.com/blogs/apn/how-to-integrate-aws-security-hub-custom-actions-with-pagerduty/) and [How to Enable Custom Actions in AWS Security Hub](http://aws.amazon.com/blogs/apn/how-to-enable-custom-actions-in-aws-security-hub/) on the AWS Partner Network \(APN\) Blog\.

## Insight results for custom actions \(Security Hub Insight Results\)<a name="securityhub-cwe-integration-types-insight-custom-action"></a>

You can also use custom actions to send a set of insight results to CloudWatch Events as **Security Hub Insight Results** events\. Insight results are the set of resources that are associated with an insight\. Note that when you send insight results to CloudWatch Events, you are not sending the findings to CloudWatch Events\. You are only sending the resource identifiers that are associated with the insight results\. You can send up to 100 resource identifiers at a time\.

Similar to custom actions for findings, you first create the custom action in Security Hub, and then create a rule in CloudWatch Events\.

See [Creating a custom action \(console\)](securityhub-cwe-custom-actions.md#securityhub-cwe-configure)\.

For example, suppose you see a particular insight result of interest that you want to share with a colleague\. In that case, you can use custom actions to send that insight result to the colleague through a chat or ticketing system\.