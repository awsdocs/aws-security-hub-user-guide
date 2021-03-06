# Configuring an EventBridge rule for automatically sent findings<a name="securityhub-cwe-all-findings"></a>

You can create a rule in EventBridge that defines an action to take when a **Security Hub Findings \- Imported** event is received\. **Security Hub Findings \- Imported** events are triggered by updates from both [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) and [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

Each rule contains an event pattern, which identifies the events that trigger the rule\. The event pattern always contains the event source \(`aws.securityhub`\) and the event type \(**Security Hub Findings \- Imported**\)\. The event pattern can also specify filters to identify the findings that the rule applies to\.

The rule then identifies the rule targets\. The targets are the actions to take when EventBridge receives a **Security Hub Findings \- Imported** event and the finding matches the filters\.

The instructions provided here use the EventBridge console\. When you use the console, EventBridge automatically creates the required resource\-based policy that enables EventBridge to write to CloudWatch Logs\.

You can also use the [https://docs.aws.amazon.com/eventbridge/latest/APIReference/API_PutRule.html](https://docs.aws.amazon.com/eventbridge/latest/APIReference/API_PutRule.html) API operation of the EventBridge API\. However, if you use the EventBridge API, then you must create the resource\-based policy\. For details on the required policy, see [CloudWatch Logs permissions](https://docs.aws.amazon.com/eventbridge/latest/userguide/resource-based-policies-eventbridge.html#cloudwatchlogs-permissions) in the *Amazon EventBridge User Guide*\.

## Format of the event pattern<a name="securityhub-cwe-all-findings-rule-format"></a>

The format of the event pattern for **Security Hub Findings \- Imported **events is as follows:

```
{
  "source": [
    "aws.securityhub"
  ],
  "detail-type": [
    "Security Hub Findings - Imported"
  ],
  "detail": {
    "findings": {
      <attribute filter values>
    }
  }
}
```
+ `source` identifies Security Hub as the service that generates the event\.
+ `detail-type` identifies the type of event\.
+ `detail` is optional and provides the filter values for the event pattern\. If the event pattern does not contain a `detail` field, then all findings trigger the rule\.

You can filter the findings based on any finding attribute\. For each attribute, you provide a comma\-separated array of one or more values\.

```
"<attribute name>": [ "<value1>", "<value2>"]
```

If you provide more than one value for an attribute, then those values are joined by `OR`\. A finding matches the filter for an individual attribute if the finding has any of the listed values\. For example, if you provide both `INFORMATIONAL` and `LOW` as values for `Severity.Label`, then the finding matches if it has a severity label of either `INFORMATIONAL` or `LOW`\.

The attributes are joined by `AND`\. A finding matches if it matches the filter criteria for all of the provided attributes\.

When you provide an attribute value, it must reflect the location of that attribute within the AWS Security Finding Format \(ASFF\) structure\.

For example, the following event pattern provides filter values for `ProductArn` and `Severity.Label`\.

```
{
    "source": [
        "aws.securityhub"
     ],
    "detail-type": [
        "Security Hub Findings - Imported"
    ],
    "detail": {
        "findings": {
            "ProductArn": ["arn:aws:securityhub:us-east-1::product/aws/inspector"],
            "Severity": {
                "Label": ["INFORMATIONAL", "LOW"]
            }
        }
    }
}
```

In this example, a finding matches if it was generated by Amazon Inspector and it has a severity label of either `INFORMATIONAL` or `LOW`\.

## Using the predefined pattern to create the rule<a name="securityhub-cwe-all-findings-predefined-pattern"></a>

EventBridge includes a predefined pattern that you can use to create the rule\. When you select the predefined pattern, EventBridge automatically fills in `source` and `detail-type`\. EventBridge also provides fields to specify filter values for the following finding attributes:
+ `AwsAccountId`
+ `Compliance.Status`
+ `Criticality`
+ `ProductArn`
+ `RecordState`
+ `Resource.Id`
+ `Resource.Type`
+ `Severity.Label`
+ `Types`
+ `Workflow.Status`

**To use the predefined pattern to create the EventBridge rule**

1. Open the Amazon EventBridge console at [https://console\.aws\.amazon\.com/events/](https://console.aws.amazon.com/events/)\.

1. In the navigation pane, under **Events**, choose **Rules**\.

1. Choose **Create rule**\.

1. Enter a name and description for the rule\.

1. For **Event source**, choose **Event Pattern**\.

1. For **Event matching pattern**, choose **Pre\-defined pattern by service**\.

1. For **Service provider**, choose **AWS**\.

1. For **Service name**, choose **Security Hub**\.

1. For **Event type**, choose **Security Hub Findings \- Imported**\.

   EventBridge populates the event pattern with the `source` and `detail-type` values and displays fields for the filter values\.

1. By default, the event pattern is configured without any filter values\. For each attribute, the **Any *attribute name*** option is selected\. For example, **Any finding type**\.

   For some attributes, such as product ARN or criticality, you enter each value manually\. For other attributes, such as the severity label, you select values from a list of valid values\.

   As you add and remove filter values, EventBridge updates the event pattern to reflect the changes\.

   For values that are added manually, perform the following steps:

   1. Choose **Specific *attribute***\. For example, **Specific Resource type\(s\)**\.

   1. To add a value, enter the value in the field, then choose **Add**\.

   1. To remove a value, choose **Remove** for that value\.

   For values that are added from a list, perform the following steps:

   1. Choose **Specific *attribute***\. For example, **Specific Workflow status\(es\)**\.

   1. From the list, choose the attribute value\.

      The selected value is added below the list\.

   1. To remove a value, choose the remove icon \(**x**\) for that value\.

1. Under **Select targets**, choose and configure the target to invoke when this rule is matched\.

1. Choose **Create**\.

## Using a custom pattern to create the rule<a name="securityhub-cwe-all-findings-custom-pattern"></a>

You can also create the rule using the custom pattern option\. For a custom pattern, you enter the entire pattern manually\.

You can use this option if you want to filter the findings based on attributes that do not have associated fields on the EventBridge console\.

**To create an EventBridge rule for a Security Hub finding**

1. Open the Amazon EventBridge console at [https://console\.aws\.amazon\.com/events/](https://console.aws.amazon.com/events/)\.

1. In the navigation pane, under **Events**, choose **Rules**\.

1. Choose **Create rule**\.

1. Enter a name and description for the rule\.

1. For **Event source**, choose **Event Pattern**\.

1. Choose **Custom pattern**\.

1. Copy the following example pattern and paste it into the **Event pattern** text area\. Be sure to replace the existing brackets\.

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

   This is the minimum required information for the event pattern\. It identifies the source and the event type\. With this pattern, all findings match the rule\.

   If you want to filter findings that trigger this rule, then you also add a `detail` entry\. The `detail` entry contains the attribute values to use to filter the findings\.

   ```
   {
     "source": [
       "aws.securityhub"
     ],
     "detail-type": [
       "Security Hub Findings - Imported"
     ],
     "detail": {
       "findings": {
         <attribute filter values>
       }
     }
   }
   ```

   For each attribute that you provide, the format is as follows\.

   ```
   "<attribute name>": [ "<value>" ]
   ```

   To match multiple values, provide a comma\-separated list\.

   ```
   "<attribute name>": [ "<value1>", "<value2>"]
   ```

   For example, to only apply the rule to findings that have a verification state of `TRUE_POSITIVE`, add the following filter\.

   ```
   "detail": {
       "findings": {
           "VerificationState": [
               "TRUE_POSITIVE"
           ]
       }
   }
   ```

1. Choose **Save** to save the pattern\.

1. Under **Select targets**, choose and configure the target to invoke when this rule is matched\.

1. Choose **Create**\.