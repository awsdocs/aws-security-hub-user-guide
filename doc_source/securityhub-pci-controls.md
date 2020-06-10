# PCI DSS controls<a name="securityhub-pci-controls"></a>

The PCI DSS security standard in Security Hub supports the following controls\. For each control, the information includes the severity, the resource type, the AWS Config rule, and the remediation steps\.

## \[PCI\.AutoScaling\.1\] Auto scaling groups associated with a load balancer should use health checks<a name="pcidss-autoscaling-1"></a>

**Severity:** Low

**Resource:** Auto scaling group

**AWS Config** rule: [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-group-elb-healthcheck-required.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-group-elb-healthcheck-required.html)

This control checks whether your Auto Scaling groups that are associated with a load balancer are using Elastic Load Balancing health checks\.

PCI DSS does not require load balancing or highly available configurations\. However, this check aligns with AWS best practices\.

### Related PCI DSS requirements<a name="pcidss-autoscaling-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 2\.2: Develop configuration standards for all system components\. Assure that these standards address all known security vulnerabilities and are consistent with industry\-accepted system hardening standards\.**  
Replicating systems using load balancing provides high availability and is a means to mitigate the effects of a DDoS event\.  
This is one method used to implement system hardening configurations\.

### Remediation<a name="pcidss-autoscaling-1-remediation"></a>

**To enable Elastic Load Balancing health checks**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the navigation pane, under **Auto Scaling**, choose **Auto Scaling Groups**\.

1. To select the group from the list, choose the right box

1. From **Actions**, choose **Edit**

1. For **Health Check Type**, choose **ELB**\.

1. For **Health Check Grace Period**, enter **300**\.

1. Choose **Save**\.

For more information on using a load balancer with an auto scaling group, see the [https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html](https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html)\.

## \[PCI\.CloudTrail\.1\] CloudTrail logs should be encrypted at rest using AWS KMS CMKs<a name="pcidss-cloudtrail-1"></a>

**Severity:** Medium

**Resource:** CloudTrail trail

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html)

This control checks whether AWS CloudTrail is configured to use the server\-side encryption \(SSE\) AWS KMS customer master key \(CMK\) encryption\.

If you are only using the default encryption option, you can choose to disable this check\.

### Related PCI DSS requirements<a name="pcidss-cloudtrail-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 3\.4: Render Primary Account Numbers \(PAN\) unreadable anywhere it is stored \(including on portable digital media, backup media, and in logs\)\.**  
If you are using AWS services to process and store PAN, your CloudTrail logs should be encrypted at rest to ensure that if logs capture PAN\(s\), the PAN\(s\) are protected\.  
By default, the log files delivered by CloudTrail to your S3 bucket are encrypted using Amazon server\-side encryption with Amazon S3\-managed encryption keys \(SSE\-S3\)\. See the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)\.  
You can configure CloudTrail logs to leverage AWS KMS customer\-created master keys \(CMKs\) to further protect CloudTrail logs\.  
These are methods used to render PAN unreadable\.

### Remediation<a name="pcidss-cloudtrail-1-remediation"></a>

**To enable encryption for CloudTrail logs**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the trail to update\.

1. Under **Storage** location, to edit the settings, choose the pencil icon\.

1. For **Encrypt log files with SSE\-KMS**, choose **Yes**\.

1. For **Create a new KMS key**, do one of the following: 
   + To create a key, choose **Yes** and then in **KMS key**, enter an alias for the key\. The key is created in the same Region as the S3 bucket\.
   + To use an existing key, choose **No** and then from **KMS key**, select the key\. 

     The AWS KMS key and S3 bucket must be in the same Region\.

1. Choose **Save**\.

You might need to modify the policy for CloudTrail to successfully interact with your CMK\. For more information on encrypting CloudTrail log files with AWS KMS managed keys \(SSE\-KMS\), see the [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html?icmpid=docs_cloudtrail_console](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html?icmpid=docs_cloudtrail_console)\.

## \[PCI\.CloudTrail\.2\] CloudTrail should be enabled<a name="pcidss-cloudtrail-2"></a>

**Severity:** High

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudtrail-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudtrail-enabled.html)

This control checks whether CloudTrail is enabled in your AWS account\.

However, some AWS services do not enable logging of all APIs and events\. You should implement any additional audit trails other than CloudTrail and review the documentation for each service in [CloudTrail Supported Services and Integrations](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-aws-service-specific-topics.html)\.

### Related PCI DSS requirements<a name="pcidss-cloudtrail-2-requirements"></a>

This control is associated with the following PCI DSS requirements:

PCI DSS 10\.1: Implement audit trails to link all access to system components to each individual user\.  
By enabling CloudTrail, Event History provides you with 90 days of readily available events and audit trails for access to system components by each individual user\.  
You can find the identity of the users in the `eventSource` section of the CloudTrail log\.

**PCI DSS 10\.2\.1: Implement automated audit trails for all system components to reconstruct the following events: All individual user accesses to cardholder data**  
Depending on where cardholder data is stored, individual user accesses to cardholder data could be found in the `userIdentity`, `eventSource`, `eventName`, or `responseElements` sections of the CloudTrail log\.

**PCI DSS 10\.2\.2: Implement automated audit trails for all system components to reconstruct the following events: All actions taken by any individual with root or administrative privileges**  
Root user identification is found in the `userIdentity` section of the log\.

**PCI DSS 10\.2\.3: Implement automated audit trails for all system components to reconstruct the following events: Access to all audit trails**  
Access to audit trails might be found in the `eventSource`, `eventName`, or `responseElements` sections of the log\.

**PCI DSS 10\.2\.4: Implement automated audit trails for all system components to reconstruct the following events: Invalid logical access attempts**  
You can find invalid logical access attempts in CloudTrail logs\. For example: `responseElements : "ConsoleLogin"` and `responseElements : "Failure"`\.

**PCI DSS 10\.2\.5: Implement automated audit trails for all system components to reconstruct the following events: Use of and changes to identification and authentication mechanisms—including but not limited to creation of new accounts and elevation of privileges—and all changes, additions, or deletions to accounts with root or administrative privileges**  
Use of and changes to identification and authentication mechanisms might be found in the `userAgent`, `eventName`, or `responseElements` sections of the log\.

**PCI DSS 10\.2\.6: Implement automated audit trails for all system components to reconstruct the following events: Initialization, stopping, or pausing of the audit logs**  
Starting and stopping logging is captured in the CloudTrail logs\.  
An example of audit log starting and stopping would look as follows within a CloudTrail Log: `eventName : "StopLogging"` and `eventName : "StartLogging"`

**PCI DSS 10\.2\.7: Implement automated audit trails for all system components to reconstruct the following events: Creation and deletion of system\- level objects**  
Creation and deletion of system level\-objects are captured in the CloudTrail logs\. An example of a system\-level object would be an AWS Lambda function\.  
CloudTrail captures the `createFunction` and `deleteFunction` API calls, as described in the [https://docs.aws.amazon.com/lambda/latest/dg/logging-using-cloudtrail.html](https://docs.aws.amazon.com/lambda/latest/dg/logging-using-cloudtrail.html)\.

**PCI DSS 10\.3\.1: Record at least the following audit trail entries for all system components for each event: User identification**  
You can find user identification in the `userIdentity` section of the CloudTrail logs\.

**PCI DSS 10\.3\.2: Record at least the following audit trail entries for all system components for each event: Type of event**  
You can find the type of event in the `eventName` section of the CloudTrail log\.

**PCI DSS 10\.3\.3: Record at least the following audit trail entries for all system components for each event: Date and time**  
You can find the date and time of an event in the `eventTime` section of the CloudTrail log\.

**PCI DSS 10\.3\.4: Record at least the following audit trail entries for all system components for each event: Success or failure indication**  
You can find the success or failure indication in the `responseElements` section of the CloudTrail log\.

**PCI DSS 10\.3\.5: Record at least the following audit trail entries for all system components for each event: Origination of event**  
You can find the origination of an event in the `userAgent` or `sourceIPAddress` section of the CloudTrail log\.

**PCI DSS 10\.3\.6: Record at least the following audit trail entries for all system components for each event: Identity or name of affected data, system component, or resource\.**  
You can find the identity of the resource in the `eventSource` section of the CloudTrail log\.

### Remediation<a name="pcidss-cloudtrail-2-remediation"></a>

**To create a new trail in CloudTrail**

1. Sign in to the AWS Management Console using the IAM user you configured for CloudTrail administration\.

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. In the **Region** selector, choose the AWS Region where you want your trail to be created\. This is the Home Region for the trail\. 

   The Home Region is the only AWS Region where you can view and update the trail after it is created, even if the trail logs events in all AWS Regions\. 

1. In the navigation pane, choose **Trails**\.

1. On the **Trails** page, choose **Get Started Now**\. If you do not see that option, choose **Create Trail**\. 

1. In **Trail name**, give your trail a name, such as **My\-Management\-Events\-Trail**\.

   As a best practice, use a name that quickly identifies the purpose of the trail\. In this case, you're creating a trail that logs management events\.

1. For **Apply trail to all regions**, keep the default **Yes**\.

1. In **Management Events**, make sure **Read/Write events** is set to **All**\.

1. In **Data Events**, do not make any changes\. This trail will not log any data events\. 

1. Create a new S3 bucket for the logs:

   1. In **Storage Location**, in **Create a new S3 bucket**, choose **Yes**\.

   1. In **S3 bucket**, give your bucket a name, such as **my\-bucket\-for\-storing\-cloudtrail\-logs**\.

      The name of your S3 bucket must be globally unique\. For more information about S3 bucket naming requirements, see the [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-s3-bucket-naming-requirements.html](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-s3-bucket-naming-requirements.html)\.

   1. Under **Advanced**, choose **Yes** for both **Encrypt log files with SSE\-KMS** and **Enable log file validation**\.

1. Choose **Create**\. 

For more details, see the tutorial in the [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-tutorial.html](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-tutorial.html)\.

## \[PCI\.CloudTrail\.3\] CloudTrail log file validation should be enabled<a name="pcidss-cloudtrail-3"></a>

**Severity:** Low

**Resource:** CloudTrail trail

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html)

This control checks whether CloudTrail log file validation is enabled\.

It does not check when configurations are altered\.

To monitor and alert on log file changes, you can use CloudWatch Events or CloudWatch Metric Filters\.

### Related PCI DSS requirements<a name="pcidss-cloudtrail-3-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 10\.5\.2: Protect audit trail files from unauthorized modifications\.**  
CloudTrail log file validation creates a digitally signed digest file containing a hash of each log that CloudTrail writes to Amazon S3\.  
You can use these digest files to determine whether a log file was changed, deleted, or unchanged after CloudTrail delivered the log\.  
This is a method that helps to protect audit trail files from unauthorized modifications\.

**PCI DSS 10\.5\.5: Use file\-integrity monitoring or change\-detection software on logs to ensure that existing log data cannot be changed without generating alerts**  
CloudTrail log file validation creates a digitally signed digest file containing a hash of each log that CloudTrail writes to Amazon S3\.  
You can use these digest files to determine whether a log file was changed, deleted, or unchanged after CloudTrail delivered the log\.  
This is a method that helps to ensure file\-integrity monitoring or change\-detection software is used on logs\.

### Remediation<a name="pcidss-cloudtrail-3-remediation"></a>

**To enable CloudTrail log file validation**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. In the **Name** column, choose the name of a trail to edit\.

1. Choose the pencil icon for the **Storage location**\.

1. For **Enable log file validation**, choose **Yes**\.

1. Choose **Save**\. 

## \[PCI\.CloudTrail\.4\] CloudTrail trails should be integrated with CloudWatch Logs<a name="pcidss-cloudtrail-4"></a>

**Severity: ** Low

**Resource:** CloudTrail trail

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-cloud-watch-logs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-cloud-watch-logs-enabled.html)

This control checks whether CloudTrail trails are configured to send logs to CloudWatch Logs\.

It does not check for user permissions to alter logs or log groups\. You should create specific CloudWatch rules to alert when CloudTrail logs are altered\.

This control also does not check for any additional audit log sources other than CloudTrail being sent to a CloudWatch Logs group\.

### Related PCI DSS requirements<a name="pcidss-cloudtrail-4-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 10\.5\.3: Promptly back up audit trail files to a centralized log server or media that is difficult to alter\.**  
CloudTrail uses Amazon S3 for log file storage and delivery, so log files are stored permanently\.  
CloudWatch Logs is a native way to promptly back up audit trail files\.

### Remediation<a name="pcidss-cloudtrail-4-remediation"></a>

**To ensure that CloudTrail trails are integrated with CloudWatch Logs**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose a trail that there is no value for in the **CloudWatch Logs Log group** column\. 

1. Scroll down to the **CloudWatch Logs** section and then choose **Configure**\. 

1. For **New or existing log group**, do one of the following:
   + To use the default log group, keep the name as is\.
   + To use an existing log group, enter the name of the log group to use\.
   + To create a new log group, enter a name for the log group to create\.

1. Choose **Continue**\.

1. You can either use the default IAM role, or specify a role\.

   To use the default IAM role, go to the next step\.

   To specify the role to use:

   1. Choose **View Details**\.

   1. For **IAM role**, do one of the following: 
      + Choose the **CloudTrail\_CloudWatchLogs\_role** and then from **Policy Name**, choose the policy to use\.
      + Choose **Create a new IAM Role** and then enter the name of the role to create\.

        The new role is assigned a policy that grants the necessary permissions\.

1. Choose **Allow**\. 

For more information about configuring CloudWatch Logs monitoring with the console, see the [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/send-cloudtrail-events-to-cloudwatch-logs.html#send-cloudtrail-events-to-cloudwatch-logs-console](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/send-cloudtrail-events-to-cloudwatch-logs.html#send-cloudtrail-events-to-cloudwatch-logs-console)\.

## \[PCI\.CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth<a name="pcidss-codebuild-1"></a>

**Severity:** Critical

**Resource:** CodeBuild project

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-source-repo-url-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-source-repo-url-check.html)

This control checks whether the GitHub or Bitbucket source repository URL contains either personal access tokens or a user name and password\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
 AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Related PCI DSS requirements<a name="pcidss-codebuild-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 8\.2\.1: Using strong cryptography, render all authentication credentials \(such as passwords/phrases\) unreadable during transmission and storage on all system components\.**  
If you are using CodeBuild in your PCI DSS environment to compile your source code, run unit tests, or produce artifacts that are ready to deploy, authentication credentials should never be stored or transmitted in clear text or appear in the repository URL\.  
You should use OAuth instead of personal access tokens or a user name and password to grant authorization for accessing GitHub or Bitbucket repositories\. This is a method to use strong cryptography to render authentication credentials unreadable\.

### Remediation<a name="pcidss-codebuild-1-remediation"></a>

**To remove basic authentication / \(GitHub\) Personal Access Token from CodeBuild Project Source**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Select your Build project that contains personal access tokens or a user name and password

1. From **Edit**, choose **Source**\.

1. Choose **Disconnect from GitHub / Bitbucket**\.

1. Choose **Connect using OAuth** and then choose **Connect to GitHub / Bitbucket**\.

1. In the message displayed by your source provider, authorize as appropriate\.

1. Reconfigure your **Repository URL** and **additional configuration** settings, as needed\.

1. Choose **Update source**\.

To see CodeBuild use case\-based samples, see the [https://docs.aws.amazon.com/codebuild/latest/userguide/use-case-based-samples.html](https://docs.aws.amazon.com/codebuild/latest/userguide/use-case-based-samples.html)\.

## \[PCI\.CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials<a name="pcidss-codebuild-2"></a>

**Severity:** Critical

**Resource:** CodeBuild project

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-envvar-awscred-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-envvar-awscred-check.html)

This control checks whether the project contains environment variables `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Related PCI DSS requirements<a name="pcidss-codebuild-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 8\.2\.1: Using strong cryptography, render all authentication credentials \(such as passwords/phrases\) unreadable during transmission and storage on all system components\.**  
If you are using CodeBuild in your PCI DSS environment to compile your source code, runs unit tests, or produce artifacts that are ready to deploy, then the authentication credentials `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` should never be stored in clear text\.  
Using environmental variables to store credentials in your CodeBuild project may violate the requirement to use strong cryptography to render authentication credentials unreadable\.

### Remediation<a name="pcidss-codebuild-2-remediation"></a>

To reference sensitive data in CodeBuild runtime using Environmental variables, use the following procedures\.

**To remove an Environmental Variable**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Expand **Build**, choose **Build project**, and then choose the build project that contains plaintext credentials\.

1. From **Edit**, choose **Environment**\.

1. Expand **Additional configuration** and then scroll to **Environment variables**\.

1. Choose **Remove** next to the environment variable\.

1. Choose **Update environment**\.

**To store sensitive values in the Amazon EC2 Systems Manager Parameter Store and then retrieve them from your build spec**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Expand **Build**, choose **Build project**, and then choose your build project that contains plaintext credentials\.

1. From **Edit**, choose **Environment**\.

1. Expand **Additional configuration** and then scroll to **Environment variables**\.

1. In AWS Systems Manager, create a systems manager parameter that contains your sensitive data\. For instructions on how to do this, refer to the tutorial in the [https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-paramstore-console.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-paramstore-console.html)\.

1. After you create the parameter, copy the parameter name\.

1. Back in the CodeBuild console, choose **Create environmental variable**\.

1. For **name**, enter the name of your variable as it appears in your build spec\.

1. For **value**, paste in the name of your parameter\.

1. From **type**, choose **Parameter**\.

1. Choose **Remove** next to your non\-compliant environmental variable that contains plaintext credentials\.

1. Choose **Update environment**\.

See the information on environment variables in build environments in the [https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-env-vars.html](https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-env-vars.html)\.

## \[PCI\.Config\.1\] AWS Config should be enabled<a name="pcidss-config-1"></a>

**Severity: ** Medium

**Resource:** Account

**AWS Config rule:** None\. To run this check, Security Hub runs through audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

This control checks whether AWS Config is enabled in the account for the local Region and is recording all resources\.

It does not check for change detection for all critical system files and content files, as AWS Config supports only a subset of resource types\.

The AWS Config service performs configuration management of supported AWS resources in your account and delivers log files to you\. The recorded information includes the configuration item \(AWS resource\), relationships between configuration items, and any configuration changes between resources\. 

Security Hub recommends that you enable AWS Config in all Regions\. The AWS configuration item history that AWS Config captures enables security analysis, resource change tracking, and compliance auditing\. 

**Note**  
Because Security Hub is a Regional service, the check performed for this control checks only the current Region for the account\. It does not check all Regions\.   
To allow security checks against global resources in each Region, you also must record global resources\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

For more information, see the [https://docs.aws.amazon.com/config/latest/developerguide/resource-config-reference.html](https://docs.aws.amazon.com/config/latest/developerguide/resource-config-reference.html)\.

### Related PCI DSS requirements<a name="pcidss-config-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 10\.5\.2: Protect audit trail files from unauthorized modifications\.**  
AWS Config continuously monitors, tracks, and evaluates your [AWS resource configurations ](https://docs.aws.amazon.com/config/latest/developerguide/resource-config-reference.html) for desired settings and generates configuration change history files every six hours\.  
You should enable AWS Config to protect audit trail files from unauthorized modifications\.

**PCI DSS 11\.5: Deploy a change\-detection mechanism to alert personnel to unauthorized modification of critical system files, configuration files, or content files; and configure the software to perform critical file comparisons at least weekly\.**  
AWS Config continuously monitors, tracks, and evaluates your [AWS resource configurations ](https://docs.aws.amazon.com/config/latest/developerguide/resource-config-reference.html) for desired settings and generates configuration change history files every six hours\.  
You should enable AWS Config to ensure a change\-detection mechanism is deployed and is configured to perform critical file comparisons at least weekly\.

### Remediation<a name="pcidss-config-1-remediation"></a>

**To configure AWS Config settings**

1. Open the AWS Config console at [https://console\.aws\.amazon\.com/config/](https://console.aws.amazon.com/config/)\.

1. Choose the Region to configure AWS Config in\.

1. If you have not used AWS Config before, choose **Get started**\. 

1. On the **Settings** page, do the following:

   1.  Under **Resource types to record**, choose **Record all resources supported in this region** and **Include global resources \(e\.g\., AWS IAM resources\)**\. 

   1.  Under **Amazon S3 bucket**, either specify the bucket to use or create a bucket and optionally include a prefix\. 

   1. Under **Amazon SNS topic**, either select an Amazon SNS topic from your account or create one\. For more information about Amazon SNS, see the [https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html)\.

   1. Under **AWS Config role**, either choose **Create AWS Config service\-linked role** or choose **Choose a role from your account** and then choose the role to use\. 

1. Choose **Next**\. 

1. On the **AWS Config rules** page, choose **Skip**\.

1. Choose **Confirm**\.

For more information about using AWS Config from the AWS CLI, see the [https://docs.aws.amazon.com/config/latest/developerguide/gs-cli-subscribe.html](https://docs.aws.amazon.com/config/latest/developerguide/gs-cli-subscribe.html)\.

You can also use an AWS CloudFormation template to automate this process\. For more information, see the [https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html)\.

## \[PCI\.CW\.1\] A log metric filter and alarm should exist for usage of the "root" user<a name="pcidss-cw-1"></a>

**Severity:** Critical

**Resource:** Account

**AWS Config rule:** Security Hub runs through audit steps without creating an AWS Config managed rules in your AWS account for this check\. 

This control checks for the CloudWatch metric filters using the following pattern:

```
{ $.userIdentity.type = "Root" && $.userIdentity.invokedBy NOT EXISTS && $.eventType != "AwsServiceEvent" }
```

It checks the following:
+ The log group name is configured for use with active multi\-region CloudTrail\.
+ There is at least one Event Selector for a Trail with `IncludeManagementEvents` set to `true` and `ReadWriteType` set to `All`\.
+ There is at least one active subscriber to an Amazon SNS topic associated with the alarm\.

### Related PCI DSS requirements<a name="pcidss-cw-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
The root user is the most privileged user in an AWS account and has unrestricted access to all resources in the AWS account\.  
You should set up log metric filters and alarms in the event that root credentials are used\.  
You should also ensure that CloudTrail is enabled to keep an audit trail of actions taken by any individual with root or administrative privileges \(see [\[PCI\.CloudTrail\.2\] CloudTrail should be enabled](#pcidss-cloudtrail-2)\)\. Root user identification would be found in the `userIdentity` section of the CloudTrail log\.

### Remediation<a name="pcidss-cw-1-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a metric filter, and an alarm for the metric filter\.

These are the same steps to remediate findings for [3\.3 – Ensure a log metric filter and alarm exist for usage of "root" account ](securityhub-cis-controls.md#securityhub-cis-controls-3.3)\. 

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\.

   For more information about creating Amazon SNS topics, see the [https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic)\.

1. Set up an active CloudTrail trail that applies to all Regions\.

   To do this, follow the remediation steps in [2\.1 – Ensure CloudTrail is enabled in all Regions](securityhub-cis-controls.md#securityhub-cis-controls-2.1)\.

   Make a note of the associated log group name\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Logs**\. 

1. Find the log group that you made a note of in the previous procedure and then choose the value in the **Metric Filters** column\. 

1. Choose **Add Metric Filter**\. 

1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

   ```
   {$.userIdentity.type="Root" && $.userIdentity.invokedBy NOT EXISTS && $.eventType !="AwsServiceEvent"}
   ```

1. Choose **Assign Metric**\. 

1. \(Optional\) Update the filter name to a name of your choice\.

1. Confirm that the value for **Metric Namespace** is `LogMetrics`\. 

   This ensures that all CIS Benchmark metrics are grouped together\.

1. Enter a name in the **Metric Name** field and then choose **Create Filter**\. 

1. Choose **Create Alarm**\. 

1. Under **Alarm details**, enter a **Name** and **Description** for the alarm, such as **CIS\-1\.1\-RootAccountUsage**\. 

1. Under **Actions**, for **Send notification to**, choose **Enter list** and then enter the name of the topic that you created in the previous procedure\.

1. Choose **Create Alarm**\. 

## \[PCI\.EC2\.1\] Amazon EBS snapshots should not be publicly restorable<a name="pcidss-ec2-1"></a>

**Severity:** Critical

**Resource:** Amazon EC2 volume

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html)

This control checks whether Amazon Elastic Block Store snapshots are not publicly restorable by everyone, which makes them public\. Amazon EBS snapshots should not be publicly restorable by everyone unless you explicitly allow it, to avoid accidental exposure of your company’s sensitive data\.

You should also ensure that permission to change Amazon EBS configurations are restricted to authorized AWS accounts only\. Learn more about managing Amazon EBS snapshot permissions in the [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modifying-snapshot-permissions.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modifying-snapshot-permissions.html)\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-ec2-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment, and specifically deny all other traffic\.**  
Amazon EBS snapshots are used to back up the data on your Amazon EBS volumes to Amazon S3 at a specific point in time, and can be used to restore previous states of EBS volumes\.  
If an Amazon EBS snapshot stores cardholder data, it should not be publicly restorable by everyone\. This would violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
Amazon EBS snapshots are used to back up the data on your Amazon EBS volumes to Amazon S3 at a specific point in time, and can be used to restore previous states of Amazon EBS volumes\.  
If an Amazon EBS snapshot stores cardholder data, it should not be publicly restorable by everyone\. This would violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the Internet\.**  
Amazon EBS snapshots are used to back up the data on your Amazon EBS volumes to Amazon S3 at a specific point in time, and can be used to restore previous states of EBS volumes\.  
If an Amazon EBS snapshot stores cardholder data, it should not be publicly restorable by everyone\. This would violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the Internet\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
Amazon EBS snapshots are used to back up the data on your Amazon EBS volumes to Amazon S3 at a specific point in time, and can be used to restore previous states of Amazon EBS volumes\.  
If an Amazon EBS snapshot stores cardholder data, it should not be publicly restorable by everyone\. This may violate the requirement to ensure access to systems components is restricted to least privilege necessary, or a user’s need to know\.

### Remediation<a name="pcidss-ec2-1-remediation"></a>

**To make a public Amazon EBS snapshot private**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the navigation pane, choose **Snapshots** and then choose your public snapshot

1. Choose **Actions**, then choose **Modify permissions**

1. Choose **Private**

1. Optionally, add AWS account numbers for authorized accounts to share your snapshot with

1. Choose **Save**

For more information about sharing an Amazon EBS snapshot, see the [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modifying-snapshot-permissions.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modifying-snapshot-permissions.html)\.

## \[PCI\.EC2\.2\] VPC default security group should prohibit inbound and outbound traffic<a name="pcidss-ec2-2"></a>

**Severity:** Medium

**Resource:** Amazon EC2 security group

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html)

This control checks that the default security group of a VPC does not allow inbound or outbound traffic\.

It does not check for access restrictions for other security groups that are not default, and other VPC configurations\.

### Related PCI DSS requirements<a name="pcidss-ec2-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment, and specifically deny all other traffic\.**  
If a service that is in scope for PCI DSS is associated with the default security group, the default rules for the security group will allow all outbound traffic, as well as all inbound traffic from network interfaces \(and their associated instances\) that are assigned to the same security group\.  
You should change the default security group rules setting to restrict inbound and outbound traffic, as using the default might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the Internet\.**  
If a service that is in scope for PCI DSS is associated with the default security group, the default rules for the security group will allow all outbound traffic, as well as all inbound traffic from network interfaces \(and their associated instances\) that are assigned to the same security group\.  
You should change the default security group rules setting to restrict unauthorized inbound and outbound traffic, as using the default may violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the Internet\.

**PCI DSS 2\.1: Always change vendor\-supplied defaults and remove or disable unnecessary default accounts before installing a system on the network\.**  
If a service that is in scope for PCI DSS is associated with the default security group, the default rules for the security group will allow all outbound traffic, as well as all inbound traffic from network interfaces \(and their associated instances\) that are assigned to the same security group\.  
You should change the default security group rules setting to restrict inbound and outbound traffic, as using the default may violate the requirement to remove or disable unnecessary default accounts\.

### Remediation<a name="pcidss-ec2-2-remediation"></a>

**To update the default security group to restrict all access**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. View the default security groups details to see the resources that are assigned to them\.

1. Create a set of least\-privilege security groups for the resources\.

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the Amazon EC2 console, change the security group for the resources that use the default security groups to the least\-privilege security group you created\.

1. For each default security group, choose the **Inbound** tab and then delete all of the inbound rules\.

1. For each default security group, choose the **Outbound** tab and then delete all of the outbound rules\.

For more information about working with security groups in Amazon VPC, see the [https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups)\.

## \[PCI\.EC2\.3\] Unused EC2 security groups should be removed<a name="pcidss-ec2-3"></a>

**Severity:** Low

**Resource: ** Amazon EC2 security group

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-security-group-attached-to-eni.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-security-group-attached-to-eni.html)

This control will help you maintain an accurate asset inventory of needed security groups in your CDE by checking that security groups are attached to Amazon EC2 instances or to an ENI\. A failed finding indicates you may have unused Amazon EC2 security groups\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-ec2-3-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 2\.4: Maintain an inventory of system components that are in scope for PCI DSS\.**  
If a security group is not attached to an Amazon EC2 instance or an elastic network interface \(ENI\), this is an indication that the resource is no longer in use\.  
Unless there is a business need to retain them, you should remove unused resources to maintain an accurate inventory of system components\.

### Remediation<a name="pcidss-ec2-3-remediation"></a>

You must perform the following steps for each security group not attached to an ENI\.

**To delete a security group**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Security groups**\.

1. Choose the security group to delete\.

1. From **Actions**, choose **Delete Security Group**\.

1. Choose **Yes, Delete**\. 

## \[PCI\.EC2\.4\] Unused EC2 EIPs should be removed<a name="pcidss-ec2-4"></a>

**Severity:** Low

**Resource:** EC2 EIP

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/eip-attached.html](https://docs.aws.amazon.com/config/latest/developerguide/eip-attached.html)

This control checks whether Elastic IP addresses that are allocated to a VPC are attached to Amazon EC2 instances or in\-use elastic network interfaces \(ENIs\)\.

A failed finding indicates you may have unused Amazon EC2 EIPs\.

This will help you maintain an accurate asset inventory of EIPs in your CDE\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-ec2-4-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 2\.4: Maintain an inventory of system components that are in scope for PCI DSS\.**  
If an EIP is not attached to an Amazon EC2 instance, this is an indication that it is no longer in use\.  
Unless there is a business need to retain them, you should remove unused resources to maintain an accurate inventory of system components\.

### Remediation<a name="pcidss-ec2-4-remediation"></a>

If you no longer need an Elastic IP address, Security Hub recommends that you release it \(the address must not be associated with an instance\)\. 

**To release an Elastic IP address using the console**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Elastic IPs**\. 

1. Choose the Elastic IP address, choose **Actions**, and then choose **Release addresses**\.

1. When prompted, choose **Release**\. 

For more information, see the information on releasing Elastic IP addresses in the [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-eips-releasing](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-eips-releasing)\.

## \[PCI\.ES\.1\] Amazon Elasticsearch Service domains should be in a VPC<a name="pcidss-es-1"></a>

**Severity: ** Critical

**Resource: ** Amazon ES domain 

**AWS Config rule: ** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-in-vpc-only.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-in-vpc-only.html)

This control checks whether Amazon Elasticsearch Service domains are in a VPC\.

It does not evaluate the VPC subnet routing configuration to determine public reachability\.

This AWS control also does not check whether the Amazon ES resource\-based policy permits public access by other accounts or external entities\. You should ensure that Amazon ES domains are not attached to public subnets\. See [Resource\-based policies](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-ac.html#es-ac-types-resource) in the *Amazon Elasticsearch Service Developer Guide*\.

You should also ensure that your VPC is configured according to the recommended best practices\. See [Security best practices for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html) in the *Amazon VPC User Guide*\.

### Related PCI DSS requirements<a name="pcidss-es-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment, and specifically deny all other traffic\.**  
If your Amazon ES clusters contain cardholder data, the Amazon ES domains should be placed in a VPC, which enables secure communication between Amazon ES and other services within the VPC without the need for an internet gateway, NAT device, or VPN connection port\.  
This method is used to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If your Amazon ES clusters contain cardholder data, the Amazon ES domains should be placed in a VPC, which enables secure communication between Amazon ES and other services within the VPC without the need for an internet gateway, NAT device, or VPN connection port\.  
This method is used to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound Internet traffic to IP addresses within the DMZ\.**  
If your Amazon ES clusters contain cardholder data, the Amazon ES domains should be placed in a VPC, which enables secure communication between Amazon ES and other services within the VPC without the need for an internet gateway, NAT device, or VPN connection port\.  
This method is used to limit inbound Internet traffic to IP addresses within the DMZ\.  
You can also use a resource\-based policy and specify an IP condition for restricting access based on source IP addresses\. See the blog post [How to control access to your Amazon Elasticsearch Service domain](http://aws.amazon.com/blogs/security/how-to-control-access-to-your-amazon-elasticsearch-service-domain/)\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the Internet\.**  
If your Amazon ES clusters contain cardholder data, the Amazon ES domains should be placed in a VPC, which enables secure communication between Amazon ES and other services within the VPC without the need for an internet gateway, NAT device, or VPN connection port\.  
This method is used to block unauthorized outbound traffic from the cardholder data environment to the Internet\.

**PCI DSS 1\.3\.6: Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If your Amazon ES clusters contain cardholder data, the Amazon ES domains should be placed in a VPC, which enables secure communication between Amazon ES and other services within the VPC without the need for an internet gateway, NAT device, or VPN connection port\.  
This method is used to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

### Remediation<a name="pcidss-es-1-remediation"></a>

If you create a domain with a public endpoint, you cannot later place it within a VPC\. Instead, you must create a new domain and migrate your data\.

The reverse is also true\. If you create a domain within a VPC, it cannot have a public endpoint\. Instead, you must either [create another domain](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createupdatedomains.html#es-createdomains) or disable this control\.

See the information on migrating from public access to VPC access in the [https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-vpc.html#es-migrating-public-to-vpc](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-vpc.html#es-migrating-public-to-vpc)\.

## \[PCI\.ES\.2\] Amazon Elasticsearch Service domains should have encryption at rest enabled<a name="pcidss-es-2"></a>

**Severity:** Medium

**Resource:** Amazon ES domain

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-encrypted-at-rest.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-encrypted-at-rest.html)

This control checks whether Amazon ES domains have encryption at rest configuration enabled\.

### Related PCI DSS requirements<a name="pcidss-es-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 3\.4: Render Primary Account Numbers \(PAN\) unreadable anywhere it is stored \(including on portable digital media, backup media, and in logs\)\.**  
If you use Amazon ES to store credit card Primary Account Numbers \(PAN\), the PAN should be protected by enabling Amazon ES domain encryption at rest\.  
If enabled, it encrypts the following aspects of a domain: Indices, automated snapshots, Amazon ES logs, swap files, all other data in the application directory\.  
This is a method used to render PAN unreadable\.

### Remediation<a name="pcidss-es-2-remediation"></a>

By default, domains do not encrypt data at rest, and you cannot configure existing domains to use the feature\.

To enable the feature, you must create another domain and migrate your data\. For information about creating domains, see the [https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createupdatedomains.html#es-createdomains](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createupdatedomains.html#es-createdomains)\.

Encryption of data at rest requires Amazon ES 5\.1 or later\. For more information about encrypting data at rest for Amazon ES, see the [https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/encryption-at-rest.html](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/encryption-at-rest.html)\.

## \[PCI\.IAM\.1\] IAM root user access key should not exist<a name="pcidss-iam-1"></a>

**Severity: ** Critical

**Resource: ** Account 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html)

This control checks whether user access keys exist for the root user\.

**Note**  
This control is not supported in Africa \(Cape Town\)\.

### Related PCI DSS requirements<a name="pcidss-iam-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 2\.1: Always change vendor\-supplied defaults and remove or disable unnecessary default accounts before installing a system on the network\.**  
The root user is the most privileged AWS user\. AWS Access Keys provide programmatic access to a given account\.  
No access keys should be created for the root user, as this may violate the requirement to remove or disable unnecessary default accounts\.

**PCI DSS 2\.2: Develop configuration standards for all system components\. Assure that these standards address all known security vulnerabilities and are consistent with industry\-accepted system hardening standards\.**  
The root user is the most privileged AWS user\. AWS Access Keys provide programmatic access to a given account\.  
No access keys should be created for the root user, as this may violate the requirement to implement system hardening configurations\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
The root user is the most privileged AWS user\. AWS Access Keys provide programmatic access to a given account\.  
No access keys should be created for the root user, as this may violate the requirement to ensure access to systems components is restricted to least privilege necessary, or a user’s need to know\.

### Remediation<a name="pcidss-iam-1-remediation"></a>

**To deactivate or delete access keys**

1. Log in to your account using the root credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\. 

1. In the pop\-up warning, choose **Continue to Security Credentials**\. 

1. Choose **Access keys \(access key ID and secret access key\)**\. 

1. For any existing keys, do one of the following:
   + To prevent the key from being used to authenticate the account, choose **Make Inactive**\. 
   + To permanently delete the key, choose **Delete** and then choose **Yes**\. You can't recover deleted keys\.

## \[PCI\.IAM\.2\] IAM users should not have IAM policies attached<a name="pcidss-iam-2"></a>

**Severity:** Low

**Resource:** IAM user

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html)

This control checks that none of your IAM users have policies attached\. IAM users must inherit permissions from IAM groups or roles\.

It does not check whether least privileged policies are applied to IAM roles and groups\.

### Related PCI DSS requirements<a name="pcidss-iam-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
IAM policies are how privileges are granted to users, groups, or roles in AWS\.  
By default, IAM users, groups, and roles have no access to AWS resources until IAM policies are attached to them\.  
To manage least privileged access and reduce the complexity of access management for PCI DSS in\-scope resources, you should assign IAM polices at the group or role level and not at the user level\.  
Reducing access management complexity reduces opportunity for a principal to inadvertently receive or retain excessive privileges\.  
This is a method used to ensure access to systems components that contain cardholder data is restricted to least privilege necessary, or a user’s need to know\.

### Remediation<a name="pcidss-iam-2-remediation"></a>

To resolve this issue, do the following:

1. Create an IAM group

1. Assign the policy to the group

1. Add the users to the group

The policy is applied to each user in the group\. 

**To create an IAM group**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Groups** and then choose **Create New Group**\.

1. Enter a name for the group to create and then choose **Next Step**\.

1. Select each policy to assign to the group and then choose **Next Step**\.

   The policies that you choose should include any policies currently attached directly to a user account\. The next step to resolve a failed check is to add users to a group and then assign the policies to that group\.

   Each user in the group gets assigned the policies assigned to the group\. 

1. Confirm the details on the **Review** page and then choose **Create Group**\. 

For more information about creating IAM groups, see the [https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_create.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_create.html)\.

**To add users to an IAM group**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Groups**\.

1. Choose **Group Actions** and then choose **Add Users to Group**\.

1. Choose the users to add to the group and then choose **Add Users**\.

For more information about adding users to groups, see the [https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_manage_add-remove-users.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_manage_add-remove-users.html)\.

**To remove a policy attached directly to a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\. 

1. For the user to detach a policy from, in the **User name** column, choose the name\. 

1. For each policy listed under **Attached directly**, to remove the policy from the user, choose the **X** on the right side of the page and then choose **Remove**\. 

1. Confirm that the user can still use AWS services as expected\.

## \[PCI\.IAM\.3\] IAM policies should not allow full "\*" administrative privileges<a name="pcidss-iam-3"></a>

**Severity:** High

**Resource:** IAM policy

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html)

This control checks whether the default version of AWS Identity and Access Management policies \(also known as customer managed policies\) do not have administrator access with a statement that has `"Effect": "Allow" with "Action": "*"` over `"Resource": "*"`\.

It only checks for the [customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies) that you created, but does not check for full access to individual services, such as "`S3:*`"\.

It does not check for [inline and AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies)\.

### Related PCI DSS requirements<a name="pcidss-iam-3-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
Providing full administrative privileges instead of restricting to the minimum required may violate the requirement to ensure access to systems components is restricted to the least privilege necessary, or a user’s need to know\.

### Remediation<a name="pcidss-iam-3-remediation"></a>

**To modify an IAM policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Policies**\.

1. Choose the radio button next to the policy to remove\.

1. From **Policy actions**, choose **Detach**\.

1. On the **Detach policy** page, choose the radio button next to each user to detach the policy from and then choose **Detach policy**\. 

1. Confirm that the user that you detached the policy from can still access AWS services and resources as expected\.

## \[PCI\.IAM\.4\] Hardware MFA should be enabled for the root user<a name="pcidss-iam-4"></a>

**Severity:** Critical

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html)

This control checks whether your AWS account is enabled to use multi\-factor authentication \(MFA\) hardware device to sign in with root credentials\.

It does not check whether you are using virtual MFA\.

To address PCI DSS requirement 8\.3\.1, you can choose between hardware MFA \(this control\) or virtual MFA \([\[PCI\.IAM\.5\] Virtual MFA should be enabled for the root user](#pcidss-iam-5)\)\.

**Note**  
This control is not supported in AWS GovCloud \(US\-East\) or AWS GovCloud \(US\-West\)\.

### Related PCI DSS requirements<a name="pcidss-iam-4-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 8\.3\.1: Incorporate multi\-factor authentication for all non\-console access into the Cardholder Data Environment \(CDE\) for personnel with administrative access\.**  
The root user is the most privileged user in an account\.  
MFA adds an extra layer of protection on top of a user name and password\. If users with administrative privileges are accessing the cardholder data environment over a network interface rather than via a direct, physical connection to the system component, and are not physically in front of the machine they are administering, MFA is required\.  
Enabling hardware MFA is a method used to incorporate multi\-factor authentication \(MFA\) for all non\-console administrative access

### Remediation<a name="pcidss-iam-4-remediation"></a>

**To enable hardware\-based MFA for the root account**

1. Log in to your account using the root credentials\.

1. Choose the account name at the top right of the page and then choose **My Security Credentials**\. 

1. In the warning, choose **Continue to Security Credentials**\. 

1. Choose **Multi\-factor authentication \(MFA\)**\. 

1. Choose **Activate MFA**\.

1. Choose a hardware\-based \(not virtual\) device to use for MFA and then choose **Continue**\. 

1. Complete the steps to configure the device type appropriate to your selection\. 

## \[PCI\.IAM\.5\] Virtual MFA should be enabled for the root user<a name="pcidss-iam-5"></a>

**Severity: ** Critical

**Resource: ** Account 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-mfa-enabled.html)

This control checks whether users of your AWS account require a multi\-factor authentication \(MFA\) device to sign in with root credentials\.

It does not check whether you are using hardware MFA\.

To address PCI DSS requirement 8\.3\.1, you can choose between virtual MFA \(this control\) or hardware MFA \([\[PCI\.IAM\.4\] Hardware MFA should be enabled for the root user](#pcidss-iam-4)\)\.

**Note**  
This control is not supported in AWS GovCloud \(US\-East\) or AWS GovCloud \(US\-West\)\.

### Related PCI DSS requirements<a name="pcidss-iam-5-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 8\.3\.1: Incorporate multi\-factor authentication for all non\-console access into the Cardholder Data Environment \(CDE\) for personnel with administrative access\.**  
The root user is the most privileged user in an account\.  
MFA adds an extra layer of protection on top of a user name and password\. If users with administrative privileges are accessing the cardholder data environment, and are not physically in front of the machine they are administering, MFA is required\.  
Enabling virtual MFA is a method used to incorporate multi\-factor authentication \(MFA\) for all non\-console administrative access\.

### Remediation<a name="pcidss-iam-5-remediation"></a>

**To enable MFA for the root account**

1. Log in to your account using the root credentials\.

1. Choose the account name at the top\-right of the page and then choose **My Security Credentials**\.

1. In the warning, choose **Continue to Security Credentials**\.

1. Choose **Multi\-factor authentication \(MFA\)**\. 

1. Choose **Activate MFA**\.

1. Choose the type of device to use for MFA and then choose **Continue**\. 

1. Complete the steps to configure the device type appropriate to your selection\.

## \[PCI\.IAM\.6\] MFA should be enabled for all IAM users<a name="pcidss-iam-6"></a>

**Severity:** Medium

**Resource:** IAM user 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-mfa-enabled.html)

This control checks whether the IAM users have multi\-factor authentication \(MFA\) enabled\.

### Related PCI DSS requirements<a name="pcidss-iam-6-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 8\.3\.1: Incorporate multi\-factor authentication for all non\-console access into the Cardholder Data Environment \(CDE\) for personnel with administrative access\.**  
Enabling MFA for all IAM users is a method used to incorporate multi\-factor authentication \(MFA\) for all non\-console administrative access\.

### Remediation<a name="pcidss-iam-6-remediation"></a>

**To configure MFA for a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the user name of the user to configure MFA for\.

1. Choose **Security credentials** and then choose **Manage** next to **Assigned MFA device**\.

1. Follow the **Manage MFA Device** wizard to assign the type of device appropriate for your environment\. 

To learn how to delegate MFA setup to users, the AWS Security Blog post [How to Delegate Management of Multi\-Factor Authentication to AWS IAM Users](http://aws.amazon.com/blogs/security/how-to-delegate-management-of-multi-factor-authentication-to-aws-iam-users/)\. 

## \[PCI\.KMS\.1\] Customer master key \(CMK\) rotation should be enabled<a name="pcidss-kms-1"></a>

**Severity:** Medium

**Resource: ** AWS KMS key 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html)

This control checks that key rotation is enabled for each customer master key \(CMK\)\. It does not check CMKs that have imported key material\.

You should ensure keys that have imported material and those that are not stored in AWS KMS are rotated\. AWS managed customer master keys are rotated once every 3 years\.

### Related PCI DSS requirements<a name="pcidss-kms-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 3\.6\.4: Cryptographic keys should be changed once they have reached the end of their cryptoperiod\.**  
While PCI DSS does not specify the time frame for cryptoperiods, if key rotation is enabled, rotation will occur annually by default\.  
If you use customer master key \(CMK\) to encrypt cardholder data, you should enable key rotation\.  
This is a method used to change cryptographic keys once they have reached the end of their cryptoperiod\.

### Remediation<a name="pcidss-kms-1-remediation"></a>

**To enable CMK rotation**

1. Open the AWS KMS console at [https://console\.aws\.amazon\.com/kms](https://console.aws.amazon.com/kms)\.

1. To change the AWS Region, use the Region selector in the upper\-right corner of the page\.

1. Choose **Customer managed keys**\. 

1. In the **Alias** column, choose the alias of the key to update\. 

1. Choose **Key rotation**\.

1. Select **Automatically rotate this CMK every year** and then choose **Save**\.

## \[PCI\.Lambda\.1\] Lambda functions should prohibit public access<a name="pcidss-lambda-1"></a>

**Severity:** Critical

**Resource:** Lambda function

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-public-access-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-public-access-prohibited.html)

This control checks whether the Lambda function resource\-based policy prohibits public access\.

It does not check for access to the Lambda function by internal principals, such as IAM roles\. You should ensure that access to the Lambda function is restricted to authorized principals only by using least privilege Lambda resource\-based policies\.

For more information about using resource\-based policies for AWS Lambda, see the [https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html)\.

### Related PCI DSS requirements<a name="pcidss-lambda-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment, and specifically deny all other traffic\.**  
If you use a Lambda function that is in scope for PCI DSS, the function should not be publicly accessible\. A publicly accessible function might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use a Lambda function that is in scope for PCI DSS, the function should not be publicly accessible\. A publicly accessible function might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound Internet traffic to IP addresses within the DMZ\.**  
If you use a Lambda function that is in scope for PCI DSS, the function should not be publicly accessible\. A publicly accessible function might violate the requirement to limit inbound Internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the Internet\.**  
If you use a Lambda function that is in scope for PCI DSS, the function must not be publicly accessible\. A publicly accessible function might violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the Internet\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
If you use a Lambda function that is in scope for PCI DSS, the function should not be publicly accessible\. A publicly accessible function might violate the requirement to ensure access to systems components that contain cardholder data is restricted to the least privilege necessary, or a user’s need to know\.

### Remediation<a name="pcidss-lambda-1-remediation"></a>

To remediate this issue, you update the resource\-based policy to change the publicly accessible Lambda function to a private Lambda function\.

You can only update resource\-based policies for Lambda resources within the scope of the [https://docs.aws.amazon.com/lambda/latest/dg/API_AddPermission.html](https://docs.aws.amazon.com/lambda/latest/dg/API_AddPermission.html) and [https://docs.aws.amazon.com/lambda/latest/dg/API_AddLayerVersionPermission.html](https://docs.aws.amazon.com/lambda/latest/dg/API_AddLayerVersionPermission.html) API actions\.

You cannot author policies for your Lambda resources in JSON, or use conditions that don't map to parameters for those actions using the CLI or the SDK\.

**To use the AWS CLI to revoke function\-use permission from an AWS service or another account**

1. To get the ID of the statement from the output of `GetPolicy`, from the AWS CLI, run the following:

   ```
   aws lambda get-policy —function-name yourfunctionname
   ```

   This command returns the Lambda resource\-based policy string associated with the publicly accessible Lambda function\.

1. From the policy statement returned by the `get-policy` command, copy the string value of the `Sid` field\.

1. From the AWS CLI, run

   ```
   aws lambda remove-permission --function-name yourfunctionname —statement-id youridvalue
   ```

**To use the Lambda console to restrict access to the Lambda function**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. Navigate to **Functions** and then select your publicly accessible Lambda function

1. Under **Designer**, choose the key icon at the top left\. It has the tool\-tip **View permissions**\.

1. Under **Function policy**, if the policy allows actions for the principal element `“*”` or `{“AWS”: “*”}`, it is publicly accessible\.

   Consider adding the following IAM condition to scope access to your account only\.

   ```
   "Condition": {
     "StringEquals": {
       "AWS:SourceAccount": "<account_id>"
        }
     }
   }
   ```

For other Lambda resource\-based policies examples that allow you to grant usage permission to other accounts on a per\-resource basis, see the information on using resource\-based policies for AWS Lambda in the [https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html)\.

## \[PCI\.Lambda\.2\] Lambda functions should be in a VPC<a name="pcidss-lambda-2"></a>

**Severity: ** Low

**Resource: ** Lambda function

**AWS Config rule: ** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-inside-vpc.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-inside-vpc.html) 

This control checks whether a Lambda function is in a VPC\.

It does not evaluate the VPC subnet routing configuration to determine public reachability\. 

### Related PCI DSS requirements<a name="pcidss-lambda-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment, and specifically deny all other traffic\.**  
By default, Lambda runs your functions in a secure default VPC with access to AWS services and the internet\.  
If you use a Lambda function that is in scope for PCI DSS, the function can be configured to use a VPC endpoint\. This would allow you to connect to your Lambda function from within a VPC without internet access, which is a method used to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
By default, Lambda runs your functions in a secure default VPC with access to AWS services and the internet\.  
If you use a Lambda function that is in scope for PCI DSS, the function can be configured to use a VPC endpoint\. This allows you to connect to your Lambda function from within a VPC without internet access, which is a method used to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound Internet traffic to IP addresses within the DMZ\.**  
By default, Lambda runs your functions in a secure default VPC with access to AWS services and the internet\.  
If you use a Lambda function that is in scope for PCI DSS, the function can be configured to use a VPC endpoint\. This allows you to connect to your Lambda function from within a VPC without internet access, which is a method used to limit inbound Internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the Internet\.**  
By default, Lambda runs your functions in a secure default VPC with access to AWS services and the internet\.  
If you use a Lambda function that is in scope for PCI DSS, the function can be configured to use a VPC endpoint\. This allows you to connect to your Lambda function from within a VPC without internet access, which is a method used to block unauthorized outbound traffic from the cardholder data environment to the Internet\.

### Remediation<a name="pcidss-lambda-2-remediation"></a>

**To configure a function to connect to private subnets in a virtual private cloud \(VPC\) in your account**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. Navigate to **Functions** and then select your Lambda function\.

1. Scroll to **Network** and then select a VPC with the connectivity requirements of the function\.

1. To run your functions in high availability mode, Security Hub recommends that you choose at least 2 subnets\.

1. Choose at least 1 security group that has the connectivity requirements of the function 

1. Choose **Save**\.

For more information see the section on configuring a Lambda function to access resources in a VPC in the [https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html)\.

## \[PCI\.RDS\.1\] RDS snapshots should prohibit public access<a name="pcidss-rds-1"></a>

**Severity:** Critical

**Resource: ** Amazon RDS DB snapshot

**AWS Config rule: ** [https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html)

This control checks whether Amazon RDS DB snapshots prohibit access by other accounts\. You should also ensure that access to the snapshot and permission to change Amazon RDS configuration is restricted to authorized principals only\.

To learn more about sharing DB snapshots in Amazon RDS, see the [https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html)\.

Note that if the configuration is changed to allow public access, the AWS Config rule may not be able to detect the change for up to 12 hours\. Until the AWS Config rule detects the change, the check passes even though the configuration violates the rule\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-rds-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment, and specifically deny all other traffic\.**  
RDS snapshots are used to back up the data on your RDS instances at a specific point in time and can be used to restore previous states of RDS instances\.  
If an RDS snapshot stores cardholder data, the RDS snapshot should not be shared by other accounts\. Sharing the RDS snapshot would allow other accounts to restore an RDS instance from the snapshot, which may violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
RDS snapshots are used to back up the data on your RDS instances at a specific point in time and can be used to restore previous states of RDS instances\.  
If an RDS snapshot stores cardholder data, the RDS snapshot should not be shared by other accounts\. Sharing the RDS snapshot would allow other accounts to restore an RDS instance from the snapshot, which may violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the Internet\.**  
RDS snapshots are used to back up the data on your RDS instances at a specific point in time and can be used to restore previous states of RDS instances\.  
If an RDS snapshot stores cardholder data, the RDS snapshot should not be shared by other accounts\. Sharing the RDS snapshot would allow other accounts to restore an RDS instance from the snapshot, which may violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the Internet\.

**PCI DSS 1\.3\.6: Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
RDS snapshots are used to back up the data on your RDS instances at a specific point in time and can be used to restore previous states of RDS instances\.  
If an RDS snapshot stores cardholder data, the RDS snapshot should not be shared by other accounts\. Sharing the RDS snapshot would allow other accounts to restore an RDS instance from the snapshot, which may violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
RDS snapshots are used to back up the data on your RDS instances at a specific point in time and can be used to restore previous states of RDS instances\.  
If an RDS snapshot stores cardholder data, the RDS snapshot should not be shared by other accounts\. Sharing the RDS snapshot would allow other accounts to restore an RDS instance from the snapshot, which may violate the requirement to ensure access to systems components that contain cardholder data is restricted to least privilege necessary, or a user's need to know\.

### Remediation<a name="pcidss-rds-1-remediation"></a>

To remove public access for Amazon RDS Snapshots

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Navigate to **Snapshots** and then select the public Snapshot you want to modify

1. From the **Actions** list, choose **Share Snapshots**

1. From **DB snapshot visibility**, choose **Private**

1. Under **DB snapshot visibility**, select **for all**

1. Choose **Save**

## \[PCI\.RDS\.2\] RDS DB Instances should prohibit public access<a name="pcidss-rds-2"></a>

**Severity: ** Critical

**Resource:** RDS DB instance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html)

This control checks whether RDS instances are publicly accessible by evaluating the `publiclyAccessible` field in the instance configuration item\. The value of `publiclyAccessible` indicates whether the DB instance is publicly accessible\. When the DB instance is publicly accessible, it is an Internet\-facing instance with a publicly resolvable DNS name, which resolves to a public IP address\. When the DB instance isn't publicly accessible, it is an internal instance with a DNS name that resolves to a private IP address\.

The control does not check VPC subnet routing settings or the Security Group rules\. You should also ensure VPC subnet routing does not allow public access, and that the security group inbound rule associated with the RDS instance does not allow unrestricted access \(0\.0\.0\.0/0\)\. You should also ensure that access to your RDS instance configuration is limited to only authorized users by restricting users' IAM permissions to modify RDS instances settings and resources\.

For more information, see [Hiding a DB instance in a VPC from the Internet](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.Hiding) in the *Amazon RDS User Guide*\.

### Related PCI DSS requirements<a name="pcidss-rds-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment, and specifically deny all other traffic\.**  
If you use an RDS instance that is in scope for PCI DSS, the RDS instance should not be publicly accessible, as this might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use an RDS instance to store cardholder data, the RDS instance should not be publicly accessible as this might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound Internet traffic to IP addresses within the DMZ\.**  
If you use an RDS instance to store cardholder data, the RDS instance should not be publicly accessible as this might violate the requirement to limit inbound Internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the Internet\.**  
If you use an RDS instance to store cardholder data, the RDS instance should not be publicly accessible, as this might violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the Internet\.

**PCI DSS 1\.3\.6: Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If you use an RDS instance to store cardholder data, the RDS instance should not be publicly accessible, as this may violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to “deny all” unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
If you use an RDS instance to store cardholder data, the RDS instance should not be publicly accessible, as this may violate the requirement to ensure access to systems components that contain cardholder data is restricted to least privilege necessary, or a user’s need to know\.

### Remediation<a name="pcidss-rds-2-remediation"></a>

**To remove public access for Amazon RDS Databases**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Navigate to **Databases** and then choose your public Database

1. Choose **Modify**

1. Scroll to **Network & Security**

1. For **Public accessibility**, choose **No**

1. Scroll to the bottom and then choose **Continue**

1. Under **Scheduling of modifications**, choose **Apply immediately**

1. Choose **Modify DB Instance**

For more information about working with a DB Instance in a VPC, see the [https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html)\.

## \[PCI\.Redshift\.1\] Amazon Redshift clusters should prohibit public access<a name="pcidss-redshift-1"></a>

**Severity: ** Critical

**Resource:** Amazon Redshift cluster

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-public-access-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-public-access-check.html)

This control checks whether Amazon Redshift clusters are publicly accessible by evaluating the `publiclyAccessible` field in the cluster configuration item\.

### Related PCI DSS requirements<a name="pcidss-redshift-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment, and specifically deny all other traffic\.**  
If you use an Amazon Redshift cluster to store cardholder data, the cluster should not be publicly accessible, as this might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use an Amazon Redshift cluster to store cardholder data, the cluster should not be publicly accessible, as this might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound Internet traffic to IP addresses within the DMZ\.**  
If you use an Amazon Redshift cluster to store cardholder data, the cluster should not be publicly accessible, as this may violate the requirement to limit inbound Internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the Internet\.**  
If you use an Amazon Redshift cluster to store cardholder data, the cluster should not be publicly accessible, as this may violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the Internet\.

**PCI DSS 1\.3\.6: Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If you use an Amazon Redshift cluster to store cardholder data, the cluster should not be publicly accessible as this may violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

### Remediation<a name="pcidss-redshift-1-remediation"></a>

**To disable public access for an Amazon Redshift cluster**

1. Open the Amazon Redshift console at [https://console\.aws\.amazon\.com/redshift/](https://console.aws.amazon.com/redshift/)\.

1. On the navigation pane, choose **Clusters** and then select your public Amazon Redshift cluster

1. From the **Cluster** drop\-down menu, choose **Modify cluster**

1. In **Publicly accessible**, choose **No**

1. Choose **Modify**

For more information about creating a cluster in a VPC, see the [https://docs.aws.amazon.com/redshift/latest/mgmt/getting-started-cluster-in-vpc.html](https://docs.aws.amazon.com/redshift/latest/mgmt/getting-started-cluster-in-vpc.html)\.

## \[PCI\.S3\.1\] S3 buckets should prohibit public write access<a name="pcidss-s3-1"></a>

**Severity:** Critical

**Resource:** S3 bucket

**AWS Config rule: **[https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html)

This control checks whether your S3 buckets allow public write access by evaluating the Block Public Access settings, the bucket policy, and the bucket access control list \(ACL\)\.

It does not check for write access to the bucket by internal principals, such as IAM roles\. You should ensure that access to the bucket is restricted to authorized principals only\.

### Related PCI DSS requirements<a name="pcidss-s3-1-requirements"></a>

This control is related to the following PCI DSS requirements:

** PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment, and specifically deny all other traffic\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public write access\. Allowing public write access might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public write access\. Allowing public write access might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.  
Unless you explicitly require everyone on the internet to be able to write to your S3 bucket, you should ensure that your S3 bucket is not publicly writable\.

**PCI DSS 1\.3\.2: Limit inbound Internet traffic to IP addresses within the DMZ\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public write access\. Allowing public write access might violate the requirement to limit inbound Internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the Internet\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public write access\. Allowing public write access might violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the Internet\.

**PCI DSS 1\.3\.6: Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public write access\. Allowing public write access may violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to “deny all” unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public write access\. Allowing public write access might violate the requirement to ensure access to systems components is restricted to least privilege necessary, or a user's need to know\.

### Remediation<a name="pcidss-s3-1-remediation"></a>

**To remove public access for an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the name of the bucket identified in the finding\.

1. Choose **Permissions** and then choose **Public access settings**\. 

1. Choose **Edit**, select all four options, and then choose **Save**\.

1. If prompted, enter **confirm** and then choose **Confirm**\.

## \[PCI\.S3\.2\] S3 buckets should prohibit public read access<a name="pcidss-s3-2"></a>

**Severity:** Critical

**Resource:** S3 bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited.html)

This control checks whether your S3 buckets allow public read access by evaluating the Block Public Access settings, the bucket policy, and the bucket access control list \(ACL\)\.

Unless you explicitly require everyone on the internet to be able to write to your S3 bucket, you should ensure that your S3 bucket is not publicly writable\.

It does not check for read access to the bucket by internal principals, such as IAM roles\. You should ensure that access to the bucket is restricted to authorized principals only\.

### Related PCI DSS requirements<a name="pcidss-s3-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment, and specifically deny all other traffic\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public read access\. Public read access might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public read access\. Public read access might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound Internet traffic to IP addresses within the DMZ\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public read access\. Public read access might violate the requirement to limit inbound Internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.6: Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public read access\. Public read access might violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public read access\. Public read access might violate the requirement to ensure access to systems components is restricted to least privilege necessary, or a user’s need to know\.

### Remediation<a name="pcidss-s3-2-remediation"></a>

**To remove public access for an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the name of the bucket identified in the finding\.

1. Choose **Permissions** and then choose **Public access settings**\. 

1. Choose **Edit**, select all four options, and then choose **Save**\. 

1. If prompted, enter **confirm** and then choose **Confirm**\.

## \[PCI\.S3\.3\] S3 buckets should have cross\-region replication enabled<a name="pcidss-s3-3"></a>

**Severity: ** Low

**Resource:** S3 bucket

**AWS Config rule: ** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-replication-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-replication-enabled.html)

This control checks whether S3 buckets have cross\-region replication enabled\.

PCI DSS does not require data replication or highly available configurations\. However, this check aligns with AWS best practices for this control\.

In addition to availability, you should consider other systems hardening settings\.

### Related PCI DSS requirements<a name="pcidss-s3-3-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 2\.2: Develop configuration standards for all system components\. Assure that these standards address all known security vulnerabilities and are consistent with industry\-accepted system hardening standards\.**  
Enabling cross\-region replication on S3 buckets ensures that multiple versions of the data are available in different distinct Regions\. This allows you to store data at even greater distances, minimize latency, increase operational efficiency, and protect against DDoS and data corruption events\.  
This is one method used to implement system hardening configuration\.

### Remediation<a name="pcidss-s3-3-remediation"></a>

**To enable S3 bucket replication**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the S3 bucket that does not have cross\-region replication enabled\.

1. Choose **Management**, then choose **Replication**

1. Choose **Add rule**\. If versioning is not already enabled, you are prompted to enable it\.

1. Choose your source bucket \- **Entire bucket**

1. Choose your destination bucket\. If versioning is not already enabled on the destination bucket for your account, you are prompted to enable it\.

1. Choose an IAM role\. For more information on setting up permissions for replication, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/setting-repl-config-perm-overview.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/setting-repl-config-perm-overview.html)\.

1. Enter a rule name, choose **Enabled** for the status, then choose **Next**

1. Choose **Save**

For more information about replication, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html)\.

## \[PCI\.S3\.4\] S3 buckets should have server\-side encryption enabled<a name="pcidss-s3-4"></a>

**Severity:** Medium

**Resource:** S3 bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html)

This control checks that your Amazon S3 bucket either has Amazon S3 default encryption enabled or that the S3 bucket policy explicitly denies put\-object requests without server\-side encryption\.

When you set default encryption on a bucket, all new objects stored in the bucket are encrypted when they are stored, including clear text PAN data\.

Server\-side encryption for all of the objects stored in a bucket can also be enforced using a bucket policy\. For more information about server\-side encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)\.

### Related PCI DSS requirements<a name="pcidss-s3-4-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 3\.4: Render Primary Account Numbers \(PAN\) unreadable anywhere it is stored \(including on portable digital media, backup media, and in logs\)\.**  
If you use an S3 bucket to store credit card Primary Account Numbers \(PAN\), then to render the PAN unreadable, the bucket default encryption should be enabled and/or the S3 bucket policy should explicitly deny put\-object requests without server\-side encryption\.

### Remediation<a name="pcidss-s3-4-remediation"></a>

**To enable default encryption on an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the bucket from the list\.

1. Choose **Properties**\.

1. Choose **Default encryption**\.

1. For the encryption, choose either **AES\-256** or **AWS\-KMS**\.
   + To use keys that are managed by Amazon S3 for default encryption, choose **AES\-256**\. For more information about using Amazon S3 server\-side encryption to encrypt your data, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)\.
   + To use keys that are managed by AWS KMS for default encryption, choose **AWS\-KMS**, and then choose a master key from the list of the AWS KMS master keys that you have created\.

     Type the Amazon Resource Name \(ARN\) of the AWS KMS key to use\. You can find the ARN for your AWS KMS key in the IAM console, under **Encryption keys**\. Or, you can choose a key name from the drop\-down list\.
**Important**  
 If you use the AWS KMS option for your default encryption configuration, you are subject to the RPS \(requests per second\) limits of AWS KMS\. For more information about AWS KMS limits and how to request a limit increase, see the [https://docs.aws.amazon.com/kms/latest/developerguide/limits.html](https://docs.aws.amazon.com/kms/latest/developerguide/limits.html)\.

     For more information about creating an AWS KMS key, see the [https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html)\.

     For more information about using AWS KMS with Amazon S3, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html)\.

   When enabling default encryption, you might need to update your bucket policy\. For more information about moving from bucket policies to default encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy)\.

1. Choose **Save**\.

For more information about default S3 bucket encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html)\.

## \[PCI\.SSM\.1\] Amazon EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation<a name="pcidss-ssm-1"></a>

**Severity:** Medium

**Resource:** SSM patch compliance and Amazon EC2 instance

**AWS Config rule: ** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html)

This control checks whether the compliance status of the Amazon EC2 Systems Manager patch compliance is COMPLIANT or NON\_COMPLIANT after the patch installation on the instance\.

It only checks instances that are managed by AWS Systems Manager Patch Manager\.

It does not check whether the patch was applied within the 30\-day limit prescribed by PCI DSS requirement 6\.2\.

It also does not validate whether the patches applied were classified as security patches\.

You should create patching groups with the appropriate baseline settings and ensure in\-scope systems are managed by those patch groups in Systems Manager\. For more information about patch groups, see the [https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-patch-group-tagging.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-patch-group-tagging.html)\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-ssm-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 6\.2: Ensure that all system components and software are protected from known vulnerabilities by installing applicable vendor\-supplied security patches\. Install critical security patches within one month of release\.**  
Patches released by the vendor for systems that are in\-scope for PCI DSS should be tested and validated prior to installation in production environment\. Once deployed, security settings and controls should be validated to ensure that deployed patches have not impacted the security of the Card Data Environment \(CDE\)\.  
If you use Amazon EC2 instances managed by AWS Systems Manager Patch Manager to patch managed instances in your CDE, ensure that the patches are successfully applied\. To do this, check that the compliance status of the Amazon EC2 Systems Manager patch compliance is "COMPLIANT"\. Patch Manager can apply both operating systems and applications applicable patches\.  
This is a method used to protect system components and software from known vulnerabilities\.

### Remediation<a name="pcidss-ssm-1-remediation"></a>

**To remediate non\-compliant patches**

This rule checks whether the compliance status of the Amazon EC2 Systems Manager patch compliance is COMPLIANT or NON\_COMPLIANT\. To find out more about patch compliance states, see the [https://docs.aws.amazon.com/systems-manager/latest/userguide/about-patch-compliance-states.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/about-patch-compliance-states.html)\. 

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation pane, under **Instances & Nodes**, choose **Run Command**\.

1. Choose **Run command**\.

1. Choose the radio button next to `AWS-RunPatchBaseline` and then change the **Operation** to **Install**\.

1. Choose **Choose instances manually** and then choose the non\-compliant instance\(s\)\.

1. Scroll to the bottom and then choose **Run**\.

1. After the command has completed, to monitor the new compliance status of your patched instances, in the navigation pane, choose **Compliance**\.

See the *AWS Systems Manager User Guide* for more information about the following
+ [Using Systems Manager documents to patch a managed instance](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-ssm-documents.html)
+ [Running commands using the Systems Manager Run command](https://docs.aws.amazon.com/systems-manager/latest/userguide/run-command.html)