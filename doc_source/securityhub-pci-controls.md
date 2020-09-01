# PCI DSS controls<a name="securityhub-pci-controls"></a>

The PCI DSS security standard in Security Hub supports the following controls\. For each control, the information includes the severity, the resource type, the AWS Config rule, and the remediation steps\.

## \[PCI\.AutoScaling\.1\] Auto Scaling groups associated with a load balancer should use health checks<a name="pcidss-autoscaling-1"></a>

**Severity:** Low

**Resource:** Auto Scaling group

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-group-elb-healthcheck-required.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-group-elb-healthcheck-required.html)

**Parameters:** None

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

1. To select the group from the list, choose the right box\.

1. From **Actions**, choose **Edit**

1. For **Health Check Type**, choose **ELB**\.

1. For **Health Check Grace Period**, enter **300**\.

1. Choose **Save**\.

For more information on using a load balancer with an Auto Scaling group, see the [https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html](https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html)\.

## \[PCI\.CloudTrail\.1\] CloudTrail logs should be encrypted at rest using AWS KMS CMKs<a name="pcidss-cloudtrail-1"></a>

**Severity:** Medium

**Resource:** CloudTrail trail

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html)

**Parameters:** None

This control checks whether AWS CloudTrail is configured to use the server\-side encryption \(SSE\) AWS KMS customer master key \(CMK\) encryption\.

If you are only using the default encryption option, you can choose to disable this check\.

### Related PCI DSS requirements<a name="pcidss-cloudtrail-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 3\.4: Render Primary Account Numbers \(PAN\) unreadable anywhere it is stored \(including on portable digital media, backup media, and in logs\)\.**  
If you are using AWS services to process and store PAN, your CloudTrail logs should be encrypted at rest\. Encrypting logs ensures that if logs capture PAN\(s\), the PAN\(s\) are protected\.  
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

**Parameters:** None

This control checks whether CloudTrail is enabled in your AWS account\.

However, some AWS services do not enable logging of all APIs and events\. You should implement any additional audit trails other than CloudTrail and review the documentation for each service in [CloudTrail Supported Services and Integrations](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-aws-service-specific-topics.html)\.

### Related PCI DSS requirements<a name="pcidss-cloudtrail-2-requirements"></a>

This control is associated with the following PCI DSS requirements:

**PCI DSS 10\.1: Implement audit trails to link all access to system components to each individual user\.**  
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

**PCI DSS 10\.2\.7: Implement automated audit trails for all system components to reconstruct the following events: Creation and deletion of system\-level objects**  
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

**Parameters:** None

This control checks whether CloudTrail log file validation is enabled\.

It does not check when configurations are altered\.

To monitor and alert on log file changes, you can use CloudWatch Events or CloudWatch metric filters\.

### Related PCI DSS requirements<a name="pcidss-cloudtrail-3-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 10\.5\.2: Protect audit trail files from unauthorized modifications\.**  
CloudTrail log file validation creates a digitally signed digest file containing a hash of each log that CloudTrail writes to Amazon S3\.  
You can use these digest files to determine whether a log file was changed, deleted, or unchanged after CloudTrail delivered the log\.  
This is a method that helps to protect audit trail files from unauthorized modifications\.

**PCI DSS 10\.5\.5: Use file\-integrity monitoring or change\-detection software on logs to ensure that existing log data cannot be changed without generating alerts\.**  
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

**Parameters:** None

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

**Parameters:** None

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
You can use CodeBuild in your PCI DSS environment to compile your source code, run unit tests, or produce artifacts that are ready to deploy\. If you do, your authentication credentials should never be stored or transmitted in clear text or appear in the repository URL\.  
You should use OAuth instead of personal access tokens or a user name and password to grant authorization for accessing GitHub or Bitbucket repositories\. This is a method to use strong cryptography to render authentication credentials unreadable\.

### Remediation<a name="pcidss-codebuild-1-remediation"></a>

**To remove basic authentication / \(GitHub\) Personal Access Token from CodeBuild Project Source**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Select your Build project that contains personal access tokens or a user name and password\.

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

**Parameters:** None

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
You can use CodeBuild in your PCI DSS environment to compile your source code, runs unit tests, or produce artifacts that are ready to deploy\. If you do, never store the authentication credentials `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` in clear text\.  
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

1. In AWS Systems Manager, create a Systems Manager parameter that contains your sensitive data\. For instructions on how to do this, refer to the tutorial in the [https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-paramstore-console.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-paramstore-console.html)\.

1. After you create the parameter, copy the parameter name\.

1. Back in the CodeBuild console, choose **Create environmental variable**\.

1. For **name**, enter the name of your variable as it appears in your build spec\.

1. For **value**, paste in the name of your parameter\.

1. From **type**, choose **Parameter**\.

1. Choose **Remove** next to your noncompliant environmental variable that contains plaintext credentials\.

1. Choose **Update environment**\.

See the information on environment variables in build environments in the [https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-env-vars.html](https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-env-vars.html)\.

## \[PCI\.Config\.1\] AWS Config should be enabled<a name="pcidss-config-1"></a>

**Severity: ** Medium

**Resource:** Account

**AWS Config rule:** None\. To run this check, Security Hub runs through audit steps prescribed for it in [Securing Amazon Web Services](https://www.cisecurity.org/benchmark/amazon_web_services/)\. No AWS Config managed rules are created in your AWS environment for this check\.

**Parameters:** None

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

**Parameters:** None

This control checks for the CloudWatch metric filters using the following pattern:

```
{ $.userIdentity.type = "Root" && $.userIdentity.invokedBy NOT EXISTS && $.eventType != "AwsServiceEvent" }
```

It checks the following:
+ The log group name is configured for use with active multi\-Region CloudTrail\.
+ There is at least one Event Selector for a Trail with `IncludeManagementEvents` set to `true` and `ReadWriteType` set to `All`\.
+ There is at least one active subscriber to an Amazon SNS topic associated with the alarm\.

### Related PCI DSS requirements<a name="pcidss-cw-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
The root user is the most privileged user in an AWS account and has unrestricted access to all resources in the AWS account\.  
You should set up log metric filters and alarms in the event that AWS account root user credentials are used\.  
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

1. Choose **Logs**, then choose **Log groups**\. 

1. Choose the log group where CloudTrail is logging\.

1. On the log group details page, choose ** Metric filters**\.

1. Choose **Create metric filter**\. 

1. Copy the following pattern and then paste it into **Filter pattern**\.

   ```
   {$.userIdentity.type="Root" && $.userIdentity.invokedBy NOT EXISTS && $.eventType !="AwsServiceEvent"}
   ```

1. Choose **Next**\.

1. Enter the name of the new filter\. For example, **RootAccountUsage**\.

1. Confirm that the value for **Metric namespace** is `LogMetrics`\. 

   This ensures that all CIS Benchmark metrics are grouped together\.

1. In **Metric name**, enter the name of the metric\.

1. In **Metric value**, enter **1**, and then choose **Next**\.

1. Choose **Create metric filter**\. 

1. Next, set up the notification\. Select the select the metric filter you just created, then choose **Create alarm**\.

1. Enter the threshold for the alarm \(for example, **1**\), then choose **Next**\.

1. Under **Select an SNS topic**, for **Send notification to**, choose an email list, then choose **Next**\.

1. Enter a **Name** and **Description** for the alarm, such as **RootAccountUsageAlarm**, then choose **Next**\. 

1. Choose **Create Alarm**\. 

## \[PCI\.DMS\.1\] AWS Database Migration Service replication instances should not be public<a name="pcidss-dms-1"></a>

**Severity: **Critical

**Resource:** DMS:ReplicationInstance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dms-replication-not-public.html](https://docs.aws.amazon.com/config/latest/developerguide/dms-replication-not-public.html)

**Parameters:** None

This control checks whether AWS DMS replication instances are public\. To do this, it examines the value of the `PubliclyAccessible` field\.

A private replication instance has a private IP address that you cannot access outside of the replication network\. A replication instance should have a private IP address when the source and target databases are in the same network, and the network is connected to the replication instance's VPC using a VPN, AWS Direct Connect, or VPC peering\. To learn more about public and private replication instances, see [Public and private replication instances](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_ReplicationInstance.html#CHAP_ReplicationInstance.PublicPrivate) in the *AWS Database Migration Service User Guide*\.

You should also ensure that access to your AWS DMS instance configuration is limited to only authorized users\. To do this, restrict users’ IAM permissions to modify AWS DMS settings and resources\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-dms-1-requirements"></a>

This control is related to the following PCI DSS requirements\.

**PCI DSS 1\.2\.1 \- Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
If you use AWS DMS in your defined CDE, set the replication instance’s `PubliclyAccessible` field to `'false'`\. Allowing public access to your replication instance might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1 \- Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use AWS DMS in your defined CDE, set the replication instance’s `PubliclyAccessible` field to `'false'`\. Allowing public access to your replication instance might violate the requirement to limit inbound traffic to only system components that provide authorized, publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2 \- Limit inbound internet traffic to IP addresses within the DMZ\.**  
If you use AWS DMS in your defined CDE, set the replication instance’s `PubliclyAccessible` field to `'false'`\. Allowing public access to your replication instance might violate the requirement to limit inbound traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4 Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
If you use AWS DMS in your defined CDE, set the replication instance’s `PubliclyAccessible` field to `'false'`\. Allowing public access to your replication instance might violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the internet\.

**PCI DSS 1\.3\.6 Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If you use AWS DMS in your defined CDE, to migrate a database storing cardholder data, set the replication instance’s `PubliclyAccessible` field to `'false'`\. Allowing public access to your replication instance might violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

### Remediation<a name="pcidss-dms-1-remediation"></a>

Note that you cannot change the public access setting once a replication instance is created\. It must be deleted and recreated\.

**To configure the AWS DMS replication instances setting to be not publicly accessible**

1. Open the AWS Database Migration Service console at [https://console\.aws\.amazon\.com/dms/](https://console.aws.amazon.com/dms/)\.

1. In the left navigation pane, under **Resource management**, navigate to** Replication instances**\. 

1. To delete the public instance, select the check box for the instance, choose **Actions**, then choose **delete**\.

1. Choose **Create replication instance**\. Provide the configuration details\.

1. To disable public access, make sure that **Publicly accessible** is not selected\.

1. Choose **Create**\.

For more information, see the section on [Creating a replication instance](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_ReplicationInstance.html#CHAP_ReplicationInstance.Creating) in the *AWS Database Migration Service User Guide*\.

## \[PCI\.EC2\.1\] Amazon EBS snapshots should not be publicly restorable<a name="pcidss-ec2-1"></a>

**Severity:** Critical

**Resource:** Amazon EC2 volume

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html)

**Parameters:** None

This control checks whether Amazon Elastic Block Store snapshots are not publicly restorable by everyone, which makes them public\. Amazon EBS snapshots should not be publicly restorable by everyone unless you explicitly allow it, to avoid accidental exposure of your company’s sensitive data\.

You should also ensure that permission to change Amazon EBS configurations are restricted to authorized AWS accounts only\. Learn more about managing Amazon EBS snapshot permissions in the [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modifying-snapshot-permissions.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modifying-snapshot-permissions.html)\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-ec2-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
Amazon EBS snapshots are used to back up the data on your Amazon EBS volumes to Amazon S3 at a specific point in time\. They can be used to restore previous states of EBS volumes\.  
If an Amazon EBS snapshot stores cardholder data, it should not be publicly restorable by everyone\. This would violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
Amazon EBS snapshots are used to back up the data on your Amazon EBS volumes to Amazon S3 at a specific point in time\. They can be used to restore previous states of Amazon EBS volumes\.  
If an Amazon EBS snapshot stores cardholder data, it should not be publicly restorable by everyone\. This would violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
Amazon EBS snapshots are used to back up the data on your Amazon EBS volumes to Amazon S3 at a specific point in time, and can be used to restore previous states of EBS volumes\.  
If an Amazon EBS snapshot stores cardholder data, it should not be publicly restorable by everyone\. This would violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the internet\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restrict access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
Amazon EBS snapshots are used to back up the data on your Amazon EBS volumes to Amazon S3 at a specific point in time\. They can be used to restore previous states of Amazon EBS volumes\.  
If an Amazon EBS snapshot stores cardholder data, it should not be publicly restorable by everyone\. This may violate the requirement to ensure access to systems components is restricted to least privilege necessary, or a user’s need to know\.

### Remediation<a name="pcidss-ec2-1-remediation"></a>

**To make a public Amazon EBS snapshot private**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Elastic Block Store**, choose **Snapshots** and then select your public snapshot\.

1. Choose **Actions**, then choose **Modify permissions**

1. Choose **Private**

1. \(Optional\) Add AWS account numbers for authorized accounts to share your snapshot with\.

1. Choose **Save**

For more information about sharing an Amazon EBS snapshot, see the [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modifying-snapshot-permissions.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modifying-snapshot-permissions.html)\.

## \[PCI\.EC2\.2\] VPC default security group should prohibit inbound and outbound traffic<a name="pcidss-ec2-2"></a>

**Severity:** Medium

**Resource:** Amazon EC2 security group

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html)

**Parameters:** None

This control checks that the default security group of a VPC does not allow inbound or outbound traffic\.

It does not check for access restrictions for other security groups that are not default, and other VPC configurations\.

### Related PCI DSS requirements<a name="pcidss-ec2-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
If a service that is in scope for PCI DSS is associated with the default security group, the default rules for the security group will allow all outbound traffic\. The rules also allow all inbound traffic from network interfaces \(and their associated instances\) that are assigned to the same security group\.  
You should change the default security group rules setting to restrict inbound and outbound traffic\. Using the default might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
If a service that is in scope for PCI DSS is associated with the default security group, the default rules for the security group will allow all outbound traffic\. The rules also allow all inbound traffic from network interfaces \(and their associated instances\) that are assigned to the same security group\.  
You should change the default security group rules setting to restrict unauthorized inbound and outbound traffic\. Using the default may violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the internet\.

**PCI DSS 2\.1: Always change vendor\-supplied defaults and remove or disable unnecessary default accounts before installing a system on the network\.**  
If a service that is in scope for PCI DSS is associated with the default security group, the default rules for the security group will allow all outbound traffic\. The rules also allow all inbound traffic from network interfaces \(and their associated instances\) that are assigned to the same security group\.  
You should change the default security group rules setting to restrict inbound and outbound traffic\. Using the default may violate the requirement to remove or disable unnecessary default accounts\.

### Remediation<a name="pcidss-ec2-2-remediation"></a>

To remediate this issue, create new security groups and assign those security groups to your resources\. To prevent the default security groups from being used, remove their inbound and outbound rules\.

**To create new security groups and assign them to your resources**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Security groups**\. View the default security groups details to see the resources that are assigned to them\.

1. Create a set of least\-privilege security groups for the resources\. For details on how to create security groups, see [Creating a security group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#CreatingSecurityGroups) in the *Amazon VPC User Guide*\.

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the Amazon EC2 console, change the security group for the resources that use the default security groups to the least\-privilege security group you created\. See [Changing an instance's security groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#SG_Changing_Group_Membership) in the *Amazon VPC User Guide*\.

After you assign the new security groups to the resources, remove the inbound and outbound rules from the default security groups\. This ensures that the default security groups are not used\.

**To remove the rules from the default security group**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Security groups**\.

1. Select a default security group, and choose the **Inbound rules** tab\. Choose **Edit inbound rules**\. Then delete all of the inbound rules\. Choose **Save rules**\.

1. Repeat the previous step for each default security group\.

1. Select a default security group and choose the **Outbound rules** tab\. Choose **Edit outbound rules**\. Then delete all of the outbound rules\. Choose **Save rules**\.

1. Repeat the previous step for each default security group\.

For more information about working with security groups in Amazon VPC, see the [https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups)\.

## \[PCI\.EC2\.3\] Unused EC2 security groups should be removed<a name="pcidss-ec2-3"></a>

**Severity:** Low

**Resource: ** Amazon EC2 security group

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-security-group-attached-to-eni.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-security-group-attached-to-eni.html)

**Parameters:** None

This control helps you maintain an accurate asset inventory of needed security groups in your cardholder data environment \(CDE\)\. It does so by checking that security groups are attached to Amazon EC2 instances or to an ENI\. A failed finding indicates you may have unused Amazon EC2 security groups\.

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

1. In the navigation pane, under **Security**, choose **Security groups**\.

1. Select the check box for the security group to delete\.

1. From **Actions**, choose **Delete security group**\.

1. Choose **Delete**\. 

## \[PCI\.EC2\.4\] Unused EC2 EIPs should be removed<a name="pcidss-ec2-4"></a>

**Severity:** Low

**Resource:** EC2 EIP

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/eip-attached.html](https://docs.aws.amazon.com/config/latest/developerguide/eip-attached.html)

**Parameters:** None

This control checks whether Elastic IP addresses that are allocated to a VPC are attached to Amazon EC2 instances or in\-use elastic network interfaces \(ENIs\)\.

A failed finding indicates you may have unused Amazon EC2 EIPs\.

This will help you maintain an accurate asset inventory of EIPs in your cardholder data environment \(CDE\)\.

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

1. In the navigation pane, under **Network & Security**, choose **Elastic IPs**\. 

1. Choose the Elastic IP address, choose **Actions**, and then choose **Release Elastic IP address**\.

1. When prompted, choose **Release**\. 

For more information, see the information on releasing Elastic IP addresses in the [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-eips-releasing](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-eips-releasing)\.

## \[PCI\.EC2\.5\] Security groups should not allow ingress from 0\.0\.0\.0/0 to port 22<a name="pcidss-ec2-5"></a>

**Severity:** High

**Resource:** EC2 security group

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/restricted-ssh.html](https://docs.aws.amazon.com/config/latest/developerguide/restricted-ssh.html)

**Parameters:** None

This control checks whether security groups in use disallow unrestricted incoming SSH traffic\. 

It does not evaluate outbound traffic\. 

Note that security groups are stateful\. If you send a request from your instance, the response traffic for that request is allowed to flow in regardless of inbound security group rules\. Responses to allowed inbound traffic are allowed to flow out regardless of outbound rules\. To learn more about security groups, see [Security groups for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) in the *Amazon VPC User Guide*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-ec2-5-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1 \- Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
You might allow SSH traffic to your instances that are in your defined CDE\. If so, restrict the inbound SSH source from 0\.0\.0\.0/0 \(anywhere\) to a specific IP address or range\. Leaving unrestricted access to SSH might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1 \- Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
You might allow SSH traffic to your instances that are in your defined CDE\. If so, restrict the inbound SSH source from 0\.0\.0\.0/0 \(anywhere\) to a specific IP address or range\. Leaving unrestricted access to SSH might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 2\.2\.2 Enable only necessary services, protocols, daemons, etc\., as required for the function of the system\.**  
You might allow SSH traffic to your instances that are in your defined CDE\. If so, restrict the inbound SSH source from 0\.0\.0\.0/0 \(anywhere\) to a specific IP address or range as required for the function of the security group\. Within a CDE, a security group could be considered a system component, which should be hardened appropriately\. Leaving unrestricted access to SSH might violate the requirement to enable only the necessary services, protocols, daemons, etc\., that are required for the function of the system\.

### Remediation<a name="pcidss-ec2-5-remediation"></a>

Perform the following steps for each security group associated with a VPC\.

**To remove access to port 22 from a security group**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, under **Security**, choose **Security groups**\.

1. Select a security group\.

1. In the bottom section of the page, choose **Inbound rules**\.

1. Choose **Edit inbound rules**\.

1. Identify the rule that allows access through port 22 and then choose the **X** to remove it\.

1. Choose **Save rules**\.

## \[PCI\.EC2\.6\] VPC flow logging should be enabled in all VPCs<a name="pcidss-ec2-6"></a>

**Severity:** Medium

**Resource:** EC2 VPC

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html)

**Parameters: **
+ `trafficType` – `REJECT`

This control checks whether VPC flow logs are found and enabled for VPCs\. The traffic type is set to `REJECT`\.

With VPC Flow Logs, you can capture information about the IP address traffic to and from network interfaces in your VPC\. After you create a flow log, you can use CloudWatch Logs to view and retrieve the log data\.

Security Hub recommends that you enable flow logging for packet rejects for VPCs\. Flow logs provide visibility into network traffic that traverses the VPC\. They can detect anomalous traffic and provide insight into security workflows\.

By default, the record includes values for the different components of the IP address flow, including the source, destination, and protocol\. For more information and descriptions of the log fields, see [VPC Flow Logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html) in the *Amazon VPC User Guide*\.

### Related PCI DSS requirements<a name="pcidss-ec2-6-requirements"></a>

This control is related to the following PCI DSS requirements\.

**PCI DSS 10\.3\.3 Verify date and time stamp is included in log entries\.**  
By enabling VPC flow logging for your VPC, you can identify the date and time of a log entry\. The event date and time are recorded in the start and end fields\. The values are displayed in Unix seconds\.

**PCI DSS 10\.3\.4 Verify success or failure indication is included in log entries\.**  
By enabling VPC flow logging for your VPC, you can identify the type of event that occurred\. The type of event is recorded in the action field, and can be either `ACCEPT` or `REJECT`\.

**PCI DSS 10\.3\.5 Verify origination of event is included in log entries\.**  
By enabling VPC flow logging for your VPC, you can verify the origin of an event\. The event origin is recorded in the `pkt-srcaddr`, `srcaddr`, and `srcport` fields\. These fields show the source IP address and source port of the traffic\. 

**PCI DSS 10\.3\.6 Verify identity or name of affected data, system component, or resources is included in log entries\.**  
By enabling VPC flow logging for your VPC, you can verify the identity or name of affected data, system components, or resources\. The `pkt-dstaddr`, `dstaddr`, and `dstport` fields show the destination IP address and destination port of the traffic\.

### Remediation<a name="pcidss-ec2-6-remediation"></a>

To remediate this issue, enable VPC flow logging\.

**To enable VPC flow logging**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, under **Virtual Private Cloud**, choose **Your VPCs**\.

1. Select a VPC to update\.

1. At the bottom of the page, choose **Flow Logs**\.

1. Choose **Create flow log**\.

1. For **Filter**, choose **Reject**\.

1. For **Destination log group**, choose the log group to use\.

1. If you chose **CloudWatch Logs** for your destination log group, for **IAM role**, choose the IAM role to use\.

1. Choose **Create**\.

## \[PCI\.ELBV2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS<a name="pcidss-elbv2-1"></a>

**Severity:** Medium

**Resource:** AwsElbv2LoadBalancer

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html](https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html) 

**Parameters:** None

This control checks whether HTTP to HTTPS redirection is configured on all HTTP listeners of Application Load Balancers\. The control fails if any of the HTTP listeners of Application Load Balancers do not have HTTP to HTTPS redirection configured\.

Before you start to use your Application Load Balancer, you must add one or more listeners\. A listener is a process that uses the configured protocol and port to check for connection requests\. Listeners support both the HTTP and HTTPS protocols\. You can use an HTTPS listener to offload the work of encryption and decryption to your load balancer\. To enforce encryption in transit, you should use redirect actions with Application Load Balancers to redirect client HTTP requests to an HTTPS request on port 443\.

To learn more, see [Listeners for your Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-listeners.html) in *User Guide for Application Load Balancers*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-elbv2-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 2\.3 Encrypt all nonconsole administrative access using strong cryptography\.**  
If you use Application Load Balancers with an HTTP listener, ensure that the listener is redirected to HTTPS for any nonconsole administrative access\. Allowing unencrypted authentication over HTTP for administrators of the cardholder data environment might violate the requirement to encrypt all nonconsole administrative access using strong cryptography\.

**PCI DSS 4\.1 Use strong cryptography and security protocols to safeguard sensitive cardholder data during transmission over open, public networks\.**  
If you use Application Load Balancers with an HTTP listener, ensure that the listener is redirected to HTTPS for any transmissions of cardholder data\. Allowing unencrypted transmissions of cardholder data might violate the requirement to use strong cryptography and security protocols to safeguard sensitive cardholder data during transmission over open, public networks\.

### Remediation<a name="pcidss-elbv2-1-remediation"></a>

To remediate this issue, you redirect HTTP request to HTTPS\.

**To redirect HTTP requests to HTTPS on an Application Load Balancer**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Load Balancing**, choose **Load balancers**\.

1. Choose an Application Load Balancer\.

1. Choose **Listeners**\.

1. Select the check box for an HTTP listener \(port 80 TCP\) and then choose **Edit**\.

1. If there is an existing rule, you must delete it\. Otherwise, choose **Add action** and then choose **Redirect to\.\.\.**\.

1. Choose **HTTPS** and then enter **443**\.

1. Choose the check mark in a circle symbol and then choose **Update**\.

## \[PCI\.ES\.1\] Amazon Elasticsearch Service domains should be in a VPC<a name="pcidss-es-1"></a>

**Severity: ** Critical

**Resource: ** Amazon ES domain 

**AWS Config rule: ** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-in-vpc-only.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-in-vpc-only.html)

**Parameters:** None

This control checks whether Amazon Elasticsearch Service domains are in a VPC\.

It does not evaluate the VPC subnet routing configuration to determine public reachability\.

This AWS control also does not check whether the Amazon ES resource\-based policy permits public access by other accounts or external entities\. You should ensure that Amazon ES domains are not attached to public subnets\. See [Resource\-based policies](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-ac.html#es-ac-types-resource) in the *Amazon Elasticsearch Service Developer Guide*\.

You should also ensure that your VPC is configured according to the recommended best practices\. See [Security best practices for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html) in the *Amazon VPC User Guide*\.

### Related PCI DSS requirements<a name="pcidss-es-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
If your Amazon ES clusters contain cardholder data, the Amazon ES domains should be placed in a VPC\. Doing so enables secure communication between Amazon ES and other services within the VPC without the need for an internet gateway, NAT device, or VPN connection port\.  
This method is used to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If your Amazon ES clusters contain cardholder data, the Amazon ES domains should be placed in a VPC\. Doing so enables secure communication between Amazon ES and other services within the VPC without the need for an internet gateway, NAT device, or VPN connection port\.  
This method is used to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound internet traffic to IP addresses within the DMZ\.**  
If your Amazon ES clusters contain cardholder data, the Amazon ES domains should be placed in a VPC, which enables secure communication between Amazon ES and other services within the VPC without the need for an internet gateway, NAT device, or VPN connection port\.  
This method is used to limit inbound internet traffic to IP addresses within the DMZ\.  
You can also use a resource\-based policy and specify an IP condition for restricting access based on source IP addresses\. See the blog post [How to control access to your Amazon Elasticsearch Service domain](http://aws.amazon.com/blogs/security/how-to-control-access-to-your-amazon-elasticsearch-service-domain/)\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
If your Amazon ES clusters contain cardholder data, the Amazon ES domains should be placed in a VPC, which enables secure communication between Amazon ES and other services within the VPC without the need for an internet gateway, NAT device, or VPN connection port\.  
This method is used to block unauthorized outbound traffic from the cardholder data environment to the internet\.

**PCI DSS 1\.3\.6: Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If your Amazon ES clusters contain cardholder data, the Amazon ES domains should be placed in a VPC\. Doing so enables secure communication between Amazon ES and other services within the VPC without the need for an internet gateway, NAT device, or VPN connection port\.  
This method is used to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

### Remediation<a name="pcidss-es-1-remediation"></a>

If you create a domain with a public endpoint, you cannot later place it within a VPC\. Instead, you must create a new domain and migrate your data\.

The reverse is also true\. If you create a domain within a VPC, it cannot have a public endpoint\. Instead, you must either [create another domain](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createupdatedomains.html#es-createdomains) or disable this control\.

See the information on migrating from public access to VPC access in the [https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-vpc.html#es-migrating-public-to-vpc](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-vpc.html#es-migrating-public-to-vpc)\.

## \[PCI\.ES\.2\] Amazon Elasticsearch Service domains should have encryption at rest enabled<a name="pcidss-es-2"></a>

**Severity:** Medium

**Resource:** Amazon ES domain

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-encrypted-at-rest.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-encrypted-at-rest.html)

**Parameters:** None

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

## \[PCI\.GuardDuty\.1\] GuardDuty should be enabled<a name="pcidss-guardduty-1"></a>

**Severity:** Medium

**Resource:** AwsAccount

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html](https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html)

**Parameters:** None

This control checks whether Amazon GuardDuty is enabled in your AWS account and Region\. 

While GuardDuty can be effective against attacks that an intrusion detection system would typically protect, it might not be a complete solution for every environment\. This rule also does not check for the generation of alerts to personnel\. For more information about GuardDuty, see the [https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(Bahrain\)
 AWS GovCloud \(US\-East\)

### Related PCI DSS requirements<a name="pcidss-guardduty-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 11\.4 Use intrusion\-detection and/or intrusion\-prevention techniques to detect and/or prevent intrusions into the network\. **  
GuardDuty can help to meet requirement 11\.4 by monitoring traffic at the perimeter of the cardholder data environment and all critical points within it\. It can also keep all intrusion\-detection engines, baselines, and signatures up to date\. Findings are generated from GuardDuty\. You can send these alerts to personnel using Amazon CloudWatch\. See [Creating custom responses to GuardDuty findings with Amazon CloudWatch Events](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings_cloudwatch.html) in the *Amazon GuardDuty User Guide*\. Not enabling GuardDuty in your AWS account might violate the requirement to use intrusion\-detection and/or prevention techniques to prevent intrusions into the network\.

### Remediation<a name="pcidss-guardduty-1-remediation"></a>

To remediate this issue, you enable GuardDuty\.

**To enable GuardDuty**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Get Started**\.

1. Choose **Enable GuardDuty**\.

## \[PCI\.IAM\.1\] IAM root user access key should not exist<a name="pcidss-iam-1"></a>

**Severity: ** Critical

**Resource: ** Account 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html)

**Parameters:** None

This control checks whether user access keys exist for the root user\.

**Note**  
This control is not supported in Africa \(Cape Town\)\.

### Related PCI DSS requirements<a name="pcidss-iam-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 2\.1: Always change vendor\-supplied defaults and remove or disable unnecessary default accounts before installing a system on the network\.**  
The AWS account root user is the most privileged AWS user\. AWS access keys provide programmatic access to a given account\.  
No access keys should be created for the root user, as this may violate the requirement to remove or disable unnecessary default accounts\.

**PCI DSS 2\.2: Develop configuration standards for all system components\. Assure that these standards address all known security vulnerabilities and are consistent with industry\-accepted system hardening standards\.**  
The root user is the most privileged AWS user\. AWS access keys provide programmatic access to a given account\.  
No access keys should be created for the root user, as this may violate the requirement to implement system hardening configurations\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
The root user is the most privileged AWS user\. AWS access keys provide programmatic access to a given account\.  
No access keys should be created for the root user\. Doing so might violate the requirement to ensure access to systems components is restricted to least privilege necessary, or a user’s need to know\.

### Remediation<a name="pcidss-iam-1-remediation"></a>

**To deactivate or delete access keys**

1. Log in to your account using the root user credentials\.

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

**Parameters:** None

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

**Parameters:** None

This control checks whether the default version of AWS Identity and Access Management policies \(also known as customer managed policies\) do not have administrator access with a statement that has `"Effect": "Allow" with "Action": "*"` over `"Resource": "*"`\.

It only checks for the [customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies) that you created, but does not check for full access to individual services, such as "`S3:*`"\.

It does not check for [inline and AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies)\.

### Related PCI DSS requirements<a name="pcidss-iam-3-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restrict access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
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

**Parameters:** None

This control checks whether your AWS account is enabled to use multi\-factor authentication \(MFA\) hardware device to sign in with root user credentials\.

It does not check whether you are using virtual MFA\.

To address PCI DSS requirement 8\.3\.1, you can choose between hardware MFA \(this control\) or virtual MFA \([\[PCI\.IAM\.5\] Virtual MFA should be enabled for the root user](#pcidss-iam-5)\)\.

**Note**  
This control is not supported in AWS GovCloud \(US\-East\) or AWS GovCloud \(US\-West\)\.

### Related PCI DSS requirements<a name="pcidss-iam-4-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 8\.3\.1: Incorporate multi\-factor authentication for all non\-console access into the cardholder data environment \(CDE\) for personnel with administrative access\.**  
The root user is the most privileged user in an account\.  
MFA adds an extra layer of protection on top of a user name and password\. If users with administrative privileges are accessing the cardholder data environment over a network interface rather than via a direct, physical connection to the system component, and are not physically in front of the machine they are administering, MFA is required\.  
Enabling hardware MFA is a method used to incorporate multi\-factor authentication \(MFA\) for all nonconsole administrative access

### Remediation<a name="pcidss-iam-4-remediation"></a>

**To enable hardware\-based MFA for the root account**

1. Log in to your account using the root user credentials\.

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

**Parameters:** None

This control checks whether users of your AWS account require a multi\-factor authentication \(MFA\) device to sign in with root user credentials\.

It does not check whether you are using hardware MFA\.

To address PCI DSS requirement 8\.3\.1, you can choose between virtual MFA \(this control\) or hardware MFA \([\[PCI\.IAM\.4\] Hardware MFA should be enabled for the root user](#pcidss-iam-4)\)\.

**Note**  
This control is not supported in AWS GovCloud \(US\-East\) or AWS GovCloud \(US\-West\)\.

### Related PCI DSS requirements<a name="pcidss-iam-5-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 8\.3\.1: Incorporate multi\-factor authentication for all non\-console access into the cardholder data environment \(CDE\) for personnel with administrative access\.**  
The root user is the most privileged user in an account\.  
MFA adds an extra layer of protection on top of a user name and password\. If users with administrative privileges are accessing the cardholder data environment, and are not physically in front of the machine they are administering, MFA is required\.  
Enabling virtual MFA is a method used to incorporate multi\-factor authentication \(MFA\) for all nonconsole administrative access\.

### Remediation<a name="pcidss-iam-5-remediation"></a>

**To enable MFA for the root account**

1. Log in to your account using the root user credentials\.

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

**Parameters:** None

This control checks whether the IAM users have multi\-factor authentication \(MFA\) enabled\.

### Related PCI DSS requirements<a name="pcidss-iam-6-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 8\.3\.1: Incorporate multi\-factor authentication for all non\-console access into the cardholder data environment \(CDE\) for personnel with administrative access\.**  
Enabling MFA for all IAM users is a method used to incorporate multi\-factor authentication \(MFA\) for all nonconsole administrative access\.

### Remediation<a name="pcidss-iam-6-remediation"></a>

**To configure MFA for a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the user name of the user to configure MFA for\.

1. Choose **Security credentials** and then choose **Manage** next to **Assigned MFA device**\.

1. Follow the **Manage MFA Device** wizard to assign the type of device appropriate for your environment\. 

To learn how to delegate MFA setup to users, the AWS Security Blog post [How to Delegate Management of Multi\-Factor Authentication to AWS IAM Users](http://aws.amazon.com/blogs/security/how-to-delegate-management-of-multi-factor-authentication-to-aws-iam-users/)\. 

## \[PCI\.IAM\.7\] IAM user credentials should be disabled if not used within a predefined number of days<a name="pcidss-iam-7"></a>

**Severity:** Medium

**Resource:** IAM User

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html)

**Parameters:** 
+ `maxCredentialUsageAge`: 90 \(days\)

This control checks whether your IAM users have passwords or active access keys that have not been used within a specified number of days\. The default is 90 days\. 

Security Hub strongly recommends that you do not generate and remove all access keys in your account\. Instead, the recommended best practice is to either create one or more IAM roles or to use [federation](http://aws.amazon.com/identity/federation/)\. These practices allow your users to use their existing corporate credentials to sign in to the AWS Management Console console and AWS CLI\.

Each approach has its use cases\. Federation is generally better for enterprises that have an existing central directory or who plan to need more than the current quota of IAM users\. Applications running outside of an AWS environment need access keys for programmatic access to AWS resources\.

However, if the resources that need programmatic access run inside AWS, the best practice is to use IAM roles\. You can use roles to grant a resource access without hardcoding an access key ID and secret access key into the configuration\.

To learn more about protecting your access keys and account, see [Best practices for managing AWS access keys](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html) in the *AWS General Reference*\. Also see the blog post [Guidelines for protecting your AWS account while using\-programmatic access](http://aws.amazon.com/blogs/security/guidelines-for-protecting-your-aws-account-while-using-programmatic-access/)\.

If you already have an access key, we recommend that you remove or deactivate unused user credentials that are inactive for 90 days or longer\.

This control only checks for inactive passwords or active access keys\. It does not disable the account from use after 90 days\. Customers are responsible for taking action and disabling the unused credentials\.

### Related PCI DSS requirements<a name="pcidss-iam-7-requirements"></a>

This control is related to the following PCI DSS requirements\.

**PCI DSS 8\.1\.4 Remove/disable inactive user accounts within 90 days\.**  
If you use IAM passwords or access keys, ensure that they are monitored for use, and disabled if not used for 90 days\. Allowing IAM user accounts to remain active with unused credentials might violate the requirement to remove/disable inactive user accounts within 90 days\.

### Remediation<a name="pcidss-iam-7-remediation"></a>

To get some of the information that you need to monitor accounts for dated credentials, use the IAM console\. For example, when you view users in your account, there are columns for **Access key age**, **Password age**, and **Last activity**\. If the value in any of these columns is greater than 90 days, make the credentials for those users inactive\.

You can also use credential reports to monitor user accounts and identify those with no activity for 90 or more days\. You can download credential reports in `.csv` format from the IAM console\. For more information about credential reports, see [Getting credential reports for your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html#getting-credential-reports-console) in the *IAM User Guide*\.

After you identify the inactive accounts or unused credentials, use the following steps to disable them\.

**To disable inactive accounts or unused IAM credentials**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Under **Access management**, choose **Users**\.

1. Choose the name of the user that has credentials older than 90 days\.

1. Choose **Security credentials**\. Choose **Make inactive** for all sign\-in credentials and access keys that were not used in 90 days or more\.

## \[PCI\.IAM\.8\] Password policies for IAM users should have strong configurations<a name="pcidss-iam-8"></a>

**Severity:** Medium

**Resource:** AWS Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Parameters:** None

This control checks whether the account password policy for IAM users uses the following minimum PCI DSS configurations\.
+ `RequireUppercaseCharacters` – Require at least one uppercase character in password\. \(Default = `true`\)
+ `RequireLowercaseCharacters` – Require at least one lowercase character in password\. \(Default = `true`\)
+ `RequireNumbers` – Require at least one number in password\. \(Default = `true`\)
+ `MinimumPasswordLength` – Password minimum length\. \(Default = 7 or longer\)
+ `PasswordReusePrevention` – Number of passwords before allowing reuse\. \(Default = 4\)
+ MaxPasswordAge – Number of days before password expiration\. \(Default = 90\)

### Related PCI DSS requirements<a name="pcidss-iam-8-requirements"></a>

This control is related to the following PCI DSS requirements\.

**PCI DSS 8\.1\.4: Remove/disable inactive user accounts within 90 days\.**  
If you have IAM users in your AWS account, you should configure the IAM password policy appropriately\. Not securing IAM users' passwords might violate the requirement to remove or disable inactive user accounts within 90 days\. By default, the `MaxPasswordAge` parameter is set to 90 days\. After their password expires, IAM users cannot access their account until the password is changed, which disables the user\.

**PCI DSS 8\.2\.3: Passwords/passphrases must meet the following: Require a minimum length of at least seven characters and Contain both numeric and alphabetic characters\.**  
If you have IAM users in your AWS account, the IAM password policy should be configured appropriately\. Not securing IAM users' passwords might violate the requirement for a password to have a minimum length of at least seven characters\. It might also violate the requirements to contain both numeric and alphabetic characters\. By default, `MinimumPasswordLength` is `7`, `RequireUppercaseCharacters` is `true`, and `RequireLowercaseCharacters` is `true`\.

**PCI DSS 8\.2\.4: Change user passwords/passphrases at least once every 90 days\.**  
If you have IAM users in your AWS account, the IAM password policy should be configured appropriately\. Not securing IAM users' passwords might violate the requirement to change user passwords or passphrases at least once every 90 days\. By default, the `MaxPasswordAge` parameter is set to 90 days\. After the password expires, the IAM user cannot access the account until the password is changed\.

**PCI DSS 8\.2\.5: Do not allow an individual to submit a new password/passphrase that is the same as any of the last four passwords/passphrases he or she has used\.**  
If you have IAM users in your AWS account, the IAM password policy should be configured appropriately\. Not securing IAM users' passwords might violate the requirement to not allow individuals to submit a new password or passphrase that is the same as any of their previous four passwords or passphrases\. By default, `PasswordReusePrevention` is set to `4`, which prevents users from reusing their last four passwords\.

### Remediation<a name="pcidss-iam-8-remediation"></a>

You can use the IAM console to modify the password policy\.

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Under **Access management**, choose **Account settings**\.

1. Select **Prevent password reuse**\. For **Number of passwords to remember**, enter **24**\.

1. Choose **Change password policy**\.

1. Select **Require at least one uppercase letter from Latin alphabet \(A\-Z\)**\.

1. Select **Require at least one lowercase letter from Latin alphabet \(a\-z\)**\.

1. Select **Require at least one non\-alphanumeric character \(\!@\#$%^&\*\(\)\_\+\-=\[\]\{\}\|'\)**\.

1. Select **Require at least one number**\.

1. For **Enforce minimum password length**, enter **14**\.

1. Select **Enable password expiration**\. For **Expire passwords in day\(s\)**, enter **90**\. 

1. Choose **Save changes**\.

## \[PCI\.KMS\.1\] Customer master key \(CMK\) rotation should be enabled<a name="pcidss-kms-1"></a>

**Severity:** Medium

**Resource: ** AWS KMS key 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html)

**Parameters:** None

This control checks that key rotation is enabled for each customer master key \(CMK\)\. It does not check CMKs that have imported key material\.

You should ensure keys that have imported material and those that are not stored in AWS KMS are rotated\. AWS managed customer master keys are rotated once every 3 years\.

### Related PCI DSS requirements<a name="pcidss-kms-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 3\.6\.4: Cryptographic keys should be changed once they have reached the end of their cryptoperiod\.**  
While PCI DSS does not specify the time frame for cryptoperiods, if key rotation is enabled, rotation occurs annually by default\.  
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

**Parameters:** None

This control checks whether the Lambda function resource\-based policy prohibits public access\.

It does not check for access to the Lambda function by internal principals, such as IAM roles\. You should ensure that access to the Lambda function is restricted to authorized principals only by using least privilege Lambda resource\-based policies\.

For more information about using resource\-based policies for AWS Lambda, see the [https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html)\.

### Related PCI DSS requirements<a name="pcidss-lambda-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
If you use a Lambda function that is in scope for PCI DSS, the function should not be publicly accessible\. A publicly accessible function might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use a Lambda function that is in scope for PCI DSS, the function should not be publicly accessible\. A publicly accessible function might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound internet traffic to IP addresses within the DMZ\.**  
If you use a Lambda function that is in scope for PCI DSS, the function should not be publicly accessible\. A publicly accessible function might violate the requirement to limit inbound internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
If you use a Lambda function that is in scope for PCI DSS, the function must not be publicly accessible\. A publicly accessible function might violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the internet\.

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

1. Navigate to **Functions** and then select your publicly accessible Lambda function\.

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

**Parameters:** None

This control checks whether a Lambda function is in a VPC\.

It does not evaluate the VPC subnet routing configuration to determine public reachability\. 

Note that if Lambda@Edge is found in the account, then this control generates failed findings\. To prevent these findings, you can disable this control\.

### Related PCI DSS requirements<a name="pcidss-lambda-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
By default, Lambda runs your functions in a secure default VPC with access to AWS services and the internet\.  
If you use a Lambda function that is in scope for PCI DSS, the function can be configured to use a VPC endpoint\. This would allow you to connect to your Lambda function from within a VPC without internet access\. This method is used to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
By default, Lambda runs your functions in a secure default VPC with access to AWS services and the internet\.  
If you use a Lambda function that is in scope for PCI DSS, the function can be configured to use a VPC endpoint\. This allows you to connect to your Lambda function from within a VPC without internet access\. This is a method used to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound internet traffic to IP addresses within the DMZ\.**  
By default, Lambda runs your functions in a secure default VPC with access to AWS services and the internet\.  
If you use a Lambda function that is in scope for PCI DSS, the function can be configured to use a VPC endpoint\. This allows you to connect to your Lambda function from within a VPC without internet access\. This is a method used to limit inbound internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
By default, Lambda runs your functions in a secure default VPC with access to AWS services and the internet\.  
If you use a Lambda function that is in scope for PCI DSS, the function can be configured to use a VPC endpoint\. This allows you to connect to your Lambda function from within a VPC without internet access\. This is a method used to block unauthorized outbound traffic from the cardholder data environment to the internet\.

### Remediation<a name="pcidss-lambda-2-remediation"></a>

**To configure a function to connect to private subnets in a virtual private cloud \(VPC\) in your account**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. Navigate to **Functions** and then select your Lambda function\.

1. Scroll to **Network** and then select a VPC with the connectivity requirements of the function\.

1. To run your functions in high availability mode, Security Hub recommends that you choose at least two subnets\.

1. Choose at least one security group that has the connectivity requirements of the function\.

1. Choose **Save**\.

For more information see the section on configuring a Lambda function to access resources in a VPC in the [https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html)\.

## \[PCI\.RDS\.1\] RDS snapshots should prohibit public access<a name="pcidss-rds-1"></a>

**Severity:** Critical

**Resource: ** Amazon RDS DB snapshot

**AWS Config rule: ** [https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html)

**Parameters:** None

This control checks whether Amazon RDS DB snapshots prohibit access by other accounts\. You should also ensure that access to the snapshot and permission to change Amazon RDS configuration is restricted to authorized principals only\.

To learn more about sharing DB snapshots in Amazon RDS, see the [https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html)\.

Note that if the configuration is changed to allow public access, the AWS Config rule may not be able to detect the change for up to 12 hours\. Until the AWS Config rule detects the change, the check passes even though the configuration violates the rule\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-rds-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
RDS snapshots are used to back up the data on your RDS instances at a specific point in time\. They can be used to restore previous states of RDS instances\.  
If an RDS snapshot stores cardholder data, the RDS snapshot should not be shared by other accounts\. Sharing the RDS snapshot would allow other accounts to restore an RDS instance from the snapshot\. Allowing this so might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
RDS snapshots are used to back up the data on your RDS instances at a specific point in time\. They can be used to restore previous states of RDS instances\.  
If an RDS snapshot stores cardholder data, the RDS snapshot should not be shared by other accounts\. Sharing the RDS snapshot would allow other accounts to restore an RDS instance from the snapshot\. Allowing this might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
RDS snapshots are used to back up the data on your RDS instances at a specific point in time\. They can be used to restore previous states of RDS instances\.  
If an RDS snapshot stores cardholder data, the RDS snapshot should not be shared by other accounts\. Sharing the RDS snapshot would allow other accounts to restore an RDS instance from the snapshot\. Allowing this might violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the internet\.

**PCI DSS 1\.3\.6: Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
RDS snapshots are used to back up the data on your RDS instances at a specific point in time\. They can be used to restore previous states of RDS instances\.  
If an RDS snapshot stores cardholder data, the RDS snapshot should not be shared by other accounts\. Sharing the RDS snapshot would allow other accounts to restore an RDS instance from the snapshot\. Allowing this might violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to "deny all" unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
RDS snapshots are used to back up the data on your RDS instances at a specific point in time\. They can be used to restore previous states of RDS instances\.  
If an RDS snapshot stores cardholder data, the RDS snapshot should not be shared by other accounts\. Sharing the RDS snapshot would allow other accounts to restore an RDS instance from the snapshot\. Allowing this might violate the requirement to ensure access to systems components that contain cardholder data is restricted to least privilege necessary, or a user's need to know\.

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

**Parameters:** None

This control checks whether RDS instances are publicly accessible by evaluating the `publiclyAccessible` field in the instance configuration item\. The value of `publiclyAccessible` indicates whether the DB instance is publicly accessible\. When the DB instance is publicly accessible, it is an Internet\-facing instance with a publicly resolvable DNS name, which resolves to a public IP address\. When the DB instance isn't publicly accessible, it is an internal instance with a DNS name that resolves to a private IP address\.

The control does not check VPC subnet routing settings or the Security Group rules\. You should also ensure VPC subnet routing does not allow public access, and that the security group inbound rule associated with the RDS instance does not allow unrestricted access \(0\.0\.0\.0/0\)\. You should also ensure that access to your RDS instance configuration is limited to only authorized users by restricting users' IAM permissions to modify RDS instances settings and resources\.

For more information, see [Hiding a DB instance in a VPC from the Internet](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.Hiding) in the *Amazon RDS User Guide*\.

### Related PCI DSS requirements<a name="pcidss-rds-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
If you use an RDS instance that is in scope for PCI DSS, the RDS instance should not be publicly accessible\. Allowing this might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use an RDS instance to store cardholder data, the RDS instance should not be publicly accessible\. Allowing this might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound internet traffic to IP addresses within the DMZ\.**  
If you use an RDS instance to store cardholder data, the RDS instance should not be publicly accessible as this might violate the requirement to limit inbound internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
If you use an RDS instance to store cardholder data, the RDS instance should not be publicly accessible\. Allowing this might violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the internet\.

**PCI DSS 1\.3\.6: Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If you use an RDS instance to store cardholder data, the RDS instance should not be publicly accessible\. Allowing this may violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

**PCI DSS 7\.2\.1: Establish an access control system\(s\) for systems components that restricts access based on a user’s need to know, and is set to “deny all” unless specifically allowed\. This access control system\(s\) must include the following: Coverage of all system components\.**  
If you use an RDS instance to store cardholder data, the RDS instance should not be publicly accessible, as this may violate the requirement to ensure access to systems components that contain cardholder data is restricted to least privilege necessary, or a user’s need to know\.

### Remediation<a name="pcidss-rds-2-remediation"></a>

**To remove public access for Amazon RDS Databases**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Navigate to **Databases** and then choose your public database\.

1. Choose **Modify**\.

1. Scroll to **Network & Security**\.

1. For **Public accessibility**, choose **No**\.

1. Scroll to the bottom and then choose **Continue**\.

1. Under **Scheduling of modifications**, choose **Apply immediately**\.

1. Choose **Modify DB Instance**\.

For more information about working with a DB Instance in a VPC, see the [https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html)\.

## \[PCI\.Redshift\.1\] Amazon Redshift clusters should prohibit public access<a name="pcidss-redshift-1"></a>

**Severity: ** Critical

**Resource:** Amazon Redshift cluster

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-public-access-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-public-access-check.html)

**Parameters:** None

This control checks whether Amazon Redshift clusters are publicly accessible by evaluating the `publiclyAccessible` field in the cluster configuration item\.

### Related PCI DSS requirements<a name="pcidss-redshift-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
If you use an Amazon Redshift cluster to store cardholder data, the cluster should not be publicly accessible\. Allowing this might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use an Amazon Redshift cluster to store cardholder data, the cluster should not be publicly accessible\. Allowing this might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound internet traffic to IP addresses within the DMZ\.**  
If you use an Amazon Redshift cluster to store cardholder data, the cluster should not be publicly accessible, as this may violate the requirement to limit inbound internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
If you use an Amazon Redshift cluster to store cardholder data, the cluster should not be publicly accessible\. Allowing this may violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the internet\.

**PCI DSS 1\.3\.6: Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If you use an Amazon Redshift cluster to store cardholder data, the cluster should not be publicly accessible\. Allowing this might violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

### Remediation<a name="pcidss-redshift-1-remediation"></a>

**To disable public access for an Amazon Redshift cluster**

1. Open the Amazon Redshift console at [https://console\.aws\.amazon\.com/redshift/](https://console.aws.amazon.com/redshift/)\.

1. On the navigation pane, choose **Clusters** and then select your public Amazon Redshift cluster\.

1. From the **Cluster** drop\-down menu, choose **Modify cluster**\.

1. In **Publicly accessible**, choose **No**\.

1. Choose **Modify**\.

For more information about creating a cluster in a VPC, see the [https://docs.aws.amazon.com/redshift/latest/mgmt/getting-started-cluster-in-vpc.html](https://docs.aws.amazon.com/redshift/latest/mgmt/getting-started-cluster-in-vpc.html)\.

## \[PCI\.S3\.1\] S3 buckets should prohibit public write access<a name="pcidss-s3-1"></a>

**Severity:** Critical

**Resource:** S3 bucket

**AWS Config rule: **[https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html)

**Parameters:** None

This control checks whether your S3 buckets allow public write access by evaluating the Block Public Access settings, the bucket policy, and the bucket access control list \(ACL\)\.

It does not check for write access to the bucket by internal principals, such as IAM roles\. You should ensure that access to the bucket is restricted to authorized principals only\.

### Related PCI DSS requirements<a name="pcidss-s3-1-requirements"></a>

This control is related to the following PCI DSS requirements:

** PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public write access\. Allowing public write access might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public write access\. Allowing public write access might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.  
Unless you explicitly require everyone on the internet to be able to write to your S3 bucket, you should ensure that your S3 bucket is not publicly writable\.

**PCI DSS 1\.3\.2: Limit inbound internet traffic to IP addresses within the DMZ\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public write access\. Allowing public write access might violate the requirement to limit inbound internet traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4: Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public write access\. Allowing public write access might violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the internet\.

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

**Parameters:** None

This control checks whether your S3 buckets allow public read access by evaluating the Block Public Access settings, the bucket policy, and the bucket access control list \(ACL\)\.

Unless you explicitly require everyone on the internet to be able to write to your S3 bucket, you should ensure that your S3 bucket is not publicly writable\.

It does not check for read access to the bucket by internal principals, such as IAM roles\. You should ensure that access to the bucket is restricted to authorized principals only\.

### Related PCI DSS requirements<a name="pcidss-s3-2-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1: Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public read access\. Public read access might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1: Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public read access\. Public read access might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2: Limit inbound internet traffic to IP addresses within the DMZ\.**  
If you use an S3 bucket to store cardholder data, the bucket should prohibit public read access\. Public read access might violate the requirement to limit inbound internet traffic to IP addresses within the DMZ\.

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

**Parameters:** None

This control checks whether S3 buckets have cross\-region replication enabled\.

PCI DSS does not require data replication or highly available configurations\. However, this check aligns with AWS best practices for this control\.

In addition to availability, you should consider other systems hardening settings\.

### Related PCI DSS requirements<a name="pcidss-s3-3-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 2\.2: Develop configuration standards for all system components\. Assure that these standards address all known security vulnerabilities and are consistent with industry\-accepted system hardening standards\.**  
Enabling cross\-Region replication on S3 buckets ensures that multiple versions of the data are available in different distinct Regions\. This allows you to store data at even greater distances, minimize latency, increase operational efficiency, and protect against DDoS and data corruption events\.  
This is one method used to implement system hardening configuration\.

### Remediation<a name="pcidss-s3-3-remediation"></a>

**To enable S3 bucket replication**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the S3 bucket that does not have cross\-region replication enabled\.

1. Choose **Management**, then choose **Replication**\.

1. Choose **Add rule**\. If versioning is not already enabled, you are prompted to enable it\.

1. Choose your source bucket \- **Entire bucket**\.

1. Choose your destination bucket\. If versioning is not already enabled on the destination bucket for your account, you are prompted to enable it\.

1. Choose an IAM role\. For more information on setting up permissions for replication, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/setting-repl-config-perm-overview.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/setting-repl-config-perm-overview.html)\.

1. Enter a rule name, choose **Enabled** for the status, then choose **Next**\.

1. Choose **Save**\.

For more information about replication, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html)\.

## \[PCI\.S3\.4\] S3 buckets should have server\-side encryption enabled<a name="pcidss-s3-4"></a>

**Severity:** Medium

**Resource:** S3 bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html)

**Parameters:** None

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
   + To use keys that are managed by AWS KMS for default encryption, choose **AWS\-KMS**\. Then choose a master key from the list of the AWS KMS master keys that you have created\.

     Type the Amazon Resource Name \(ARN\) of the AWS KMS key to use\. You can find the ARN for your AWS KMS key in the IAM console, under **Encryption keys**\. Or, you can choose a key name from the drop\-down list\.
**Important**  
 If you use the AWS KMS option for your default encryption configuration, you are subject to the RPS \(requests per second\) limits of AWS KMS\. For more information about AWS KMS limits and how to request a limit increase, see the [https://docs.aws.amazon.com/kms/latest/developerguide/limits.html](https://docs.aws.amazon.com/kms/latest/developerguide/limits.html)\.

     For more information about creating an AWS KMS key, see the [https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html)\.

     For more information about using AWS KMS with Amazon S3, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html)\.

   When enabling default encryption, you might need to update your bucket policy\. For more information about moving from bucket policies to default encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy)\.

1. Choose **Save**\.

For more information about default S3 bucket encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html)\.

## \[PCI\.S3\.5\] S3 buckets should require requests to use Secure Socket Layer<a name="pcidss-s3-5"></a>

**Severity:** Medium

**Resource:** S3 Bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-ssl-requests-only.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-ssl-requests-only.html)

**Parameters:** None

This control checks whether Amazon S3 buckets have policies that require requests to use Secure Socket Layer \(SSL\)\. 

S3 buckets should have policies that require all requests \(`Action: S3:*`\) to only accept transmission of data over HTTPS in the S3 resource policy, indicated by the condition key `aws:SecureTransport`\.

This does not check the SSL or TLS version\. You should not allow early versions of SSL or TLS \(SSLv3, TLS1\.0\) per PCI DSS requirements\.

### Related PCI DSS requirements<a name="pcidss-s3-5-requirements"></a>

This control is related to the following PCI DSS requirements\.

PCI DSS 4\.1 Use strong cryptography and security protocols to safeguard sensitive cardholder data during transmission over open, public networks\.  
If you use S3 buckets to store cardholder data, ensure that bucket policies require that requests to the bucket only accept transmission of data over HTTPS\. For example, you could use the policy statement `"aws:SecureTransport": "false"` to deny any requests not accessed through HTTPS\. Allowing unencrypted transmissions of cardholder data might violate the requirement to use strong cryptography and security protocols to safeguard sensitive cardholder data during transmission over open, public networks\.

### Remediation<a name="pcidss-s3-5-remediation"></a>

To remediate this issue, update the permissions policy of the S3 bucket\.

**To configure an S3 bucket to deny nonsecure transport**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Navigate to the noncompliant bucket, and then choose the bucket name\.

1. Choose **Permissions**, then choose **Bucket Policy**\.

1. Add a similar policy statement to that in the policy below\. Replace `awsexamplebucket` with the name of the bucket you are modifying\.

   ```
   {
       "Id": "ExamplePolicy",
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "AllowSSLRequestsOnly",
               "Action": "s3:*",
               "Effect": "Deny",
               "Resource": [
                   "arn:aws:s3:::awsexamplebucket",
                   "arn:aws:s3:::awsexamplebucket/*"
               ],
               "Condition": {
                   "Bool": {
                        "aws:SecureTransport": "false"
                   }
               },
              "Principal": "*"
           }
       ]
   }
   ```

1. Choose **Save**\.

For more information, see the knowledge center article [What S3 bucket policy should I use to comply with the AWS Config rule s3\-bucket\-ssl\-requests\-only?](http://aws.amazon.com/premiumsupport/knowledge-center/s3-bucket-policy-for-config-rule/)\.

## \[PCI\.S3\.6\] S3 Block Public Access setting should be enabled<a name="pcidss-s3-6"></a>

**Severity:** Medium

**Resource:** S3 AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks.html)

**Parameters:**
+ `ignorePublicAcls`: `true`
+ `blockPublicPolicy`: `true`
+ `blockPublicAcls`: `true`
+ `restrictPublicBuckets`: `true`

This control checks whether the following public access block settings are configured at the account level\.
+ `ignorePublicAcls`: `true`, 
+ `blockPublicPolicy`: `true`
+ `blockPublicAcls`: `true`
+ `restrictPublicBuckets`: `true`

As an AWS best practice, S3 buckets should block public access\. Unless you explicitly require everyone on the internet to be able to access your S3 bucket, you should ensure that your S3 bucket is not publicly accessible\.

**Note**  
This control is not supported in Europe \(Milan\) or Middle East \(Bahrain\)\.

### Related PCI DSS requirements<a name="pcidss-s3-6-requirements"></a>

This control is related to the following PCI DSS requirements\.

**PCI DSS 1\.2\.1 \- Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
If you use S3 buckets to store cardholder data, ensure that the bucket does not allow public access\. Public access to your S3 bucket might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1 \- Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use S3 buckets to store cardholder data, ensure that the bucket does not allow public access\. Allowing public access to your S3 bucket might violate the requirement to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2 \- Limit inbound internet traffic to IP addresses within the DMZ\.**  
If you use S3 buckets to store cardholder data, ensure that the bucket does not allow public access\. Allowing public access to your S3 bucket might violate the requirement to limit inbound traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4 Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
If you use S3 buckets to store cardholder data, ensure that the bucket does not allow public access\. Allowing public access to your S3 bucket might violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the internet\.

**PCI DSS 1\.3\.6 Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If you use S3 buckets to store cardholder data, ensure that the bucket does not allow public access\. Allowing public access to your S3 bucket might violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

### Remediation<a name="pcidss-s3-6-remediation"></a>

**To enable Amazon S3 Block Public Access**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the navigation pane, choose **Block public access \(account settings\)**\.

1. Choose **Edit**\. Then select **Block *all* public access**\.

1. Choose **Save changes**\.

For more information, see [Using Amazon S3 block public access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service Developer Guide*\.

## \[PCI\.SageMaker\.1\] Amazon SageMaker notebook instances should not have direct internet access<a name="pcidss-sagemaker-1"></a>

**Severity:** High

**Resource:** SageMaker:NotebookInstance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/sagemaker-notebook-no-direct-internet-access.html](https://docs.aws.amazon.com/config/latest/developerguide/sagemaker-notebook-no-direct-internet-access.html)

**Parameters:** None

This control checks whether direct internet access is disabled for an SageMaker notebook instance\. To do this, it checks whether the `DirectInternetAccess` field is disabled for the notebook instance\. 

If you configure your SageMaker instance without a VPC, then by default direct internet access is enabled on your instance\. You should configure your instance with a VPC and change the default setting to **Disable — Access the internet through a VPC**\.

To train or host models from a notebook, you need internet access\. To enable internet access, make sure that your VPC has a NAT gateway and your security group allows outbound connections\. To learn more about how to connect a notebook instance to resources in a VPC, see [Connect a notebook instance to resources in a VPC](https://docs.aws.amazon.com/sagemaker/latest/dg/appendix-notebook-and-internet-access.html) in the *Amazon SageMaker Developer Guide*\.

You should also ensure that access to your SageMaker configuration is limited to only authorized users\. Restrict users' IAM permissions to modify SageMaker settings and resources\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
 AWS GovCloud \(US\-East\)

### Related PCI DSS requirements<a name="pcidss-sagemaker-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 1\.2\.1 \- Restrict inbound and outbound traffic to that which is necessary for the cardholder data environment \(CDE\), and specifically deny all other traffic\.**  
If you use SageMaker notebook instances within your CDE, ensure that the notebook instance does not allow direct internet access\. Allowing direct public access to your notebook instance might violate the requirement to allow only necessary traffic to and from the CDE\.

**PCI DSS 1\.3\.1 \- Implement a DMZ to limit inbound traffic to only system components that provide authorized publicly accessible services, protocols, and ports\.**  
If you use SageMaker notebook instances within your CDE, ensure that the notebook instance does not allow direct internet access\. Allowing direct public access to your notebook instance might violate the requirement to only allow access to system components that provide authorized publicly accessible services, protocols, and ports\.

**PCI DSS 1\.3\.2 \- Limit inbound internet traffic to IP addresses within the DMZ\.**  
If you use SageMaker notebook instances within your CDE, ensure that the notebook instance does not allow direct internet access\. Allowing direct public access to your notebook instance might violate the requirement to limit inbound traffic to IP addresses within the DMZ\.

**PCI DSS 1\.3\.4 Do not allow unauthorized outbound traffic from the cardholder data environment to the internet\.**  
If you use SageMaker notebook instances within your CDE, ensure that the notebook instance does not allow direct internet access\. Allowing direct public access to your notebook instance might violate the requirement to block unauthorized outbound traffic from the cardholder data environment to the internet

**PCI DSS 1\.3\.6 Place system components that store cardholder data \(such as a database\) in an internal network zone, segregated from the DMZ and other untrusted networks\.**  
If you use SageMaker notebook instances, and the notebook instance contains cardholder data, restrict direct internet access\. Allowing direct public access to your notebook instance might violate the requirement to place system components that store cardholder data in an internal network zone, segregated from the DMZ and other untrusted networks\.

### Remediation<a name="pcidss-sagemaker-1-remediation"></a>

Note that you cannot change the internet access setting after a notebook instance is created\. It must be stopped, deleted, and recreated\.

**To configure an SageMaker notebook instance to deny direct internet access**

1. Open the SageMaker console at [https://console.aws.amazon.com/sagemaker/](https://console.aws.amazon.com/sagemaker/)

1. Navigate to **Notebook instances**\.

1. Delete the instance that has direct internet access enabled\. Choose the instance, choose **Actions**, then choose stop\.

   After the instance is stopped, choose **Actions**, then choose **delete**\.

1. Choose **Create notebook instance**\. Provide the configuration details\.

1. Expand the **Network** section\. Then choose a VPC, subnet, and security group\. Under **Direct internet access**, choose **Disable — Access the internet through a VPC**\.

1. Choose **Create notebook instance**\.

For more information, see [Connect a notebook instance to resources in a VPC](https://docs.aws.amazon.com/sagemaker/latest/dg/appendix-notebook-and-internet-access.html) in the *Amazon SageMaker Developer Guide*\.

## \[PCI\.SSM\.1\] Amazon EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation<a name="pcidss-ssm-1"></a>

**Severity:** Medium

**Resource:** SSM patch compliance and Amazon EC2 instance

**AWS Config rule: ** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html)

**Parameters:** None

This control checks whether the compliance status of the Amazon EC2 Systems Manager patch compliance is `COMPLIANT` or `NON_COMPLIANT` after the patch installation on the instance\.

It only checks instances that are managed by AWS Systems Manager Patch Manager\.

It does not check whether the patch was applied within the 30\-day limit prescribed by PCI DSS requirement 6\.2\.

It also does not validate whether the patches applied were classified as security patches\.

You should create patching groups with the appropriate baseline settings and ensure in\-scope systems are managed by those patch groups in Systems Manager\. For more information about patch groups, see the [https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-patch-group-tagging.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-patch-group-tagging.html)\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-ssm-1-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 6\.2: Ensure that all system components and software are protected from known vulnerabilities by installing applicable vendor\-supplied security patches\. Install critical security patches within one month of release\.**  
Patches released by the vendor for systems that are in\-scope for PCI DSS should be tested and validated before installation in production environment\. Once deployed, security settings and controls should be validated to ensure that deployed patches have not impacted the security of the cardholder data environment \(CDE\)\.  
If you use Amazon EC2 instances managed by AWS Systems Manager Patch Manager to patch managed instances in your CDE, ensure that the patches are successfully applied\. To do this, check that the compliance status of the Amazon EC2 Systems Manager patch compliance is "COMPLIANT"\. Patch Manager can apply both operating systems and applications applicable patches\.  
This is a method used to protect system components and software from known vulnerabilities\.

### Remediation<a name="pcidss-ssm-1-remediation"></a>

**To remediate noncompliant patches**

This rule checks whether the compliance status of the Amazon EC2 Systems Manager patch compliance is COMPLIANT or NON\_COMPLIANT\. To find out more about patch compliance states, see the [https://docs.aws.amazon.com/systems-manager/latest/userguide/about-patch-compliance-states.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/about-patch-compliance-states.html)\. 

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation pane, under **Instances & Nodes**, choose **Run Command**\.

1. Choose **Run command**\.

1. Choose the radio button next to `AWS-RunPatchBaseline` and then change the **Operation** to **Install**\.

1. Choose **Choose instances manually** and then choose the noncompliant instance\(s\)\.

1. Scroll to the bottom and then choose **Run**\.

1. After the command has completed, to monitor the new compliance status of your patched instances, in the navigation pane, choose **Compliance**\.

See the *AWS Systems Manager User Guide* for more information about the following
+ [Using Systems Manager documents to patch a managed instance](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-ssm-documents.html)
+ [Running commands using the Systems Manager Run command](https://docs.aws.amazon.com/systems-manager/latest/userguide/run-command.html)

## \[PCI\.SSM\.2\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT<a name="pcidss-ssm-2"></a>

**Severity:** Low

**Resource:** AwsSSMAssociationCompliance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-association-compliance-status-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-association-compliance-status-check.html) 

**Parameters:** None

This control checks whether the status of the AWS Systems Manager association compliance is `COMPLIANT` or `NON_COMPLIANT` after the association is run on an instance\. The control passes if the association compliance status is `COMPLIANT`\.

A State Manager association is a configuration that is assigned to your managed instances\. The configuration defines the state that you want to maintain on your instances\. For example, an association can specify that antivirus software must be installed and running on your instances, or that certain ports must be closed\.

After you create one or more State Manager associations, compliance status information is immediately available to you in the console or in response to AWS CLI commands or corresponding Systems Manager API operations\. For associations, **Configuration Compliance** shows statuses of **Compliant** or **Non\-compliant** and the severity level assigned to the association, such as **Critical** or **Medium**\. To learn more about State Manager association compliance, see [About State Manager association compliance](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-compliance-about.html#sysman-compliance-about-association) in the *AWS Systems Manager User Guide*\.

You must configure your in\-scope EC2 instances for Systems Manager association\. You must also configure the patch baseline for the security rating of the vendor of patches, and set the autoapproval date to meet PCI DSS 3\.2\.1 requirement 6\.2\. For additional guidance on how to create an association, see [Create an association](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-state-assoc.html) in the *AWS Systems Manager User Guide*\. For additional information on working with patching in Systems Manager, see [AWS Systems Manager Patch Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-patch.html) in the *AWS Systems Manager User Guide*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Related PCI DSS requirements<a name="pcidss-ssm-2-requirements"></a>

This control is related to the following PCI DSS requirements\.

PCI DSS 2\.4 Maintain an inventory of system components that are in scope for PCI DSS\.  
If you use EC2 instances managed by Systems Manager to collect inventory for your cardholder data environment \(CDE\), make sure that the instances are successfully associated\. To do this, check whether the compliance status of the Systems Manager association compliance is `COMPLIANT`\. Using Systems Manager can help to maintain an inventory of system components that are in scope for PCI DSS\. For additional guidance on how to organize inventory, see [Configuring Resource Data Sync for Inventory](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-inventory-datasync.html) in the *AWS Systems Manager User Guide*\.

### Remediation<a name="pcidss-ssm-2-remediation"></a>

A failed association can be related to different things, including targets and SSM document names\. To remediate this issue, you must first identify and investigate the association\. You can then update the association to correct the specific issue\.

You can edit an association to specify a new name, schedule, severity level, or targets\. After you edit an association, Systems Manager creates a new version\.

**To investigate and update a failed association**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation pane, under **Instances & Nodes**, choose **Managed Instances**\.

1. Choose the instance ID that has an **Association status** of **Failed**\.

1. Choose **View details**\.

1. Choose **Associations**\.

1. Note the name of the association that has an **Association status **of **Failed**\. This is the association that you need to investigate\. You need to use the association name in the next step\.

1. In the navigation pane, choose **State Manager**\. Search for the association name, then select the association\.

   After you determine the issue, edit the failed association to correct the problem\. For information on how to edit an association, see [Edit an association](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-state-assoc-edit.html)\.

For more information on creating and editing State Manager associations, see [Working with associations in Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-associations.html) in the *AWS Systems Manager User Guide*\.

## \[PCI\.SSM\.3\] EC2 instances should be managed by AWS Systems Manager<a name="pcidss-ssm-3"></a>

**Severity:** Medium 

**Resource:** AwsEc2Instance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-managed-by-systems-manager.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-managed-by-systems-manager.html) 

**Parameters:** None

This control checks whether the EC2 instances in your account are managed by Systems Manager\.

AWS Systems Manager is an AWS service that you can use to view and control your AWS infrastructure\. To help you to maintain security and compliance, Systems Manager scans your managed instances\. A managed instance is a machine that is configured for use with Systems Manager\. Systems Manager then reports or takes corrective action on any policy violations that it detects\. Systems Manager also helps you to configure and maintain your managed instances\. Additional configuration is needed in Systems Manager for patch deployment to managed EC2 instances\.

To learn more, see the [https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)\.

### Related PCI DSS requirements<a name="pcidss-ssm-3-requirements"></a>

This control is related to the following PCI DSS requirements:

**PCI DSS 2\.4 Maintain an inventory of system components that are in scope for PCI DSS\.**  
If you use EC2 instances managed by Systems Manager to collect inventory for your cardholder data environment \(CDE\), make sure that the instances are managed by Systems Manager\. Using Systems Manager can help to maintain an inventory of system components that are in scope for PCI DSS\. For additional guidance on how to organize inventory, see [Configuring resource data sync for inventory](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-inventory-datasync.html) in the *AWS Systems Manager User Guide*\.

**PCI DSS 6\.2 Ensure that all system components and software are protected from known vulnerabilities by installing applicable vendor supplied security patches\. Install critical security patches within one month of release\.**  
For systems that are in scope for PCI DSS, before you install vendor patches in a production environment, you should test and validate them\. After you deploy patches, validate security settings and controls to ensure that deployed patches have not affected the security of the CDE\. If you use EC2 instances managed by Systems Manager to patch managed instances in your CDE, ensure that the instances are managed by Systems Manager\. Systems Manager deploys system patches, which helps to protect system components and software from known vulnerabilities\.

### Remediation<a name="pcidss-ssm-3-remediation"></a>

You can use the Systems Manager quick setup to set up Systems Manager to manage your EC2 instances\.

To determine whether your instances can support Systems Manager associations, see [Systems Manager prerequisites](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html) in the *AWS Systems Manager User Guide*\.

**To ensure EC2 instances are managed by Systems Manager**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation pane, choose **Quick setup**\.

1. On the configuration screen, keep the default options\.

1. Choose **Set up Systems Manager**\.