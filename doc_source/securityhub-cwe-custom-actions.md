# Using custom actions to send findings and insight results to EventBridge<a name="securityhub-cwe-custom-actions"></a>

To use Security Hub custom actions to send findings or insight results to EventBridge, you first create the custom action in Security Hub\. Then define the rule in EventBridge\.

You can create up to 50 custom actions\.

The rule in EventBridge uses the ARN from the custom action\.

## Creating a custom action \(console\)<a name="securityhub-cwe-configure"></a>

When you create a custom action, you specify the name, description, and a unique identifier\.

**To create a custom action in Security Hub \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings** and then choose **Custom actions**\.

1. Choose **Create custom action**\.

1. Provide a **Name**, **Description**, and **Custom action ID** for the action\.

   The **Name** must be fewer than 20 characters\.

   The **Custom action ID** must be unique for each AWS account\.

1. Choose **Create custom action**\.

1. Make a note of the **Custom action ARN**\. You need to use the ARN when you create a rule to associate with this action in EventBridge\.

## Creating a custom action \(Security Hub API, AWS CLI\)<a name="securityhub-cwe-configure-api"></a>

To create a custom action, you can use an API call or the AWS Command Line Interface\.

**To create a custom action \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateActionTarget.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_CreateActionTarget.html) operation\. When you create a custom action, you provide the name, description, and custom action identifier\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/create-action-target.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/create-action-target.html) command\.

  ```
  create-action-target --name <customActionName> --description <customActionDescription> --id <customActionidentifier>
  ```

  **Example**

  ```
  aws securityhub create-action-target --name "Send to remediation" --description "Action to send the finding for remediation tracking" --id "Remediation"
  ```

## Defining a rule in EventBridge<a name="securityhub-cwe-define-rule"></a>

To process the custom action, you must create a corresponding rule in EventBridge\. The rule definition includes the ARN of the custom action\.

The event pattern for a **Security Hub Findings \- Custom Action** event has the following format:

```
{
  "source": [
    "aws.securityhub"
  ],
  "detail-type": [
    "Security Hub Findings - Custom Action"
  ],
  "resources": [ "<custom action ARN>" ]
}
```

The event pattern for a **Security Hub Insight Results** event has the following format:

```
{
  "source": [
    "aws.securityhub"
  ],
  "detail-type": [
    "Security Hub Insight Results"
  ],
  "resources": [ "<custom action ARN>" ]
}
```

In both formats, `<custom action ARN>` is the ARN of a custom action\. You can configure a rule that applies to more than one custom action\.

The instructions provided here are for the EventBridge console\. When you use the console, EventBridge automatically creates the required resource\-based policy that enables EventBridge to write to CloudWatch Logs\.

You can also use the [https://docs.aws.amazon.com/eventbridge/latest/APIReference/API_PutRule.html](https://docs.aws.amazon.com/eventbridge/latest/APIReference/API_PutRule.html) API operation of the EventBridge API\. However, if you use the EventBridge API, then you must create the resource\-based policy\. For details on the required policy, see [CloudWatch Logs permissions](https://docs.aws.amazon.com/eventbridge/latest/userguide/resource-based-policies-eventbridge.html#cloudwatchlogs-permissions) in the *Amazon EventBridge User Guide*\.

**To define a rule in EventBridge**

1. Open the Amazon EventBridge console at [https://console\.aws\.amazon\.com/events/](https://console.aws.amazon.com/events/)\.

1. In the navigation pane, choose **Rules**\.

1. Choose **Create rule**\.

1. Enter a name and description for the rule\.

1. For **Event source**, choose **Event Pattern**\.

1. For **Event matching** pattern, choose **Pre\-defined pattern by service**\.

1. For **Service provider**, choose **AWS**\.

1. For **Service name**, choose **Security Hub**\.

1. For **Event type**, to create a rule to apply when you send findings to a custom action, choose **Security Hub Findings \- Custom Action**\.

   To create a rule to apply when you send insight results to a custom action, choose **Security Hub Insight Results**\.

1. For each custom action that this rule applies to, perform the following steps:

   1. Choose **Specific custom action**\.

   1. To add a custom action ARN, enter the ARN in the field, and then choose **Add**\.

   1. To remove a custom action ARN, choose **Remove** for that value\.

1. Under **Select targets**, choose and configure the target to invoke when this rule is matched\.

1. Choose **Create**\.

After this rule is created in EventBridge, when you perform a custom action on findings or insight results in your account, events are generated in EventBridge\.

## Selecting a custom action for findings and insight results<a name="securityhub-cwe-send"></a>

After you create your Security Hub custom actions and EventBridge rules, you can send findings and insight results to EventBridge for further management and processing\.

Events are sent to EventBridge only in the account in which they are viewed\. If you view a finding using an administrator account, the event is sent to EventBridge in the administrator account\.

For AWS API calls to be effective, the implementations of target code must switch roles into member accounts\. This also means that the role you switch into must be deployed to each member where action is needed\.

**To send findings to EventBridge**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Display a list of findings:
   + From **Findings**, you can view findings from all of the enabled product integrations and controls\.
   + From **Security standards**, you can navigate to a list of findings generated from a selected control\. See [Viewing details for a control](securityhub-standards-control-details.md)\.
   + From **Integrations**, you can navigate to a list of findings generated by an enabled integration\. See [Viewing the findings from an integration](securityhub-integrations-managing.md#securityhub-integration-view-findings)\.
   + From **Insights**, you can navigate to a list of findings for an insight result\. See [Viewing and taking action on insight results and findings](securityhub-insights-view-take-action.md)\.

1. Select the findings to send to EventBridge\. You can select up to 20 findings at a time\.

1. From **Actions**, choose the custom action that aligns with the EventBridge rule to apply\.

   Security Hub sends a separate **Security Hub Findings \- Custom Action** event for each finding\.

**To send insight results to EventBridge**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Insights**\.

1. On the **Insights** page, choose the insight that includes the results to send to EventBridge\.

1. Select the insight results to send to EventBridge\. You can select up to 20 results at a time\.

1. From **Actions**, choose the custom action that aligns with the EventBridge rule to apply\.