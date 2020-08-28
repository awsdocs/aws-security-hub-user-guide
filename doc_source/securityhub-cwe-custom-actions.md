# Using custom actions to send findings and insight results to CloudWatch Events<a name="securityhub-cwe-custom-actions"></a>

To use Security Hub custom actions to send findings or insight results to CloudWatch Events, you first create the custom action in Security Hub\. Then define the rule in CloudWatch Events\.

The rule in CloudWatch Events uses the ARN from the custom action\.

## Creating a custom action \(console\)<a name="securityhub-cwe-configure"></a>

When you create a custom action, you specify the name, description, and a unique identifier\.

**To create a custom action in Security Hub \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings** and then choose **Custom actions**\.

1. Choose **Create custom action**\.

1. Provide a **Name**, **Description**, and **Custom action ID** for the action\.

   The **Name** must be fewer than 20 characters\.

   The **Custom action ID** must be unique per AWS account\.

1. Choose **Create custom action**\.

1. Make a note of the **Custom action ARN**\. You need to use the ARN when you create a rule to associate with this action in CloudWatch Events\.

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

## Defining a rule in CloudWatch Events<a name="securityhub-cwe-define-rule"></a>

To process the custom action, you must create a corresponding rule in CloudWatch Events\. The rule definition includes the ARN of the custom action\.

**To define a rule in CloudWatch Events**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Rules**\.

1. Choose **Create rule**\.

1. For **Event source**, confirm that **Event Pattern** is selected\.

1. Choose **Edit** for **Event Pattern Preview**\.

1. Copy one of the following example patterns, and paste it into the preview window\. Be sure to replace the existing brackets\.

   For an event associated with a finding custom action \(**Security Hub Findings \- Custom Action** event type\), use the following format\. Replace the placeholder ARN with the **Custom Action ARN** for the custom action you created\.

   ```
   {
     "source": [
       "aws.securityhub"
     ],
     "detail-type": [
       "Security Hub Findings - Custom Action"
     ],
     "resources": [
       "arn:aws:securityhub:us-west-2:123456789012:action/custom/test-action1"
     ]
   }
   ```

   For an event associated with an insight custom action \(**Security Hub Insight Results** event type\), use the following format\. Replace the placeholder ARN with the **Custom Action ARN** for the custom action you created\.

   ```
   {
     "source": [
       "aws.securityhub"
     ],
     "detail-type": [
       "Security Hub Insight Results"
     ],
     "resources": [
       "arn:aws:securityhub:us-west-2:123456789012:action/custom/test-action1"
     ]
   }
   ```

1. Choose **Save** to close the window\.

1. Choose **Add target** and then select the target to invoke when this rule is matched\.

1. Choose **Configure details**\.

1. Enter a name and description for the rule\.

   To enable the rule now, for **State**, select **Enabled**\. To save the rule without enabling it, clear **Enabled**\.

1. Choose **Create rule**\.

After this rule is created in CloudWatch Events, when you perform a custom action on findings or insight results in your account, events are generated in CloudWatch Events\.

## Selecting a custom action for findings and insight results<a name="securityhub-cwe-send"></a>

After you create your Security Hub custom actions and CloudWatch Events rules, you can send findings and insight results to CloudWatch Events for further management and processing\.

Events are sent to CloudWatch Events only in the account in which they are viewed\. If you view a finding using a master account, the event is sent to CloudWatch Events in the master account\.

For AWS API calls to be effective, the implementations of target code must switch roles into member accounts\. This also means that the role you must switch into must be deployed to each member where action is needed\.

**To send findings to CloudWatch Events**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. Display a list of findings:
   + From **Findings**, you can view findings from all of the enabled product integrations and controls\.
   + From **Security standards**, you can navigate to a list of findings generated from a selected control\. See [Viewing details for a control](securityhub-standards-control-details.md)\.
   + From **Integrations**, you can navigate to a list of findings generated by an enabled integration\. See [Viewing the findings from an integration](securityhub-integrations-managing.md#securityhub-integration-view-findings)\.
   + From **Insights**, you can navigate to a list of findings for an insight result\. See [Viewing and taking action on insight results and findings](securityhub-insights-view-take-action.md)\.

1. Select the findings to send to CloudWatch Events\. You can select up to 20 findings at a time\.

1. From **Actions**, choose the custom action that aligns with the CloudWatch Events rule to apply\.

**To send insight results to CloudWatch Events**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Insights**\.

1. On the **Insights** page, choose the insight that includes the results to send to CloudWatch Events\.

1. Select the insight results to send to CloudWatch Events\. You can select up to 20 results at a time\.

1. From **Actions**, choose the custom action that aligns with the CloudWatch Events rule to apply\.