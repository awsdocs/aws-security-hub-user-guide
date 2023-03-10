# Amazon CloudWatch controls<a name="cloudwatch-controls"></a>

These controls are related to CloudWatch resources\.

## \[CloudWatch\.1\] A log metric filter and alarm should exist for usage of the "root" user<a name="cloudwatch-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/7\.2\.1, CIS AWS Foundations Benchmark v1\.2\.0/1\.1,CIS AWS Foundations Benchmark v1\.2\.0/3\.3, CIS AWS Foundations Benchmark v1\.4\.0/1\.7,CIS AWS Foundations Benchmark v1\.4\.0/4\.3

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

The root user has unrestricted access to all services and resources in an AWS account\. We highly recommend that you avoid using the root user for daily tasks\. Minimizing the use of the root user and adopting the principle of least privilege for access management reduce the risk of accidental changes and unintended disclosure of highly privileged credentials\.

As a best practice, use your root user credentials only when required to [ perform account and service management tasks](https://docs.aws.amazon.com/general/latest/gr/aws_tasks-that-require-root.html)\. Apply IAM policies directly to groups and roles but not users\. For a tutorial on how to set up an administrator for daily use, see [ Creating your first IAM admin user and group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 1\.7 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-1-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {$.userIdentity.type="Root" && $.userIdentity.invokedBy NOT EXISTS && $.eventType !="AwsServiceEvent"}
      ```

   1. Choose **Next**\.

1. Under **Assign Metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric Namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric Name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. In the navigation pane, choose **Alarms** and then **All alarms**\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Choose **Select metric**\.

   1. On the **Select metric** panel, scroll down to **Metrics**\. Choose the **LogMetrics** namespace\. You can also use the search bar to search for it\.

   1. Choose **Metrics with no dimensions**\.

   1. Select the check box for the metric that you created\. Then choose **Select metric**\.

   1. Under **Metric**, leave the default values\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm, such as **CIS\-1\.7\-RootAccountUsage**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.2\] Ensure a log metric filter and alarm exist for unauthorized API calls<a name="cloudwatch-2"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.1

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None \(custom Security Hub rule\)

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm unauthorized API calls\. Monitoring unauthorized API calls helps reveal application errors and might reduce time to detect malicious activity\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.1 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-2-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.errorCode="*UnauthorizedOperation") || ($.errorCode="AccessDenied*")}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, for **Statistic**, choose **Average**\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-3\.1\-UnauthorizedAPICalls**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.3\] Ensure a log metric filter and alarm exist for Management Console sign\-in without MFA<a name="cloudwatch-3"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.2

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None \(custom Security Hub rule\)

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm console logins that aren't protected by MFA\. Monitoring for single\-factor console logins increases visibility into accounts that aren't protected by MFA\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 3\.2 in the [CIS AWS Foundations Benchmark v1\.2](https://d1.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-3-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      { ($.eventName = "ConsoleLogin") && ($.additionalEventData.MFAUsed != "Yes") && ($.userIdentity.type = "IAMUser") && ($.responseElements.ConsoleLogin = "Success") }
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-3\.2\-ConsoleSigninWithoutMFA**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.4\] Ensure a log metric filter and alarm exist for IAM policy changes<a name="cloudwatch-4"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.4, CIS AWS Foundations Benchmark v1\.4\.0/4\.4

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for changes made to IAM policies\. Monitoring these changes helps ensure that authentication and authorization controls remain intact\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.4 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-4-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

Note that the alarm checks for specific API operations by name\. One of these operations is `DeletePolicy`\. The alarm does not check that the call was issued from IAM\. Because of this, the alarm also is triggered when Auto Scaling calls `DeletePolicy`\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=DeleteGroupPolicy) || ($.eventName=DeleteRolePolicy) || ($.eventName=DeleteUserPolicy) || ($.eventName=PutGroupPolicy) || ($.eventName=PutRolePolicy) || ($.eventName=PutUserPolicy) || ($.eventName=CreatePolicy) || ($.eventName=DeletePolicy) || ($.eventName=CreatePolicyVersion) || ($.eventName=DeletePolicyVersion) || ($.eventName=AttachRolePolicy) || ($.eventName=DetachRolePolicy) || ($.eventName=AttachUserPolicy) || ($.eventName=DetachUserPolicy) || ($.eventName=AttachGroupPolicy) || ($.eventName=DetachGroupPolicy)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, for **Statistic**, choose **Average**\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.4\-IAMPolicyChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.5\] Ensure a log metric filter and alarm exist for CloudTrail AWS Configuration changes<a name="cloudwatch-5"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.5, CIS AWS Foundations Benchmark v1\.4\.0/4\.5

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for changes to CloudTrail configuration settings\. Monitoring these changes helps ensure sustained visibility to activities in the account\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.5 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-5-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=CreateTrail) || ($.eventName=UpdateTrail) || ($.eventName=DeleteTrail) || ($.eventName=StartLogging) || ($.eventName=StopLogging)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.5\-CloudTrailChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.6\] Ensure a log metric filter and alarm exist for AWS Management Console authentication failures<a name="cloudwatch-6"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.6, CIS AWS Foundations Benchmark v1\.4\.0/4\.6

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for failed console authentication attempts\. Monitoring failed console logins might decrease lead time to detect an attempt to brute\-force a credential, which might provide an indicator, such as source IP, that you can use in other event correlations\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.6 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-6-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=ConsoleLogin) && ($.errorMessage="Failed authentication")}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.6\-ConsoleAuthenticationFailure**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.7\] Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer managed keys<a name="cloudwatch-7"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.7, CIS AWS Foundations Benchmark v1\.4\.0/4\.7

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for customer managed keys that have changed state to disabled or scheduled deletion\. Data encrypted with disabled or deleted keys is no longer accessible\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.7 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\. The control also fails if `ExcludeManagementEventSources` contains `kms.amazonaws.com`\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-7-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventSource=kms.amazonaws.com) && (($.eventName=DisableKey) || ($.eventName=ScheduleKeyDeletion))}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.7\-DisableOrDeleteCMK**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.8\] Ensure a log metric filter and alarm exist for S3 bucket policy changes<a name="cloudwatch-8"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.8, CIS AWS Foundations Benchmark v1\.4\.0/4\.8

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for changes to S3 bucket policies\. Monitoring these changes might reduce time to detect and correct permissive policies on sensitive S3 buckets\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.8 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-8-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventSource=s3.amazonaws.com) && (($.eventName=PutBucketAcl) || ($.eventName=PutBucketPolicy) || ($.eventName=PutBucketCors) || ($.eventName=PutBucketLifecycle) || ($.eventName=PutBucketReplication) || ($.eventName=DeleteBucketPolicy) || ($.eventName=DeleteBucketCors) || ($.eventName=DeleteBucketLifecycle) || ($.eventName=DeleteBucketReplication))}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, for **Statistic**, choose **Average**\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.8\-S3BucketPolicyChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.9\] Ensure a log metric filter and alarm exist for AWS Config configuration changes<a name="cloudwatch-9"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.9, CIS AWS Foundations Benchmark v1\.4\.0/4\.9

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for changes to AWS Config configuration settings\. Monitoring these changes helps ensure sustained visibility of configuration items in the account\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.9 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-9-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventSource=config.amazonaws.com) && (($.eventName=StopConfigurationRecorder) || ($.eventName=DeleteDeliveryChannel) || ($.eventName=PutDeliveryChannel) || ($.eventName=PutConfigurationRecorder))}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.9\-AWSConfigChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.10\] Ensure a log metric filter and alarm exist for security group changes<a name="cloudwatch-10"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.10, CIS AWS Foundations Benchmark v1\.4\.0/4\.10

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Security groups are a stateful packet filter that controls ingress and egress traffic in a VPC\.

CIS recommends that you create a metric filter and alarm for changes to security groups\. Monitoring these changes helps ensure that resources and services aren't unintentionally exposed\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.10 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-10-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=AuthorizeSecurityGroupIngress) || ($.eventName=AuthorizeSecurityGroupEgress) || ($.eventName=RevokeSecurityGroupIngress) || ($.eventName=RevokeSecurityGroupEgress) || ($.eventName=CreateSecurityGroup) || ($.eventName=DeleteSecurityGroup)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.10\-SecurityGroupChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.11\] Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)<a name="cloudwatch-11"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.11, CIS AWS Foundations Benchmark v1\.4\.0/4\.11

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. NACLs are used as a stateless packet filter to control ingress and egress traffic for subnets in a VPC\.

CIS recommends that you create a metric filter and alarm for changes to NACLs\. Monitoring these changes helps ensure that AWS resources and services aren't unintentionally exposed\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.11 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-11-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=CreateNetworkAcl) || ($.eventName=CreateNetworkAclEntry) || ($.eventName=DeleteNetworkAcl) || ($.eventName=DeleteNetworkAclEntry) || ($.eventName=ReplaceNetworkAclEntry) || ($.eventName=ReplaceNetworkAclAssociation)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.11\-NetworkACLChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.12\] Ensure a log metric filter and alarm exist for changes to network gateways<a name="cloudwatch-12"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.12, CIS AWS Foundations Benchmark v1\.4\.0/4\.12

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Network gateways are required to send and receive traffic to a destination outside a VPC\.

CIS recommends that you create a metric filter and alarm for changes to network gateways\. Monitoring these changes helps ensure that all ingress and egress traffic traverses the VPC border via a controlled path\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.12 in the [CIS AWS Foundations Benchmark v1\.2](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-12-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=CreateCustomerGateway) || ($.eventName=DeleteCustomerGateway) || ($.eventName=AttachInternetGateway) || ($.eventName=CreateInternetGateway) || ($.eventName=DeleteInternetGateway) || ($.eventName=DetachInternetGateway)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.12\-NetworkGatewayChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.13\] Ensure a log metric filter and alarm exist for route table changes<a name="cloudwatch-13"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.13, CIS AWS Foundations Benchmark v1\.4\.0/4\.13

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Routing tables route network traffic between subnets and to network gateways\.

CIS recommends that you create a metric filter and alarm for changes to route tables\. Monitoring these changes helps ensure that all VPC traffic flows through an expected path\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.13 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-13-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=CreateRoute) || ($.eventName=CreateRouteTable) || ($.eventName=ReplaceRoute) || ($.eventName=ReplaceRouteTableAssociation) || ($.eventName=DeleteRouteTable) || ($.eventName=DeleteRoute) || ($.eventName=DisassociateRouteTable)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, for **Statistic**, choose **Average**\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.13\-RouteTableChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.14\] Ensure a log metric filter and alarm exist for VPC changes<a name="cloudwatch-14"></a>

**Related requirements:** CIS AWS Foundations Benchmark v1\.2\.0/3\.14, CIS AWS Foundations Benchmark v1\.4\.0/4\.14

**Category:** Detect > Detection services

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. You can have more than one VPC in an account, and you can create a peer connection between two VPCs, enabling network traffic to route between VPCs\.

CIS recommends that you create a metric filter and alarm for changes to VPCs\. Monitoring these changes helps ensure that authentication and authorization controls remain intact\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.14 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cloudwatch-14-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [\[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events](cloudtrail-controls.md#cloudtrail-1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=CreateVpc) || ($.eventName=DeleteVpc) || ($.eventName=ModifyVpcAttribute) || ($.eventName=AcceptVpcPeeringConnection) || ($.eventName=CreateVpcPeeringConnection) || ($.eventName=DeleteVpcPeeringConnection) || ($.eventName=RejectVpcPeeringConnection) || ($.eventName=AttachClassicLinkVpc) || ($.eventName=DetachClassicLinkVpc) || ($.eventName=DisableVpcClassicLink) || ($.eventName=EnableVpcClassicLink)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, for **Statistic**, choose **Average**\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.14\-VPCChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## \[CloudWatch\.15\] CloudWatch alarms should have an action configured for the ALARM state<a name="cloudwatch-15"></a>

**Category:** Detect > Detection services

**Related requirements:** NIST\.800\-53\.r5 AU\-6\(1\), NIST\.800\-53\.r5 AU\-6\(5\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 IR\-4\(1\), NIST\.800\-53\.r5 IR\-4\(5\), NIST\.800\-53\.r5 SI\-2, NIST\.800\-53\.r5 SI\-20, NIST\.800\-53\.r5 SI\-4\(12\), NIST\.800\-53\.r5 SI\-4\(5\)

**Severity:** High

**Resource type:** `AWS::CloudWatch::Alarm`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudwatch-alarm-action-check.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudwatch-alarm-action-check.html) ``

**Schedule type:** Change triggered

**Parameters:**
+ `alarmActionRequired: true`
+ `insufficientDataActionRequired: false`
+ `okActionRequired: false`

This control checks if CloudWatch alarms have at least one action configured for the ALARM state\. The control fails if the alarm doesn't have an action activated for the ALARM state\.

Whereas this control focuses on whether any `ALARM` action is configured in a CloudWatch alarm, [CloudWatch\.17](#cloudwatch-17) focuses on the activation status of a CloudWatch alarm action\.

Security Hub recommends activating alarm actions to automatically alert you when a monitored metric is outside the defined threshold\. Monitoring alarms help you identify unusual activities and quickly respond to security and operational issues\. You can specify what actions an alarm should take when it goes into OK, ALARM, and INSUFFICIENT\_DATA states\. The most common type of alarm action is to notify one or more users by sending a message to an Amazon Simple Notification Service \(Amazon SNS\) topic\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="cloudwatch-15-remediation"></a>

For information about actions supported by CloudWatch alarms, see [Alarm actions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html#alarms-and-actions) in the *Amazon CloudWatch User Guide*\.

## \[CloudWatch\.16\] CloudWatch log groups should be retained for at least 1 year<a name="cloudwatch-16"></a>

**Category:** Identify > Logging

**Related requirements:** NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-11, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SI\-12

**Severity:** Medium

**Resource type:** `AWS::Logs::LogGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cw-loggroup-retention-period-check.html](https://docs.aws.amazon.com/config/latest/developerguide/cw-loggroup-retention-period-check.html) ``

**Schedule type:** Periodic

**Parameters:** None

This controls evaluates if a CloudWatch log group has a retention period of at least 1 year\. The control fails if the retention period is less than 1 year\.

CloudWatch Logs centralize logs from all of your systems, applications, and AWS services in a single, highly scalable service\. You can use Amazon CloudWatch Logs to monitor, store, and access your log files from Amazon EC2 instances, CloudTrail, Route 53, and other sources\. Retaining your logs for at least 1 year can help you comply with log retention standards\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="cloudwatch-16-remediation"></a>

To configure log retention settings, see [Change log data retention in Amazon CloudWatch Logs](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html#SettingLogRetention) in the *Amazon CloudWatch User Guide*\.

## \[CloudWatch\.17\] CloudWatch alarm actions should be activated<a name="cloudwatch-17"></a>

**Category:** Detect > Detection services

**Related requirements:** NIST\.800\-53\.r5 AU\-6\(1\), NIST\.800\-53\.r5 AU\-6\(5\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SI\-2, NIST\.800\-53\.r5 SI\-4\(12\)

**Severity:** High

**Resource type:** `AWS::CloudWatch::Alarm`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudwatch-alarm-action-enabled-check.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudwatch-alarm-action-enabled-check.html) ``

**Schedule type:** Change triggered

**Parameters:** None

This control checks if CloudWatch alarm actions are activated \(`ActionEnabled` should be set to true\)\. The control fails if the alarm action for a CloudWatch alarm is deactivated\.

Whereas this control focuses on the activation status of a CloudWatch alarm action, [CloudWatch\.15](#cloudwatch-15) focuses on whether any `ALARM` action is configured in a CloudWatch alarm\.

Alarm actions automatically alert you when a monitored metric is outside the defined threshold\. If the alarm action is deactivated, no actions are executed when the alarm changes state, so you won't be alerted to changes in monitored metrics\. Security Hub recommends activating CloudWatch alarms actions to help you quickly respond to security and operational issues\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="cloudwatch-17-remediation"></a>

**To activate a CloudWatch alarm action \(console\)**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, under **Alarms**, choose **All alarms**\.

1. Select the alarm that you want to activate actions for\.

1. For **Actions**, choose **Alarm actions–new**, and then choose **Enable**\.

For more information about activating CloudWatch alarm actions, see [Alarm actions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html#alarms-and-actions) in the *Amazon CloudWatch User Guide*\.