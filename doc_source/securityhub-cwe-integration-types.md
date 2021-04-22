# Types of Security Hub integration with EventBridge<a name="securityhub-cwe-integration-types"></a>

Security Hub uses the following EventBridge event types to support the following types of integration with EventBridge\.

On the EventBridge dashboard for Security Hub, **All Events** includes all of these event types\.

## All findings \(Security Hub Findings \- Imported\)<a name="securityhub-cwe-integration-types-all-findings"></a>

 Security Hub automatically sends all new findings and all updates to existing findings to EventBridge as **Security Hub Findings \- Imported** events\.

Every [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) and [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) request triggers a **Security Hub Findings \- Imported** event\.

For administrator accounts, the event feed in EventBridge includes events for findings from both their account and from their member accounts\.

You can define rules in EventBridge that automatically route findings to an Amazon S3 bucket, a remediation workflow, or a third\-party tool\. The rules can include filters to only apply the rule if the finding has specific attribute values\.

You use this method to automatically send all findings, or all findings that have specific characteristics, to a response or remediation workflow\.

See [Configuring an EventBridge rule for automatically sent findings](securityhub-cwe-all-findings.md)\.

## Findings for custom actions \(Security Hub Findings \- Custom Action\)<a name="securityhub-cwe-integration-types-finding-custom-action"></a>

Security Hub also sends findings associated with custom actions to EventBridge as **Security Hub Findings \- Custom Action** events\.

This is useful for analysts working with the Security Hub console who want to send a specific finding, or a small set of findings, to a response or remediation workflow\. You can select a custom action for up to 20 findings at a time\. The set of findings is sent to EventBridge as a single EventBridge event\.

When you create a custom action, you specify a custom action ID for the custom action\. You can use this ID to create an EventBridge rule that takes a specified action after receiving a finding that is associated with that custom action ID\.

See [Using custom actions to send findings and insight results to EventBridge](securityhub-cwe-custom-actions.md)\.

For example, you can create a custom action in Security Hub called `send_to_ticketing`\. Then in EventBridge, you create a rule that is triggered when EventBridge receives a finding that includes the `send_to_ticketing` custom action ID\. The rule includes logic to send the finding to your ticketing system\. You can then select findings within Security Hub and use the custom action in Security Hub to manually send findings to your ticketing system\.

For examples of how to send Security Hub findings to EventBridge for further processing, see [How to Integrate AWS Security Hub Custom Actions with PagerDuty](http://aws.amazon.com/blogs/apn/how-to-integrate-aws-security-hub-custom-actions-with-pagerduty/) and [How to Enable Custom Actions in AWS Security Hub](http://aws.amazon.com/blogs/apn/how-to-enable-custom-actions-in-aws-security-hub/) on the AWS Partner Network \(APN\) Blog\.

## Insight results for custom actions \(Security Hub Insight Results\)<a name="securityhub-cwe-integration-types-insight-custom-action"></a>

You can also use custom actions to send sets of insight results to EventBridge as **Security Hub Insight Results** events\. Insight results are the resources that match an insight\. Note that when you send insight results to EventBridge, you are not sending the findings to EventBridge\. You are only sending the resource identifiers that are associated with the insight results\. You can send up to 100 resource identifiers at a time\.

Similar to custom actions for findings, you first create the custom action in Security Hub, and then create a rule in EventBridge\.

See [Using custom actions to send findings and insight results to EventBridge](securityhub-cwe-custom-actions.md)\.

For example, suppose you see a particular insight result of interest that you want to share with a colleague\. In that case, you can use a custom action to send that insight result to the colleague through a chat or ticketing system\.