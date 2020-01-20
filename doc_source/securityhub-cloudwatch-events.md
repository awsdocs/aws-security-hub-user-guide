# Automating AWS Security Hub with CloudWatch Events<a name="securityhub-cloudwatch-events"></a>

Amazon CloudWatch Events enables you to automate your AWS services and respond automatically to system events such as application availability issues or resource changes\. Events from AWS services are delivered to CloudWatch Events in near real time\. You can write simple rules to indicate which events you're interested in and what automated actions to take when an event matches a rule\. The actions that can be automatically triggered include the following:
+ Invoking an AWS Lambda function
+ Invoking Amazon EC2 Run Command
+ Relaying the event to Amazon Kinesis Data Streams
+ Activating an AWS Step Functions state machine
+ Notifying an Amazon SNS topic or an AWS SMS queue

For more information, see the [Amazon CloudWatch Events User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/)\.

**Note**  
As a best practice, make sure that the permissions granted to your users to access CloudWatch Events use least\-privilege IAM policies, and that only the required permissions are granted\.  
For more information, see [Authentication and Access Control for Amazon CloudWatch Events](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/auth-and-access-control-cwe.html)\. 

## Types of Security Hub Integration with CloudWatch Events<a name="securityhub-cwe-integration-types"></a>

Security Hub supports the following types of integration with CloudWatch Events:
+ **All findings \-** Security Hub automatically sends all findings to CloudWatch Events as events\.

  You can define rules in CloudWatch Events that automatically route generated findings to an Amazon S3 bucket, a remediation workflow, or a third\-party tool\.

  Use this method to automatically send all findings, or all findings with specific characteristics, to a response or remediation workflow\.
+ **Findings for custom actions \- **Security Hub also sends findings associated with custom actions to CloudWatch Events\. This is useful for analysts working with the Security Hub console who want to send a specific finding, or a small set of findings, to a response or remediation workflow\.

  When you create a custom action, you specify a custom action ID for the custom action\. You can use the custom action ID to create a rule in CloudWatch Events that defines a specific action to take when a finding is received that is associated with the custom action ID\.

  For example, you can create a custom action in Security Hub that sends findings to a ticketing system with a custom action ID set to "send\_to\_ticketing"\. Then in CloudWatch Events, create a rule that is triggered for any finding received that includes a custom action ID of "send\_to\_ticketing"\. The rule in CloudWatch Events includes logic to send the finding to your ticketing system\. You can then also select findings within Security Hub and use the custom action in Security Hub to manually send findings to your ticketing system\.
+ **Insight results \-** You can also use custom actions to send a set of insight results to CloudWatch Events\.

  For example, if you see a particular insight result of interest that you want to share with a colleague, you can use custom actions to send that insight result to the colleague via a chat or ticketing system\.

For examples of how to send Security Hub findings to CloudWatch Events for further processing, see [How to Integrate AWS Security Hub Custom Actions with PagerDuty](http://aws.amazon.com/blogs/apn/how-to-integrate-aws-security-hub-custom-actions-with-pagerduty/) and [How to Enable Custom Actions in AWS Security Hub](http://aws.amazon.com/blogs/apn/how-to-enable-custom-actions-in-aws-security-hub/) on the AWS Partner Network \(APN\) Blog\.

## Configuring a CloudWatch Events Rule for Security Hub Findings That Are Automatically Sent to CloudWatch Events<a name="securityhub-cwe-all-findings"></a>

You can create a rule in CloudWatch Events that defines an action to take when an event is received, such as a finding from Security Hub\.

**To create a CloudWatch Events rule for a Security Hub finding**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Rules**\.

1. Choose **Create rule**\.

1. For **Event source**, confirm that **Event Pattern** is selected\.

1. Choose **Edit** for **Event Pattern Preview**\.

1. Copy the following example pattern and paste it into the preview window\. Be sure to replace the existing brackets\.

   ```
   {
     "source": [
       "aws.securityhub"
     ],
     "detail-type": [
       "Security Hub Findings - Imported"
     ]
   }
   ```

1. Choose **Save** to close the window\.

1. Choose **Add target**, then select the target to invoke when this rule is matched\.

   You might need to configure the settings for the selected target\.

## Creating a Custom Action and Associating It with a CloudWatch Events Rule<a name="securityhub-cwe-configure"></a>

To configure Security Hub and CloudWatch Events to send Security Hub findings that are associated with custom actions to CloudWatch Events, complete the following procedures\.

**To create a custom action in Security Hub**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings** and then choose **Custom actions**\.

1. Choose **Create custom action**\.

1. Provide a **Name**, **Description**, and **Custom action ID** for the action\.

   The **Name** must be fewer than 20 characters\. The **Custom action ID** must be unique per AWS account\.

1. Choose **Create custom action**\.

1. Make a note of the **Custom action ARN** because you need to use the ARN when you create a rule to associate with this action in CloudWatch Events\.

**To define a rule in CloudWatch Events**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Rules**\.

1. Choose **Create rule**\.

1. For **Event source**, confirm that **Event Pattern** is selected\.

1. Choose **Edit** for **Event Pattern Preview**\.

1. Copy the following example pattern, and paste it into the preview window\. Be sure to replace the existing brackets\.

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

1. Replace the ARN listed in the `resources` section with the **Custom Action ARN** for the custom action you created\. This value is displayed on the **Custom actions** page\.

1. Choose **Save** to close the window\.

1. Choose **Add target** and then select the target to invoke when this rule is matched\.

1. Choose **Configure details**\.

1. Enter a name and description for the rule\.

   To enable the rule now, for **State**, choose **Enabled**\. To save the rule without enabling it, clear **Enabled**\.

1. Choose **Create rule**\.

After this rule is created in CloudWatch Events, when you perform a custom action on findings in your account, events are generated in CloudWatch Events\.

The format of the example pattern for associating custom actions with findings generated by insights is:

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

## CloudWatch Events Formats for Security Hub<a name="securityhub-cwe-configure"></a>

Security Hub aggregates findings from enabled AWS services \(Amazon GuardDuty, Amazon Inspector, and Amazon Macie\) and from supported AWS partner products\.

Security Hub also consolidates findings into insights that identify security areas that require attention or intervention\.

Security Hub also conducts automated and continuous compliance checks using CloudWatch Events best practices and supported industry standards \(such as CIS Foundations Benchmarks\)\.

The CloudWatch event for Security Hub findings is in the following format\.

```
{
   "version":"0",
   "id":"CWE-event-id",
   "detail-type":"Security Hub Findings - Imported",
   "source":"aws.securityhub",
   "account":"111122223333",
   "time":"2019-04-11T21:52:17Z",
   "region":"us-west-2",
   "resources":[
      "arn:aws:securityhub:us-west-2::product/aws/macie/arn:aws:macie:us-west-2:111122223333:integtest/trigger/6294d71b927c41cbab915159a8f326a3/alert/f2893b211841"
   ],
   "detail":{
      "findings”: [AMAZON_FINDING_JSON]
   }
}
```

The CloudWatch event for Security Hub aggregated findings with a custom action is in the following format\.

```
{
  "version": "0",
  "id": "1a1111a1-b22b-3c33-444d-5555e5ee5555",
  "detail-type": "Security Hub Findings - Custom Action",
  "source": "aws.securityhub",
  "account": "111122223333",
  "time": "2019-04-11T18:43:48Z",
  "region": "us-west-1",
  "resources": [
    "arn:aws:securityhub:us-west-1:111122223333:action/custom/custom-action-name"
  ],
  "detail": {
    "actionName":"custom-action-name",
    "actionDescription": "description of the action",
    "findings": [AMAZON_FINDING_JSON for each specified finding]
  }
}
```

For a complete list of parameters included in `AMAZON_FINDING_JSON`, see [AWS Security Finding Format](securityhub-findings-format.md)\.

The CloudWatch Events event for Security Hub insights results has the following format\.

```
{ 
  "version": "0",
  "id": "1a1111a1-b22b-3c33-444d-5555e5ee5555",
  "detail-type": "Security Hub Insight Results",
  "source": "aws.securityhub",
  "account": "111122223333",
  "time": "2017-12-22T18:43:48Z",
  "region": "us-west-1",
  "resources": [
      "arn:aws:securityhub:us-west-1:111122223333::product/aws/macie:us-west-1:222233334444:test/trigger/1ec9cf700ef6be062b19584e0b7d84ec/alert/f2893b211841"
  ],
  "detail": {
    "actionName":"name of the action",
    "actionDescription":"description of the action",
    "insightArn":"ARN of the insight",
    "insightName":"Name of the insight",
    "resultType":"ResourceAwsIamAccessKeyUserName",
    "number of results":"number of results, max of 100",
    "insightResults": [
        {"result 1": 5},
        {"result 2": 6}
    ]
  }
}
```

## Use Custom Actions to Send Security Hub Findings to CloudWatch Events<a name="securityhub-cwe-send"></a>

After you've created one or more Security Hub custom actions and CloudWatch Events rules, you can send findings and insight results to CloudWatch Events for further management and processing\.

Events are sent to CloudWatch Events only in the account in which they are viewed\. If you are viewing a finding using a master account, the event is sent to CloudWatch Events in the master account\.

For AWS API calls to be effective, the implementations of target code must switch roles into member accounts\. This also means that the role you must switch into must be deployed to each member where action is needed\.

**To send findings to CloudWatch Events**

1. On the Security Hub console, choose **Findings**\.

1. On the **Findings** page, select one or more findings to send to CloudWatch Events\. You can select up to 20 findings at a time\.

1. From the **Actions** drop down, choose the custom action that aligns with the CloudWatch Events rule to apply\.

   If successful, the message **Successfully sent findings to Amazon CloudWatch Events** is displayed\.

**To send insight results to CloudWatch Events**

1. On the Security Hub console, choose **Insights**\.

1. On the **Insights** page , choose the insight that includes the findings results to send to CloudWatch Events\.

1. Select the findings from the insight to send to CloudWatch Events\. You can select up to 20 findings at a time\.

1. For **Actions**, choose the custom action that aligns with the CloudWatch Events rule to apply\.

   If successful, the message **Successfully sent findings to Amazon CloudWatch Events** is displayed\.