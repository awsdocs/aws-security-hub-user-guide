# Configuring a CloudWatch Events rule for automatically sent findings<a name="securityhub-cwe-all-findings"></a>

You can create a rule in CloudWatch Events that defines an action to take when a **Security Hub Findings \- Imported** event is received\. A **Security Hub Findings \- Imported** events are triggered by updates from both [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) and [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

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