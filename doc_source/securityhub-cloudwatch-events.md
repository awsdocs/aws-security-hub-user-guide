# Automated response and remediation<a name="securityhub-cloudwatch-events"></a>

With Amazon CloudWatch Events, you can automate your AWS services and respond automatically to system events such as application availability issues or resource changes\. Events from AWS services are delivered to CloudWatch Events in near\-real time\. You can write simple rules to indicate which events you are interested in and what automated actions to take when an event matches a rule\. The actions that can be automatically triggered include the following:
+ Invoking an AWS Lambda function
+ Invoking the Amazon EC2 run command
+ Relaying the event to Amazon Kinesis Data Streams
+ Activating an AWS Step Functions state machine
+ Notifying an Amazon SNS topic or an Amazon SQS queue
+ Sending a finding to a third\-party ticketing, chat, SIEM, or incident response and management tool

You can configure CloudWatch Events rules to respond automatically to all findings\. You can also create CloudWatch Events rules and Security Hub custom actions to respond to selected findings\.

A set of templates for cross\-account automated response and remediation is also available in AWS Solutions\. The templates leverage CloudWatch event rules and Lambda functions\. You deploy the solution using AWS CloudFormation and AWS Systems Manager\. The solution can create fully automated response and remediation actions\. It can also use Security Hub custom actions to create user\-triggered response and remediation actions\. For details on how to configure and use the solution, see the [AWS Solutions page for the Security Hub Automated Response and Remediation Solution](http://aws.amazon.com/solutions/implementations/aws-security-hub-automated-response-and-remediation/)\.

For more information about using CloudWatch Events, see the [https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html)\.

**Note**  
As a best practice, make sure that the permissions granted to your users to access CloudWatch Events use least\-privilege IAM policies that grant only the required permissions\.  
For more information, see [Authentication and Access Control for Amazon CloudWatch Events](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/auth-and-access-control-cwe.html)\. 

**Topics**
+ [Types of Security Hub integration with CloudWatch Events](securityhub-cwe-integration-types.md)
+ [CloudWatch Events formats for Security Hub](securityhub-cwe-event-formats.md)
+ [Configuring a CloudWatch Events rule for automatically sent findings](securityhub-cwe-all-findings.md)
+ [Using custom actions to send findings and insight results to CloudWatch Events](securityhub-cwe-custom-actions.md)