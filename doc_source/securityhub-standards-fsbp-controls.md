# AWS Foundational Security Best Practices controls<a name="securityhub-standards-fsbp-controls"></a>

The AWS Foundational Security Best Practices standard contains the following controls\. For each control, the information includes the following information\.
+ The category that the control applies to\. For descriptions of the categories, see [Control categories](control-categories.md)\.
+ The severity
+ The applicable resource that the control evaluates\. We also list dependent resources for the control\. For change triggered controls, you must record resources in AWS Config for the control to work\. For more information, see [AWS Config resources required for AWS Foundational Security Best Practices controls](standards-fsbp-config-resources.md)\.
+ The required AWS Config rule, and any specific parameter values set by AWS Security Hub
+ Remediation steps

Note that gaps in the control numbers indicate controls that are not yet released\. If a control is noted as **Retired**, Security Hub removed it within the last 90 days and doesn't generate findings for that control\. Older retired controls aren't noted in the documentation\.

## Controls categorized by service<a name="controls-categorized-service"></a>

[AWS Certificate Manager](#fsbp-acm-1)

[Amazon API Gateway](#fsbp-apigateway-1)

[Amazon EC2 Auto Scaling](#fsbp-autoscaling-1)

[AWS CloudFormation](#fsbp-cloudformation-1)

[Amazon CloudFront](#fsbp-cloudfront-1)

[AWS CloudTrail](#fsbp-cloudtrail-1)

[AWS CodeBuild](#fsbp-codebuild-1)

[AWS Config](#fsbp-config-1)

[AWS Database Migration Service](#fsbp-dms-1)

[Amazon DynamoDB](#fsbp-dynamodb-1)

[Amazon EC2](#fsbp-ec2-1)

[Amazon ECR](#fsbp-ecr-1)

[Amazon ECS](#fsbp-ecs-1)

[Amazon EFS](#fsbp-efs-1)

[Amazon EKS](#fsbp-eks-2)

[AWS Elastic Beanstalk](#fsbp-elasticbeanstalk-1)

[Elastic Load Balancing](#fsbp-elb-2)

[Amazon EMR](#fsbp-emr-1)

[Amazon ES](#fsbp-es-1)

[Amazon GuardDuty](#fsbp-guardduty-1)

[AWS Identity and Access Management](#fsbp-iam-1)

[Amazon Kinesis](#fsbp-kinesis-1)

[AWS Key Management Service](#fsbp-kms-1)

[AWS Lambda](#fsbp-lambda-1)

[AWS Network Firewall](#fsbp-networkfirewall-3)

[Amazon OpenSearch Service](#fsbp-opensearch-1)

[Amazon Relational Database Service](#fsbp-rds-1)

[Amazon Redshift](#fsbp-redshift-1)

[Amazon Simple Storage Service](#fsbp-s3-1)

[Amazon SageMaker](#fsbp-sagemaker-1)

[AWS Secrets Manager](#fsbp-secretsmanager-1)

[Amazon Simple Notification Service](#fsbp-sns-1)

[Amazon Simple Queue Service](#fsbp-sqs-1)

[Amazon EC2 Systems Manager](#fsbp-ssm-1)

[AWS WAF](#fsbp-waf-1)

## \[ACM\.1\] Imported and ACM\-issued certificates should be renewed after a specified time period<a name="fsbp-acm-1"></a>

**Category:** Protect > Data protection > Encryption of data in transit

**Severity:** Medium

**Resource type:** `AWS::ACM::Certificate`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/acm-certificate-expiration-check.html](https://docs.aws.amazon.com/config/latest/developerguide/acm-certificate-expiration-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `daysToExpiration`: 30

This control checks whether ACM certificates in your account are marked for expiration within 30 days\. It checks both imported certificates and certificates provided by AWS Certificate Manager\.

ACM can automatically renew certificates that use DNS validation\. For certificates that use email validation, you must respond to a domain validation email\. ACM does not automatically renew certificates that you import\. You must renew imported certificates manually\.

For more information about managed renewal for ACM certificates, see [Managed renewal for ACM certificates](https://docs.aws.amazon.com/acm/latest/userguide/managed-renewal.html) in the *AWS Certificate Manager User Guide*\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\) 
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)

### Remediation<a name="acm-1-remediation"></a>

ACM provides managed renewal for your SSL/TLS certificates issued by Amazon\. This means that ACM either renews your certificates automatically \(if you use DNS validation\), or it sends you email notices when the certificate expiration approaches\. These services are provided for both public and private ACM certificates\.

**For domains validated by email**  
When a certificate is 45 days from expiration, ACM sends to the domain owner an email for each domain name\. To validate the domains and complete the renewal, you must respond to the email notifications\.  
For more information, see [Renewal for domains validated by email](https://docs.aws.amazon.com/acm/latest/userguide/email-renewal-validation.html) in the *AWS Certificate Manager User Guide*\.

**For domains validated by DNS**  
ACM automatically renews certificates that use DNS validation\. 60 days before the expiration, ACM verifies that the certificate can be renewed\.  
If it cannot validate a domain name, then ACM sends a notification that manual validation is required\. It sends these notifications 45 days, 30 days, 7 days, and 1 day before the expiration\.  
For more information, see [Renewal for domains validated by DNS](https://docs.aws.amazon.com/acm/latest/userguide/dns-renewal-validation.html) in the *AWS Certificate Manager User Guide*\.

## \[APIGateway\.1\] API Gateway REST and WebSocket API logging should be enabled<a name="fsbp-apigateway-1"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::ApiGateway::Stage`, `AWS::ApiGatewayV2::Stage`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/api-gw-execution-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/api-gw-execution-logging-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether all stages of an Amazon API Gateway REST or WebSocket API have logging enabled\. The control fails if logging is not enabled for all methods of a stage or if `loggingLevel` is neither `ERROR` nor `INFO`\.

API Gateway REST or WebSocket API stages should have relevant logs enabled\. API Gateway REST and WebSocket API execution logging provides detailed records of requests made to API Gateway REST and WebSocket API stages\. The stages include API integration backend responses, Lambda authorizer responses, and the `requestId` for AWS integration endpoints\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Europe \(Milan\)

### Remediation<a name="apigateway-1-remediation"></a>

To enable logging for REST and WebSocket API operations, see [Set up CloudWatch API logging using the API Gateway console](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-logging.html#set-up-access-logging-using-console) in the *API Gateway Developer Guide*\.

## \[APIGateway\.2\] API Gateway REST API stages should be configured to use SSL certificates for backend authentication<a name="fsbp-apigateway-2"></a>

**Category:** Protect > Data protection

**Severity:** Medium

**Resource type:** `AWS::ApiGateway::Stage`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/api-gw-ssl-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/api-gw-ssl-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon API Gateway REST API stages have SSL certificates configured\. Backend systems use these certificates to authenticate that incoming requests are from API Gateway\.

API Gateway REST API stages should be configured with SSL certificates to allow backend systems to authenticate that requests originate from API Gateway\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="apigateway-2-remediation"></a>

For detailed instructions on how to generate and configure API Gateway REST API SSL certificates, see [Generate and configure an SSL certificate for backend authentication](https://docs.aws.amazon.com/apigateway/latest/developerguide/getting-started-client-side-ssl-authentication.html) in the *API Gateway Developer Guide*\.

## \[APIGateway\.3\] API Gateway REST API stages should have AWS X\-Ray tracing enabled<a name="fsbp-apigateway-3"></a>

**Category:** Detect > Detection services

**Severity:** Low

**Resource type:** `AWS::ApiGateway::Stage`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/api-gw-xray-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/api-gw-xray-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether AWS X\-Ray active tracing is enabled for your Amazon API Gateway REST API stages\.

X\-Ray active tracing enables a more rapid response to performance changes in the underlying infrastructure\. Changes in performance could result in a lack of availability of the API\. X\-Ray active tracing provides real\-time metrics of user requests that flow through your API Gateway REST API operations and connected services\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="apigateway-3-remediation"></a>

For detailed instructions on how to enable X\-Ray active tracing for API Gateway REST API operations, see [Amazon API Gateway active tracing support for AWS X\-Ray](https://docs.aws.amazon.com/xray/latest/devguide/xray-services-apigateway.html) in the *AWS X\-Ray Developer Guide*\. 

## \[APIGateway\.4\] API Gateway should be associated with an AWS WAF web ACL<a name="fsbp-apigateway-4"></a>

**Category:** Protect > Protective services

**Severity:** Medium

**Resource type:** `AWS::ApiGateway::Stage`

**AWS Configrule:** [https://docs.aws.amazon.com/config/latest/developerguide/api-gw-associated-with-waf.html](https://docs.aws.amazon.com/config/latest/developerguide/api-gw-associated-with-waf.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an API Gateway stage uses an AWS WAF web access control list \(ACL\)\. This control fails if an AWS WAF web ACL is not attached to a REST API Gateway stage\.

AWS WAF is a web application firewall that helps protect web applications and APIs from attacks\. It enables you to configure an ACL, which is a set of rules that allow, block, or count web requests based on customizable web security rules and conditions that you define\. Ensure that your API Gateway stage is associated with an AWS WAF web ACL to help protect it from malicious attacks\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="apigateway-4-remediation"></a>

For information on how to use the API Gateway console to associate an AWS WAF Regional web ACL with an existing API Gateway API stage, see [Using AWS WAF to protect your APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-control-access-aws-waf.html) in the *API Gateway Developer Guide*\.

## \[APIGateway\.5\] API Gateway REST API cache data should be encrypted at rest<a name="fsbp-apigateway-5"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::ApiGateway::Stage`

AWS Config rule: `api-gw-cache-encrypted` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether all methods in API Gateway REST API stages that have cache enabled are encrypted\. The control fails if any method in an API Gateway REST API stage is configured to cache and the cache is not encrypted\.

Encrypting data at rest reduces the risk of data stored on disk being accessed by a user not authenticated to AWS\. It adds another set of access controls to limit unauthorized users ability access the data\. For example, API permissions are required to decrypt the data before it can be read\.

API Gateway REST API caches should be encrypted at rest for an added layer of security\.

### Remediation<a name="apigateway-5-remediation"></a>

To remediate this control, configure the stage to encrypt the cache data\.

**To configure API caching for a given stage**

1. Open the API Gateway console at [https://console\.aws\.amazon\.com/apigateway/](https://console.aws.amazon.com/apigateway/)\. 

1. Choose the API\.

1. Choose **Stages**\.

1. In the **Stages** list for the API, choose the stage to add caching to\.

1. Choose **Settings**\.

1. Choose **Enable API cache**\.

1. Update the desired settings, then select **Encrypt cache data**\.

1. Choose **Save Changes**\.

## \[AutoScaling\.1\] Auto Scaling groups associated with a load balancer should use load balancer health checks<a name="fsbp-autoscaling-1"></a>

**Category:** Identify > Inventory

**Severity:** Low

**Resource type:** `AWS::AutoScaling::AutoScalingGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-group-elb-healthcheck-required.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-group-elb-healthcheck-required.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether your Auto Scaling groups that are associated with a load balancer are using Elastic Load Balancing health checks\.

This ensures that the group can determine an instance's health based on additional tests provided by the load balancer\. Using Elastic Load Balancing health checks can help support the availability of applications that use EC2 Auto Scaling groups\. 

### Remediation<a name="autoscaling-1-remediation"></a>

To remediate this issue, update your Auto Scaling groups to use Elastic Load Balancing health checks\.

**To enable Elastic Load Balancing health checks**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Auto Scaling**, choose **Auto Scaling Groups**\.

1. Select the check box for your group\.

1. Choose **Edit**\.

1. Under **Health checks**, for **Health check type**, choose **ELB**\.

1. For **Health check grace period**, enter **300**\.

1. At the bottom of the page, choose **Update**\.

For more information on using a load balancer with an Auto Scaling group, see the [https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html](https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html)\.

## \[AutoScaling\.2\] Amazon EC2 Auto Scaling group should cover multiple Availability Zones<a name="fsbp-autoscaling-2"></a>

**Category:** Recover > Resilience > High Availability

**Severity:** Medium

**Resource type:** `AWS::AutoScaling::AutoScalingGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-multiple-az.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-multiple-az.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Auto Scaling group spans multiple Availability Zones\. The control fails if an Auto Scaling group does not span multiple availability zones\.

Amazon EC2 Auto Scaling groups can be configured to use multiple Availability Zones\. An Auto Scaling group with a single Availability Zone is preferred in some use cases, such as batch\-jobs or when inter\-AZ transfer costs need to be kept to a minimum\. However, an Auto Scaling group that does not span multiple Availability Zones will not launch instances in another Availability Zone to compensate if the configured single Availability Zone becomes unavailable\.

### Remediation<a name="autoscaling-2-remediation"></a>

For information on how to add Availability Zones to an existing auto scaling group, see [Availability zones](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-add-availability-zone.html) in the *Amazon EC2 Auto Scaling User Guide*\.

## \[AutoScaling\.3\] Auto Scaling group should configure EC2 instances to require Instance Metadata Service Version 2 \(IMDSv2\)<a name="fsbp-autoscaling-3"></a>

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::AutoScaling::LaunchConfiguration`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launchconfig-requires-imdsv2.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launchconfig-requires-imdsv2.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether IMDSv2 is enabled on all instances launched by Amazon EC2 Auto Scaling groups\. The control fails if the Instance Metadata Service \(IMDS\) version is not included in the launch configuration or if both IMDSv1 and IMDSv2 are enabled\.

IMDS provides data about your instance that you can use to configure or manage the running instance\.

Version 2 of the IMDS adds new protections that weren't available in IMDSv1 to further safeguard your EC2 instances\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="autoscaling-3-remediation"></a>

An Auto Scaling group is associated with one launch configuration at a time\. You cannot modify a launch configuration after you create it\. To change the launch configuration for an Auto Scaling group, use an existing launch configuration as the basis for a new launch configuration with IMDSv2 enabled\. For more information, see [Configure instance metadata options for new instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-options.html#configuring-IMDS-new-instances) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[AutoScaling\.4\] Auto Scaling group launch configuration should not have metadata response hop limit greater than `1`<a name="fsbp-autoscaling-4"></a>

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::AutoScaling::LaunchConfiguration`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-config-hop-limit.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-config-hop-limit.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks the number of network hops that a metadata token can travel\. The control fails if the metadata response hop limit is greater than `1`\.

The Instance Metadata Service \(IMDS\) provides metadata information about an Amazon EC2 instance and is useful for application configuration\. Restricting the HTTP `PUT` response for the metadata service to only the EC2 instance protects the IMDS from unauthorized use\.

The Time To Live \(TTL\) field in the IP packet is reduced by one on every hop\. This reduction can be used to ensure that the packet does not travel outside EC2\. IMDSv2 protects EC2 instances that may have been misconfigured as open routers, layer 3 firewalls, VPNs, tunnels, or NAT devices, which prevents unauthorized users from retrieving metadata\. With IMDSv2, the `PUT` response that contains the secret token cannot travel outside the instance because the default metadata response hop limit is set to `1`\. However, if this value is greater than `1`, the token can leave the EC2 instance\. 

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="autoscaling-4-remediation"></a>

For detailed instructions on how to modify the metadata response hop limit for an existing launch configuration, see [Modify instance metadata options for existing instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-options.html#configuring-IMDS-existing-instances) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[AutoScaling\.5\] Amazon EC2 instances launched using Auto Scaling group launch configurations should not have Public IP addresses<a name="fsbp-autoscaling-5"></a>

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::AutoScaling::LaunchConfiguration`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-config-public-ip-disabled.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-config-public-ip-disabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Auto Scaling group's associated launch configuration assigns a [public IP address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html#public-ip-addresses) to the group’s instances\. The control fails if the associated launch configuration assigns a public IP address\.

Amazon EC2 instances in an Auto Scaling group launch configuration should not have an associated public IP address, except for in limited edge cases\. Amazon EC2 instances should only be accessible from behind a load balancer instead of being directly exposed to the internet\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="autoscaling-5-remediation"></a>

An Auto Scaling group is associated with one launch configuration at a time\. You cannot modify a launch configuration after you have create it\. To change the launch configuration for an Auto Scaling group, use an existing launch configuration as the basis for a new launch configuration\. Then, update the Auto Scaling group to use the new launch configuration as described in steps below\.

After you change the launch configuration for an Auto Scaling group, any new instances are launched with the new configuration options\. Existing instances are not affected\. To update existing instances, either terminate them so that they are replaced by your Auto Scaling group, or allow automatic scaling to gradually replace older instances with newer instances based on your [termination policies](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-instance-termination.html)\.

**To enable Elastic Load Balancing health checks**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Auto Scaling**, choose **Launch Configurations**\.

1. Select the launch configuration and choose **Actions**, then **Copy launch configuration**\. This sets up a new launch configuration with the same options as the original, but with "Copy" added to the name\. 

1. On the **Create Launch Configuration** page, expand **Advanced details** under **Additional configuration \- optional**\.

1. Under **IP address type**, choose **Do not assign a public IP address to any instances**\.

1. When you have finished, Choose **Create launch configuration**\.

1. On the navigation pane, under **Auto Scaling**, choose **Auto Scaling Groups**\.

1. Select the check box next to the Auto Scaling group\.

1. A split pane opens up in the bottom part of the page, showing information about the group that's selected\.

1. On the **Details** tab, choose **Launch configuration**, **Edit**\.

1. For **Launch configuration**, select the new launch configuration\.

1. When you have finished changing your launch configuration, choose **Update**\.

## \[AutoScaling\.6\] Auto Scaling groups should use multiple instance types in multiple Availability Zones<a name="fsbp-autoscaling-6"></a>

**Category:** Recover > Resilience > High Availability

**Severity:** Medium

**Resource type:** `AWS::AutoScaling::AutoScalingGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-multiple-instance-types.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-multiple-instance-types.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon EC2 Auto Scaling group uses multiple instance types\. The control fails if the Auto Scaling group has only one instance type defined\.

You can enhance availability by deploying your application across multiple instance types running in multiple Availability Zones\. Security Hub recommends using multiple instance types so that the Auto Scaling group can launch another instance type if there is insufficient instance capacity in your chosen Availability Zones\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="autoscaling-6-remediation"></a>

For instructions on creating an Auto Scaling group with multiple instance types, see [Auto Scaling groups with multiple instance types and purchase options](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-mixed-instances-groups.html) in the *Amazon EC2 Auto Scaling User Guide*\.

## \[AutoScaling\.9\] EC2 Auto Scaling groups should use EC2 launch templates<a name="fsbp-autoscaling-9"></a>

**Category:** Identify > Resource Configuration

**Severity:** Medium

**Resource type:** `AWS::AutoScaling::AutoScalingGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-template.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-template.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon EC2 Auto Scaling group is created from an EC2 launch template\. This control fails if an Amazon EC2 Auto Scaling group is not created with a launch template or if a launch template is not specified in a mixed instances policy\.

An EC2 Auto Scaling group can be created from either an EC2 launch template or a launch configuration\. However, using a launch template to create an Auto Scaling group ensures that you have access to the latest features and improvements\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="autoscaling-9-remediation"></a>

To create an Auto Scaling group with an EC2 launch template, see [Create an Auto Scaling group using a launch template](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-asg-launch-template.html) in the *Amazon EC2 Auto Scaling User Guide*\. For information about how to replace a launch configuration with a launch template, see [Replace a launch configuration with a launch template](https://docs.aws.amazon.com/autoscaling/ec2/userguide/replace-launch-config.html) in the *Amazon EC2 User Guide for Windows Instances*\.

## \[CloudFormation\.1\] CloudFormation stacks should be integrated with Simple Notification Service \(SNS\)<a name="fsbp-cloudformation-1"></a>

**Category:** Detect > Detection services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::CloudFormation::Stack`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudformation-stack-notification-check.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudformation-stack-notification-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `SNSTopic1`: 30
+ `SNSTopic2`: 30
+ `SNSTopic3`: 30
+ `SNSTopic4`: 30
+ `SNSTopic5`: 30
+ `(Optional): SNS topic ARN`: 30

This control checks whether an Amazon Simple Notification Service notification is integrated with a CloudFormation stack\. The control fails for a CloudFormation stack if there is no SNS notification associated with it\. 

Configuring an SNS notification with your CloudFormation stack helps immediately notify stakeholders of any events or changes occurring with the stack\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="cloudformation-1-remediation"></a>

For information about how to update a CloudFormation stack, see [AWS CloudFormation stack updates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks) in the AWS CloudFormation User Guide\.

## \[CloudFront\.1\] CloudFront distributions should have a default root object configured<a name="fsbp-cloudfront-1"></a>

**Category:** Protect > Secure access management > Resources not publicly accessible

**Severity:** Critical

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-default-root-object-configured.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-default-root-object-configured.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon CloudFront distribution is configured to return a specific object that is the default root object\. The control fails if the CloudFront distribution does not have a default root object configured\.

A user might sometimes request the distribution’s root URL instead of an object in the distribution\. When this happens, specifying a default root object can help you to avoid exposing the contents of your web distribution\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-1-remediation"></a>

For detailed instructions on how to specify a default root object for your distribution, see [How to specify a default root object](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/DefaultRootObject.html#DefaultRootObjectHowToDefine) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.2\] CloudFront distributions should have origin access identity enabled<a name="fsbp-cloudfront-2"></a>

**Category:** Protect > Secure access management > Resource policy configuration

**Severity:** Medium

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-origin-access-identity-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-origin-access-identity-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon CloudFront distribution with Amazon S3 Origin type has Origin Access Identity \(OAI\) configured\. The control fails if OAI is not configured\.

CloudFront OAI prevents users from accessing S3 bucket content directly\. When users access an S3 bucket directly, they effectively bypass the CloudFront distribution and any permissions that are applied to the underlying S3 bucket content\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-2-remediation"></a>

For detailed remediation instructions, see [Creating a CloudFront OAI and adding it to your distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html#private-content-creating-oai) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.3\] CloudFront distributions should require encryption in transit<a name="fsbp-cloudfront-3"></a>

**Category:** Protect > Data protection > Encryption of data in transit

**Severity:** Medium

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-viewer-policy-https.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-viewer-policy-https.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon CloudFront distribution requires viewers to use HTTPS directly or whether it uses redirection\. The control fails if `ViewerProtocolPolicy` is set to `allow-all` for `defaultCacheBehavior` or for `cacheBehaviors`\.

HTTPS \(TLS\) can be used to help prevent potential attackers from using person\-in\-the\-middle or similar attacks to eavesdrop on or manipulate network traffic\. Only encrypted connections over HTTPS \(TLS\) should be allowed\. Encrypting data in transit can affect performance\. You should test your application with this feature to understand the performance profile and the impact of TLS\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-3-remediation"></a>

For detailed remediation instructions, see [Requiring HTTPS for communication between viewers and CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-viewers-to-cloudfront.html) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.4\] CloudFront distributions should have origin failover configured<a name="fsbp-cloudfront-4"></a>

**Category:** Recover > Resilience > High availability

**Severity:** Low

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-origin-failover-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-origin-failover-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon CloudFront distribution is configured with an origin group that has two or more origins\.

CloudFront origin failover can increase availability\. Origin failover automatically redirects traffic to a secondary origin if the primary origin is unavailable or if it returns specific HTTP response status codes\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-4-remediation"></a>

For detailed remediation instructions, see [Creating an origin group](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html#concept_origin_groups.creating) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.5\] CloudFront distributions should have logging enabled<a name="fsbp-cloudfront-5"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-accesslogs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-accesslogs-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether server access logging is enabled on CloudFront distributions\. The control fails if access logging is not enabled for a distribution\.

CloudFront access logs provide detailed information about every user request that CloudFront receives\. Each log contains information such as the date and time the request was received, the IP address of the viewer that made the request, the source of the request, and the port number of the request from the viewer\.

These logs are useful for applications such as security and access audits and forensics investigation\. For additional guidance on how to analyze access logs, see [Querying Amazon CloudFront logs](https://docs.aws.amazon.com/athena/latest/ug/cloudfront-logs.html) in the *Amazon Athena User Guide*\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-5-remediation"></a>

For information on how to configure access logging for a CloudFront distribution, see [Configuring and using standard logs \(access logs\)](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/AccessLogs.html) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled<a name="fsbp-cloudfront-6"></a>

**Category:** Protect > Protective services

**Severity:** Medium

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-associated-with-waf.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-associated-with-waf.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether CloudFront distributions are associated with either AWS WAF or AWS WAFv2 web ACLs\. The control fails if the distribution is not associated with a web ACL\.

AWS WAF is a web application firewall that helps protect web applications and APIs from attacks\. It allows you to configure a set of rules, called a web access control list \(web ACL\), that allow, block, or count web requests based on customizable web security rules and conditions that you define\. Ensure your CloudFront distribution is associated with an AWS WAF web ACL to help protect it from malicious attacks\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-6-remediation"></a>

For information on how to associate a web ACL with a CloudFront distribution, see [Using AWS WAF to control access to your content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-awswaf.html) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.7\] CloudFront distributions should use custom SSL/TLS certificates<a name="fsbp-cloudfront-7"></a>

**Category:** Protect > Data protection > Encryption of data\-in\-transit

**Severity:** Medium

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-custom-ssl-certificate.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-custom-ssl-certificate.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether CloudFront distributions are using the default SSL/TLS certificate CloudFront provides\. This control passes if the CloudFront distribution uses a custom SSL/TLS certificate\. This control fails if the CloudFront distribution uses the default SSL/TLS certificate\.

 Custom SSL/TLS allow your users to access content by using alternate domain names\. You can store custom certificates in AWS Certificate Manager \(recommended\), or in IAM\. 

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-7-remediation"></a>

To add an alternate domain name using a custom SSL/TLS certificate for your CloudFront distributions, see [Adding an alternate domain name](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html#CreatingCNAME) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.8\] CloudFront distributions should use SNI to serve HTTPS requests<a name="fsbp-cloudfront-8"></a>

**Category:** Protect > Secure network configuration

**Severity:** Low

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-sni-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-sni-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon CloudFront distributions are using a custom SSL/TLS certificate and are configured to use SNI to serve HTTPS requests\. This control fails if a custom SSL/TLS certificate is associated but the SSL/TLS support method is a dedicated IP address\.

Server Name Indication \(SNI\) is an extension to the TLS protocol that is supported by browsers and clients released after 2010\. If you configure CloudFront to serve HTTPS requests using SNI, CloudFront associates your alternate domain name with an IP address for each edge location\. When a viewer submits an HTTPS request for your content, DNS routes the request to the IP address for the correct edge location\. The IP address to your domain name is determined during the SSL/TLS handshake negotiation; the IP address isn't dedicated to your distribution\. 

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-8-remediation"></a>

To configure your CloudFront distributions to use SNI to serve HTTPS requests, see [Using SNI to Serve HTTPS Requests \(works for Most Clients\)](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cnames-https-dedicated-ip-or-sni.html#cnames-https-sni) in the CloudFront Developer Guide\.

## \[CloudFront\.9\] CloudFront distributions should encrypt traffic to custom origins<a name="fsbp-cloudfront-9"></a>

**Category:** Protect > Data protection > Encryption of data\-in\-transit

**Severity:** Medium

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-traffic-to-origin-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-traffic-to-origin-encrypted.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon CloudFront distributions are encrypting traffic to custom origins\. This control fails for a CloudFront distribution whose origin protocol policy allows 'http\-only'\. This control also fails if the distribution's origin protocol policy is 'match\-viewer' while the viewer protocol policy is 'allow\-all'\.

HTTPS \(TLS\) can be used to help prevent eavesdropping or manipulation of network traffic\. Only encrypted connections over HTTPS \(TLS\) should be allowed\. 

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-9-remediation"></a>

To update the Origin Protocol Policy to require encryption for your CloudFront connections, see [Requiring HTTPS for communication between CloudFront and your custom origin](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-cloudfront-to-custom-origin.html) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.10\] CloudFront distributions should not use deprecated SSL protocols between edge locations and custom origins<a name="fsbp-cloudfront-10"></a>

**Category:** Protect > Data protection > Encryption of data\-in\-transit

**Severity:** Medium

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-no-deprecated-ssl-protocols.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-no-deprecated-ssl-protocols.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon CloudFront distributions are using deprecated SSL protocols for HTTPS communication between CloudFront edge locations and your custom origins\. This control fails if a CloudFront distribution has a `CustomOriginConfig` where `OriginSslProtocols` includes `SSLv3`\.

In 2015, the Internet Engineering Task Force \(IETF\) officially announced that SSL 3\.0 should be deprecated due to the protocol being insufficiently secure\. It is recommended that you use TLSv1\.2 or later for HTTPS communication to your custom origins\. 

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-10-remediation"></a>

To update the Origin SSL Protocols for your CloudFront distributions, see [Requiring HTTPS for communication between CloudFront and your custom origin](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-cloudfront-to-custom-origin.html) in the *Amazon CloudFront Developer Guide*\.

## \[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail that includes read and write management events<a name="fsbp-cloudtrail-1"></a>

**Category:** Identify > Logging

**Severity:** High

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloudtrail-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloudtrail-enabled.html)

**Schedule type:** Periodic

**Parameters:**
+ `readWriteType`: `ALL`

This control checks that there is at least one multi\-Region CloudTrail trail\. It also checks that the `ExcludeManagementEventSources` parameter is empty for at least one of those trails\.

AWS CloudTrail records AWS API calls for your account and delivers log files to you\. The recorded information includes the following information\.
+ Identity of the API caller
+ Time of the API call
+ Source IP address of the API caller
+ Request parameters
+ Response elements returned by the AWS service

CloudTrail provides a history of AWS API calls for an account, including API calls made from the AWS Management Console, AWS SDKs, command line tools\. The history also includes API calls from higher\-level AWS services such as AWS CloudFormation\.

The AWS API call history produced by CloudTrail enables security analysis, resource change tracking, and compliance auditing\. Multi\-Region trails also provide the following benefits\.
+ A multi\-Region trail helps to detect unexpected activity occurring in otherwise unused Regions\.
+ A multi\-Region trail ensures that global service event logging is enabled for a trail by default\. Global service event logging records events generated by AWS global services\.
+ For a multi\-Region trail, management events for all read and write operations ensure that CloudTrail records management operations on all of an AWS account’s resources\.

By default, CloudTrail trails that are created using the AWS Management Console are multi\-Region trails\.

### Remediation<a name="cloudtrail-1-remediation"></a>

To remediate this issue, create a new multi\-Region trail in CloudTrail\.

**To create a new trail in CloudTrail**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. If you haven't used CloudTrail before, choose **Get Started Now**\.

1. Choose **Trails** and then choose **Create trail**\.

1. Enter a name for the trail\.

1. Under **Storage location**, do one of the following:

   1. To create a new S3 bucket for CloudTrail logs, for **Create a new S3 bucket**, choose **Yes**, then enter a name for the new S3 bucket\.

   1. To use an existing S3 bucket, for **Create a new S3 bucket**, choose **No**, then select the S3 bucket to use\.

1. Under **Additional settings**, choose **Advanced**\. For **Enable log file validation**, select **Enabled**\.

1. Choose **Create**\.

**To update an existing trail in CloudTrail**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. In the **Name** column, choose the name of the trail\.

1. For **Management events**, choose **Edit**\.

1. For **Read/Write events**, select **Management events**\.

1. Under **API Activity**, select **Read** and **Write**\.

## \[CloudTrail\.2\] CloudTrail should have encryption at rest enabled<a name="fsbp-cloudtrail-2"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::CloudTrail::Trail`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether CloudTrail is configured to use the server\-side encryption \(SSE\) AWS KMS key encryption\. The check passes if the `KmsKeyId` is defined\.

For an added layer of security for your sensitive CloudTrail log files, you should use [server\-side encryption with AWS KMS–managed keys \(SSE\-KMS\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html) for your CloudTrail log files for encryption at rest\. Note that by default, the log files delivered by CloudTrail to your buckets are encrypted by [Amazon server\-side encryption with Amazon S3\-managed encryption keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)\. 

### Remediation<a name="cloudtrail-2-remediation"></a>

To remediate this issue, update your trail to enable SSE\-KMS encryption for the log files\.

**To enable encryption for CloudTrail logs**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the trail to update\.

1. Under **General details**, choose **Edit**\.

1. For **Log file SSE\-KMS encryption**, select **Enabled**\.

1. For **Create a new KMS key**, do one of the following:
   + To create a key, choose **New**\. Then in **AWS KMS alias**, enter an alias for the key\. The key is created in the same Region as the S3 bucket\.
   + To use an existing key, choose **Existing**, then from **AWS KMS alias**, choose the key\.

     The AWS KMS key and S3 bucket must be in the same Region\.

1. Choose **Save**\.

   You might need to modify the policy for CloudTrail to successfully interact with your KMS key\. For more information, see [Encrypting CloudTrail log files with AWS KMS–managed keys \(SSE\-KMS\)](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html) in the *AWS CloudTrail User Guide*\.

## \[CloudTrail\.4\] Ensure CloudTrail log file validation is enabled<a name="fsbp-cloudtrail-4"></a>

**Category:** Data protection > Data integrity

**Severity:** Low

**Resource type:** `AWS::CloudTrail::Trail`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether log file integrity validation is enabled on a CloudTrail trail\.

CloudTrail log file validation creates a digitally signed digest file that contains a hash of each log that CloudTrail writes to Amazon S3\. You can use these digest files to determine whether a log file was changed, deleted, or unchanged after CloudTrail delivered the log\.

Security Hub recommends that you enable file validation on all trails\. Log file validation provides additional integrity checks of CloudTrail logs\.

For more information, see [Enabling validation and validating files](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-intro.html#cloudtrail-log-file-validation-intro-enabling-and-using) in the *AWS CloudTrail User Guide*\.

### Remediation<a name="cloudtrail-4-remediation"></a>

To remediate this issue, update your CloudTrail trail to enable log file validation\.

**To enable CloudTrail log file validation**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Under **Name**, choose the name of a trail to edit\.

1. Under **General details**, choose **Edit**\.

1. Under **Additional settings**, for **Log file validation**, choose **Enabled**\.

1. Choose **Save changes**\.

For more information, see [Validating CloudTrail log file integrity](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-intro.html) in the *AWS CloudTrail User Guide*\.

## \[CloudTrail\.5\] Ensure CloudTrail trails are integrated with Amazon CloudWatch Logs<a name="fsbp-cloudtrail-5"></a>

**Category:** Identify > Logging

**Severity:** Low

**Resource type:** `AWS::CloudTrail::Trail`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-cloud-watch-logs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-cloud-watch-logs-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether CloudTrail trails are configured to send logs to CloudWatch Logs\. The control fails if the `CloudWatchLogsLogGroupArn` property of the trail is empty\.

CloudTrail records AWS API calls that are made in a given account\. The recorded information includes the following:
+ The identity of the API caller
+ The time of the API call
+ The source IP address of the API caller
+ The request parameters
+ The response elements returned by the AWS service

CloudTrail uses Amazon S3 for log file storage and delivery\. You can capture CloudTrail logs in a specified S3 bucket for long\-term analysis\. To perform real\-time analysis, you can configure CloudTrail to send logs to CloudWatch Logs\.

For a trail that is enabled in all Regions in an account, CloudTrail sends log files from all of those Regions to a CloudWatch Logs log group\.

Security Hub recommends that you send CloudTrail logs to CloudWatch Logs\. Note that this recommendation is intended to ensure that account activity is captured, monitored, and appropriately alarmed on\. You can use CloudWatch Logs to set this up with your AWS services\. This recommendation does not preclude the use of a different solution\.

Sending CloudTrail logs to CloudWatch Logs facilitates real\-time and historic activity logging based on user, API, resource, and IP address\. You can use this approach to establish alarms and notifications for anomalous or sensitivity account activity\.

### Remediation<a name="cloudtrail-5-remediation"></a>

You can use the console to enable CloudTrail integration with CloudWatch Logs\.

**To enable CloudTrail integration with CloudWatch Logs**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the trail that does not have a value for **CloudWatch Logs Log group**\.

1. Under **CloudWatch Logs**, choose **Edit**\.

1. Select **Enabled**\.

1. For **Log group**, do one of the following:
   + To use the default log group, keep the name as is\.
   + To use an existing log group, choose **Existing** and then enter the name of the log group to use\.
   + To create a new log group, choose **New** and then enter a name for the log group to create\.

1. For **IAM role**, do one of the following:
   + To use an existing role, choose **Existing** and then choose the role from the drop\-down list\.
   + To create a new role, choose **New** and then enter a name for the role to create\. The new role is assigned a policy that grants the necessary permissions\.

   To view the permissions granted to the role, expand **Policy document**\.

1. Choose **Save changes**\.

For more information, see [Configuring CloudWatch Logs monitoring with the console](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/send-cloudtrail-events-to-cloudwatch-logs.html#send-cloudtrail-events-to-cloudwatch-logs-console) in the *AWS CloudTrail User Guide*\.

## \[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth<a name="fsbp-codebuild-1"></a>

**Category:** Protect > Secure development

**Severity:** Critical

**Resource type:** `AWS::CodeBuild::Project`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-source-repo-url-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-source-repo-url-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the GitHub or Bitbucket source repository URL contains either personal access tokens or a user name and password\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Europe \(Milan\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

Authentication credentials should never be stored or transmitted in clear text or appear in the repository URL\. Instead of personal access tokens or user name and password, you should use OAuth to grant authorization for accessing GitHub or Bitbucket repositories\. Using personal access tokens or a user name and password could expose your credentials to unintended data exposure and unauthorized access\.

### Remediation<a name="codebuild-1-remediation"></a>

You can update your CodeBuild project to use OAuth\.

**To remove basic authentication / \(GitHub\) Personal Access Token from CodeBuild project source**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Choose the build project that contains personal access tokens or a user name and password\.

1. From **Edit**, choose **Source**\.

1. Choose **Disconnect from GitHub / Bitbucket**\.

1. Choose **Connect using OAuth**, then choose **Connect to GitHub / Bitbucket**\.

1. When prompted, choose **authorize as appropriate**\.

1. Reconfigure your repository URL and additional configuration settings, as needed\.

1. Choose **Update source**\.

For more information, refer to [CodeBuild use case\-based samples](https://docs.aws.amazon.com/codebuild/latest/userguide/use-case-based-samples.html) in the *AWS CodeBuild User Guide*\.

## \[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials<a name="fsbp-codebuild-2"></a>

**Category:** Protect > Secure development

**Severity:** Critical

**Resource type:** `AWS::CodeBuild::Project`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-envvar-awscred-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-envvar-awscred-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the project contains the environment variables `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`\.

Authentication credentials `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` should never be stored in clear text, as this could lead to unintended data exposure and unauthorized access\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Europe \(Milan\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="codebuild-2-remediation"></a>

To remediate this issue, update your CodeBuild project to remove the environment variable\.

**To remove environment variables from a CodeBuild project**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Expand **Build**\.

1. Choose **Build project**, and then choose the build project that contains plaintext credentials\.

1. From **Edit**, choose **Environment**\.

1. Expand **Additional configuration**\.

1. Choose **Remove** next to the environment variables\.

1. Choose **Update environment**\.

**To store sensitive values in the Amazon EC2 Systems Manager Parameter Store and then retrieve them from your build spec**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Expand **Build**\.

1. Choose **Build project**, and then choose the build project that contains plaintext credentials\.

1. From **Edit**, choose **Environment**\.

1. Expand **Additional configuration** and scroll to **Environment variables**\.

1. Follow [this tutorial](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-paramstore-console.html) to create a Systems Manager parameter that contains your sensitive data\.

1. After you create the parameter, copy the parameter name\.

1. Back in the CodeBuild console, choose **Create environmental variable**\.

1. Enter the name of your variable as it appears in your build spec\.

1. For **Value**, paste the name of your parameter\.

1. For **Type**, choose **Parameter**\.

1. To remove your noncompliant environmental variable that contains plaintext credentials, choose **Remove**\.

1. Choose **Update environment**\.

For more information, see [Environment variables in build environments](https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-env-vars.html) in the *AWS CodeBuild User Guide*\.

## \[CodeBuild\.4\] CodeBuild project environments should have a logging configuration<a name="fsbp-codebuild-4"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::CodeBuild::Project`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-logging-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a CodeBuild project environment has at least one log option, either to S3 or CloudWatch logs enabled\. This control fails if a CodeBuild project environment does not have at least one log option enabled\. 

From a security perspective, logging is an important feature to enable for future forensics efforts in the case of any security incidents\. Correlating anomalies in CodeBuild projects with threat detections can increase confidence in the accuracy of those threat detections\.

### Remediation<a name="codebuild-4-remediation"></a>

For more information on how to configure CodeBuild project log settings, see [Create a build project \(console\)](https://docs.aws.amazon.com/codebuild/latest/userguide/create-project-console.html#create-project-console-logs) in the CodeBuild User Guide\.

## \[CodeBuild\.5\] CodeBuild project environments should not have privileged mode enabled<a name="fsbp-codebuild-5"></a>

**Category:** Protect > Secure Access Management

**Severity:** High

**Resource type:** `AWS::CodeBuild::Project`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-environment-privileged-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-environment-privileged-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if an AWS CodeBuild project environment has privileged mode enabled\. This control fails when an AWS CodeBuild project environment has privileged mode enabled\.

By default, Docker containers do not allow access to any devices\. Privileged mode grants a build project's Docker container access to all devices\. Setting `privilegedMode` with value `true` enables running the Docker daemon inside a Docker container\. The Docker daemon listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes\. This parameter should only be set to true if the build project is used to build Docker images\. Otherwise, this setting should be disabled to prevent unintended access to Docker APIs as well as the container’s underlying hardware as unintended access to `privilegedMode` may risk malicious tampering or deletion of critical resources\.

### Remediation<a name="codebuild-5-remediation"></a>

For more information on how to configure CodeBuild project environment settings, see [Create a build project \(console\)](https://docs.aws.amazon.com/codebuild/latest/userguide/create-project-console.html#create-project-console-environment) in the CodeBuild User Guide

## \[Config\.1\] AWS Config should be enabled<a name="fsbp-config-1"></a>

**Category:** Identify > Inventory

**Severity:** Medium

**Resource type:** AWS account

**AWS Config rule:** None

**Schedule type:** Periodic

**Parameters:** None

This control checks whether AWS Config is enabled in the account for the local Region and is recording all resources\.

The AWS Config service performs configuration management of supported AWS resources in your account and delivers log files to you\. The recorded information includes the configuration item \(AWS resource\), relationships between configuration items, and any configuration changes between resources\. 

Security Hub recommends that you enable AWS Config in all Regions\. The AWS configuration item history that AWS Config captures enables security analysis, resource change tracking, and compliance auditing\. 

**Note**  
Config\.1 requires that AWS Config is enabled in all Regions in which you use Security Hub\.  
Because Security Hub is a Regional service, the check performed for this control checks only the current Region for the account\. It does not check all Regions\.   
To allow security checks against global resources in each Region, you also must record global resources\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.  
You may also consider disabling IAM\.1, IAM\.2, IAM\.3, IAM\.5, IAM\.8, and IAM\.21 in Regions in which global resource recording not enabled\. Since IAM is a global service, IAM resources will only be recorded in the Region in which global resource recording is enabled\.

To learn more, see [Getting started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.

### Remediation<a name="config-1-remediation"></a>

After you enable AWS Config, configure it to record all resources\.

**To configure AWS Config settings**

1. Open the AWS Config console at [https://console\.aws\.amazon\.com/config/](https://console.aws.amazon.com/config/)\.

1. Select the Region to configure AWS Config in\.

1. If you haven't used AWS Config before, see [Getting Started](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.

1. Navigate to the Settings page from the menu, and do the following:
   + Choose **Edit**\.
   + Under **Resource types to record**, select **Record all resources supported in this region** and **Include global resources \(e\.g\., AWS IAM resources\)**\.
   + Under **Data retention period**, choose the default retention period for AWS Config data, or specify a custom retention period\.
   + Under **AWS Config role**, either choose **Create AWS Config service\-linked role** or choose **Choose a role from your account** and then select the role to use\.
   + Under **Amazon S3 bucket**, specify the bucket to use or create a bucket and optionally include a prefix\.
   + Under **Amazon SNS topic**, select an Amazon SNS topic from your account or create one\. For more information about Amazon SNS, see the [https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html)\.

1. Choose **Save**\.

For more information about using AWS Config from the AWS CLI, see [Turning on AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/gs-cli-subscribe.html) in the *AWS Config Developer Guide*\. 

You can also use an AWS CloudFormation template to automate this process\. For more information, see the [AWS CloudFormation StackSets sample template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html) in the *AWS CloudFormation User Guide*\. 

## \[DMS\.1\] AWS Database Migration Service replication instances should not be public<a name="fsbp-dms-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::DMS::ReplicationInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dms-replication-not-public.html](https://docs.aws.amazon.com/config/latest/developerguide/dms-replication-not-public.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether AWS DMS replication instances are public\. To do this, it examines the value of the `PubliclyAccessible` field\.

A private replication instance has a private IP address that you cannot access outside of the replication network\. A replication instance should have a private IP address when the source and target databases are in the same network\. The network must also be connected to the replication instance's VPC using a VPN, AWS Direct Connect, or VPC peering\. To learn more about public and private replication instances, see [Public and private replication instances](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_ReplicationInstance.html#CHAP_ReplicationInstance.PublicPrivate) in the *AWS Database Migration Service User Guide*\.

You should also ensure that access to your AWS DMS instance configuration is limited to only authorized users\. To do this, restrict users’ IAM permissions to modify AWS DMS settings and resources\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="dms-1-remediation"></a>

Note that you cannot change the public access setting once a replication instance is created\. It must be deleted and recreated\.

**To configure the AWS DMS replication instances setting to block public access**

1. Open the AWS Database Migration Service console at [https://console\.aws\.amazon\.com/dms/](https://console.aws.amazon.com/dms/)\.

1. Navigate to** Replication instances**, then delete the public instance\. Choose the instance, choose **Actions**, then choose **delete**\.

1. Choose **Create replication instance**\. Provide the configuration details\.

1. To disable public access, make sure that **Publicly accessible** is not selected\.

1. Choose **Create**\.

For more information, see the section on [Creating a replication instance](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_ReplicationInstance.html#CHAP_ReplicationInstance.Creating) in the *AWS Database Migration Service User Guide*\.

## \[DynamoDB\.1\] DynamoDB tables should automatically scale capacity with demand<a name="fsbp-dynamodb-1"></a>

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::DynamoDB::Table`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-autoscaling-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-autoscaling-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether an Amazon DynamoDB table can scale its read and write capacity as needed\. This control passes if the table uses either on\-demand capacity mode or provisioned mode with auto scaling configured\. Scaling capacity with demand avoids throttling exceptions, which helps to maintain availability of your applications\.

DynamoDB tables in on\-demand capacity mode are only limited by the DynamoDB throughput default table quotas\. To raise these quotas, you can file a support ticket through [AWS Support](http://aws.amazon.com/support)\.

DynamoDB tables in provisioned mode with auto scaling adjust the provisioned throughput capacity dynamically in response to traffic patterns\. For additional information on DynamoDB request throttling, see [Request throttling and burst capacity](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/ProvisionedThroughput.html#ProvisionedThroughput.Throttling) in the *Amazon DynamoDB Developer Guide*\.

**Note**  
This control is not supported in AWS GovCloud \(US\-East\) or AWS GovCloud \(US\-West\)\.

### Remediation<a name="dynamodb-1-remediation"></a>

For detailed instructions on enabling DynamoDB automatic scaling on existing tables in capacity mode, see [Enabling DynamoDB auto scaling on existing tables](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/AutoScaling.Console.html#AutoScaling.Console.ExistingTable) in the*Amazon DynamoDB Developer Guide*\.

## \[DynamoDB\.2\] DynamoDB tables should have point\-in\-time recovery enabled<a name="fsbp-dynamodb-2"></a>

**Category:** Recover > Resilience > Backups enabled

**Severity:** Medium

**Resource type:** `AWS::DynamoDB::Table`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-pitr-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-pitr-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether point\-in\-time recovery \(PITR\) is enabled for an Amazon DynamoDB table\.

Backups help you to recover more quickly from a security incident\. They also strengthen the resilience of your systems\. DynamoDB point\-in\-time recovery automates backups for DynamoDB tables\. It reduces the time to recover from accidental delete or write operations\. DynamoDB tables that have PITR enabled can be restored to any point in time in the last 35 days\.

### Remediation<a name="dynamodb-2-remediation"></a>

To remediate this issue, add point\-in\-time recovery to your DynamoDB table\.

**To enable DynamoDB point\-in\-time recovery for an existing table**

1. Open the DynamoDB console at [https://console\.aws\.amazon\.com/dynamodb/](https://console.aws.amazon.com/dynamodb/)\.

1. Choose the table that you want to work with, and then choose **Backups**\. 

1. In the **Point\-in\-time Recovery** section, under **Status**, choose **Enable**\.

1. Choose **Enable** again to confirm the change\.

## \[DynamoDB\.3\] DynamoDB Accelerator \(DAX\) clusters should be encrypted at rest<a name="fsbp-dynamodb-3"></a>

**Category:** Protect > Data protection > Encryption of data at rest 

**Severity:** Medium

**Resource type:** `AWS::DAX::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dax-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/dax-encryption-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether a DAX cluster is encrypted at rest\. 

Encrypting data at rest reduces the risk of data stored on disk being accessed by a user not authenticated to AWS\. The encryption adds another set of access controls to limit the ability of unauthorized users to access to the data\. For example, API permissions are required to decrypt the data before it can be read\.

### Remediation<a name="dynamodb-3-remediation"></a>

You cannot enable or disable encryption at rest after a cluster is created\. You must recreate the cluster in order to enable encryption at rest\. For detailed instructions on how to create a DAX cluster with encryption at rest enabled, see[ Enabling encryption at rest using the AWS Management Console](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DAXEncryptionAtRest.html#dax.encryption.tutorial-console) in the *Amazon DynamoDB Developer Guide*\.

## \[EC2\.1\] Amazon EBS snapshots should not be public, determined by the availability to be restorable by anyone<a name="fsbp-ec2-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical 

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether Amazon Elastic Block Store snapshots are not public\. The control fails if Amazon EBS snapshots are restorable by anyone\.

EBS snapshots are used to back up the data on your EBS volumes to Amazon S3 at a specific point in time\. You can use the snapshots to restore previous states of EBS volumes\. It is rarely acceptable to share a snapshot with the public\. Typically the decision to share a snapshot publicly was made in error or without a complete understanding of the implications\. This check helps ensure that all such sharing was fully planned and intentional\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="ec2-1-remediation"></a>

To remediate this issue, update your EBS snapshot to make it private instead of public\.

**To make a public EBS snapshot private**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Elastic Block Store**, choose **Snapshots** menu and then choose your public snapshot\.

1. From **Actions**, choose **Modify permissions**\.

1. Choose **Private**\.

1. \(Optional\) Add the AWS account numbers of the authorized accounts to share your snapshot with and choose **Add Permission**\.

1. Choose **Save**\.

## \[EC2\.2\] The VPC default security group should not allow inbound and outbound traffic<a name="fsbp-ec2-2"></a>

**Category:** Protect > Secure network configuration

**Severity:** High 

**Resource type:** `AWS::EC2::SecurityGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks that the default security group of a VPC does not allow inbound or outbound traffic\.

The rules for the [default security group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#DefaultSecurityGroup) allow all outbound and inbound traffic from network interfaces \(and their associated instances\) that are assigned to the same security group\.

We do not recommend using the default security group\. Because the default security group cannot be deleted, you should change the default security group rules setting to restrict inbound and outbound traffic\. This prevents unintended traffic if the default security group is accidentally configured for resources such as EC2 instances\.

### Remediation<a name="ec2-2-remediation"></a>

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

1. Select a default security group and choose the **Inbound rules** tab\. Choose **Edit inbound rules**\. Then delete all inbound rules\. Choose **Save rules**\.

1. Repeat the previous step for each default security group\.

1. Select a default security group and choose the **Outbound rule** tab\. Choose **Edit outbound rules**\. Then delete all outbound rules\. Choose **Save rules**\.

1. Repeat the previous step for each default security group\.

For more information, see [Working with security groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the *Amazon VPC User Guide*\.

## \[EC2\.3\] Attached EBS volumes should be encrypted at rest<a name="fsbp-ec2-3"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::EC2::Volume`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/encrypted-volumes.html](https://docs.aws.amazon.com/config/latest/developerguide/encrypted-volumes.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the EBS volumes that are in an attached state are encrypted\. To pass this check, EBS volumes must be in use and encrypted\. If the EBS volume is not attached, then it is not subject to this check\.

For an added layer of security of your sensitive data in EBS volumes, you should enable EBS encryption at rest\. Amazon EBS encryption offers a straightforward encryption solution for your EBS resources that doesn't require you to build, maintain, and secure your own key management infrastructure\. It uses KMS keys when creating encrypted volumes and snapshots\.

To learn more about Amazon EBS encryption, see [Amazon EBS encryption](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html) in the *Amazon EC2 User Guide for Linux Instances*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="ec2-3-remediation"></a>

There is no direct way to encrypt an existing unencrypted volume or snapshot\. You can only encrypt a new volume or snapshot when you create it\.

If you enabled encryption by default, Amazon EBS encrypts the resulting new volume or snapshot using your default key for Amazon EBS encryption\. Even if you have not enabled encryption by default, you can enable encryption when you create an individual volume or snapshot\. In both cases, you can override the default key for Amazon EBS encryption and choose a symmetric customer managed key\.

For more information, see [Creating an Amazon EBS volume](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-creating-volume.html) and [Copying an Amazon EBS snapshot](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-copy-snapshot.html) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.4\] Stopped EC2 instances should be removed after a specified time period<a name="fsbp-ec2-4"></a>

**Category:** Identify > Inventory

**Severity:** Medium

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-stopped-instance.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-stopped-instance.html)

**Schedule type:** Periodic

**Parameters:**
+ `allowedDays`: 30

This control checks whether any EC2 instances have been stopped for more than the allowed number of days\. An EC2 instance fails this check if it is stopped for longer than the maximum allowed time period, which by default is 30 days\.

A failed finding indicates that an EC2 instance has not run for a significant period of time\. This creates a security risk because the EC2 instance is not being actively maintained \(analyzed, patched, updated\)\. If it is later launched, the lack of proper maintenance could result in unexpected issues in your AWS environment\. To safely maintain an EC2 instance over time in a nonrunning state, start it periodically for maintenance and then stop it after maintenance\. Ideally this is an automated process\. 

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="ec2-4-remediation"></a>

You can terminate an EC2 instance using either the console or the command line\.

Before you terminate the EC2 instance, verify that you won't lose any data:
+ Check that your Amazon EBS volumes will not be deleted on termination\.
+ Copy any data that you need from your EC2 instance store volumes to Amazon EBS or Amazon S3\. 

**To terminate an EC2 instance \(console\)**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Instances**, choose **Instances**\.

1. Select the instance, and then choose **Actions**, **Instance State**, **Terminate**\. 

1. When prompted for confirmation, choose **Yes, Terminate**\. 

**To terminate an EC2 instance \(AWS CLI, Tools for Windows PowerShell\)**  
Use one of the following commands\. For more information about the command line interface, see [Accessing Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html#access-ec2) in the *Amazon EC2 User Guide for Linux Instances*\.
+ From the AWS CLI, use [https://docs.aws.amazon.com/cli/latest/reference/ec2/terminate-instances.html](https://docs.aws.amazon.com/cli/latest/reference/ec2/terminate-instances.html)
+ From the Tools for Windows PowerShell, use [https://docs.aws.amazon.com/powershell/latest/reference/items/Stop-EC2Instance.html](https://docs.aws.amazon.com/powershell/latest/reference/items/Stop-EC2Instance.html)\.

To learn more about terminating instances, see [Terminating an instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/terminating-instances.html#terminating-instances-console) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.6\] VPC flow logging should be enabled in all VPCs<a name="fsbp-ec2-6"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::EC2::VPC`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html)

**Schedule type:** Periodic

**Parameters:**
+ `trafficType`: `REJECT`

This control checks whether Amazon VPC Flow Logs are found and enabled for VPCs\. The traffic type is set to `Reject`\. 

With the VPC Flow Logs feature, you can capture information about the IP address traffic going to and from network interfaces in your VPC\. After you create a flow log, you can view and retrieve its data in CloudWatch Logs\. To reduce cost, you can also send your flow logs to Amazon S3\. 

Security Hub recommends that you enable flow logging for packet rejects for VPCs\. Flow logs provide visibility into network traffic that traverses the VPC and can detect anomalous traffic or provide insight during security workflows\. 

By default, the record includes values for the different components of the IP address flow, including the source, destination, and protocol\. For more information and descriptions of the log fields, see [VPC Flow Logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html) in the *Amazon VPC User Guide*\.

### Remediation<a name="ec2-6-remediation"></a>

To remediate this issue, enable VPC flow logging\.

**To enable VPC flow logging**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Under **Virtual Private Cloud**, choose **Your VPCs**\.

1. Select a VPC to update\.

1. At the bottom of the page, choose **Flow Logs**\.

1. Choose **Create flow log**\.

1. For **Filter**, choose **Reject**\.

1. For **Destination log group**, choose the log group to use\.

1. For **IAM role**, choose the IAM role to use\.

1. Choose **Create**\.

## \[EC2\.7\] EBS default encryption should be enabled<a name="fsbp-ec2-7"></a>

**Category:** Protect > Data protection > Encryption of data at rest 

**Severity:** Medium

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-ebs-encryption-by-default.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-ebs-encryption-by-default.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether account\-level encryption is enabled by default for Amazon Elastic Block Store\(Amazon EBS\)\. The control fails if the account level encryption is not enabled\. 

When encryption is enabled for your account, Amazon EBS volumes and snapshot copies are encrypted at rest\. This adds an additional layer of protection for your data\. For more information, see [Encryption by default](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html#encryption-by-default) in the *Amazon EC2 User Guide for Linux Instances*\.

Note that following instance types do not support encryption: R1, C1, and M1\.

**Note**  
This control is not supported in Asia Pacific \(Jakarta\) or Asia Pacific \(Osaka\)\.

### Remediation<a name="ec2-7-remediation"></a>

You can use the Amazon EC2 console to enable default encryption for Amazon EBS volumes\.

**To configure the default encryption for Amazon EBS encryption for a Region**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the navigation pane, select **EC2 Dashboard**\.

1. In the upper\-right corner of the page, choose **Account Attributes, EBS encryption**\.

1. Choose **Manage**\.

1. Select **Enable**\. You can keep the AWS managed key with the alias `alias/aws/ebs` created on your behalf as the default encryption key, or choose a symmetric customer managed key\.

1. Choose **Update EBS encryption**\.

## \[EC2\.8\] EC2 instances should use IMDSv2<a name="fsbp-ec2-8"></a>

**Category:** Protect > Network security

**Severity:** High

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-imdsv2-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-imdsv2-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether your EC2 instance metadata version is configured with Instance Metadata Service Version 2 \(IMDSv2\)\. The control passes if `HttpTokens` is set to required for IMDSv2\. The control fails if `HttpTokens` is set to `optional`\.

You use instance metadata to configure or manage the running instance\. The IMDS provides access to temporary, frequently rotated credentials\. These credentials remove the need to hard code or distribute sensitive credentials to instances manually or programmatically\. The IMDS is attached locally to every EC2 instance\. It runs on a special "link local" IP address of 169\.254\.169\.254\. This IP address is only accessible by software that runs on the instance\.

Version 2 of the IMDS adds new protections for the following types of vulnerabilities\. These vulnerabilities could be used to try to access the IMDS\.
+ Open website application firewalls
+ Open reverse proxies
+ Server\-side request forgery \(SSRF\) vulnerabilities
+ Open Layer 3 firewalls and network address translation \(NAT\)

Security Hub recommends that you configure your EC2 instances with IMDSv2\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="ec2-8-remediation"></a>

To remediate an EC2 instance that is not configured with IMDSv2, you can require the use of IMDSv2\.

To require IMDSv2 on an existing instance, when you request instance metadata, modify the Amazon EC2 metadata options\. Follow the instructions in [Configuring instance metadata options for existing instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html) in the *Amazon EC2 User Guide for Linux Instances*\.

To require the use of IMDSv2 on a new instance when you launch it, follow the instructions in [Configuring instance metadata options for new instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html) in the *Amazon EC2 User Guide for Linux Instances*\.

**To configure your new EC2 instance with IMDSv2 from the console**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. Choose **Launch instance**, and then choose **Launch instance**\.

1. Under **Advanced details**, for **Metadata version**, choose **V2 only \(token required\)**\.

1. In the Summary panel, review your changes, and then choose **Launch instance**\.

If your software uses IMDSv1, you can reconfigure your software to use IMDSv2\. For details, see [Transitioning to using Instance Metadata Service Version 2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html#instance-metadata-transition-to-version-2) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.9\] EC2 instances should not have a public IP address<a name="fsbp-ec2-9"></a>

**Category:** Protect > Secure network configuration > Public IP addresses

**Severity:** High

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-no-public-ip.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-no-public-ip.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether EC2 instances have a public IP address\. The control fails if the `publicIp` field is present in the EC2 instance configuration item\. This control applies to IPv4 addresses only\. 

A public IPv4 address is an IP address that is reachable from the internet\. If you launch your instance with a public IP address, then your EC2 instance is reachable from the internet\. A private IPv4 address is an IP address that is not reachable from the internet\. You can use private IPv4 addresses for communication between EC2 instances in the same VPC or in your connected private network\.

IPv6 addresses are globally unique, and therefore are reachable from the internet\. However, by default all subnets have the IPv6 addressing attribute set to false\. For more information about IPv6, see [IP addressing in your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-ip-addressing.html) in the *Amazon VPC User Guide*\.

If you have a legitimate use case to maintain EC2 instances with public IP addresses, then you can suppress the findings from this control\. For more information about front\-end architecture options, see the [AWS Architecture Blog](http://aws.amazon.com/blogs/architecture/) or the [This Is My Architecture series](http://aws.amazon.com/this-is-my-architecture/?tma.sort-by=item.additionalFields.airDate&tma.sort-order=desc&awsf.category=categories%23mobile)\.

### Remediation<a name="ec2-9-remediation"></a>

Use a non\-default VPC so that your instance is not assigned a public IP address by default\.

When you launch an EC2 instance into a default VPC, it is assigned a public IP address\. When you launch an EC2 instance into a non\-default VPC, the subnet configuration determines whether it receives a public IP address\. The subnet has an attribute to determine if new EC2 instances in the subnet receive a public IP address from the public IPv4 address pool\.

You cannot manually associate or disassociate an automatically\-assigned public IP address from your EC2 instance\. To control whether your EC2 instance receives a public IP address, do one of the following:
+ Modify the public IP addressing attribute of your subnet\. For more information, see [Modifying the public IPv4 addressing attribute for your subnet](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-ip-addressing.html#subnet-public-ip) in the *Amazon VPC User Guide*\. 
+ Enable or disable the public IP addressing feature during launch\. This overrides the subnet's public IP addressing attribute\. For more information, see[ Assign a public IPv4 address during instance launch](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html#public-ip-addresses) in the *Amazon EC2 User Guide for Linux Instances*\.

For more information, see [Public IPv4 addresses and external DNS hostnames](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html#concepts-public-addresses) in the *Amazon EC2 User Guide for Linux Instances*\.

If your EC2 instance is associated with an Elastic IP address, then your EC2 instance is reachable from the internet\. You can disassociate an Elastic IP address from an instance or network interface at any time\.

**To disassociate an Elastic IP address**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Elastic IPs**\.

1. Select the Elastic IP address to disassociate\.

1. From **Actions**, choose **Disassociate Elastic IP address**\.

1. Choose **Disassociate**\.

## \[EC2\.10\] Amazon EC2 should be configured to use VPC endpoints that are created for the Amazon EC2 service<a name="fsbp-ec2-10"></a>

**Category:** Protect \- Secure network configuration > API private access

**Severity:** Medium

**Resource type:** `AWS::EC2::VPC`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/service-vpc-endpoint-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/service-vpc-endpoint-enabled.html)

**Schedule type:** Periodic

**Parameters:** 
+ `serviceName`: `ec2`

This control checks whether a service endpoint for Amazon EC2 is created for each VPC\. The control fails if a VPC does not have a VPC endpoint created for the Amazon EC2 service\. 

This control evaluates resources in single account\. It cannot describe resources that are outside of the account\. Because AWS Config and Security Hub do not conduct cross\-account checks, you will see `FAILED` findings for VPCs that are shared across accounts\. Security Hub recommends that you suppress these `FAILED` findings\.

To improve the security posture of your VPC, you can configure Amazon EC2 to use an interface VPC endpoint\. Interface endpoints are powered by AWS PrivateLink, a technology that enables you to access Amazon EC2 API operations privately\. It restricts all network traffic between your VPC and Amazon EC2 to the Amazon network\. Because endpoints are supported within the same Region only, you cannot create an endpoint between a VPC and a service in a different Region\. This prevents unintended Amazon EC2 API calls to other Regions\. 

To learn more about creating VPC endpoints for Amazon EC2, see [Amazon EC2 and interface VPC endpoints ](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/interface-vpc-endpoints.html)in the *Amazon EC2 User Guide for Linux Instances*\.

### Remediation<a name="ec2-10-remediation"></a>

To remediate this issue, you can create an interface VPC endpoint to Amazon EC2\.

**To create an interface endpoint to Amazon EC2 from the Amazon VPC console**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Endpoints**\.

1. Choose **Create Endpoint**\. 

1. For **Service category**, choose **AWS services**\. 

1. For **Service Name**, choose **com\.amazonaws\.<region>\.ec2**\.

1. For **Type**, choose **Interface**\. 

1. Complete the following information\. 

   1. For **VPC**, select a VPC in which to create the endpoint\. 

   1. For **Subnets**, select the subnets \(Availability Zones\) in which to create the endpoint network interfaces\. Not all Availability Zones are supported for all AWS services\. 

   1. To enable private DNS for the interface endpoint, select the check box for **Enable DNS Name**\. This option is enabled by default\.

      To use the private DNS option, the following attributes of your VPC must be set to true:
      + `enableDnsHostnames`
      + `enableDnsSupport`

      For more information, see [Viewing and updating DNS support for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-dns-updating) in the *Amazon VPC User Guide*\. 

   1. For **Security group**, select the security groups to associate with the endpoint network interfaces\. 

   1. \(Optional\) Add or remove a tag\. To add a tag, choose **Add tag** and do the following: 
      + For **Key**, enter the tag name\. 
      + For **Value**, enter the tag value\.

   1. To remove a tag, choose the delete button \(**x**\) to the right of the tag **Key** and **Value**\. 

1. Choose **Create endpoint**\.

**To create an interface VPC endpoint policy**

You can attach a policy to your VPC endpoint to control access to the Amazon EC2 API\. The policy specifies the following: 
+ The principal that can perform actions
+ The actions that can be performed
+ The resource on which the actions can be performed

For more details on creating a VPC endpoint policy, see [Amazon EC2 and interface VPC endpoints](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/interface-vpc-endpoints.html) In the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.15\] EC2 subnets should not automatically assign public IP addresses<a name="fsbp-ec2-15"></a>

**Category:** Protect > Network security

**Severity:** Medium

**Resource type:** `AWS::EC2::Subnet`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/subnet-auto-assign-public-ip-disabled.html](https://docs.aws.amazon.com/config/latest/developerguide/subnet-auto-assign-public-ip-disabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the assignment of public IPs in Amazon Virtual Private Cloud \(Amazon VPC\) subnets have `MapPublicIpOnLaunch` set to `FALSE`\. The control passes if the flag is set to `FALSE`\. 

All subnets have an attribute that determines whether a network interface created in the subnet automatically receives a public IPv4 address\. Instances that are launched into subnets that have this attribute enabled have a public IP address assigned to their primary network interface\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-15-remediation"></a>

You can configure a subnet from the Amazon VPC console\.

**To configure a subnet to not assign public IP addresses**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Subnets**\.

1. Select your subnet and then choose **Subnet Actions**, **Modify auto\-assign IP settings**\.

1. Clear the **Enable auto\-assign public IPv4 address** check box and then choose **Save**\.

## \[EC2\.16\] Unused network access control lists should be removed<a name="fsbp-ec2-16"></a>

**Category:** Prevent > Network security 

**Severity:** Low

**Resource type:** `AWS::EC2::NetworkAcl`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-network-acl-unused-check.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-network-acl-unused-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether there are any unused network access control lists \(ACLs\)\.

The control checks the item configuration of the resource `AWS::EC2::NetworkAcl` and determines the relationships of the network ACL\.

If the only relationship is the VPC of the network ACL, then the control fails\.

If other relationships are listed, then the control passes\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-16-remediation"></a>

For instructions on how to delete an unused network ACL, see [Deleting a network ACL](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html#DeleteNetworkACL) in the *Amazon VPC User Guide*\. You cannot delete the default network ACL or an ACL that is associated with subnets\.

## \[EC2\.17\] EC2 instances should not use multiple ENIs<a name="fsbp-ec2-17"></a>

**Category:** Network security 

**Severity:** Low

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-multiple-eni-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-multiple-eni-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `Adapterids` \(Optional\) – A list of network interface IDs that are attached to EC2 instances

This control checks whether an EC2 instance uses multiple Elastic Network Interfaces \(ENIs\) or Elastic Fabric Adapters \(EFAs\)\. This control passes if a single network adapter is used\. The control includes an optional parameter list to identify the allowed ENIs\.

Multiple ENIs can cause dual\-homed instances, meaning instances that have multiple subnets\. This can add network security complexity and introduce unintended network paths and access\.

This control also fails if an Amazon EKS cluster that belongs to an Amazon EKS cluster has more than one ENI\. If you need to use EC2 instances that have multiple ENIs as part of an Amazon EKS cluster, you can suppress those findings\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-17-remediation"></a>

To remediate this issue, detach the additional ENIs\.

**To detach a network interface**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. Under **Network & Security**, choose **Network Interfaces**\.

1. Filter the list by the noncompliant instance IDs to see the associated ENIs\.

1. Select the ENIs that you want to remove\.

1. From the **Actions** menu, choose **Detach**\.

1. If you see the prompt **Are you sure that you want to detach the following network interface?**, choose **Detach**\.

## \[EC2\.18\] Security groups should only allow unrestricted incoming traffic for authorized ports<a name="fsbp-ec2-18"></a>

**Category:** Protect > Secure network configuration > Security group configuration

**Severity:** High

**Resource type:** `AWS::EC2::SecurityGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-sg-open-only-to-authorized-ports.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-sg-open-only-to-authorized-ports.html)

**Schedule type:** Change triggered

**Parameters:**
+ `authorizedTcpPorts` \(Optional\) – Comma\-separated list of ports to which to allow unrestricted access\. For example: `'80, 443'`\. For this rule, the default values for `authorizedTcpPorts` are 80 and 443\.

This control checks whether the security groups that are in use allow unrestricted incoming traffic\. Optionally the rule checks whether the port numbers are listed in the `authorizedTcpPorts` parameter\.
+ If the security group rule port number allows unrestricted incoming traffic, but the port number is specified in `authorizedTcpPorts`, then the control passes\. The default value for `authorizedTcpPorts` is `80, 443`\.
+ If the security group rule port number allows unrestricted incoming traffic, but the port number is not specified in `authorizedTcpPorts` input parameter, then the control fails\.
+ If the parameter is not used, then the control fails for any security group that has an unrestricted inbound rule\.

Security groups provide stateful filtering of ingress and egress network traffic to AWS\. Security group rules should follow the principal of least privileged access\. Unrestricted access \(IP address with a /0 suffix\) increases the opportunity for malicious activity such as hacking, denial\-of\-service attacks, and loss of data\.

Unless a port is specifically allowed, the port should deny unrestricted access\.

**Note**  
This control is not supported in Asia Pacific \(Osaka\)\.

### Remediation<a name="ecs-18-remediation"></a>

For information on how to modify a security group, see [Add, remove, or update rules](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#AddRemoveRules) in the *Amazon VPC User Guide*\.

## \[EC2\.19\] Security groups should not allow unrestricted access to ports with high risk<a name="fsbp-ec2-19"></a>

**Category:** Protect > Restricted network access

**Severity:** Critical

**Resource type:** `AWS::EC2::SecurityGroup`

**AWS Config rule:** `vpc-sg-restricted-common-ports` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether unrestricted incoming traffic for the security groups is accessible to the specified ports that have the highest risk\. This control passes when none of the rules in a security group allow ingress traffic from 0\.0\.0\.0/0 for those ports\.

Unrestricted access \(0\.0\.0\.0/0\) increases opportunities for malicious activity, such as hacking, denial\-of\-service attacks, and loss of data\.

Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\. No security group should allow unrestricted ingress access to the following ports:
+ 20, 21 \(FTP\)
+ 22 \(SSH\)
+ 23 \(Telnet\)
+ 25 \(SMTP\)
+ 110 \(POP3\)
+ 135 \(RPC\)
+ 143 \(IMAP\)
+ 445 \(CIFS\)
+ 1433, 1434 \(MSSQL\)
+ 3000 \(Go, Node\.js, and Ruby web development frameworks\)
+ 3306 \(mySQL\)
+ 3389 \(RDP\)
+ 4333 \(ahsp\)
+ 5000 \(Python web development frameworks\)
+ 5432 \(postgresql\)
+ 5500 \(fcp\-addr\-srvr1\) 
+ 5601 \(OpenSearch Dashboards\)
+ 8080 \(proxy\)
+ 8088 \(legacy HTTP port\)
+ 8888 \(alternative HTTP port\)
+ 9200 or 9300 \(OpenSearch\)

### Remediation<a name="ec2-19-remediation"></a>

For information on how to delete rules from a security group, see [Delete rules from a security group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-security-groups.html#deleting-security-group-rule) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.20\] Both VPN tunnels for an AWS Site\-to\-Site VPN connection should be up<a name="fsbp-ec2-20"></a>

**Category:** Resilience > Recover > High availability

**Severity:** Medium 

**Resource type:**`AWS::EC2::VPNConnection`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-vpn-2-tunnels-up.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-vpn-2-tunnels-up.html)

**Schedule type:** Change triggered

**Parameters:** None

A VPN tunnel is an encrypted link where data can pass from the customer network to or from AWS within an AWS Site\-to\-Site VPN connection\. Each VPN connection includes two VPN tunnels which you can simultaneously use for high availability\. Ensuring that both VPN tunnels are up for a VPN connection is important for confirming a secure and highly available connection between an AWS VPC and your remote network\.

This control checks that both VPN tunnels provided by AWS Site\-to\-Site VPN are in UP status\. The control fails if one or both tunnels are in DOWN status\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)

### Remediation<a name="ec2-20-remediation"></a>

To modify VPN tunnel options, see [Modifying Site\-to\-Site VPN tunnel options](https://docs.aws.amazon.com/vpn/latest/s2svpn/modify-vpn-tunnel-options.html) in the AWS Site\-to\-Site VPN User Guide\.

## \[EC2\.21\] Network ACLs should not allow ingress from 0\.0\.0\.0/0 to port 22 or port 3389<a name="fsbp-ec2-21"></a>

**Category:** Protect > Secure Network Configuration

**Severity:** Medium 

**Resource type:**`AWS::EC2::NetworkAcl`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/nacl-no-unrestricted-ssh-rdp.html](https://docs.aws.amazon.com/config/latest/developerguide/nacl-no-unrestricted-ssh-rdp.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a network access control list \(NACL\) allows unrestricted access to the default TCP ports for SSH/RDP ingress traffic\. The rule fails if a NACL inbound entry allows a source CIDR block of '0\.0\.0\.0/0' or '::/0' for TCP ports 22 or 3389\.

Access to remote server administration ports, such as port 22 \(SSH\) and port 3389 \(RDP\), should not be publicly accessible, as this may allow unintended access to resources within your VPC\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-21-remediation"></a>

For more information about NACLs, see [Network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html) in the VPC User Guide\.

## \[EC2\.22\] Unused EC2 security groups should be removed<a name="fsbp-ec2-22"></a>

**Category:** Identify > Inventory

**Severity:** Medium 

**Resource type:**`AWS::EC2::SecurityGroup`, `AWS::EC2::NetworkInterface`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-security-group-attached-to-eni-periodic.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-security-group-attached-to-eni-periodic.html)

**Schedule type:** Periodic

**Parameters:** None

This AWS control checks that security groups are attached to Amazon Elastic Compute Cloud \(Amazon EC2\) instances or to an elastic network interface\. The control will fail if the security group is not associated with an Amazon EC2 instance or an elastic network interface\.

### Remediation<a name="ec2-22-remediation"></a>

To create, assign and delete security groups, see [Security groups](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/working-with-security-groups.html#deleting-security-group) in Amazon EC2 user guide\.

## \[EC2\.23\] EC2 Transit Gateways should not automatically accept VPC attachment requests<a name="fsbp-ec2-23"></a>

**Category:** Protect > Secure network configuration

**Severity:** High 

**Resource type:**`AWS::EC2::TransitGateway`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-transit-gateway-auto-vpc-attach-disabled.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-transit-gateway-auto-vpc-attach-disabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if EC2 Transit Gateways are automatically accepting shared VPC attachments\. This control fails for a Transit Gateway that automatically accepts shared VPC attachment requests\.

Turning on `AutoAcceptSharedAttachments` configures a Transit Gateway to automatically accept any cross\-account VPC attachment requests without verifying the request or the account the attachment is originating from\. To follow the best practices of authorization and authentication, we recommended turning off this feature to ensure that only authorized VPC attachment requests are accepted\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Hong Kong\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-23-remediation"></a>

For information about how to modify a Transit Gateway, see [Modify a transit gateway](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-transit-gateways.html#tgw-modifying) in the Amazon VPC Developer Guide\.

## \[EC2\.24\] Paravirtual EC2 instance types should not be used<a name="fsbp-ec2-24"></a>

**Category:** Identify > Vulnerability, patch, and version management

**Severity:** Medium 

**Resource type:**`AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-paravirtual-instance-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-paravirtual-instance-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the virtualization type of an EC2 instance is paravirtual\. The control fails if the `virtualizationType` of the EC2 instance is set to `paravirtual`\.

Linux Amazon Machine Images \(AMIs\) use one of two types of virtualization: paravirtual \(PV\) or hardware virtual machine \(HVM\)\. The main differences between PV and HVM AMIs are the way in which they boot and whether they can take advantage of special hardware extensions \(CPU, network, and storage\) for better performance\.

Historically, PV guests had better performance than HVM guests in many cases, but because of enhancements in HVM virtualization and the availability of PV drivers for HVM AMIs, this is no longer true\. For more information, see [Linux AMI virtualization types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/virtualization_types.html) in the Amazon EC2 User Guide for Linux Instances\.

**Note**  
This control is not supported in the following Regions:  
US East \(Ohio\)
Africa \(Cape Town\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Jakarta\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Osaka\)
Asia Pacific \(Seoul\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ec2-24-remediation"></a>

For information about how to update an EC2 instance to a new instance type, see [Change the instance type](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-resize.html) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[ECR\.1\] ECR private repositories should have image scanning configured<a name="fsbp-ecr-1"></a>

**Category:** Identify > Vulnerability, patch, and version management

**Severity:** High

**Resource type:** `AWS::ECR::Repository`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-image-scanning-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-image-scanning-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a private ECR repository has image scanning configured\. This control fails if a private ECR repository doesn't have image scanning configured\. Note that you must also configure [scan on push](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html#image-scanning-filters) for each repository to pass this control\.

ECR image scanning helps in identifying software vulnerabilities in your container images\. ECR uses the Common Vulnerabilities and Exposures \(CVEs\) database from the [open\-source Clair project ](https://github.com/quay/clair) and provides a list of scan findings\. Enabling image scanning on ECR repositories adds a layer of verification for the integrity and safety of the images being stored\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecr-1-remediation"></a>

To configure image scanning for an ECR repository, see [Image scanning](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html) in the *Amazon Elastic Container Registry User Guide*\.

## \[ECR\.2\] ECR private repositories should have tag immutability configured<a name="fsbp-ecr-2"></a>

**Category:** Identify > Inventory > Tagging

**Severity:** Medium

**Resource type:** `AWS::ECR::Repository`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-tag-immutability-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-tag-immutability-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a private ECR repository has tag immutability enabled\. This control fails if a private ECR repository has tag immutability disabled\. This rule passes if tag immutability is enabled and has the value `IMMUTABLE`\.

Amazon ECR Tag Immutability enables customers to rely on the descriptive tags of an image as a reliable mechanism to track and uniquely identify images\. An immutable tag is static, which means each tag refers to a unique image\. This improves reliability and scalability as the use of a static tag will always result in the same image being deployed\. When configured, tag immutability prevents the tags from being overridden, which reduces the attack surface\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecr-2-remediation"></a>

To create a repository with immutable tags configured or to update the image tag mutability settings for an existing repository, see [Image tag mutability](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-tag-mutability.html) in the *Amazon Elastic Container Registry User Guide*\.

## \[ECR\.3\] ECR repositories should have at least one lifecycle policy configured<a name="fsbp-ecr-3"></a>

**Category:** Identify > Resource configuration

**Severity:** Medium

**Resource type:** `AWS::ECR::Repository`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-lifecycle-policy-configured.html](https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-lifecycle-policy-configured.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon ECR repository has at least one lifecycle policy configured\. This control fails if an ECR repository does not have any lifecycle policies configured\.

Amazon ECR lifecycle policies enable you to specify the lifecycle management of images in a repository\. By configuring lifecycle policies, you can automate the cleanup of unused images and the expiration of images based on age or count\. Automating these tasks can help you avoid unintentionally using outdated images in your repository\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecr-3-remediation"></a>

To configure a lifecycle policy, see [Creating a lifecycle policy preview](https://docs.aws.amazon.com/AmazonECR/latest/userguide/lpp_creation.html) in the *Amazon Elastic Container Registry User Guide*\.

## \[ECS\.1\] Amazon ECS task definitions should have secure networking modes and user definitions<a name="fsbp-ecs-1"></a>

**Category:** Protect > Secure access management

**Severity:** High

**Resource type:** `AWS::ECS::TaskDefinition`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecs-task-definition-user-for-host-mode-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ecs-task-definition-user-for-host-mode-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `SkipInactiveTaskDefinitions`: `true`

This control checks whether an active Amazon ECS task definition that has host networking mode also has `privileged` or `user` container definitions\. The control fails for task definitions that have host network mode and container definitions where `privileged=false` or is empty and `user=root` or is empty\. This control only evaluates the latest active revision of an Amazon ECS task definition\.

If a task definition has elevated privileges, it is because the customer has specifically opted in to that configuration\. This control checks for unexpected privilege escalation when a task definition has host networking enabled but the customer has not opted in to elevated privileges\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-1-remediation"></a>

For information on how to update a task definition, see [Updating a task definition](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/update-task-definition.html) in the *Amazon Elastic Container Service Developer Guide*\.

Note that when you update a task definition, it does not update running tasks that were launched from the previous task definition\. To update a running task, you must redeploy the task with the new task definition\.

## \[ECS\.2\] Amazon ECS services should not have public IP addresses assigned to them automatically<a name="fsbp-ecs-2"></a>

**Category:** Protect > Secure network configuration > Resources not publicly accessible

**Severity:** High

**Resource type:** `AWS::ECS::Service`

**AWS Configrule:** `ecs-service-assign-public-ip-disabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:**
+ `exemptEcsServiceArns` \(Optional\)\. Security Hub does not populate this parameter\. Comma\-separated list of ARNs of Amazon ECS services that are exempt from this rule\.

  This rule is `COMPLIANT` if an Amazon ECS service has `AssignPublicIP` set to `ENABLED` and is specified in this parameter list\.

  This rule is `NON_COMPLIANT` if an Amazon ECS service has `AssignPublicIP` set to `ENABLED` and is not specified in this parameter list\.

This control checks whether Amazon ECS services are configured to automatically assign public IP addresses\. This control fails if `AssignPublicIP` is `ENABLED`\. This control passes if `AssignPublicIP` is `DISABLED`\.

A public IP address is an IP address that is reachable from the internet\. If you launch your Amazon ECS instances with a public IP address, then your Amazon ECS instances are reachable from the internet\. Amazon ECS services should not be publicly accessible, as this may allow unintended access to your container application servers\.

**Note**  
This control is not supported in the Asia Pacific \(Osaka\) Region\.

### Remediation<a name="ecs-2-remediation"></a>

To disable automatic public IP assignment, see [To configure VPC and security group settings for your service](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-configure-network.html) in the *Amazon Elastic Container Service Developer Guide*\.

## \[ECS\.3\] ECS task definitions should not share the host's process namespace<a name="fsbp-ecs-3"></a>

**Category:** Identify > Resource configuration

**Severity:** High

**Resource type:** `AWS::ECS::TaskDefinition`

**AWS Configrule:** [ecs\-task\-definition\-pid\-mode\-check](https://docs.aws.amazon.com/config/latest/developerguide/ecs-task-definition-pid-mode-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon ECS task definitions are configured to share a host’s process namespace with its containers\. The control fails if the task definition shares the host's process namespace with the containers running on it\. This control only evaluates the latest active revision of an Amazon ECS task definition\.

A process ID \(PID\) namespace provides separation between processes\. It prevents system processes from being visible, and allows PIDs to be reused, including PID 1\. If the host’s PID namespace is shared with containers, it would allow containers to see all of the processes on the host system\. This reduces the benefit of process level isolation between the host and the containers\. These circumstances could lead to unauthorized access to processes on the host itself, including the ability to manipulate and terminate them\. Customers shouldn’t share the host’s process namespace with containers running on it\.

### Remediation<a name="ecs-3-remediation"></a>

To configure the `pidMode` on a task definition, see [Task definition parameters](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definition_parameters.html#task_definition_pidmode) in the Amazon Elastic Container Service Developer Guide\.

## \[ECS\.4\] ECS containers should run as non\-privileged<a name="fsbp-ecs-4"></a>

**Category:** Protect > Secure access management > Root user access restrictions

**Severity:** High

**Resource type:** `AWS::ECS::TaskDefinition`

**AWS Configrule:** [ecs\-containers\-nonprivileged](https://docs.aws.amazon.com/config/latest/developerguide/ecs-containers-nonprivileged.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if the `privileged` parameter in the container definition of Amazon ECS Task Definitions is set to `true`\. The control fails if this parameter is equal to `true`\. This control only evaluates the latest active revision of an Amazon ECS task definition\.

We recommend that you remove elevated privileges from your ECS task definitions\. When the privilege parameter is `true`, the container is given elevated privileges on the host container instance \(similar to the root user\)\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-4-remediation"></a>

To configure the `privileged` parameter on a task definition, see [Advanced container definition parameters](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definition_parameters.html#container_definition_security) in the Amazon Elastic Container Service Developer Guide\.

## \[ECS\.5\] ECS containers should be limited to read\-only access to root filesystems<a name="fsbp-ecs-5"></a>

**Category:** Protect > Secure access management

**Severity:** High

**Resource type:** `AWS::ECS::TaskDefinition`

**AWS Configrule:** [ecs\-containers\-readonly\-access](https://docs.aws.amazon.com/config/latest/developerguide/ecs-containers-readonly-access.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon ECS containers are limited to read\-only access to mounted root filesystems\. This control fails if the `ReadonlyRootFilesystem` parameter in the container definition of Amazon ECS task definitions is set to `false`\. This control only evaluates the latest active revision of an Amazon ECS task definition\.

Enabling this option reduces security attack vectors since the container instance’s filesystem cannot be tampered with or written to unless it has explicit read\-write permissions on its filesystem folder and directories\. This control also adheres to the principle of least privilege\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-5-remediation"></a>

**To limit container definitions to read\-only access to root filesystems**

1. Open the Amazon ECS console at [https://console\.aws\.amazon\.com/ecs/](https://console.aws.amazon.com/ecs/)\.

1. In the left navigation pane, choose **Task Definitions**\.

1. For each task definition that has container definitions that need to be updated, do the following:
   + Select the container definition that needs to be updated\.
   + Choose **Edit Container**\. For **Storage and Logging**, select **Read only root file system**\.
   + Choose **Update** at the bottom of the **Edit Container** tab\.
   + Choose **Create**\.

## \[ECS\.8\] Secrets should not be passed as container environment variables<a name="fsbp-ecs-8"></a>

**Category:** Protect > Secure development > Credentials not hard\-coded

**Severity:** High

**Resource type:** `AWS::ECS::TaskDefinition`

**AWS Configrule:** [ecs\-no\-environment\-secrets](https://docs.aws.amazon.com/config/latest/developerguide/ecs-no-environment-secrets.html) 

**Schedule type:** Change triggered

**Parameters:** 
+  secretKeys = `AWS_ACCESS_KEY_ID`,`AWS_SECRET_ACCESS_KEY`,`ECS_ENGINE_AUTH_DATA` 

This control checks if the key value of any variables in the `environment` parameter of container definitions includes `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, or `ECS_ENGINE_AUTH_DATA`\. This control fails if a single environment variable in any container definition equals `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, or `ECS_ENGINE_AUTH_DATA`\. This control does not cover environmental variables passed in from other locations such as Amazon S3\. This control only evaluates the latest active revision of an Amazon ECS task definition\.

AWS Systems Manager Parameter Store can help you improve the security posture of your organization\. We recommend using the Parameter Store to store secrets and credentials instead of directing passing them into your container instances or hard coding them into your code\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-8-remediation"></a>

To create parameters using SSM, see [Creating Systems Manager parameters](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-paramstore-su-create.html) in the *AWS Systems Manager User Guide*\. For more information about creating a task definition that specifies a secret, see [Specifying sensitive data using Secrets Manager](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/specifying-sensitive-data-secrets.html#secrets-create-taskdefinition) in the *Amazon Elastic Container Service Developer Guide*\.

## \[ECS\.10\] Fargate services should run on the latest Fargate platform version<a name="fsbp-ecs-10"></a>

**Category:** Identify > Vulnerability, patch, and version management

**Severity:** Medium

**Resource type:** `AWS::ECS::Service`

**AWS Configrule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecs-fargate-latest-platform-version.html](https://docs.aws.amazon.com/config/latest/developerguide/ecs-fargate-latest-platform-version.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon ECS Fargate services are running the latest Fargate platform version\. This control fails if the platform version is not the latest\.

AWS Fargate platform versions refer to a specific runtime environment for Fargate task infrastructure, which is a combination of kernel and container runtime versions\. New platform versions are released as the runtime environment evolves\. For example, a new version may be released for kernel or operating system updates, new features, bug fixes, or security updates\. Security updates and patches are deployed automatically for your Fargate tasks\. If a security issue is found that affects a platform version, AWS patches the platform version\. 

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-10-remediation"></a>

To update an existing service, including its platform version, see [Updating a service](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/update-service.html) in the *Amazon Elastic Container Service Developer Guide*\.

## \[ECS\.12\] ECS clusters should have Container Insights enabled<a name="fsbp-ecs-12"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::ECS::Cluster`

**AWS Configrule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecs-container-insights-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/ecs-container-insights-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if ECS clusters use Container Insights\. This control fails if Container Insights are not set up for a cluster\.

Monitoring is an important part of maintaining the reliability, availability, and performance of Amazon ECS clusters\. Use CloudWatch Container Insights to collect, aggregate, and summarize metrics and logs from your containerized applications and microservices\. CloudWatch automatically collects metrics for many resources, such as CPU, memory, disk, and network\. Container Insights also provides diagnostic information, such as container restart failures, to help you isolate issues and resolve them quickly\. You can also set CloudWatch alarms on metrics that Container Insights collects\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-12-remediation"></a>

To use Container Insights, see [Updating a service](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/deploy-container-insights-ECS.html) in the *Amazon CloudWatch User Guide*\.

## \[EFS\.1\] Amazon EFS should be configured to encrypt file data at rest using AWS KMS<a name="fsbp-efs-1"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::EFS::FileSystem`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether Amazon Elastic File System is configured to encrypt the file data using AWS KMS\. The check fails in the following cases\.
+ `Encrypted` is set to `false` in the [https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html](https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html) response\.
+ The `KmsKeyId` key in the [https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html](https://docs.aws.amazon.com/efs/latest/ug/API_DescribeFileSystems.html) response does not match the `KmsKeyId` parameter for [https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html)\.

Note that this control does not use the `KmsKeyId` parameter for [https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html)\. It only checks the value of `Encrypted`\.

For an added layer of security for your sensitive data in Amazon EFS, you should create encrypted file systems\. Amazon EFS supports encryption for file systems at\-rest\. You can enable encryption of data at rest when you create an Amazon EFS file system\. To learn more about Amazon EFS encryption, see[ Data encryption in Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/encryption.html) in the *Amazon Elastic File System User Guide*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="efs-1-remediation"></a>

For details on how to encrypt a new Amazon EFS file system, see [Encrypting data at rest](https://docs.aws.amazon.com/efs/latest/ug/encryption-at-rest.html) in the *Amazon Elastic File System User Guide*\.

## \[EFS\.2\] Amazon EFS volumes should be in backup plans<a name="fsbp-efs-2"></a>

**Category:** Recover > Resilience > Backup

**Severity:** Medium

**Resource type:** `AWS::EFS::FileSystem`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-in-backup-plan.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-in-backup-plan.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether Amazon Elastic File System \(Amazon EFS\) file systems are added to the backup plans in AWS Backup\. The control fails if Amazon EFS file systems are not included in the backup plans\. 

Including EFS file systems in the backup plans helps you to protect your data from deletion and data loss\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Europe \(Milan\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="efs-2-remediation"></a>

To remediate this issue, update your file system to enable automatic backups\.

**To enable automatic backups for an existing file system**

1. Open the Amazon Elastic File System console at [https://console\.aws\.amazon\.com/efs/](https://console.aws.amazon.com/efs/)\.

1. On the **File systems** page, choose the file system for which to enable automatic backups\.

   The **File system details** page is displayed\.

1. Under **General**, choose **Edit**\.

1. To enable automatic backups, select **Enable automatic backups**\. 

1. Choose **Save changes**\.

To learn more, visit [Using AWS Backup with Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/awsbackup.html) in the *Amazon Elastic File System User Guide*\.

## \[EFS\.3\] EFS access points should enforce a root directory<a name="fsbp-efs-3"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::EFS::AccessPoint`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-access-point-enforce-root-directory.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-access-point-enforce-root-directory.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon EFS access points are configured to enforce a root directory\. The control fails if the value of `Path` is set to `/` \(the default root directory of the file system\)\.

When you enforce a root directory, the NFS client using the access point uses the root directory configured on the access point instead of the file system's root directory\. Enforcing a root directory for an access point helps restrict data access by ensuring that users of the access point can only reach files of the specified subdirectory\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="efs-3-remediation"></a>

For instructions on how to enforce a root directory for an Amazon EFS access point, see [Enforcing a root directory with an access point](https://docs.aws.amazon.com/efs/latest/ug/efs-access-points.html#enforce-root-directory-access-point) in the *Amazon Elastic File System User Guide*\. 

## \[EFS\.4\] EFS access points should enforce a user identity<a name="fsbp-efs-4"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::EFS::AccessPoint`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-access-point-enforce-user-identity.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-access-point-enforce-user-identity.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon EFS access points are configured to enforce a user identity\. This control fails if a POSIX user identity is not defined while creating the EFS access point\.

Amazon EFS access points are application\-specific entry points into an EFS file system that make it easier to manage application access to shared datasets\. Access points can enforce a user identity, including the user's POSIX groups, for all file system requests that are made through the access point\. Access points can also enforce a different root directory for the file system so that clients can only access data in the specified directory or its subdirectories\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="efs-4-remediation"></a>

To enforce a user identity for an Amazon EFS access point, see [Enforcing a user identity using an access point](https://docs.aws.amazon.com/efs/latest/ug/efs-access-points.html#enforce-identity-access-points) in the *Amazon Elastic File System User Guide*\. 

## \[EKS\.2\] EKS clusters should run on a supported Kubernetes version<a name="fsbp-eks-2"></a>

**Category:** Identify > Vulnerability, patch, and version management

**Severity:** High

**Resource type:** `AWS::EKS::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/eks-cluster-supported-version.html](https://docs.aws.amazon.com/config/latest/developerguide/eks-cluster-supported-version.html)

**Schedule type:** Change triggered

**Parameters:**
+ `eks:oldestVersionSupported` \(Current oldest supported version is 1\.19\)

This control checks whether an Amazon EKS cluster is running on a supported Kubernetes version\. The control fails if the EKS cluster is running on an unsupported version\.

If your application doesn't require a specific version of Kubernetes, we recommend that you use the latest available Kubernetes version that's supported by EKS for your clusters\. For more information about supported Kubernetes versions for Amazon EKS, see [Amazon EKS Kubernetes release calendar](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html#kubernetes-release-calendar) and [Amazon EKS version support and FAQ](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html#version-deprecation)/para> in the **Amazon EKS User Guide**\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="eks-2-remediation"></a>

To update an EKS cluster, [Updating an Amazon EKS cluster Kubernetes version](https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html)/para> in the **Amazon EKS User Guide**\. 

## \[ElasticBeanstalk\.1\] Elastic Beanstalk environments should have enhanced health reporting enabled<a name="fsbp-elasticbeanstalk-1"></a>

**Category:** Detect > Detection services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::ElasticBeanstalk::Environment`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/beanstalk-enhanced-health-reporting-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/beanstalk-enhanced-health-reporting-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether enhanced health reporting is enabled for your AWS Elastic Beanstalk environments\.

Elastic Beanstalk enhanced health reporting enables a more rapid response to changes in the health of the underlying infrastructure\. These changes could result in a lack of availability of the application\.

Elastic Beanstalk enhanced health reporting provides a status descriptor to gauge the severity of the identified issues and identify possible causes to investigate\. The Elastic Beanstalk health agent, included in supported Amazon Machine Images \(AMIs\), evaluates logs and metrics of environment EC2 instances\.

For additional information, see [Enhanced health reporting and monitoring](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/health-enhanced.html) in the *AWS Elastic Beanstalk Developer Guide*\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticbeanstalk-1-remediation"></a>

For instructions on how to enable enhanced health reporting, see [Enabling enhanced health reporting using the Elastic Beanstalk console](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/health-enhanced-enable.html#health-enhanced-enable-console) in the *AWS Elastic Beanstalk Developer Guide*\.

## \[ElasticBeanstalk\.2\] Elastic Beanstalk managed platform updates should be enabled<a name="fsbp-elasticbeanstalk-2"></a>

**Category:** Detect > Vulnerability, patch, and version management

**Severity:** High

**Resource type:** `AWS::ElasticBeanstalk::Environment`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elastic-beanstalk-managed-updates-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/elastic-beanstalk-managed-updates-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether managed platform updates are enabled for the Elastic Beanstalk environment\.

Enabling managed platform updates ensures that the latest available platform fixes, updates, and features for the environment are installed\. Keeping up to date with patch installation is an important step in securing systems\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticbeanstalk-2-remediation"></a>

For instructions on how to enable managed platform updates, see [To configure managed platform updates under Managed platform updates](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environment-platform-update-managed.html) in the *AWS Elastic Beanstalk Developer Guide*\.

## \[ELB\.2\] Classic Load Balancers with HTTPS/SSL listeners should use a certificate provided by AWS Certificate Manager<a name="fsbp-elb-2"></a>

**Category:** Protect > Encryption of data in transit

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elb-acm-certificate-required.html](https://docs.aws.amazon.com/config/latest/developerguide/elb-acm-certificate-required.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the Classic Load Balancer uses HTTPS/SSL certificates provided by AWS Certificate Manager \(ACM\)\. The control fails if the Classic Load Balancer configured with HTTPS/SSL listener does not use a certificate provided by ACM\.

To create a certificate, you can use either ACM or a tool that supports the SSL and TLS protocols, such as OpenSSL\. Security Hub recommends that you use ACM to create or import certificates for your load balancer\.

ACM integrates with Classic Load Balancers so that you can deploy the certificate on your load balancer\. You also should automatically renew these certificates\.

**Note**  
These controls are not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
AWS GovCloud \(US\-East\)

### Remediation<a name="elb-2-remediation"></a>

For information about how to associate an ACM SSL/TLS certificate with a Classic Load Balancer, see the AWS Knowledge Center article [How can I associate an ACM SSL/TLS certificate with a Classic, Application, or Network Load Balancer?](http://aws.amazon.com/premiumsupport/knowledge-center/associate-acm-certificate-alb-nlb/)

## \[ELB\.3\] Classic Load Balancer listeners should be configured with HTTPS or TLS termination<a name="fsbp-elb-3"></a>

**Category:** Protect > Data protection > Encryption of data in transit 

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elb-tls-https-listeners-only.html](https://docs.aws.amazon.com/config/latest/developerguide/elb-tls-https-listeners-only.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether your Classic Load Balancer listeners are configured with HTTPS or TLS protocol for front\-end \(client to load balancer\) connections\. The control is applicable if a Classic Load Balancer has listeners\. If your Classic Load Balancer does not have a listener configured, then the control does not report any findings\.

The control passes if the Classic Load Balancer listeners are configured with TLS or HTTPS for front\-end connections\.

The control fails if the listener is not configured with TLS or HTTPS for front\-end connections\.

Before you start to use a load balancer, you must add one or more listeners\. A listener is a process that uses the configured protocol and port to check for connection requests\. Listeners can support both HTTP and HTTPS/TLS protocols\. You should always use an HTTPS or TLS listener, so that the load balancer does the work of encryption and decryption in transit\.

### Remediation<a name="elb-3-remediation"></a>

To remediate this issue, update your listeners to use the TLS or HTTPS protocol\.

**To change all noncompliant listeners to TLS/HTTPS listeners**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Load Balancers**\. Then choose your Classic Load Balancer\.

1. Choose the **Listeners** tab, and then choose **Edit**\.

1. For all listeners where **Load Balancer Protocol** is not set to HTTPS or SSL, change the setting to HTTPS or SSL\.

1. For all modified listeners, under **SSL Certificate**, choose **Change**\.

1. For all modified listeners, select **Choose a certificate from ACM**\.

1. Select the certificate from the **Certificates** drop\-down list\. Then choose **Save**\.

1. After you update all of the listeners, choose **Save**\.

## \[ELB\.4\] Application load balancers should be configured to drop HTTP headers<a name="fsbp-elb-4"></a>

**Category:** Protect > Network security

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/alb-http-drop-invalid-header-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/alb-http-drop-invalid-header-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control evaluates AWS Application Load Balancers to ensure they are configured to drop invalid HTTP headers\. The control fails if the value of `routing.http.drop_invalid_header_fields.enabled` is set to `false`\.

By default, Application Load Balancers are not configured to drop invalid HTTP header values\. Removing these header values prevents HTTP desync attacks\.

Note that you can disable this control if [ELB\.12](#fsbp-elb-12) is enabled\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
Europe \(Milan\)

### Remediation<a name="elb-4-remediation"></a>

To remediate this issue, configure your load balancer to drop invalid header fields\.

**To configure the load balancer to drop invalid header fields**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Load balancers**\.

1. Choose an Application Load Balancer\.

1. From **Actions**, choose **Edit attributes**\.

1. Under **Drop Invalid Header Fields**, choose **Enable**\.

1. Choose **Save**\.

## \[ELB\.5\] Application and Classic Load Balancers logging should be enabled<a name="fsbp-elb-5"></a>

**Category:** Logging

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elb-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/elb-logging-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the Application Load Balancer and the Classic Load Balancerhave logging enabled\. The control fails if `access_logs.s3.enabled` is `false`\.

Elastic Load Balancing provides access logs that capture detailed information about requests sent to your load balancer\. Each log contains information such as the time the request was received, the client's IP address, latencies, request paths, and server responses\. You can use these access logs to analyze traffic patterns and to troubleshoot issues\. 

To learn more, see [Access logs for your Classic Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/access-log-collection.html) in *User Guide for Classic Load Balancers*\.

### Remediation<a name="elb-5-remediation"></a>

To remediate this issue, update your load balancers to enable logging\.

**To enable access logs**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Load balancers**\. 

1. Choose an Application Load Balancer\.

1. From **Actions**, choose **Edit attributes**\.

1. Under **Access logs**, choose **Enable**\.

1. Enter your S3 location\. This location can exist or it can be created for you\. If you do not specify a prefix, the access logs are stored in the root of the S3 bucket\.

1. Choose **Save**\.

## \[ELB\.6\] Application Load Balancer deletion protection should be enabled<a name="fsbp-elb-6"></a>

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancingV2::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elb-deletion-protection-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/elb-deletion-protection-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Application Load Balancer has deletion protection enabled\. The control fails if deletion protection is not configured\.

Enable deletion protection to protect your Application Load Balancer from deletion\. 

### Remediation<a name="elb-6-remediation"></a>

To prevent your load balancer from being deleted accidentally, you can enable deletion protection\. By default, deletion protection is disabled for your load balancer\.

If you enable deletion protection for your load balancer, you must disable delete protection before you can delete the load balancer\.

To enable deletion protection from the console

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the navigation pane, under **LOAD BALANCING**, choose **Load Balancers**\.

1. Choose the load balancer\.

1. On the **Description** tab, choose **Edit attributes**\.

1. On the **Edit load balancer attributes** page, select **Enable for Delete Protection**, and then choose **Save**\.

1. Choose **Save**\.

To learn more, see [Deletion protection](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancers.html#deletion-protection) in *User Guide for Application Load Balancers*\.

## \[ELB\.7\] Classic Load Balancers should have connection draining enabled<a name="fsbp-elb-7"></a>

**Category:** Recover > Resilience

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Configrule:** `elb-connection-draining-enabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Classic Load Balancers have connection draining enabled\.

Enabling connection draining on Classic Load Balancers ensures that the load balancer stops sending requests to instances that are de\-registering or unhealthy\. It keeps the existing connections open\. This is particularly useful for instances in Auto Scaling groups, to ensure that connections aren’t severed abruptly\.

### Remediation<a name="elb-7-remediation"></a>

To enable connection draining on Classic Load Balancers, following the steps in [Configure connection draining for your Classic Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/config-conn-drain.html) in *User Guide for Classic Load Balancers*\.

## \[ELB\.8\] Classic Load Balancers with HTTPS/SSL listeners should use a predefined security policy that has strong configuration<a name="fsbp-elb-8"></a>

**Category:** Protect > Encryption of data in transit 

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elb-predefined-security-policy-ssl-check.html](https://docs.aws.amazon.com/config/latest/developerguide/elb-predefined-security-policy-ssl-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `predefinedPolicyName`: `ELBSecurityPolicy-TLS-1-2-2017-01`

This control checks whether your Classic Load Balancer HTTPS/SSL listeners use the predefined policy `ELBSecurityPolicy-TLS-1-2-2017-01`\. The control fails if the Classic Load Balancer HTTPS/SSL listeners do not use `ELBSecurityPolicy-TLS-1-2-2017-01`\.

A security policy is a combination of SSL protocols, ciphers, and the Server Order Preference option\. Predefined policies control the ciphers, protocols, and preference orders to support during SSL negotiations between a client and load balancer\.

Using `ELBSecurityPolicy-TLS-1-2-2017-01` can help you to meet compliance and security standards that require you to disable specific versions of SSL and TLS\. For more information, see [Predefined SSL security policies for Classic Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-security-policy-table.html) in *User Guide for Classic Load Balancers*\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
Europe \(Milan\)
AWS GovCloud \(US\-East\)

### Remediation<a name="elb-8-remediation"></a>

For information on how to use the predefined security policy `ELBSecurityPolicy-TLS-1-2-2017-01` with a Classic Load Balancer, see [Configure security settings](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-create-https-ssl-load-balancer.html#config-backend-auth) in *User Guide for Classic Load Balancers*\.

## \[ELB\.9\] Classic Load Balancers should have cross\-zone load balancing enabled<a name="fsbp-elb-9"></a>

**Category:** Recover > Resilience > High Availability 

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elb-cross-zone-load-balancing-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/elb-cross-zone-load-balancing-enabled.html)

**Schedule type:** Change triggered

**Parameters:**
+ `predefinedPolicyName`: `ELBSecurityPolicy-TLS-1-2-2017-01`

This control checks if cross\-zone load balancing is enabled for the Classic Load Balancers \(CLBs\)\. This control fails if cross\-zone load balancing is not enabled for a CLB\.

A load balancer node distributes traffic only across the registered targets in its Availability Zone\. When cross\-zone load balancing is disabled, each load balancer node distributes traffic only across the registered targets in its Availability Zone\. If the number of registered targets is not same across the Availability Zones, traffic wont be distributed evenly and the instances in one zone may end up over utilized compared to the instances in another zone\. With cross\-zone load balancing enabled, each load balancer node for your Classic Load Balancer distributes requests evenly across the registered instances in all enabled Availability Zones\. For details see [Cross\-zone load balancing](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html#cross-zone-load-balancing) in the Elastic Load Balancing User Guide\.

**Note**  
This control is not supported in Africa \(Cape Town\)\.

### Remediation<a name="elb-9-remediation"></a>

To enable cross\-zone load balancing in a Classic Load Balancer, see [Enable cross\-zone load balancing](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/enable-disable-crosszone-lb.html#enable-cross-zone) in the Elastic Load Balancing User Guide\.

## \[ELB\.10\] Classic Load Balancers should span multiple Availability Zones<a name="fsbp-elb-10"></a>

**Category:** Recover > Resilience > High Availability 

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/clb-multiple-az.html](https://docs.aws.amazon.com/config/latest/developerguide/clb-multiple-az.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a Classic Load Balancer has been configured to span multiple Availability Zones\. The control fails if the Classic Load Balancer does not span multiple Availability Zones\.

 A Classic Load Balancer can be set up to distribute incoming requests across Amazon EC2 instances in a single Availability Zone or multiple Availability Zones\. A Classic Load Balancer that does not span multiple Availability Zones is unable to redirect traffic to targets in another Availability Zone if the sole configured Availability Zone becomes unavailable\. 

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elb-10-remediation"></a>

 For information on how to add Availability Zones to a Classic Load Balancer, see [Add or remove Availability Zones](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/enable-disable-az.html) in the *User Guide for Classic Load Balancers*\. 

## \[ELB\.12\] Application Load Balancers should be configured with defensive or strictest desync mitigation mode<a name="fsbp-elb-12"></a>

**Category:** Data protect > Data integrity 

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/alb-desync-mode-check.html](https://docs.aws.amazon.com/config/latest/developerguide/alb-desync-mode-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `desyncMode`: defensive, strictest

This control checks whether an Application Load Balancer is configured with defensive or strictest desync mitigation mode\. The control fails if an Application Load Balancer is not configured with defensive or strictest desync mitigation mode\.

HTTP Desync issues can lead to request smuggling and make applications vulnerable to request queue or cache poisoning\. In turn, these vulnerabilities can lead to credential stuffing or execution of unauthorized commands\. Application Load Balancers configured with defensive or strictest desync mitigation mode protect your application from security issues that may be caused by HTTP Desync\. 

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elb-12-remediation"></a>

To update desync mitigation mode of an Application Load Balancer, see [Desync mitigation mode](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancers.html#desync-mitigation-mode) in the *User Guide for Application Load Balancers*\. 

## \[ELB\.13\] Application, Network, and Gateway Load Balancers should span multiple Availability Zones<a name="fsbp-elb-13"></a>

**Category:** Recover > Resilience > High availability 

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancingV2::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elbv2-multiple-az.html](https://docs.aws.amazon.com/config/latest/developerguide/elbv2-multiple-az.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Elastic Load Balancer V2 \(Application, Network, or Gateway Load Balancer\) has registered instances from multiple Availability Zones\. The control fails if an Elastic Load Balancer V2 has instances registered in fewer than two Availability Zones\.

Elastic Load Balancing automatically distributes your incoming traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more Availability Zones\. Elastic Load Balancing scales your load balancer as your incoming traffic changes over time\. It is recommended to configure at least two availability zones to ensure availability of services, as the Elastic Load Balancer will be able to direct traffic to another availability zone if one becomes unavailable\. Having multiple availability zones configured will help eliminate having a single point of failure for the application\. 

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elb-13-remediation"></a>

To add an Availability Zone to an Application Load Balancer, see [Availability Zones for your Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-subnets.html) in the *User Guide for Application Load Balancers*\. To add an Availability Zone to an Network Load Balancer, see [Network Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/network-load-balancers.html#availability-zones) in the *User Guide for Network Load Balancers*\. To add an Availability Zone to a Gateway Load Balancer, see [Create a Gateway Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/create-load-balancer.html) in the *User Guide for Gateway Load Balancers*\. 

## \[ELB\.14\] Classic Load Balancers should be configured with defensive or strictest desync mitigation mode<a name="fsbp-elb-14"></a>

**Category:** Data Protect > Data Integrity

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/clb-desync-mode-check.html](https://docs.aws.amazon.com/config/latest/developerguide/clb-desync-mode-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `desyncMode`: defensive, strictest

This control checks whether a Classic Load Balancer is configured with defensive or strictest desync mitigation mode\. This control will fail if the Application Load Balancer is not configured with defensive or strictest desync mitigation mode\.

HTTP Desync issues can lead to request smuggling and make applications vulnerable to request queue or cache poisoning\. In turn, these vulnerabilities can lead to credential hijacking or execution of unauthorized commands\. Classic Load Balancers configured with defensive or strictest desync mitigation mode protect your application from security issues that may be caused by HTTP Desync\. 

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elb-14-remediation"></a>

To update desync mitigation mode of a Classic Load Balancer, see [Modify desync mitigation mode](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/config-desync-mitigation-mode.html#update-desync-mitigation-mode) in the *User Guide for Classic Load Balancers*\. 

## \[ELBv2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS<a name="fsbp-elbv2-1"></a>

**Category:** Protect > Data protection > Encryption of data in transit

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancingV2::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html](https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether HTTP to HTTPS redirection is configured on all HTTP listeners of Application Load Balancers\. The check fails if one or more HTTP listeners of Application Load Balancers do not have HTTP to HTTPS redirection configured\.

Before you start to use your Application Load Balancer, you must add one or more listeners\. A listener is a process that uses the configured protocol and port to check for connection requests\. Listeners support both HTTP and HTTPS protocols\. You can use an HTTPS listener to offload the work of encryption and decryption to your Application Load Balancer\. You should use redirect actions with Application Load Balancer to redirect client HTTP request to an HTTPS request on port 443 to enforce encryption in\-transit\.

To learn more, see [Listeners for your Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-listeners.html) in *User Guide for Application Load Balancers*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="elbv2-1-remediation"></a>

To remediate this issue, update your load balancers to redirect HTTP requests\.

**To redirect HTTP requests to HTTPS on an Application Load Balancer**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Load balancers**\.

1. Choose an Application Load Balancer\.

1. Choose the **Listeners** tab\.

1. Choose an HTTP listener \(port 80 TCP\) and then choose **Edit**\.

1. If there is an existing rule, you must delete it\. Otherwise, choose **Add action** and then choose **Redirect to\.\.\.**

1. Choose **HTTPS** and then enter **443**\.

1. Choose the check mark in a circle symbol and then choose **Update**\.

## \[EMR\.1\] Amazon EMR cluster master nodes should not have public IP addresses<a name="fsbp-emr-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::EMR::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/emr-master-no-public-ip.html](https://docs.aws.amazon.com/config/latest/developerguide/emr-master-no-public-ip.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether master nodes on Amazon EMR clusters have public IP addresses\. 

The control fails if the master node has public IP addresses that are associated with any of its instances\. Public IP addresses are designated in the `PublicIp` field of the `NetworkInterfaces` configuration for the instance\. This control only checks Amazon EMR clusters that are in a `RUNNING` or `WAITING` state\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="emr-1-remediation"></a>

During launch, you can control whether your instance in a default or nondefault subnet is assigned a public IPv4 address\.

By default, default subnets have this attribute set to `true`\. Nondefault subnets have the IPv4 public addressing attribute set to `false`, unless it was created by the Amazon EC2 launch instance wizard\. In that case, the wizard sets the attribute to `true`\.

You need to launch your cluster in a VPC with a private subnet that has the IPv4 public addressing attribute set to `false`\. 

After launch, you cannot manually disassociate a public IPv4 address from your instance\.

To remediate this finding, you need to create a new cluster in VPC private subnet\. For information on how to launch a cluster in into a VPC private subnet, see [Launch clusters into a VPC](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-vpc-launching-job-flows.html) in the *Amazon EMR Management Guide*\.

## \[ES\.1\] Elasticsearch domains should have encryption at rest enabled<a name="fsbp-es-1"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::Elasticsearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-encrypted-at-rest.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-encrypted-at-rest.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether Elasticsearch domains have encryption at rest configuration enabled\. The check fails if encryption at rest is not enabled\.

For an added layer of security for your sensitive data in OpenSearch, you should configure your OpenSearch to be encrypted at rest\. Elasticsearch domains offer encryption of data at rest\. The feature uses AWS KMS to store and manage your encryption keys\. To perform the encryption, it uses the Advanced Encryption Standard algorithm with 256\-bit keys \(AES\-256\)\.

To learn more about OpenSearch encryption at rest, see [Encryption of data at rest for Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/encryption-at-rest.html) in the *Amazon OpenSearch Service Developer Guide*\.

**Note**  
Certain instance types, such as `t.small` and `t.medium`, do not support encryption of data at rest\. For details, see [Supported instance types](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/supported-instance-types.html) in the *Amazon OpenSearch Service Developer Guide*\.

### Remediation<a name="es-1-remediation"></a>

By default, domains do not encrypt data at rest, and you cannot configure existing domains to use the feature\.

To enable the feature, you must create another domain and migrate your data\. For information about creating domains, see the [https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createupdatedomains.html](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createupdatedomains.html)\.

Encryption of data at rest requires OpenSearch Service 5\.1 or later\. For more information about encrypting data at rest for OpenSearch Service, see the [https://docs.aws.amazon.com/opensearch-service/latest/developerguide/encryption-at-rest.html](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/encryption-at-rest.html)\.

## \[ES\.2\] Elasticsearch domains should be in a VPC<a name="fsbp-es-2"></a>

**Category:** Protect > Secure network configuration > Resources within VPC 

**Severity:** Critical

**Resource type:** `AWS::Elasticsearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-in-vpc-only.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-in-vpc-only.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether Elasticsearch domains are in a VPC\. It does not evaluate the VPC subnet routing configuration to determine public access\. You should ensure that Elasticsearch domains are not attached to public subnets\. See [Resource\-based policies](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/ac.html#ac-types-resource) in the *Amazon OpenSearch Service Developer Guide*\. You should also ensure that your VPC is configured according to the recommended best practices\. See [Security best practices for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html) in the *Amazon VPC User Guide*\.

Elasticsearch domains deployed within a VPC can communicate with VPC resources over the private AWS network, without the need to traverse the public internet\. This configuration increases the security posture by limiting access to the data in transit\. VPCs provide a number of network controls to secure access to Elasticsearch domains, including network ACL and security groups\. Security Hub recommends that you migrate public Elasticsearch domains to VPCs to take advantage of these controls\.

### Remediation<a name="es-2-remediation"></a>

If you create a domain with a public endpoint, you cannot later place it within a VPC\. Instead, you must create a new domain and migrate your data\. The reverse is also true\. If you create a domain within a VPC, it cannot have a public endpoint\. Instead, you must either [create another domain](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createupdatedomains.html) or disable this control\.

See [Launching your Amazon OpenSearch Service domains within a VPC](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/vpc.html) in the *Amazon OpenSearch Service Developer Guide*\.

## \[ES\.3\] Elasticsearch domains should encrypt data sent between nodes<a name="fsbp-es-3"></a>

**Category:** Protect > Data protection > Encryption of data in transit 

**Severity:** Medium

**Resource type:** `AWS::Elasticsearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-node-to-node-encryption-check.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-node-to-node-encryption-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Elasticsearch domains have node\-to\-node encryption enabled\.

HTTPS \(TLS\) can be used to help prevent potential attackers from eavesdropping on or manipulating network traffic using person\-in\-the\-middle or similar attacks\. Only encrypted connections over HTTPS \(TLS\) should be allowed\. Enabling node\-to\-node encryption for Elasticsearch domains ensures that intra\-cluster communications are encrypted in transit\.

There can be a performance penalty associated with this configuration\. You should be aware of and test the performance trade\-off before enabling this option\. 

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)

### Remediation<a name="es-3-remediation"></a>

For information about enabling node\-to\-node encryption on new and existing domains, see [Enabling node\-to\-node encryption](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/ntn.html#enabling-ntn) in the *Amazon OpenSearch Service Developer Guide*\.

## \[ES\.4\] Elasticsearch domain error logging to CloudWatch Logs should be enabled<a name="fsbp-es-4"></a>

**Category:** Identify \- Logging

**Severity:** Medium

**Resource type:** `AWS::Elasticsearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-logs-to-cloudwatch.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-logs-to-cloudwatch.html)

**Schedule type:** Change triggered

**Parameters:**
+ `logtype = 'error'`

This control checks whether Elasticsearch domains are configured to send error logs to CloudWatch Logs\.

You should enable error logs for Elasticsearch domains and send those logs to CloudWatch Logs for retention and response\. Domain error logs can assist with security and access audits, and can help to diagnose availability issues\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="es-4-remediation"></a>

For information on how to enable log publishing, see [Enabling log publishing \(console\)](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createdomain-configure-slow-logs.html#createdomain-configure-slow-logs-console) in the *Amazon OpenSearch Service Developer Guide*\.

## \[ES\.5\] Elasticsearch domains should have audit logging enabled<a name="fsbp-es-5"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::Elasticsearch::Domain`

**AWS Config rule:** `elasticsearch-audit-logging-enabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:**
+ `cloudWatchLogsLogGroupArnList` \(Optional\)\. Security Hub does not populate this parameter\. Comma\-separated list of CloudWatch Logs log groups that should be configured for audit logs\.

  This rule is `NON_COMPLIANT` if the CloudWatch Logs log group of the Elasticsearch domain is not specified in this parameter list\.

This control checks whether Elasticsearch domains have audit logging enabled\. This control fails if an Elasticsearch domain does not have audit logging enabled\. 

Audit logs are highly customizable\. They allow you to track user activity on your Elasticsearch clusters, including authentication successes and failures, requests to OpenSearch, index changes, and incoming search queries\.

### Remediation<a name="es-5-remediation"></a>

For detailed instructions on enabling audit logs, see [Enabling audit logs](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/audit-logs.html#audit-log-enabling) in the *Amazon OpenSearch Service Developer Guide*\.

## \[ES\.6\] Elasticsearch domains should have at least three data nodes<a name="fsbp-es-6"></a>

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::Elasticsearch::Domain`

**AWS Config rule:** `elasticsearch-data-node-fault-tolerance` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Elasticsearch domains are configured with at least three data nodes and `zoneAwarenessEnabled` is `true`\.

An Elasticsearch domain requires at least three data nodes for high availability and fault\-tolerance\. Deploying an Elasticsearch domain with at least three data nodes ensures cluster operations if a node fails\.

### Remediation<a name="es-6-remediation"></a>

**To modify the number of data nodes in an Elasticsearch domain**

1. Open the Amazon OpenSearch Service console at [https://console\.aws\.amazon\.com/es/](https://console.aws.amazon.com/es/)\.

1. Under **My domains**, choose the name of the domain to edit\.

1. Choose **Edit domain**\.

1. Under **Data nodes**, set **Number of nodes** to a number greater than or equal to `3`\.

   For three Availability Zone deployments, set to a multiple of three to ensure equal distribution across Availability Zones\.

1. Choose **Submit**\.

## \[ES\.7\] Elasticsearch domains should be configured with at least three dedicated master nodes<a name="fsbp-es-7"></a>

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::Elasticsearch::Domain`

**AWS Configrule:** `elasticsearch-primary-node-fault-tolerance` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Elasticsearch domains are configured with at least three dedicated master nodes\. This control fails if the domain does not use dedicated master nodes\. This control passes if Elasticsearch domains have five dedicated master nodes\. However, using more than three master nodes might be unnecessary to mitigate the availability risk, and will result in additional cost\.

An Elasticsearch domain requires at least three dedicated master nodes for high availability and fault\-tolerance\. Dedicated master node resources can be strained during data node blue/green deployments because there are additional nodes to manage\. Deploying an Elasticsearch domain with at least three dedicated master nodes ensures sufficient master node resource capacity and cluster operations if a node fails\.

### Remediation<a name="es-7-remediation"></a>

**To modify the number of dedicated master nodes in an OpenSearch domain**

1. Open the Amazon OpenSearch Service console at [https://console\.aws\.amazon\.com/es/](https://console.aws.amazon.com/es/)\.

1. Under **My domains**, choose the name of the domain to edit\.

1. Choose **Edit domain**\.

1. Under **Dedicated master nodes**, set **Instance type** to the desired instance type\.

1. Set **Number of master nodes** equal to three or greater\.

1. Choose **Submit**\.

## \[ES\.8\] Connections to Elasticsearch domains should be encrypted using TLS 1\.2<a name="fsbp-es-8"></a>

**Category:** Protect > Data protection > Encryption of data in transit

**Severity:** Medium

**Resource type:** `AWS::Elasticsearch::Domain`

**AWS Config rule:** `elasticsearch-https-required` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether connections to Elasticsearch domains are required to use TLS 1\.2\. The check fails if the Elasticsearch domain `TLSSecurityPolicy` is not Policy\-Min\-TLS\-1\-2\-2019\-07\.

HTTPS \(TLS\) can be used to help prevent potential attackers from using person\-in\-the\-middle or similar attacks to eavesdrop on or manipulate network traffic\. Only encrypted connections over HTTPS \(TLS\) should be allowed\. Encrypting data in transit can affect performance\. You should test your application with this feature to understand the performance profile and the impact of TLS\. TLS 1\.2 provides several security enhancements over previous versions of TLS\.

### Remediation<a name="es-8-remediation"></a>

To enable TLS encryption, use the [https://docs.aws.amazon.com/opensearch-service/latest/developerguide/configuration-api.html#configuration-api-actions-updatedomainconfig](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/configuration-api.html#configuration-api-actions-updatedomainconfig) API operation to configure the [https://docs.aws.amazon.com/opensearch-service/latest/developerguide/configuration-api.html#configuration-api-datatypes-domainendpointoptions](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/configuration-api.html#configuration-api-datatypes-domainendpointoptions) in order to set the `TLSSecurityPolicy`\. For more information, see the *Amazon OpenSearch Service Developer Guide*\.

## \[GuardDuty\.1\] GuardDuty should be enabled<a name="fsbp-guardduty-1"></a>

**Category:** Detect > Detection services 

**Severity:** High

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html](https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether Amazon GuardDuty is enabled in your GuardDuty account and Region\.

It is highly recommended that you enable GuardDuty in all supported AWS Regions\. Doing so allows GuardDuty to generate findings about unauthorized or unusual activity, even in Regions that you do not actively use\. This also allows GuardDuty to monitor CloudTrail events for global AWS services such as IAM\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
Middle East \(Bahrain\)
AWS GovCloud \(US\-East\)

### Remediation<a name="guardduty-1-remediation"></a>

To remediate this issue, you enable GuardDuty\.

For details on how to enable GuardDuty, including how to use AWS Organizations to manage multiple accounts, see [Getting started with GuardDuty](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_settingup.html) in the *Amazon GuardDuty User Guide*\.

## \[IAM\.1\] IAM policies should not allow full "\*" administrative privileges<a name="fsbp-iam-1"></a>

**Category:** Protect > Secure access management

**Severity:** High

**Resource type:** `AWS::IAM::Policy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the default version of IAM policies \(also known as customer managed policies\) has administrator access by including a statement with `"Effect": "Allow"` with `"Action": "*"` over `"Resource": "*"`\. The control fails if you have IAM policies with such a statement\.

The control only checks the customer managed policies that you create\. It does not check inline and AWS managed policies\.

IAM policies define a set of privileges that are granted to users, groups, or roles\. Following standard security advice, AWS recommends that you grant least privilege, which means to grant only the permissions that are required to perform a task\. When you provide full administrative privileges instead of the minimum set of permissions that the user needs, you expose the resources to potentially unwanted actions\.

Instead of allowing full administrative privileges, determine what users need to do and then craft policies that let the users perform only those tasks\. It is more secure to start with a minimum set of permissions and grant additional permissions as necessary\. Do not start with permissions that are too lenient and then try to tighten them later\.

You should remove IAM policies that have a statement with `"Effect": "Allow" `with `"Action": "*"` over `"Resource": "*"`\.

**Note**  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-1-remediation"></a>

To modify your IAM policies so that they do not allow full "\*" administrative privileges, see [Editing IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-edit.html) in the *IAM User Guide*\.

## \[IAM\.2\] IAM users should not have IAM policies attached<a name="fsbp-iam-2"></a>

**Category:** Protect > Secure access management

**Severity:** Low

**Resource type:** `AWS::IAM::User`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks that none of your IAM users have policies attached\. Instead, IAM users must inherit permissions from IAM groups or roles\.

By default, IAM users, groups, and roles have no access to AWS resources\. IAM policies grant privileges to users, groups, or roles\. We recommend that you apply IAM policies directly to groups and roles but not to users\. Assigning privileges at the group or role level reduces the complexity of access management as the number of users grows\. Reducing access management complexity might in turn reduce the opportunity for a principal to inadvertently receive or retain excessive privileges\. 

**Note**  
IAM users created by Amazon Simple Email Service are automatically created using inline policies\. Security Hub automatically exempts these users from this control\.  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-2-remediation"></a>

To resolve this issue, [create an IAM group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_create.html), and attach the policy to the group\. Then, [add the users to the group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_manage_add-remove-users.html)\. The policy is applied to each user in the group\. To remove a policy attached directly to a user, see [Adding and removing IAM identity permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html) in the *IAM User Guide*\.

## \[IAM\.3\] IAM users' access keys should be rotated every 90 days or less<a name="fsbp-iam-3"></a>

**Category:** Protect > Secure access management

**Severity:** Medium 

**Resource type:** `AWS::IAM::User`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html](https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html)

**Schedule type:** Periodic

**Parameters:**
+ `maxAccessKeyAge`: 90

This control checks whether the active access keys are rotated within 90 days\.

We highly recommend that you do not generate and remove all access keys in your account\. Instead, the recommended best practice is to either create one or more IAM roles or to use [federation](http://aws.amazon.com/identity/federation/)\. You can use these methods to allow your users to use their existing corporate credentials to log into the AWS Management Console and AWS CLI\.

Each approach has its use cases\. Federation is generally better for enterprises that have an existing central directory or plan to need more than the current limit IAM users\. Applications that run outside of an AWS environment need access keys for programmatic access to AWS resources\.

However, if the resources that need programmatic access run inside AWS, the best practice is to use IAM roles\. Roles allow you to grant a resource access without hardcoding an access key ID and secret access key into the configuration\.

To learn more about protecting your access keys and account, see [Best practices for managing AWS access keys](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html) in the *AWS General Reference*\. Also see the blog post [Guidelines for protecting your AWS account while using programmatic access](http://aws.amazon.com/blogs/security/guidelines-for-protecting-your-aws-account-while-using-programmatic-access/)\.

If you already have an access key, Security Hub recommends that you rotate the access keys every 90 days\. Rotating access keys reduces the chance that an access key that is associated with a compromised or terminated account is used\. It also ensures that data cannot be accessed with an old key that might have been lost, cracked, or stolen\. Always update your applications after you rotate access keys\. 

Access keys consist of an access key ID and a secret access key\. They are used to sign programmatic requests that you make to AWS\. AWS users need their own access keys to make programmatic calls to AWS from the AWS CLI, Tools for Windows PowerShell, the AWS SDKs, or direct HTTP calls using the API operations for individual AWS services\.

If your organization uses AWS IAM Identity Center \(successor to AWS Single Sign\-On\) \(IAM Identity Center\), your users can sign in to Active Directory, a built\-in IAM Identity Center directory, or [another identity provider \(IdP\) connected to IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-idp.html)\. They can then be mapped to an IAM role that enables them to run AWS CLI commands or call AWS API operations without the need for IAM user access keys\. To learn more, see [Configuring the AWS CLI to use AWS IAM Identity Center \(successor to AWS Single Sign\-On\)](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html) in the *AWS Command Line Interface User Guide*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-3-remediation"></a>

To remediate this issue, replace any keys that are older than 90 days\.

**To ensure that access keys aren't more than 90 days old**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. For each user that shows an **Access key age** that is greater than 90 days, choose the **User name** to open the settings for that user\.

1. Choose **Security credentials**\.

1. Create a new key for the user:

   1. Choose **Create access key**\.

   1. To save the key content, either download the secret access key, or choose **Show** and then copy it from the page\.

   1. Store the key in a secure location to provide to the user\.

   1. Choose **Close**\.

1. Update all applications that were using the previous key to use the new key\.

1. For the previous key, choose **Make inactive** to make the access key inactive\. The user now cannot use that key to make requests\.

1. Confirm that all applications work as expected with the new key\.

1. After confirming that all applications work with the new key, delete the previous key\. After you delete the access key, you cannot recover it\.

   To delete the previous key, choose the **X** at the end of the row and then choose **Delete**\.

## \[IAM\.4\] IAM root user access key should not exist<a name="fsbp-iam-4"></a>

**Category:** Protect > Secure access management

**Severity:** Critical 

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether the root user access key is present\. 

The root user is the most privileged user in an AWS account\. AWS access keys provide programmatic access to a given account\.

Security Hub recommends that you remove all access keys that are associated with the root user\. This limits that vectors that can be used to compromise your account\. It also encourages the creation and use of role\-based accounts that are least privileged\. 

**Note**  
This control is not supported in Asia Pacific \(Jakarta\) or Asia Pacific \(Osaka\)\.

### Remediation<a name="iam-4-remediation"></a>

To delete the root user access key, see [Deleting access keys for the root user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_delete-key) in the *IAM User Guide*\.

## \[IAM\.5\] MFA should be enabled for all IAM users that have a console password<a name="fsbp-iam-5"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::IAM::User`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html](https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether AWS multi\-factor authentication \(MFA\) is enabled for all IAM users that use a console password\.

Multi\-factor authentication \(MFA\) adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they are prompted for their user name and password\. In addition, they are prompted for an authentication code from their AWS MFA device\.

We recommend that you enable MFA for all accounts that have a console password\. MFA is designed to provide increased security for console access\. The authenticating principal must possess a device that emits a time\-sensitive key and must have knowledge of a credential\.

**Note**  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-5-remediation"></a>

To add MFA for IAM users, see [Using multi\-factor authentication \(MFA\) in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) in the *IAM User Guide*\.

We are offering a free MFA security key to eligible customers\. [See if you quality, and order your free key](https://console.aws.amazon.com/securityhub/home/?region=us-east-1#/free-mfa-security-key/)\.

## \[IAM\.6\] Hardware MFA should be enabled for the root user<a name="fsbp-iam-6"></a>

**Category:** Protect > Secure access management

**Severity:** Critical

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether your AWS account is enabled to use a hardware multi\-factor authentication \(MFA\) device to sign in with root user credentials\.

Virtual MFA might not provide the same level of security as hardware MFA devices\. We recommend that you use only a virtual MFA device while you wait for hardware purchase approval or for your hardware to arrive\. To learn more, see[ Enabling a virtual multi\-factor authentication \(MFA\) device \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html) in the *IAM User Guide*\.

Both time\-based one\-time password \(TOTP\) and Universal 2nd Factor \(U2F\) tokens are viable as hardware MFA options\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)\.

### Remediation<a name="iam-6-remediation"></a>

To add a hardware MFA device for the root user, see [Enable a hardware MFA device for the AWS account root user \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_physical.html#enable-hw-mfa-for-root) in the *IAM User Guide*\.

We are offering a free MFA security key to eligible customers\. [See if you quality, and order your free key](https://console.aws.amazon.com/securityhub/home/?region=us-east-1#/free-mfa-security-key/)\.

## \[IAM\.7\] Password policies for IAM users should have strong configurations<a name="fsbp-iam-7"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

**Parameters:**
+ `RequireUppercaseCharacters`: `true`
+ `RequireLowercaseCharacters`: `true`
+ `RequireSymbols`: `true`
+ `RequireNumbers`: `true`
+ `MinimumPasswordLength`: `8`

This control checks whether the account password policy for IAM users uses the recommended configurations\.

To access the AWS Management Console, IAM users need passwords\. As a best practice, Security Hub highly recommends that instead of creating IAM users, you use federation\. Federation allows users to use their existing corporate credentials to log into the AWS Management Console\. Use AWS IAM Identity Center \(successor to AWS Single Sign\-On\) \(IAM Identity Center\) to create or federate the user, and then assume an IAM role into an account\.

To learn more about identity providers and federation, see [Identity providers and federation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html) in the *IAM User Guide*\. To learn more about IAM Identity Center, see the [https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)\.

 If you need to use IAM users, Security Hub recommends that you enforce the creation of strong user passwords\. You can set a password policy on your AWS account to specify complexity requirements and mandatory rotation periods for passwords\. When you create or change a password policy, most of the password policy settings are enforced the next time users change their passwords\. Some of the settings are enforced immediately\.

### Remediation<a name="iam-7-remediation"></a>

To update your password policy to use the recommended configuration, see [Setting an account password policy for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html) in the *IAM User Guide*\.

## \[IAM\.8\] Unused IAM user credentials should be removed<a name="fsbp-iam-8"></a>

**Category:** Protect > Secure access management 

**Severity:** Medium 

**Resource type:** `AWS::IAM::User`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html)

**Schedule type:** Periodic

**Parameters:**
+ `maxCredentialUsageAge`: 90 

This control checks whether your IAM users have passwords or active access keys that have not been used for 90 days\.

IAM users can access AWS resources using different types of credentials, such as passwords or access keys\. 

Security Hub recommends that you remove or deactivate all credentials that were unused for 90 days or more\. Disabling or removing unnecessary credentials reduces the window of opportunity for credentials associated with a compromised or abandoned account to be used\.

**Note**  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-8-remediation"></a>

To get some of the information that you need to monitor accounts for dated credentials, use the IAM console\. For example, when you view users in your account, there is a column for **Access key age**, **Password age**, and **Last activity**\. If the value in any of these columns is greater than 90 days, make the credentials for those users inactive\.

You can also use credential reports to monitor user accounts and identify those with no activity for 90 or more days\. You can download credential reports in `.csv` format from the IAM console\. For more information about credential reports, see [Getting credential reports for your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html#getting-credential-reports-console) in the *IAM User Guide*\.

After you identify the inactive accounts or unused credentials, use the following steps to disable them\.

**To disable credentials for inactive accounts**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the name of the user that has credentials over 90 days old\.

1. Choose** Security credentials**\.

1. For each sign\-in credential and access key that hasn't been used in at least 90 days, choose **Make inactive**\.

## \[IAM\.21\] IAM customer managed policies that you create should not allow wildcard actions for services<a name="fsbp-iam-21"></a>

**Category:** Detect > Secure access management 

**Severity:** Low

**Resource type:** `AWS::IAM::Policy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-full-access.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-full-access.html)

**Schedule type:** Change triggered

**Parameters:**
+ `excludePermissionBoundaryPolicy`: `True`

This control checks whether the IAM identity\-based policies that you create have Allow statements that use the \* wildcard to grant permissions for all actions on any service\. The control fails if any policy statement includes `"Effect": "Allow"` with `"Action": "Service:*"`\. 

For example, the following statement in a policy results in a failed finding\.

```
"Statement": [
{
  "Sid": "EC2-Wildcard",
  "Effect": "Allow",
  "Action": "ec2:*",
  "Resource": "*"
}
```

The control also fails if you use `"Effect": "Allow"` with `"NotAction": "service:*"`\. In that case, the `NotAction` element provides access to all of the actions in an AWS service, except for the actions specified in `NotAction`\.

This control only applies to customer managed IAM policies\. It does not apply to IAM policies that are managed by AWS\.

When you assign permissions to AWS services, it is important to scope the allowed IAM actions in your IAM policies\. You should restrict IAM actions to only those actions that are needed\. This helps you to provision least privilege permissions\. Overly permissive policies might lead to privilege escalation if the policies are attached to an IAM principal that might not require the permission\.

In some cases, you might want to allow IAM actions that have a similar prefix, such as `DescribeFlowLogs` and `DescribeAvailabilityZones`\. In these authorized cases, you can add a suffixed wildcard to the common prefix\. For example, `ec2:Describe*`\.

This control passes if you use a prefixed IAM action with a suffixed wildcard\. For example, the following statement in a policy results in a passed finding\.

```
"Statement": [
{
  "Sid": "EC2-Wildcard",
  "Effect": "Allow",
  "Action": "ec2:Describe*",
  "Resource": "*"
}
```

When you group related IAM actions in this way, you can also avoid exceeding the IAM policy size limits\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)
AWS Config should be enabled in all Regions in which you use Security Hub\. However, global resource recording can be enabled in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="iam-21-remediation"></a>

To remediate this issue, update your IAM policies so that they do not allow full "\*" administrative privileges\. For details about how to edit an IAM policy, see [Editing IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-edit.html) in the *IAM User Guide*\.

## \[Kinesis\.1\] Kinesis Data Streams should be encrypted at rest<a name="fsbp-kinesis-1"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::Kinesis::Stream`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/kinesis-stream-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/kinesis-stream-encrypted.html)

**Schedule type:** Change triggered

**Parameters:** None 

This control checks if Kinesis Data Streams are encrypted at rest with server\-side encryption\. This control fails if a Kinesis stream is not encrypted at rest with server\-side encryption\.

Server\-side encryption is a feature in Amazon Kinesis Data Streams that automatically encrypts data before it's at rest by using an AWS KMS key\. Data is encrypted before it's written to the Kinesis stream storage layer, and decrypted after it’s retrieved from storage\. As a result, your data is encrypted at rest within the Amazon Kinesis Data Streams service\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="kinesis-1-remediation"></a>

For information about enabling server\-side encryption for Kinesis streams, see [How Do I Get Started with Server\-Side Encryption?](https://docs.aws.amazon.com/streams/latest/dev/getting-started-with-sse.html) in the *Amazon Kinesis Developer Guide*\.

## \[KMS\.1\] IAM customer managed policies should not allow decryption and re\-encryption actions on all KMS keys<a name="fsbp-kms-1"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::IAM::Policy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-customer-policy-blocked-kms-actions.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-customer-policy-blocked-kms-actions.html)

**Schedule type:** Change triggered

**Parameters:** 
+ `blockedActionsPatterns: kms:ReEncryptFrom, kms:Decrypt`
+ `excludePermissionBoundaryPolicy`: `True`

Checks whether the default version of IAM customer managed policies allow principals to use the AWS KMS decryption actions on all resources\. This control uses [Zelkova](http://aws.amazon.com/blogs/security/protect-sensitive-data-in-the-cloud-with-automated-reasoning-zelkova/), an automated reasoning engine, to validate and warn you about policies that may grant broad access to your secrets across AWS accounts\.

This control fails, and flags the policy as `FAILED`, if the policy is open enough to allow `kms:Decrypt` or `kms:ReEncryptFrom` actions on any arbitrary KMS key\.

The control evaluates both attached and unattached customer managed policies\. It does not check inline policies or AWS managed policies\.

With AWS KMS, you control who can use your KMS keys and gain access to your encrypted data\. IAM policies define which actions an identity \(user, group, or role\) can perform on which resources\. Following security best practices, AWS recommends that you allow least privilege\. In other words, you should grant to identities only the `kms:Decrypt` or `kms:ReEncryptFrom` permissions and only for the keys that are required to perform a task\. Otherwise, the user might use keys that are not appropriate for your data\.

Instead of granting permissions for all keys, determine the minimum set of keys that users need to access encrypted data\. Then design policies that allow users to use only those keys\. For example, do not allow `kms:Decrypt` permission on all KMS keys\. Instead, allow `kms:Decrypt` only on keys in a particular Region for your account\. By adopting the principle of least privilege, you can reduce the risk of unintended disclosure of your data\.

**Note**  
This control is not supported in Asia Pacific \(Jakarta\) or Asia Pacific \(Osaka\)\.

### Remediation<a name="kms-1-remediation"></a>

To remediate this issue, you modify the IAM customer managed policies to restrict access to the keys\.

**To modify an IAM customer managed policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the IAM navigation pane, choose **Policies**\.

1. Choose the arrow next to the policy you want to modify\.

1. Choose **Edit policy**\.

1. Choose the **JSON** tab\.

1. Change the `“Resource”` value to the specific key or keys that you want to allow\.

1. After you modify the policy, choose **Review policy**\.

1. Choose **Save changes**\.

For more information, see [Using IAM policies with AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html) in the *AWS Key Management Service Developer Guide*\.

## \[KMS\.2\] IAM principals should not have IAM inline policies that allow decryption and re\-encryption actions on all KMS keys<a name="fsbp-kms-2"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:**
+ `AWS::IAM::Role`
+ `AWS::IAM::User`
+ `AWS::IAM::Group`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-inline-policy-blocked-kms-actions.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-inline-policy-blocked-kms-actions.html) 

**Schedule type:** Change triggered

**Parameters:**
+ `blockedActionsPatterns: kms:ReEncryptFrom, kms:Decrypt`

Checks whether the inline policies that are embedded in your IAM identities \(role, user, or group\) allow the AWS KMS decryption and re\-encryption actions on all KMS keys\. This control uses [Zelkova](http://aws.amazon.com/blogs/security/protect-sensitive-data-in-the-cloud-with-automated-reasoning-zelkova/), an automated reasoning engine, to validate and warn you about policies that may grant broad access to your secrets across AWS accounts\.

This control fails if the policy is open enough to allow `kms:Decrypt` or `kms:ReEncryptFrom` actions on any arbitrary KMS key\.

With AWS KMS, you control who can use your KMS keys and gain access to your encrypted data\. IAM policies define which actions an identity \(user, group, or role\) can perform on which resources\. Following security best practices, AWS recommends that you allow least privilege\. In other words, you should grant to identities only the permissions they need and only for keys that are required to perform a task\. Otherwise, the user might use keys that are not appropriate for your data\.

Instead of granting permission for all keys, determine the minimum set of keys that users need to access encrypted data\. Then design policies that allow the users to use only those keys\. For example, do not allow `kms:Decrypt` permission on all KMS keys\. Instead, allow the permission only on specific keys in a specific Region for your account\. By adopting the principle of least privilege, you can reduce the risk of unintended disclosure of your data\.

**Note**  
This control is not supported in Asia Pacific \(Jakarta\) or Asia Pacific \(Osaka\)\.

### Remediation<a name="kms-2-remediation"></a>

To remediate this issue, you modify the inline policy to restrict access to the keys\.

**To modify an IAM inline policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the IAM navigation pane, choose **Users**, **Groups**, or **Roles**\. 

1. Choose the name of the user, group or role for which to modify IAM inline policies\. 

1. Choose the arrow next to the policy to modify\.

1. Choose **Edit policy**\.

1. Choose the **JSON** tab\.

1. Change the `"Resource"` value to the specific keys you want to allow\.

1. After you modify the policy, choose **Review policy**\.

1. Choose **Save changes**\.

For more information, see [Using IAM policies with AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html) in the *AWS Key Management Service Developer Guide*\.

## \[KMS\.3\] AWS KMS keys should not be unintentionally deleted<a name="fsbp-kms-3"></a>

**Category:** Protect > Data protection > Data deletion protection

**Severity:** Critical

**Resource type:** `AWS::KMS::Key`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/kms-cmk-not-scheduled-for-deletion.html](https://docs.aws.amazon.com/config/latest/developerguide/kms-cmk-not-scheduled-for-deletion.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether KMS keys are scheduled for deletion\. The control fails if a KMS key is scheduled for deletion\.

KMS keys cannot be recovered once deleted\. Data encrypted under a KMS key is also permanently unrecoverable if the KMS key is deleted\. If meaningful data has been encrypted under a KMS key scheduled for deletion, consider decrypting the data or re\-encrypting the data under a new KMS key unless you are intentionally performing a *cryptographic erasure*\.

When a KMS key is scheduled for deletion, a mandatory waiting period is enforced to allow time to reverse the deletion, if it was scheduled in error\. The default waiting period is 30 days, but it can be reduced to as short as 7 days when the KMS key is scheduled for deletion\. During the waiting period, the scheduled deletion can be canceled and the KMS key will not be deleted\.

For additional information regarding deleting KMS keys, see [Deleting KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/deleting-keys.html) in the *AWS Key Management Service Developer Guide*\.

**Note**  
This control is not supported in the Asia Pacific \(Osaka\) and Europe \(Milan\) Regions\.

### Remediation<a name="kms-3-remediation"></a>

For detailed remediation instructions to cancel a scheduled KMS key deletion, see **To cancel key deletion** under [Scheduling and canceling key deletion \(console\)](https://docs.aws.amazon.com/kms/latest/developerguide/deleting-keys.html#deleting-keys-scheduling-key-deletion) in the AWS Key Management Service Developer Guide\. 

## \[Lambda\.1\] Lambda function policies should prohibit public access<a name="fsbp-lambda-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::Lambda::Function`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-public-access-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-public-access-prohibited.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the Lambda function resource\-based policy prohibits public access outside of your account\.

The control also fails if a Lambda function is invoked from Amazon S3 and the policy does not include a condition for `AWS:SourceAccount`\.

The Lambda function should not be publicly accessible, as this may allow unintended access to your code stored in the function\.

**Note**  
This control is not supported in the China \(Beijing\) or China \(Ningxia\) Regions\.

### Remediation<a name="lambda-1-remediation"></a>

If a Lambda function fails this control, it indicates that the resource\-based policy statement for the Lambda function allows public access\.

To remediate the issue, you must update the policy to remove the permissions or to add the `AWS:SourceAccount` condition\. You can only update the resource\-based policy from the Lambda API\.

The following instructions use the console to review the policy and the AWS Command Line Interface to remove the permissions\.

**To view the resource\-based policy for a Lambda function**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. In the navigation pane, choose **Functions**\.

1. Choose the function\.

1. Choose **Permissions**\. The resource\-based policy shows the permissions that are applied when another account or AWS service attempts to access the function\. 

1. Examine the resource\-based policy\. Identify the policy statement that has `Principal` field values that make the policy public\. For example, allowing `"*"` or `{ "AWS": "*" }`\.

   You cannot edit the policy from the console\. To remove permissions from the function, you use the `remove-permission` command from the AWS CLI\.

   Note the value of the statement ID \(`Sid`\) for the statement that you want to remove\.

To use the AWS CLI to remove permissions from a Lambda function, issue the [https://docs.aws.amazon.com/cli/latest/reference/lambda/remove-permission.html](https://docs.aws.amazon.com/cli/latest/reference/lambda/remove-permission.html) command\.

```
$ aws lambda remove-permission --function-name <function-name> --statement-id <statement-id>
```

Replace `<function-name>` with the name of the Lambda function, and `<statement-id>` with the statement ID of the statement to remove\.

**To verify that the permissions are updated**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. In the navigation pane, choose **Functions**\.

1. Choose the function that you updated\.

1. Choose **Permissions**\.

   The resource\-based policy should be updated\. If there was only one statement in the policy, then the policy is empty\.

For more information, see [Using resource\-based policies for AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html) in the *AWS Lambda Developer Guide*\.

## \[Lambda\.2\] Lambda functions should use supported runtimes<a name="fsbp-lambda-2"></a>

**Category:** Protect > Secure development

**Severity:** Medium

**Resource type:** `AWS::Lambda::Function`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-settings-check.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-settings-check.html)

**Schedule type:** Change triggered

**Parameters:** 
+ `runtime`: `nodejs18.x, nodejs16.x, nodejs14.x, nodejs12.x, python3.9, python3.8, python3.7, ruby2.7, java11, java8, java8.al2, go1.x, dotnetcore3.1, dotnet6`

This control checks that the Lambda function settings for runtimes match the expected values set for the supported runtimes for each language\. This control checks function settings for the following runtimes: `nodejs18.x,`, `nodejs16.x`, `nodejs14.x`, `nodejs12.x`, `python3.9`, `python3.8`, `python3.7`, `ruby2.7`, `java11`, `java8`, `java8.al2`, `go1.x`, `dotnetcore3.1`, and `dotnet6`\.

The AWS Config rule ignores functions that have a package type of `Image`\.

[Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) are built around a combination of operating system, programming language, and software libraries that are subject to maintenance and security updates\. When a runtime component is no longer supported for security updates, Lambda deprecates the runtime\. Even though you cannot create functions that use the deprecated runtime, the function is still available to process invocation events\. Make sure that your Lambda functions are current and do not use out\-of\-date runtime environments\.

To learn more about the supported runtimes that this control checks for the supported languages, see [AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) in the *AWS Lambda Developer Guide*\.

**Note**  
This control is not supported in Asia Pacific \(Osaka\)or China \(Ningxia\)\.

### Remediation<a name="lambda-2-remediation"></a>

For more information on supported runtimes and deprecation schedules, see the [Runtime support policy](https://docs.aws.amazon.com/lambda/latest/dg/runtime-support-policy.html) section of the *AWS Lambda Developer Guide*\. When you migrate your runtimes to the latest version, follow the syntax and guidance from the publishers of the language\.

## \[Lambda\.5\] VPC Lambda functions should operate in more than one Availability Zone<a name="fsbp-lambda-5"></a>

**Category:** Recover > Resilience > High Availability

**Severity:** Medium

**Resource type:** `AWS::Lambda::Function`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-vpc-multi-az-check.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-vpc-multi-az-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Lambda has more than one availability zone associated\. The rule fails if only one availability zone is associated with Lambda\. 

Deploying resources across multiple Availability Zones is an AWS best practice to ensure high availability within your architecture\. Availability is a core pillar in the confidentiality, integrity, and availability triad security model\. All Lambda functions should have a multi\-Availability Zone deployment to ensure that a single zone of failure does not cause a total disruption of operations\.

### Remediation<a name="lambda-5-remediation"></a>

**To deploy a Lambda function in multiple Availability Zones through console:**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)

1. From the **Functions** page on the Lambda console choose a function\.

1. Choose **Configuration** and then choose **VPC**\.

1. Choose **Edit**\.

1. If the function was not originally connected to a VPC, select a VPC from the dropdown menu\. If the function was not originally connected to a VPC, choose at least one security group to attach to the function
**Note**  
The function execution role must have permissions to call `CreateNetworkInterface` on EC2\.

1. Choose **Save**\.

## \[NetworkFirewall\.3\] Network Firewall policies should have at least one rule group associated<a name="fsbp-networkfirewall-3"></a>

**Category:** Protect > Secure Network Configuration

**Severity:** Medium

**Resource type:** `AWS::NetworkFirewall::FirewallPolicy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-rule-group-associated.html](https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-rule-group-associated.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a Network Firewall policy has any stateful or stateless rule groups associated\. The control fails if stateless or stateful rule groups are not assigned\.

A firewall policy defines how your firewall monitors and handles traffic in Amazon Virtual Private Cloud \(Amazon VPC\)\. Configuration of stateless and stateful rule groups helps to filter packets and traffic flows, and defines default traffic handling\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="networkfirewall-3-remediation"></a>

To add a rule group to a Network Firewall policy, see [Updating a firewall policy](https://docs.aws.amazon.com/network-firewall/latest/developerguide/firewall-policy-updating.html) in the *AWS Network Firewall Developer Guide*\. For information about creating and managing rule groups, see [Rule groups in AWS Network Firewall](https://docs.aws.amazon.com/network-firewall/latest/developerguide/rule-groups.html)\.

## \[NetworkFirewall\.4\] The default stateless action for Network Firewall policies should be drop or forward for full packets<a name="fsbp-networkfirewall-4"></a>

**Category:** Protect > Secure Network Configuration

**Severity:** Medium

**Resource type:** `AWS::NetworkFirewall::FirewallPolicy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-default-action-full-packets.html](https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-default-action-full-packets.html)

**Schedule type:** Change triggered

**Parameters:**
+ `statelessDefaultActions: aws:drop,aws:forward_to_sfe`

This control checks whether the default stateless action for full packets for a Network Firewall policy is drop or forward\. The control passes if `Drop` or `Forward` is selected, and fails if `Pass` is selected\.

A firewall policy defines how your firewall monitors and handles traffic in Amazon VPC\. You configure stateless and stateful rule groups to filter packets and traffic flows\. Defaulting to `Pass` can allow unintended traffic\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="networkfirewall-4-remediation"></a>

**To change the firewall policy:**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, under **Network Firewall**, choose **Firewall policies**\.

1. Select the name of the firewall policy that you want to edit\. This takes you to the firewall policy’s details page\.

1. In **Stateless Default Actions**, choose **Edit**\. Then choose **Drop** or **Forward to stateful rule groups** as the **Default actions for full packets**\.

## \[NetworkFirewall\.5\] The default stateless action for Network Firewall policies should be drop or forward for fragmented packets<a name="fsbp-networkfirewall-5"></a>

**Category:** Protect > Secure Network Configuration

**Severity:** Medium

**Resource type:** `AWS::NetworkFirewall::FirewallPolicy`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-default-action-fragment-packets.html](https://docs.aws.amazon.com/config/latest/developerguide/netfw-policy-default-action-fragment-packets.html)

**Schedule type:** Change triggered

**Parameters:**
+ `statelessFragDefaultActions (Required) : aws:drop, aws:forward_to_sfe`

This control checks whether the default stateless action for fragmented packets for a Network Firewall policy is drop or forward\. The control passes if `Drop` or `Forward` is selected, and fails if `Pass` is selected\.

A firewall policy defines how your firewall monitors and handles traffic in Amazon VPC\. You configure stateless and stateful rule groups to filter packets and traffic flows\. Defaulting to `Pass` can allow unintended traffic\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="networkfirewall-5-remediation"></a>

**To change the firewall policy:**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, under **Network Firewall**, choose **Firewall policies**\.

1. Select the name of the firewall policy that you want to edit\. This takes you to the firewall policy’s details page\.

1. In **Stateless Default Actions**, choose **Edit**\. Then choose **Drop** or **Forward to stateful rule groups** as the **Default actions for fragmented packets**\.

## \[NetworkFirewall\.6\] Stateless Network Firewall rule groups should not be empty<a name="fsbp-networkfirewall-6"></a>

**Category:** Protect > Secure Network Configuration

**Severity:** Medium

**Resource type:** `AWS::NetworkFirewall::RuleGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/netfw-stateless-rule-group-not-empty.html](https://docs.aws.amazon.com/config/latest/developerguide/netfw-stateless-rule-group-not-empty.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if a stateless rule group in AWS Network Firewall contains rules\. The rule will fail if there are no rules in the rule group\.

A rule group contains rules that define how your firewall processes traffic in your VPC\. An empty stateless rule group, when present in a firewall policy, might give the impression that the rule group will process traffic\. However, when the stateless rule group is empty, it does not process traffic\.

### Remediation<a name="networkfirewall-6-remediation"></a>

**To add rules to a Network Firewall rule group:**

1. Sign in to the AWS Management Console and open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)

1. In the navigation pane, under **Network Firewall**, choose **Network Firewall rule groups**\.

1. In the **Network Firewall rule groups** page, choose the name of the rule group that you want to edit\. This takes you to the firewall rule groups details page\.

1. For stateless rule groups, choose **Edit Rules** to add rules to the rule group\.

## \[OpenSearch\.1 \] OpenSearch domains should have encryption at rest enabled<a name="fsbp-opensearch-1"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-encrypted-at-rest.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-encrypted-at-rest.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether OpenSearch domains have encryption\-at\-rest configuration enabled\. The check fails if encryption at rest is not enabled\.

For an added layer of security for sensitive data, you should configure your OpenSearch Service domain to be encrypted at rest\. When you configure encryption of data at rest, AWS KMS stores and manages your encryption keys\. To perform the encryption, AWS KMS uses the Advanced Encryption Standard algorithm with 256\-bit keys \(AES\-256\)\.

To learn more about OpenSearch Service encryption at rest, see [Encryption of data at rest for Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/encryption-at-rest.html) in the *Amazon OpenSearch Service* *Developer Guide*\.

### Remediation<a name="opensearch-1-remediation"></a>

By default, domains do not encrypt data at rest, and you cannot configure existing domains to use the feature\. To enable the feature, you must create another domain and migrate your data\.

For information about creating domains, see [Creating and managing Amazon OpenSearch Service domains](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createupdatedomains.html#es-createdomains) in the Amazon OpenSearch Service Developer Guide\.

Encryption of data at rest requires Amazon OpenSearch 1\.0 or later\. For more information about encrypting data at rest for Amazon OpenSearch, see [Encryption of data at rest for Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/encryption-at-rest.html) in the *Amazon OpenSearch Service Developer Guide*\.

## \[OpenSearch\.2\] OpenSearch domains should be in a VPC<a name="fsbp-opensearch-2"></a>

**Category:** Protect > Secure network configuration > Resources within VPC

**Severity:** Critical

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-in-vpc-only.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-in-vpc-only.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether OpenSearch domains are in a VPC\. It does not evaluate the VPC subnet routing configuration to determine public access\.

You should ensure that OpenSearch domains are not attached to public subnets\. See [Resource\-based policies](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/ac.html#ac-types-resource) in the Amazon OpenSearch Service Developer Guide\. You should also ensure that your VPC is configured according to the recommended best practices\. See [Security best practices for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html) in the Amazon VPC User Guide\.

OpenSearch domains deployed within a VPC can communicate with VPC resources over the private AWS network, without the need to traverse the public internet\. This configuration increases the security posture by limiting access to the data in transit\. VPCs provide a number of network controls to secure access to OpenSearch domains, including network ACL and security groups\. Security Hub recommends that you migrate public OpenSearch domains to VPCs to take advantage of these controls\.

### Remediation<a name="opensearch-2-remediation"></a>

If you create a domain with a public endpoint, you cannot later place it within a VPC\. Instead, you must create a new domain and migrate your data\. The reverse is also true\. If you create a domain within a VPC, it cannot have a public endpoint\.

Instead, you must either [create another domain](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createupdatedomains.html#es-createdomains) or disable this control\.

See [Launching your Amazon OpenSearch Service domains within a VPC](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/vpc.html) in the Amazon OpenSearch Service Developer Guide\.

## \[OpenSearch\.3\] OpenSearch domains should encrypt data sent between nodes<a name="fsbp-opensearch-3"></a>

**Category:** Protect > Data protection > Encryption of data in transit

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-node-to-node-encryption-check.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-node-to-node-encryption-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether OpenSearch domains have node\-to\-node encryption enabled\. This control fails if node\-to\-node encryption is disabled on the domain\.

HTTPS \(TLS\) can be used to help prevent potential attackers from eavesdropping on or manipulating network traffic using person\-in\-the\-middle or similar attacks\. Only encrypted connections over HTTPS \(TLS\) should be allowed\. Enabling node\-to\-node encryption for OpenSearch domains ensures that intra\-cluster communications are encrypted in transit\.

There can be a performance penalty associated with this configuration\. You should be aware of and test the performance trade\-off before enabling this option\.

### Remediation<a name="opensearch-3-remediation"></a>

Node\-to\-node encryption can only be enabled on a new domain\. To remediate this finding, create a new domain with **Node\-to\-node encryption** enabled and migrate your data to the new domain\. Follow the instructions to [create a new domain](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createupdatedomains.html#es-createdomains) in the Amazon OpenSearch Service Developer Guide and ensure that you select the **Node\-to\-node encryption** option when creating the new domain\. Then follow [Using a snapshot to migrate data](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/version-migration.html#snapshot-based-migration) to migrate your data to the new domain\.

## \[OpenSearch\.4\] OpenSearch domain error logging to CloudWatch Logs should be enabled<a name="fsbp-opensearch-4"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-logs-to-cloudwatch.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-logs-to-cloudwatch.html)

**Schedule type:** Change triggered

**Parameters:**
+ `logtype = 'error'`

This control checks whether OpenSearch domains are configured to send error logs to CloudWatch Logs\. This control fails if error logging to CloudWatch is not enabled for a domain\.

You should enable error logs for OpenSearch domains and send those logs to CloudWatch Logs for retention and response\. Domain error logs can assist with security and access audits, and can help to diagnose availability issues\.

### Remediation<a name="opensearch-4-remediation"></a>

For information on how to enable log publishing, see [Enabling log publishing \(console\)](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createdomain-configure-slow-logs.html#createdomain-configure-slow-logs-console) in the Amazon OpenSearch Service Developer Guide\.

## \[OpenSearch\.5\] OpenSearch domains should have audit logging enabled<a name="fsbp-opensearch-5"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-audit-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-audit-logging-enabled.html)

**Schedule type:** Change triggered

**Parameters:**
+ `cloudWatchLogsLogGroupArnList` \(Optional\)\. Security Hub does not populate this parameter\. Comma\-separated list of CloudWatch Logs log groups that should be configured for audit logs\.

This rule is `NON_COMPLIANT` if the CloudWatch Logs log group of the OpenSearch domain is not specified in this parameter list\.

This control checks whether OpenSearch domains have audit logging enabled\. This control fails if an OpenSearch domain does not have audit logging enabled\.

Audit logs are highly customizable\. They allow you to track user activity on your OpenSearch clusters, including authentication successes and failures, requests to OpenSearch, index changes, and incoming search queries\.

### Remediation<a name="opensearch-5-remediation"></a>

For detailed instructions on enabling audit logs, see [Enabling audit logs](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/audit-logs.html#audit-log-enabling) in the Amazon OpenSearch Service Developer Guide\.

## \[OpenSearch\.6\] OpenSearch domains should have at least three data nodes<a name="fsbp-opensearch-6"></a>

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-data-node-fault-tolerance.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-data-node-fault-tolerance.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether OpenSearch domains are configured with at least three data nodes and `zoneAwarenessEnabled` is `true`\. This control fails for an OpenSearch domain if `instanceCount` is less than 3 or `zoneAwarenessEnabled` is `false`\.

An OpenSearch domain requires at least three data nodes for high availability and fault\-tolerance\. Deploying an OpenSearch domain with at least three data nodes ensures cluster operations if a node fails\.

### Remediation<a name="opensearch-6-remediation"></a>

**To modify the number of data nodes in an OpenSearch domain**

1. Sign in to the AWS console and open the Amazon OpenSearch Service console at [https://console\.aws\.amazon\.com/es/](https://console.aws.amazon.com/es/)\.

1. Under **My domains**, choose the name of the domain to edit, and choose **Edit**\.

1. Under **Data nodes** set **Number of nodes** to a number greater than `3`\. If you are deploying to three Availability Zone, set the number to a multiple of three to ensure equal distribution across Availability Zones\. 

1. Choose **Submit**\.

## \[OpenSearch\.7\] OpenSearch domains should have fine\-grained access control enabled<a name="fsbp-opensearch-7"></a>

**Category:** Protect > Secure Access Management > Sensitive API actions restricted

**Severity:** High

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-access-control-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-access-control-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether OpenSearch domains have fine\-grained access control enabled\. The control fails if the fine\-grained access control is not enabled\. Fine\-grained access control requires `advanced-security-options`in the OpenSearch parameter `update-domain-config` to be enabled\.

Fine\-grained access control offers additional ways of controlling access to your data on Amazon OpenSearch Service\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="opensearch-7-remediation"></a>

To enable fine\-grained access control, see [Fine\-grained access control in Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/fgac.html) in the *Amazon OpenSearch Service Developer Guide*\.

## \[OpenSearch\.8\] Connections to OpenSearch domains should be encrypted using TLS 1\.2<a name="fsbp-opensearch-8"></a>

**Category:** Protect > Data protection > Encryption of data\-in\-transit

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-https-required.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-https-required.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether connections to OpenSearch domains are required to use TLS 1\.2\. The check fails if the OpenSearch domain `TLSSecurityPolicy` is not `Policy-Min-TLS-1-2-2019-07`\.

HTTPS \(TLS\) can be used to help prevent potential attackers from using person\-in\-the\-middle or similar attacks to eavesdrop on or manipulate network traffic\. Only encrypted connections over HTTPS \(TLS\) should be allowed\. Encrypting data in transit can affect performance\. You should test your application with this feature to understand the performance profile and the impact of TLS\. TLS 1\.2 provides several security enhancements over previous versions of TLS\. 

### Remediation<a name="opensearch-8-remediation"></a>

To enable TLS encryption, use the [UpdateDomainConfig](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/configuration-api.html#configuration-api-actions-updatedomainconfig) API operation to configure the [DomainEndpointOptions](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/configuration-api.html#configuration-api-datatypes-domainendpointoptions) in order to set the `TLSSecurityPolicy`\. For more information, see [Node\-to\-node encryption](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/ntn.html) in the Amazon OpenSearch Service Developer Guide\.

## \[RDS\.1\] RDS snapshots should be private<a name="fsbp-rds-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::RDS::DBSnapshot`, `AWS::RDS::DBClusterSnapshot`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon RDS snapshots are public\. The control fails if RDS snapshots are public\. This control evaluates RDS instances, Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters\.

RDS snapshots are used to back up the data on your RDS instances at a specific point in time\. They can be used to restore previous states of RDS instances\.

An RDS snapshot must not be public unless intended\. If you share an unencrypted manual snapshot as public, this makes the snapshot available to all AWS accounts\. This may result in unintended data exposure of your RDS instance\.

Note that if the configuration is changed to allow public access, the AWS Config rule may not be able to detect the change for up to 12 hours\. Until the AWS Config rule detects the change, the check passes even though the configuration violates the rule\.

To learn more about sharing a DB snapshot, see [Sharing a DB snapshot](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html) in the *Amazon RDS User Guide*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="rds-1-remediation"></a>

To remediate this issue, update your RDS snapshots to remove public access\.

**To remove public access for RDS snapshots**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Navigate to **Snapshots** and then choose the public snapshot you want to modify\.

1. From **Actions**, choose **Share Snapshots**\.

1. From **DB snapshot visibility**, choose **Private**\.

1. Under **DB snapshot visibility**, choose **all**\.

1. Choose **Save**\.

## \[RDS\.2\] Amazon RDS DB instances should prohibit public access, as determined by the PubliclyAccessible configuration<a name="fsbp-rds-2"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon RDS instances are publicly accessible by evaluating the `PubliclyAccessible` field in the instance configuration item\.

Neptune DB instances and Amazon DocumentDB clusters do not have the `PubliclyAccessible` flag and cannot be evaluated\. However, this control can still generate findings for these resources\. You can suppress these findings\.

The `PubliclyAccessible` value in the RDS instance configuration indicates whether the DB instance is publicly accessible\. When the DB instance is configured with `PubliclyAccessible`, it is an Internet\-facing instance with a publicly resolvable DNS name, which resolves to a public IP address\. When the DB instance isn't publicly accessible, it is an internal instance with a DNS name that resolves to a private IP address\.

Unless you intend for your RDS instance to be publicly accessible, the RDS instance should not be configured with `PubliclyAccessible` value\. Doing so might allow unnecessary traffic to your database instance\.

### Remediation<a name="rds-2-remediation"></a>

To remediate this issue, update your RDS DB instances to remove public access\.

**To remove public access from RDS DB instances**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Navigate to **Databases** and then choose your public database\.

1. Choose **Modify**\.

1. Under **Connectivity**, expand **Additional connectivity configuration**\.

1. Under **Public access**, choose **Not publicly accessible**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose **Apply immediately**\.

1. Choose **Modify DB Instance**\.

For more information, see [Working with a DB instance in a VPC](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html) in the *Amazon RDS User Guide*\.

## \[RDS\.3\] RDS DB instances should have encryption at rest enabled<a name="fsbp-rds-3"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether storage encryption is enabled for your Amazon RDS DB instances\.

This control is intended for RDS DB instances\. However, it can also generate findings for Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters\. If these findings are not useful, then you can suppress them\.

For an added layer of security for your sensitive data in RDS DB instances, you should configure your RDS DB instances to be encrypted at rest\. To encrypt your RDS DB instances and snapshots at rest, enable the encryption option for your RDS DB instances\. Data that is encrypted at rest includes the underlying storage for DB instances, its automated backups, read replicas, and snapshots\. 

RDS encrypted DB instances use the open standard AES\-256 encryption algorithm to encrypt your data on the server that hosts your RDS DB instances\. After your data is encrypted, Amazon RDS handles authentication of access and decryption of your data transparently with a minimal impact on performance\. You do not need to modify your database client applications to use encryption\. 

Amazon RDS encryption is currently available for all database engines and storage types\. Amazon RDS encryption is available for most DB instance classes\. To learn about DB instance classes that do not support Amazon RDS encryption, see [Encrypting Amazon RDS resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-3-remediation"></a>

For information about encrypting DB instances in Amazon RDS, see [Encrypting Amazon RDS resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html) in the *Amazon RDS User Guide*\.

## \[RDS\.4\] RDS cluster snapshots and database snapshots should be encrypted at rest<a name="fsbp-rds-4"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::RDS::DBClusterSnapshot`,` AWS::RDS::DBSnapshot`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshot-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshot-encrypted.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether RDS DB snapshots are encrypted\.

This control is intended for RDS DB instances\. However, it can also generate findings for snapshots of Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters\. If these findings are not useful, then you can suppress them\.

Encrypting data at rest reduces the risk that an unauthenticated user gets access to data that is stored on disk\. Data in RDS snapshots should be encrypted at rest for an added layer of security\.

### Remediation<a name="rds-4-remediation"></a>

You can use the Amazon RDS console to remediate this issue\.

**To encrypt an unencrypted RDS snapshot**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Snapshots**\.

1. Find the snapshot to encrypt under **Manual** or **System**\.

1. Select the check box next to the snapshot to encrypt\.

1. Choose **Actions**, then choose **Copy Snapshot**\.

1. Under **New DB Snapshot Identifier**, type a name for the new snapshot\.

1. Under **Encryption**, select **Enable Encryption**\.

1. Choose the KMS key to use to encrypt the snapshot\.

1. Choose **Copy Snapshot**\.

1. After the new snapshot is created, delete the original snapshot\.

1. For **Backup Retention Period**, choose a positive nonzero value\. For example, 30 days\.

## \[RDS\.5\] RDS DB instances should be configured with multiple Availability Zones<a name="fsbp-rds-5"></a>

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-multi-az-support.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-multi-az-support.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether high availability is enabled for your RDS DB instances\.

RDS DB instances should be configured for multiple Availability Zones \(AZs\)\. This ensures the availability of the data stored\. Multi\-AZ deployments allow for automated failover if there is an issue with Availability Zone availability and during regular RDS maintenance\.

### Remediation<a name="rds-5-remediation"></a>

To remediate this issue, update your DB instances to enable multiple Availability Zones\.

**To enable multiple Availability Zones for a DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**, and then choose the DB instance that you want to modify\. 

1. Choose **Modify**\. The **Modify DB Instance** page appears\. 

1. Under **Instance Specifications**, set **Multi\-AZ deployment** to **Yes**\.

1. Choose **Continue** and then check the summary of modifications\. 

1. \(Optional\) Choose **Apply immediately** to apply the changes immediately\. Choosing this option can cause an outage in some cases\. For more information, see [Using the Apply Immediately setting](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.DBInstance.Modifying.html#USER_ModifyInstance.ApplyImmediately) in the *Amazon RDS User Guide*\.

1. On the confirmation page, review your changes\. If they are correct, choose **Modify DB Instance** to save your changes\.

## \[RDS\.6\] Enhanced monitoring should be configured for RDS DB instances and clusters<a name="fsbp-rds-6"></a>

**Category:** Detect > Detection services

**Severity:** Low

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-enhanced-monitoring-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-enhanced-monitoring-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether enhanced monitoring is enabled for your RDS DB instances\.

In Amazon RDS, Enhanced Monitoring enables a more rapid response to performance changes in underlying infrastructure\. These performance changes could result in a lack of availability of the data\. Enhanced Monitoring provides real\-time metrics of the operating system that your RDS DB instance runs on\. An agent is installed on the instance\. The agent can obtain metrics more accurately than is possible from the hypervisor layer\.

Enhanced Monitoring metrics are useful when you want to see how different processes or threads on a DB instance use the CPU\. For more information, see [Enhanced Monitoring](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-6-remediation"></a>

For detailed instructions on how to enable Enhanced Monitoring for your DB instance, see [Setting up for and enabling Enhanced Monitoring](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.html#USER_Monitoring.OS.Enabling) in the *Amazon RDS User Guide*\.

## \[RDS\.7\] RDS clusters should have deletion protection enabled<a name="fsbp-rds-7"></a>

**Category:** Protect > Data protection > Data deletion protection

**Severity:** Low

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-deletion-protection-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-deletion-protection-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether RDS clusters have deletion protection enabled\. 

This control is intended for RDS DB instances\. However, it can also generate findings for Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters\. If these findings are not useful, then you can suppress them\.

Enabling cluster deletion protection is an additional layer of protection against accidental database deletion or deletion by an unauthorized entity\.

When deletion protection is enabled, an RDS cluster cannot be deleted\. Before a deletion request can succeed, deletion protection must be disabled\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)
South America \(São Paulo\)\.

### Remediation<a name="rds-7-remediation"></a>

To remediate this issue, update your RDS DB cluster to enable delete protection\.

**To enable deletion protection for an RDS DB cluster**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**, then choose the DB cluster that you want to modify\. 

1. Choose **Modify**\.

1. Under **Deletion protection**, choose **Enable deletion protection**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. The options are **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. Choose **Modify Cluster**\.

## \[RDS\.8\] RDS DB instances should have deletion protection enabled<a name="fsbp-rds-8"></a>

**Category: **Protect > Data protection > Data deletion protection

**Severity:** Low

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-deletion-protection-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-deletion-protection-enabled.html)

**Schedule type:** Change triggered

**Parameters:**
+ `databaseEngines`: `mariadb,mysql,oracle-ee,oracle-se2,oracle-se1,oracle-se,postgres,sqlserver-ee,sqlserver-se,sqlserver-ex,sqlserver-web`

This control checks whether your RDS DB instances that use one of the listed database engines have deletion protection enabled\.

Enabling instance deletion protection is an additional layer of protection against accidental database deletion or deletion by an unauthorized entity\.

While deletion protection is enabled, an RDS DB instance cannot be deleted\. Before a deletion request can succeed, deletion protection must be disabled\.

### Remediation<a name="rds-8-remediation"></a>

To remediate this issue, update your RDS DB instance to enable deletion protection\.

**To enable deletion protection for an RDS DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**, then choose the DB instance that you want to modify\. 

1. Choose **Modify**\.

1. Under **Deletion protection**, choose **Enable deletion protection**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. The options are **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. Choose **Modify DB Instance**\.

## \[RDS\.9\] Database logging should be enabled<a name="fsbp-rds-9"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-logging-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the following logs of Amazon RDS are enabled and sent to CloudWatch Logs:
+ Oracle: \(Alert, Audit, Trace, Listener\)
+ PostgreSQL: \(Postgresql, Upgrade\)
+ MySQL: \(Audit, Error, General, SlowQuery\)
+ MariaDB: \(Audit, Error, General, SlowQuery\)
+ SQL Server: \(Error, Agent\)
+ Aurora: \(Audit, Error, General, SlowQuery\)
+ Aurora\-MySQL: \(Audit, Error, General, SlowQuery\)
+ Aurora\-PostgreSQL: \(Postgresql, Upgrade\)\.

RDS databases should have relevant logs enabled\. Database logging provides detailed records of requests made to RDS\. Database logs can assist with security and access audits and can help to diagnose availability issues\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
China \(Ningxia\)
Europe \(Milan\)

### Remediation<a name="rds-9-remediation"></a>

Logging options are contained in the DB parameter group associated with the RDS DB cluster or instance\. To enable logging when the default parameter group for the database engine is used, you must create a new DB parameter group that has the required parameter values\. You must then associate the customer DB parameter group with the DB cluster or instance\.

To enable and publish MariaDB, MySQL, or PostgreSQL logs to CloudWatch Logs from the AWS Management Console, set the following parameters in a custom DB Parameter Group:


|  Database engine  |  Parameters  | 
| --- | --- | 
|  MariaDB  |  `general_log=1` `slow_query_log=1` `log_output = FILE` MariaDB also requires a custom options group, explained below\.  | 
|  MySQL  |  `general_log=1` `slow_query_log=1` `log_output = FILE`  | 
|  PostgreSQL  |  `log_statement=all` `log_min_duration_statement=minimum query duration (ms) to log`  | 

**To create a custom DB parameter group**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Parameter groups**\.

1. Choose **Create parameter group**\. The **Create parameter group** window appears\. 

1. In the **Parameter group** family list, choose a DB parameter group family\. 

1. In the **Type** list, choose **DB Parameter Group**\.

1. In **Group name**, enter the name of the new DB parameter group\.

1. In **Description**, enter a description for the new DB parameter group\. 

1. Choose **Create**\.

**To create a new option group for MariaDB logging by using the console**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Option groups**\. 

1. Choose **Create group**\. 

1. In the **Create option group** window, do the following: 

   1. For **Name**, type a name for the option group that is unique within your AWS account\. The name can contain only letters, digits, and hyphens\.

   1. For **Description**, type a brief description of the option group\. The description is used for display purposes\.

   1. For **Engine**, choose the DB engine that you want\. 

   1. For **Major engine version**, choose the major version of the DB engine that you want\.

1. To continue, choose **Create**\. 

1. Choose the name of the option group you just created\.

1. Choose **Add option**\.

1. Choose **MARIADB\_AUDIT\_PLUGIN** from the** Option name** list\.

1. Set `SERVER_AUDIT_EVENTS` to `CONNECT, QUERY, TABLE, QUERY_DDL, QUERY_DML, QUERY_DCL`\.

1. Choose **Add option**\.

**To publish SQL Server DB, Oracle DB, or PostgreSQL logs to CloudWatch Logs from the AWS Management Console**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**\.

1. Choose the DB instance that you want to modify\. 

1. Choose **Modify**\.

1. Under **Log exports**, choose all of the log files to start publishing to CloudWatch Logs\.

   **Log exports** is available only for database engine versions that support publishing to CloudWatch Logs\.

1. Choose **Continue**\. Then on the summary page, choose** Modify DB Instance**\.

**To apply a new DB parameter group or DB options group to an RDS DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**\.

1. Choose the DB instance that you want to modify\. 

1. Choose **Modify**\. The **Modify DB Instance** page appears\. 

1. Under **Database options**, change the DB parameter group and DB options group as needed\.

1. When you finish you changes, choose **Continue**\. Check the summary of modifications\. 

1. \(Optional\) Choose **Apply immediately** to apply the changes immediately\. Choosing this option can cause an outage in some cases\. For more information, see [Using the Apply Immediately setting](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.DBInstance.Modifying.html#USER_ModifyInstance.ApplyImmediately) in the *Amazon RDS User Guide*\. 

1. Choose **Modify DB Instance** to save your changes\. 

## \[RDS\.10\] IAM authentication should be configured for RDS instances<a name="fsbp-rds-10"></a>

**Category:** Protect > Secure access management > Passwordless authentication

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-iam-authentication-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-iam-authentication-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an RDS DB instance has IAM database authentication enabled\.

IAM database authentication allows authentication to database instances with an authentication token instead of a password\. Network traffic to and from the database is encrypted using SSL\. For more information, see [IAM database authentication](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/UsingWithRDS.IAMDBAuth.html) in the *Amazon Aurora User Guide*\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)

### Remediation<a name="rds-10-remediation"></a>

To remediate this issue, update your DB instance to enable IAM authentication\.

**To enable IAM authentication for an existing DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Select the DB instance to modify\.

1. Choose **Modify**\. 

1. Under **Database authentication**, choose **Password and IAM database authentication**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. The options are **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. For clusters, choose **Modify DB Instance**\.

## \[RDS\.11\] Amazon RDS instances should have automatic backups enabled<a name="fsbp-rds-11"></a>

**Category:** Recover > Resilience > Backups enabled 

**Severity:** Medium

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/db-instance-backup-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/db-instance-backup-enabled.html)

**Schedule type:** Change triggered

**Parameters:** 
+ `backupRetentionMinimum:` 7

This control checks whether Amazon Relational Database Service instances have automated backups enabled and the backup retention period is greater than or equal to seven days\. The control fails if backups are not enabled, and if the retention period is less than 7 days\.

Backups help you more quickly recover from a security incident and strengthens the resilience of your systems\. Amazon RDS provides an easy way to configure daily full instance volume snapshots\. For more details on Amazon RDS automated backups, see [Working with Backups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html) in the Amazon RDS User Guide\.

**Note**  
This control is not supported in Asia Pacific \(Osaka\)\.

### Remediation<a name="rds-11-remediation"></a>

**To enable automated backups immediately**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**, and then choose the DB instance that you want to modify\. 

1. Choose **Modify** to open the **Modify DB Instance** page\. 

1. Under **Backup Retention Period**, choose a positive nonzero value, for example 30 days, then choose **Continue**\. 

1. Select the **Scheduling of modifications** section and choose when to apply modifications: you can choose to **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. Then, on the confirmation page, choose **Modify DB Instance** to save your changes and enable automated backups\.

## \[RDS\.12\] IAM authentication should be configured for RDS clusters<a name="fsbp-rds-12"></a>

**Category:** Protect > Secure access management > Passwordless authentication

**Severity:** Medium

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-iam-authentication-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-iam-authentication-enabled.html)

**Schedule type:** Change triggered

**Parameters:**None

This control checks whether an Amazon RDS DB cluster has IAM database authentication enabled\.

IAM database authentication allows for password\-free authentication to database instances\. The authentication uses an authentication token\. Network traffic to and from the database is encrypted using SSL\. For more information, see [IAM database authentication](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/UsingWithRDS.IAMDBAuth.html) in the *Amazon Aurora User Guide*\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)
South America \(São Paulo\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="rds-12-remediation"></a>

You can enable IAM authentication for a DB cluster from the Amazon RDS console\.

**To enable IAM authentication for an existing DB cluster**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Choose the DB cluster to modify\.

1. Choose **Modify**\.

1. Under **Database options**, select **Enable IAM DB authentication**\.

1. Choose **Continue**\. 

1. Under **Scheduling of modifications**, choose when to apply modifications: **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. Choose **Modify cluster**\.

## \[RDS\.13\] RDS automatic minor version upgrades should be enabled<a name="fsbp-rds-13"></a>

**Category:** Detect > Vulnerability and patch management 

**Severity:** High

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-automatic-minor-version-upgrade-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-automatic-minor-version-upgrade-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether automatic minor version upgrades are enabled for the RDS database instance\.

Enabling automatic minor version upgrades ensures that the latest minor version updates to the relational database management system \(RDBMS\) are installed\. These upgrades might include security patches and bug fixes\. Keeping up to date with patch installation is an important step in securing systems\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="rds-13-remediation"></a>

You can enable minor version upgrades for a DB instance from the Amazon RDS console\.

**To enable automatic minor version upgrades for an existing DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Choose the DB instance to modify\.

1. Choose **Modify**\. 

1. Under **Maintenance**, select **Yes** for **Auto minor version upgrade**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications: **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. Choose **Modify DB Instance**\.

## \[RDS\.14\] Amazon Aurora clusters should have backtracking enabled<a name="fsbp-rds-14"></a>

**Category:** Recover > Resilience > Backups enabled 

**Severity:** Medium

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/aurora-mysql-backtracking-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/aurora-mysql-backtracking-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon Aurora clusters have backtracking enabled\.

Backups help you to recover more quickly from a security incident\. They also strengthens the resilience of your systems\. Aurora backtracking reduces the time to recover a database to a point in time\. It does not require a database restore to do so\.

For more information about backtracking in Aurora, see [Backtracking an Aurora DB cluster](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Managing.Backtrack.html) in the *Amazon Aurora User Guide*\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
South America \(São Paulo\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="rds-14-remediation"></a>

For detailed instructions on how to enable Aurora backtracking, see [Configuring backtracking](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Managing.Backtrack.html#AuroraMySQL.Managing.Backtrack.Configuring) in the *Amazon Aurora User Guide*\.

Note that you cannot enable backtracking on an existing cluster\. Instead, you can create a clone that has backtracking enabled\. For more information about the limitations of Aurora backtracking, see the list of limitations in [Overview of backtracking](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Managing.Backtrack.html)\.

For information about pricing for backtracking, see the [Aurora pricing page](http://aws.amazon.com/rds/aurora/pricing/)\.

## \[RDS\.15\] RDS DB clusters should be configured for multiple Availability Zones<a name="fsbp-rds-15"></a>

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-multi-az-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-multi-az-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether high availability is enabled for your RDS DB clusters\.

RDS DB clusters should be configured for multiple Availability Zones to ensure availability of the data that is stored\. Deployment to multiple Availability Zones allows for automated failover in the event of an Availability Zone availability issue and during regular RDS maintenance events\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)
South America \(São Paulo\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="rds-15-remediation"></a>

To remediate this control, configure your DB cluster for multiple Availability Zones\.

**To enable multi\-AZ for a DB cluster**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Databases**, and then choose the DB instance to modify\. 

1. Choose **Modify**\. The **Modify DB Instance** page appears\.

1. Under **Instance Specifications**, set **Multi\-AZ deployment** to **Yes**\.

1. Choose **Continue** and check the summary of modifications\.

1. \(Optional\) Choose **Apply immediately** to apply the changes immediately\. Choosing this option can cause an outage in some cases\. For more information, see [Using the Apply Immediately setting](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.DBInstance.Modifying.html#USER_ModifyInstance.ApplyImmediately) in the *Amazon RDS User Guide*\.

   On the confirmation page, review your changes\. If they are correct, choose **Modify DB Instance**\.

**Note**  
Remediation steps differ for Aurora global databases\. To configure multiple Availability Zones for an Aurora global database, select your DB cluster\. Then, choose **Actions** and **Add reader**\. For more information, see [Adding Aurora Replicas to a DB cluster](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-replicas-adding.html) in the *Amazon Aurora User Guide*\.

## \[RDS\.16\] RDS DB clusters should be configured to copy tags to snapshots<a name="fsbp-rds-16"></a>

**Category:** Identify > Inventory

**Severity:** Low

**Resource type:** `AWS::RDS::DBCluster`

**AWS Config rule:** `rds-cluster-copy-tags-to-snapshots-enabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether RDS DB clusters are configured to copy all tags to snapshots when the snapshots are created\.

Identification and inventory of your IT assets is a crucial aspect of governance and security\. You need to have visibility of all your RDS DB clusters so that you can assess their security posture and take action on potential areas of weakness\. Snapshots should be tagged in the same way as their parent RDS database clusters\. Enabling this setting ensures that snapshots inherit the tags of their parent database clusters\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
Middle East \(Bahrain\)
South America \(São Paulo\)

### Remediation<a name="rds-16-remediation"></a>

**To enable automatic tag copying to snapshots for a DB cluster**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Select the DB cluster to modify\.

1. Choose **Modify**\.

1. Under **Backup**, select **Copy tags to snapshots**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. You can choose either **Apply during the next scheduled maintenance window** or **Apply immediately**\.

## \[RDS\.17\] RDS DB instances should be configured to copy tags to snapshots<a name="fsbp-rds-17"></a>

**Category:** Identify > Inventory

**Severity:** Low

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** `rds-instance-copy-tags-to-snapshots-enabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether RDS DB instances are configured to copy all tags to snapshots when the snapshots are created\.

Identification and inventory of your IT assets is a crucial aspect of governance and security\. You need to have visibility of all your RDS DB instances so that you can assess their security posture and take action on potential areas of weakness\. Snapshots should be tagged in the same way as their parent RDS database instances\. Enabling this setting ensures that snapshots inherit the tags of their parent database instances\.

### Remediation<a name="rds-17-remediation"></a>

**To enable automatic tag copying to snapshots for a DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Select the DB instance to modify\.

1. Choose **Modify**\.

1. Under **Backup**, select **Copy tags to snapshots**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. You can choose either** Apply during the next scheduled maintenance window** or **Apply immediately**\.

## \[RDS\.18\] RDS instances should be deployed in a VPC<a name="fsbp-rds-18"></a>

**Category:** Protect > Secure network configuration > Resources within VPC 

**Severity:** High

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** `rds-deployed-in-vpc` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS instance is deployed on EC2\-VPC\.

VPCs provide a number of network controls to secure access to RDS resources\. These controls include VPC Endpoints, network ACLs, and security groups\. To take advantage of these controls, we recommend that you create your RDS instances on EC2\-VPC\.

### Remediation<a name="rds-18-remediation"></a>

For detailed instructions on how to move RDS instances to VPC, see [Updating the VPC for a DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.html#USER_VPC.VPC2VPC) in the *Amazon RDS User Guide*\.

## \[RDS\.19\] An RDS event notifications subscription should be configured for critical cluster events<a name="fsbp-rds-19"></a>

**Category:** Detect > Detection services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::RDS::EventSubscription`

**AWS Config rule:** `rds-cluster-event-notifications-configured` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS event subscription exists that has notifications enabled for the following source type, event category key\-value pairs\.

```
DBCluster: ["maintenance","failure"]
```

RDS event notifications uses Amazon SNS to make you aware of changes in the availability or configuration of your RDS resources\. These notifications allow for rapid response\. For additional information about RDS event notifications, see [Using Amazon RDS event notification](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-19-remediation"></a>

**To subscribe to RDS cluster event notifications**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Event subscriptions**\.

1. Under **Event subscriptions**, choose **Create event subscription**\.

1. In the **Create event subscription** dialog, do the following: 

   1. For **Name**, enter a name for the event notification subscription\. 

   1. For **Send notifications to**, choose an existing Amazon SNS ARN for an SNS topic\. To use a new topic, choose **create topic** to enter the name of a topic and a list of recipients\. 

   1. For **Source type**, choose **Clusters**\.

   1. Under **Instances to include**, select **All clusters**\.

   1. Under **Event categories to include**, select **Specific event categories**\. The control also passes if you select **All event categories**\.

   1. Select **maintenance** and **failure**\.

   1. Choose **Create**\.

## \[RDS\.20\] An RDS event notifications subscription should be configured for critical database instance events<a name="fsbp-rds-20"></a>

**Category:** Detect > Detection services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::RDS::EventSubscription`

**AWS Config rule:** `rds-instance-event-notifications-configured` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS event subscription exists with notifications enabled for the following source type, event category key\-value pairs\.

```
DBInstance: ["maintenance","configuration change","failure"]
```

RDS event notifications use Amazon SNS to make you aware of changes in the availability or configuration of your RDS resources\. These notifications allow for rapid response\. For additional information about RDS event notifications, see [Using Amazon RDS event notification](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-20-remediation"></a>

**To subscribe to RDS instance event notifications**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Event subscriptions**\. 

1. Under **Event subscriptions**, choose **Create event subscription**\.

1. In the **Create event subscription** dialog, do the following: 

   1. For **Name**, enter a name for the event notification subscription\. 

   1. For **Send notifications to**, choose an existing Amazon SNS ARN for an SNS topic\. To use a new topic, choose **create topic** to enter the name of a topic and a list of recipients\. 

   1. For **Source type**, choose **Instances**\.

   1. Under **Instances to include**, select **All instances**\.

   1. Under **Event categories to include**, select **Specific event categories**\. The control also passes if you select **All event categories**\.

   1. Select **maintenance**, **configuration change**, and **failure**\.

   1. Choose **Create**\.

## \[RDS\.21\] An RDS event notifications subscription should be configured for critical database parameter group events<a name="fsbp-rds-21"></a>

**Category:** Detect > Detection services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::RDS::EventSubscription`

**AWS Config rule:** `rds-pg-event-notifications-configured` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS event subscription exists with notifications enabled for the following source type, event category key\-value pairs\.

```
DBParameterGroup: ["configuration change"]
```

RDS event notifications use Amazon SNS to make you aware of changes in the availability or configuration of your RDS resources\. These notifications allow for rapid response\. For additional information about RDS event notifications, see [Using Amazon RDS event notification](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-21-remediation"></a>

**To subscribe to RDS database parameter group event notifications**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Event subscriptions**\. 

1. Under **Event subscriptions**, choose **Create event subscription**\.

1. In the **Create event subscription** dialog, do the following: 

   1. For **Name**, enter a name for the event notification subscription\. 

   1. For **Send notifications to**, choose an existing Amazon SNS ARN for an SNS topic\. To use a new topic, choose **create topic** to enter the name of a topic and a list of recipients\. 

   1. For **Source type**, choose **Parameter groups**\.

   1. Under **Instances to include**, select **All parameter groups**\.

   1. Under **Event categories to include**, select **Specific event categories**\. The control also passes if you select **All event categories**\.

   1. Select **configuration change**\.

   1. Choose **Create**\.

## \[RDS\.22\] An RDS event notifications subscription should be configured for critical database security group events<a name="fsbp-rds-22"></a>

**Category:** Detect > Detection Services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::RDS::EventSubscription`

**AWS Config rule:** `rds-sg-event-notifications-configured` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS event subscription exists with notifications enabled for the following source type, event category key\-value pairs\.

```
DBSecurityGroup: ["configuration change","failure"]
```

RDS event notifications use Amazon SNS to make you aware of changes in the availability or configuration of your RDS resources\. These notifications allow for a rapid response\. For additional information about RDS event notifications, see [Using Amazon RDS event notification](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-22-remediation"></a>

**To subscribe to RDS database security group event notifications**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the navigation pane, choose **Event subscriptions**\. 

1. Under **Event subscriptions**, choose **Create event subscription**\.

1. In the **Create event subscription** dialog, do the following: 

   1. For **Name**, enter a name for the event notification subscription\. 

   1. For **Send notifications to**, choose an existing Amazon SNS ARN for an SNS topic\. To use a new topic, choose** create topic** to enter the name of a topic and a list of recipients\. 

   1. For **Source type**, choose **Security groups**\.

   1. Under **Instances to include**, select **All security groups**\.

   1. Under **Event categories to include**, select **Specific event categories**\. The control also passes if you select **All event categories**\.

   1. Select **configuration change** and **failure**\.

   1. Choose **Create**\.

## \[RDS\.23\] RDS databases and clusters should not use a database engine default port<a name="fsbp-rds-23"></a>

**Category:** Protect > Secure network configuration

**Severity:** Low

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** `rds-no-default-ports` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the RDS cluster or instance uses a port other than the default port of the database engine\.

If you use a known port to deploy an RDS cluster or instance, an attacker can guess information about the cluster or instance\. The attacker can use this information in conjunction with other information to connect to an RDS cluster or instance or gain additional information about your application\.

When you change the port, you must also update the existing connection strings that were used to connect to the old port\. You should also check the security group of the DB instance to ensure that it includes an ingress rule that allows connectivity on the new port\.

### Remediation<a name="rds-23-remediation"></a>

**To modify the default port of an existing DB instance**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Databases**\.

1. Select the DB instance to modify

1. Choose **Modify**\.

1. Under **Database options**, change **Database port** to a non\-default value\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. You can choose either **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. For clusters, choose **Modify cluster**\. For instances, choose **Modify DB Instance**\.

## \[RDS\.24\] RDS database clusters should use a custom administrator username<a name="fsbp-rds-24"></a>

**Category:** Identify > Resource Configuration

**Severity:** Medium

**Resource type:** `AWS::RDS:DBCluster`

**AWS Config rule:** `[rds\-cluster\-default\-admin\-check](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-default-admin-check.html)`

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon RDS database cluster has changed the admin username from its default value\. The control does not apply to engines of the type neptune \(Neptune DB\) or docdb \(DocumentDB\)\. This rule will fail if the admin username is set to the default value\.

When creating an Amazon RDS database, you should change the default admin username to a unique value\. Default usernames are public knowledge and should be changed during RDS database creation\. Changing the default usernames reduces the risk of unintended access\.

### Remediation<a name="rds-24-remediation"></a>

For changing the admin username associated with the Amazon RDS database cluster, [create a new RDS database cluster](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.CreateInstance.html) and change the default admin username while creating the database\.

## \[RDS\.25\] RDS database instances should use a custom administrator username<a name="fsbp-rds-25"></a>

**Category:** Identify > Resource Configuration

**Severity:** Medium

**Resource type:** `AWS::RDS::DBInstance`

**AWS Config rule:** `[rds\-instance\-default\-admin\-check](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-default-admin-check.html)`

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether you’ve changed the administrative username for Amazon Relational Database Service \(Amazon RDS\) database instances from the default value\. The control does not apply to engines of the type neptune \(Neptune DB\) or docdb \(DocumentDB\)\. The control fails if the administrative username is set to the default value\.

Default administrative usernames on Amazon RDS databases are public knowledge\. When creating an Amazon RDS database, you should change the default administrative username to a unique value to reduce the risk of unintended access\.

### Remediation<a name="rds-25-remediation"></a>

To change the administrative username associated with an RDS database instance, first [create a new RDS database instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateDBInstance.html)\. Change the default administrative username while creating the database\.

## \[Redshift\.1\] Amazon Redshift clusters should prohibit public access<a name="fsbp-redshift-1"></a>

**Category:** Protect > Secure network configuration > Resources not publicly accessible

**Severity:** Critical

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-public-access-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-public-access-check.html)

**Schedule type:** Change triggered

**Parameters:** None 

This control checks whether Amazon Redshift clusters are publicly accessible\. It evaluates the `PubliclyAccessible` field in the cluster configuration item\. 

The `PubliclyAccessible` attribute of the Amazon Redshift cluster configuration indicates whether the cluster is publicly accessible\. When the cluster is configured with `PubliclyAccessible` set to `true`, it is an Internet\-facing instance that has a publicly resolvable DNS name, which resolves to a public IP address\.

When the cluster is not publicly accessible, it is an internal instance with a DNS name that resolves to a private IP address\. Unless you intend for your cluster to be publicly accessible, the cluster should not be configured with `PubliclyAccessible` set to `true`\.

### Remediation<a name="redshift-1-remediation"></a>

To remediate this issue, update your Amazon Redshift cluster to disable public access\.

**To disable public access to an Amazon Redshift cluster**

1. Open the Amazon Redshift console at [https://console\.aws\.amazon\.com/redshift/](https://console.aws.amazon.com/redshift/)\.

1. In the navigation menu, choose **Clusters**, then choose the name of the cluster with the security group to modify\.

1. Choose **Actions**, then choose **Modify publicly accessible setting**\.

1. Under **Allow instances and devices outside the VPC to connect to your database through the cluster endpoint**, choose **No**\.

1. Choose **Confirm**\.

## \[Redshift\.2\] Connections to Amazon Redshift clusters should be encrypted in transit<a name="fsbp-redshift-2"></a>

**Category:** Protect > Data protection > Encryption of data in transit 

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`, `AWS::Redshift::ClusterParameterGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-require-tls-ssl.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-require-tls-ssl.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether connections to Amazon Redshift clusters are required to use encryption in transit\. The check fails if the Amazon Redshift cluster parameter `require_SSL` is not set to 1\.

TLS can be used to help prevent potential attackers from using person\-in\-the\-middle or similar attacks to eavesdrop on or manipulate network traffic\. Only encrypted connections over TLS should be allowed\. Encrypting data in transit can affect performance\. You should test your application with this feature to understand the performance profile and the impact of TLS\. 

**Note**  
This control is not supported in Europe \(Milan\)\.

### Remediation<a name="redshift-2-remediation"></a>

To remediate this issue, update the parameter group to require encryption\.

**To modify a parameter group**

1. Open the Amazon Redshift console at [https://console\.aws\.amazon\.com/redshift/](https://console.aws.amazon.com/redshift/)\.

1. In the navigation menu, choose **Config**, then choose **Workload management** to display the **Workload management** page\. 

1. Choose the parameter group that you want to modify\. 

1. Choose **Parameters**\.

1. Choose **Edit parameters** then set `require_ssl` to 1\.

1. Enter your changes and then choose **Save**\.

## \[Redshift\.3\] Amazon Redshift clusters should have automatic snapshots enabled<a name="fsbp-redshift-3"></a>

**Category:** Recover > Resilience > Backups enabled 

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-backup-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-backup-enabled.html)

**Schedule type:** Change triggered

**Parameters:**
+ `MinRetentionPeriod = 7`

This control checks whether Amazon Redshift clusters have automated snapshots enabled\. It also checks whether the snapshot retention period is greater than or equal to seven\.

Backups help you to recover more quickly from a security incident\. They strengthen the resilience of your systems\. Amazon Redshift takes periodic snapshots by default\. This control checks whether automatic snapshots are enabled and retained for at least seven days\. For more details on Amazon Redshift automated snapshots, see [Automated snapshots](https://docs.aws.amazon.com/redshift/latest/mgmt/working-with-snapshots.html#about-automated-snapshots) in the *Amazon Redshift Management Guide*\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
Asia Pacific \(Sydney\)
China \(Ningxia\)
Europe \(Milan\)

### Remediation<a name="redshift-3-remediation"></a>

To remediate this issue, update the snapshot retention period to at least 7\.

**To modify the snapshot retention period**

1. Open the Amazon Redshift console at [https://console\.aws\.amazon\.com/redshift/](https://console.aws.amazon.com/redshift/)\.

1. In the navigation menu, choose **Clusters**, then choose the name of the cluster to modify\.

1. Choose **Edit**\.

1. Under **Backup**, set **Snapshot retention** to a value of 7 or greater\.

1. Choose **Modify Cluster**\.

## \[Redshift\.4\] Amazon Redshift clusters should have audit logging enabled<a name="fsbp-redshift-4"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** `redshift-cluster-audit-logging-enabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:**
+ `loggingEnabled = true`

This control checks whether an Amazon Redshift cluster has audit logging enabled\.

Amazon Redshift audit logging provides additional information about connections and user activities in your cluster\. This data can be stored and secured in Amazon S3 and can be helpful in security audits and investigations\. For more information, see [Database audit logging](https://docs.aws.amazon.com/redshift/latest/mgmt/db-auditing.html) in the *Amazon Redshift Management Guide*\.

### Remediation<a name="redshift-4-remediation"></a>

**To enable cluster audit logging**

1. Open the Amazon Redshift console at [https://console\.aws\.amazon\.com/redshift/](https://console.aws.amazon.com/redshift/)\.

1. In the navigation menu, choose **Clusters**, then choose the name of the cluster to modify\.

1. Choose **Maintenance and monitoring**\.

1. Under **Audit logging**, choose **Edit**\.

1. Set **Enable audit logging** to **yes**, then enter the log destination bucket details\.

1. Choose **Confirm**\.

## \[Redshift\.6\] Amazon Redshift should have automatic upgrades to major versions enabled<a name="fsbp-redshift-6"></a>

**Category:** Detect > Vulnerability and patch management

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-maintenancesettings-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-maintenancesettings-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `allowVersionUpgrade = true`

This control checks whether automatic major version upgrades are enabled for the Amazon Redshift cluster\.

Enabling automatic major version upgrades ensures that the latest major version updates to Amazon Redshift clusters are installed during the maintenance window\. These updates might include security patches and bug fixes\. Keeping up to date with patch installation is an important step in securing systems\.

**Note**  
This control is not supported in Middle East \(Bahrain\)\.

### Remediation<a name="redshift-6-remediation"></a>

To remediate this issue from the AWS CLI, use the Amazon Redshift `modify-cluster` command to set the `--allow-version-upgrade` attribute\.

```
aws redshift modify-cluster --cluster-identifier clustername --allow-version-upgrade
```

Where `clustername` is the name of your Amazon Redshift cluster\.

## \[Redshift\.7\] Amazon Redshift clusters should use enhanced VPC routing<a name="fsbp-redshift-7"></a>

**Category:** Protect > Secure network configuration > API private access

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-enhanced-vpc-routing-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-enhanced-vpc-routing-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon Redshift cluster has `EnhancedVpcRouting` enabled\.

Enhanced VPC routing forces all `COPY` and `UNLOAD` traffic between the cluster and data repositories to go through your VPC\. You can then use VPC features such as security groups and network access control lists to secure network traffic\. You can also use VPC Flow Logs to monitor network traffic\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="redshift-7-remediation"></a>

For detailed remediation instructions, see [Enabling enhanced VPC routing](https://docs.aws.amazon.com/redshift/latest/mgmt/enhanced-vpc-enabling-cluster.html) in the *Amazon Redshift Management Guide*\.

## \[Redshift\.8\] Amazon Redshift clusters should not use the default Admin username<a name="fsbp-redshift-8"></a>

**Category:** Identify > Resource Configuration

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-default-admin-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-default-admin-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon Redshift cluster has changed the admin username from its default value\. This control will fail if the admin username for a Redshift cluster is set to `awsuser`\.

When creating a Redshift cluster, you should change the default admin username to a unique value\. Default usernames are public knowledge and should be changed upon configuration\. Changing the default usernames reduces the risk of unintended access\.

### Remediation<a name="redshift-8-remediation"></a>

You can't change the admin username for your Amazon Redshift cluster after it is created\. To create a new cluster, follow the instructions [here](https://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-prereq.html)\.

## \[Redshift\.9\] Redshift clusters should not use the default database name<a name="fsbp-redshift-9"></a>

**Category:** Identify > Resource Configuration

**Severity:** Medium

**Resource type:** `AWS::Redshift::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-default-db-name-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-default-db-name-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon Redshift cluster has changed the database name from its default value\. The control will fail if the database name for a Redshift cluster is set to `dev`\.

When creating a Redshift cluster, you should change the default database name to a unique value\. Default names are public knowledge and should be changed upon configuration\. As an example, a well\-known name could lead to inadvertent access if it was used in IAM policy conditions\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="redshift-9-remediation"></a>

You can't change the database name for your Amazon Redshift cluster after it is created\. For instructions on creating a new cluster, see [Getting started with Amazon Redshift](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html) in the * Amazon Redshift Getting Started Guide*\.

## \[S3\.1\] S3 Block Public Access setting should be enabled<a name="fsbp-s3-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** AWS account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks-periodic.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks-periodic.html) 

**Schedule type:** Periodic

**Parameters:** 
+ `ignorePublicAcls`: `true`
+ `blockPublicPolicy`: `true`
+ `blockPublicAcls`: `true`
+ `restrictPublicBuckets`: `true`

This control checks whether the following Amazon S3 public access block settings are configured at the account level:
+ `ignorePublicAcls`: `true`
+ `blockPublicPolicy`: `true`
+ `blockPublicAcls`: `true`
+ `restrictPublicBuckets`: `true`

The control passes if all of the public access block settings are set to `true`\.

The control fails if any of the settings are set to `false`, or if any of the settings are not configured\.

Amazon S3 public access block is designed to provide controls across an entire AWS account or at the individual S3 bucket level to ensure that objects never have public access\. Public access is granted to buckets and objects through access control lists \(ACLs\), bucket policies, or both\.

Unless you intend to have your S3 buckets be publicly accessible, you should configure the account level Amazon S3 Block Public Access feature\.

To learn more, see [Using Amazon S3 Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service User Guide*\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-1-remediation"></a>

To remediate this issue, enable Amazon S3 Block Public Access\.

**To enable Amazon S3 Block Public Access**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Block public access \(account settings\)**\.

1. Choose **Edit**\.

1. Select **Block *all* public access**\.

1. Choose **Save changes**\.

For more information, see [Using Amazon S3 block public access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service User Guide*\.

## \[S3\.2\] S3 buckets should prohibit public read access<a name="fsbp-s3-2"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited)

**Schedule type:** Periodic and change triggered

**Parameters:** None

This control checks whether your S3 buckets allow public read access\. It evaluates the Block Public Access settings, the bucket policy, and the bucket access control list \(ACL\)\.

Some use cases require that everyone on the internet be able to read from your S3 bucket\. However, those situations are rare\. To ensure the integrity and security of your data, your S3 bucket should not be publicly readable\.

### Remediation<a name="s3-2-remediation"></a>

To remediate this issue, update your S3 bucket to remove public access\.

**To remove public access from an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the left navigation pane, choose **Buckets**\.

1. Choose the name of the S3 bucket to update\.

1. Choose **Permissions** and then choose **Block public access**\. 

1. Choose **Edit**\.

1. Select **Block *all* public access**\. Then choose **Save**\.

1. If prompted, enter **confirm** and then choose **Confirm**\.

## \[S3\.3\] S3 buckets should prohibit public write access<a name="fsbp-s3-3"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html) 

**Schedule type:** Periodic and change triggered

**Parameters:** None

This control checks whether your S3 buckets allow public write access\. It evaluates the block public access settings, the bucket policy, and the bucket access control list \(ACL\)\.

Some use cases require that everyone on the internet be able to write to your S3 bucket\. However, those situations are rare\. To ensure the integrity and security of your data, your S3 bucket should not be publicly writable\.

### Remediation<a name="s3-3-remediation"></a>

To remediate this issue, update your S3 bucket to remove public access\.

**To remove public access for an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the left navigation pane, choose **Buckets**\.

1. Choose the name of the S3 bucket to update\.

1. Choose **Permissions** and then choose **Block public access**\.

1. Choose **Edit**\.

1. Select **Block *all* public access**\. Then choose **Save**\.

1. If prompted, enter **confirm** and then choose **Confirm**\.

## \[S3\.4\] S3 buckets should have server\-side encryption enabled<a name="fsbp-s3-4"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks that your S3 bucket either has Amazon S3 default encryption enabled or that the S3 bucket policy explicitly denies put\-object requests without server\-side encryption\.

For an added layer of security for your sensitive data in S3 buckets, you should configure your buckets with server\-side encryption to protect your data at rest\. Amazon S3 encrypts each object with a unique key\. As an additional safeguard, Amazon S3 encrypts the key itself with a root key that it rotates regularly\. Amazon S3 server\-side encryption uses one of the strongest block ciphers available to encrypt your data, 256\-bit Advanced Encryption Standard \(AES\-256\)\.

To learn more, see [Protecting data using server\-side encryption with Amazon S3\-managed encryption keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html) in the *Amazon Simple Storage Service User Guide*\.

### Remediation<a name="s3-4-remediation"></a>

To remediate this issue, update your S3 bucket to enable default encryption\.

**To enable default encryption on an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the left navigation pane, choose **Buckets**\.

1. Choose the S3 bucket from the list\.

1. Choose **Properties**\.

1. Choose **Default encryption**\.

1. For the encryption, choose either **AES\-256** or **AWS\-KMS**\.
   + Choose **AES\-256** to use keys that are managed by Amazon S3 for default encryption\. For more information about using Amazon S3 server\-side encryption to encrypt your data, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)\.
   + Choose **AWS\-KMS** to use keys that are managed by AWS KMS for default encryption\. Then choose a root key from the list of the AWS KMS root keys that you have created\.

     Type the Amazon Resource Name \(ARN\) of the AWS KMS key to use\. You can find the ARN for your AWS KMS key in the IAM console, under **Encryption keys**\. Or, you can choose a key name from the drop\-down list\.
**Important**  
If you use the AWS KMS option for your default encryption configuration, you are subject to the RPS \(requests per second\) quotas of AWS KMS\. For more information about AWS KMS quotas and how to request a quota increase, see the [https://docs.aws.amazon.com/kms/latest/developerguide/limits.html](https://docs.aws.amazon.com/kms/latest/developerguide/limits.html)\.

     For more information about creating an AWS KMS key, see the [https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html)\.

     For more information about using AWS KMS with Amazon S3, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html)\.

   When enabling default encryption, you might need to update your bucket policy\. For more information about moving from bucket policies to default encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy)\.

1. Choose **Save**\.

For more information about default S3 bucket encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html)\.

## \[S3\.5\] S3 buckets should require requests to use Secure Socket Layer<a name="fsbp-s3-5"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-ssl-requests-only.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-ssl-requests-only.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether S3 buckets have policies that require requests to use Secure Socket Layer \(SSL\)\. 

S3 buckets should have policies that require all requests \(`Action: S3:*`\) to only accept transmission of data over HTTPS in the S3 resource policy, indicated by the condition key `aws:SecureTransport`\.

### Remediation<a name="s3-5-remediation"></a>

To remediate this issue, update the permissions policy of the S3 bucket\.

**To configure an S3 bucket to deny nonsecure transport**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Navigate to the noncompliant bucket, then choose the bucket name\.

1. Choose **Permissions**, and then choose **Bucket Policy**\.

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

## \[S3\.6\] Amazon S3 permissions granted to other AWS accounts in bucket policies should be restricted<a name="fsbp-s3-6"></a>

**Category:** Protect > Secure access management > Sensitive API operations actions restricted 

**Severity:** High

**Resource type:** `AWS::S3::Bucket`

**AWS Config** rule: [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-blacklisted-actions-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-blacklisted-actions-prohibited.html)

**Schedule type:** Change triggered

**Parameters:**
+ `blacklistedactionpatterns`: `s3:DeleteBucketPolicy, s3:PutBucketAcl, s3:PutBucketPolicy, s3:PutEncryptionConfiguration, s3:PutObjectAcl`

This control checks whether the S3 bucket policy prevents principals from other AWS accounts from performing denied actions on resources in the S3 bucket\. The control fails if the S3 bucket policy allows any of the following actions for a principal in another AWS account:
+ `s3:DeleteBucketPolicy`
+ `s3:PutBucketAcl`
+ `s3:PutBucketPolicy`
+ `s3:PutEncryptionConfiguration`
+ `s3:PutObjectAcl`

Implementing least privilege access is fundamental to reducing security risk and the impact of errors or malicious intent\. If an S3 bucket policy allows access from external accounts, it could result in data exfiltration by an insider threat or an attacker\.

The `blacklistedactionpatterns` parameter allows for successful evaluation of the rule for S3 buckets\. The parameter grants access to external accounts for action patterns that are not included in the `blacklistedactionpatterns` list\.

### Remediation<a name="s3-6-remediation"></a>

To remediate this issue, edit the S3 bucket policy to remove the permissions\.

**To edit an S3 bucket policy**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the **Bucket name** list, choose the name of the S3 bucket for which you want to edit the policy\. 

1. Choose **Permissions**, and then choose **Bucket Policy**\.

1. In the **Bucket policy editor** text box, do one of the following:
   + Remove the statements that grant access to denied actions to other AWS accounts
   + Remove the permitted denied actions from the statements

1. Choose **Save**\.

## \[S3\.8\] S3 Block Public Access setting should be enabled at the bucket level<a name="fsbp-s3-8"></a>

**Category:** Protect > Secure access management > Access control

**Severity:** High

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-level-public-access-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-level-public-access-prohibited.html)

**Schedule type:** Change triggered

**Parameters:**
+ `excludedPublicBuckets` \(Optional\) – A comma\-separated list of known allowed public S3 bucket names\.

This control checks whether S3 buckets have bucket\-level public access blocks applied\. This control fails is if any of the following settings are set to `false`:
+ `ignorePublicAcls`
+ `blockPublicPolicy`
+ `blockPublicAcls`
+ `restrictPublicBuckets`

Block Public Access at the S3 bucket level provides controls to ensure that objects never have public access\. Public access is granted to buckets and objects through access control lists \(ACLs\), bucket policies, or both\.

Unless you intend to have your S3 buckets publicly accessible, you should configure the bucket level Amazon S3 Block Public Access feature\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-8-remediation"></a>

For information on how to remove public access at a bucket level, see [Blocking public access to your Amazon S3 storage](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon S3 User Guide*\.

## \[S3\.9\] S3 bucket server access logging should be enabled<a name="fsbp-s3-9"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-logging-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether server access logging is enabled for S3 buckets\. When logging is enabled, Amazon S3 delivers access logs for a source bucket to a chosen target bucket\. The target bucket must be in the same AWS Region as the source bucket and must not have a default retention period configuration\. This control passes if server access logging is enabled\. The target logging bucket does not need to have server access logging enabled, and you should suppress findings for this bucket\. 

Server access logging provides detailed records of requests made to a bucket\. Server access logs can assist in security and access audits\. For more information, see [Security Best Practices for Amazon S3: Enable Amazon S3 server access logging](https://docs.aws.amazon.com/AmazonS3/latest/dev/security-best-practices.html)\.

### Remediation<a name="s3-9-remediation"></a>

**To enable S3 bucket access logging**

1. Sign in to the AWS Management Console and open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Select the bucket from the list\.

1. Choose **Properties**\.

1. Under **Server access logging**, choose **Edit**\.

1. Under **Server access logging**, choose **Enable**\. Then, choose **Save changes**\. 

## \[S3\.10\] S3 buckets with versioning enabled should have lifecycle policies configured<a name="fsbp-s3-10"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-version-lifecycle-policy-check.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-version-lifecycle-policy-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon Simple Storage Service \(Amazon S3\) version enabled buckets have lifecycle policy configured\. This rule fails if Amazon S3 lifecycle policy is not enabled\.

It is recommended to configure lifecycle rules on your Amazon S3 bucket as these rules help you define actions that you want Amazon S3 to take during an object's lifetime\. 

### Remediation<a name="s3-10-remediation"></a>

For more information on configuring lifecycle on an Amazon S3 bucket, see [Setting lifecycle configuration on a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-set-lifecycle-configuration-intro.html) and [Managing your storage lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html)\.

## \[S3\.11\] S3 buckets should have event notifications enabled<a name="fsbp-s3-11"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-event-notifications-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-event-notifications-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether S3 Event Notifications are enabled on an Amazon S3 bucket\. This control fails if S3 Event Notifications are not enabled on a bucket\.

By enabling Event Notifications, you receive alerts on your Amazon S3 buckets when specific events occur\. For example, you can be notified of object creation, object removal, and object restoration\. These notifications can alert relevant teams to accidental or intentional modifications that may lead to unauthorized data access\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-11-remediation"></a>

For information about detecting changes to S3 buckets and objects, see [Amazon S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/NotificationHowTo.html) in the *Amazon S3 User Guide*\.

## \[S3\.12\] S3 access control lists \(ACLs\) should not be used to manage user access to buckets<a name="fsbp-s3-12"></a>

**Category:** Protect > Secure access management > Access control

**Severity:** Medium

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-acl-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-acl-prohibited.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon S3 buckets provide user permissions via ACLs\. The control fails if ACLs are configured for managing user access on S3 buckets\.

ACLs are legacy access control mechanisms that predate IAM\. Instead of ACLs, we recommend using IAM policies or S3 bucket policies to more easily manage access to your S3 buckets\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-12-remediation"></a>

For more information on managing access to S3 buckets, see [Bucket policies and user policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-iam-policies.html)in the *Amazon S3 User Guide*\. For details on how to review your current ACL permissions, see [Access control list \(ACL\) overview](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html) in the *Amazon S3 User Guide*\.

## \[S3\.13\] S3 buckets should have lifecycle policies configured<a name="fsbp-s3-13"></a>

**Category:** Protect > Data protection 

**Severity:** Low

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-lifecycle-policy-check.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-lifecycle-policy-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if a lifecycle policy is configured for an Amazon S3 bucket\. This control fails if a lifecycle policy is not configured for an S3 bucket\.

Configuring lifecycle rules on your S3 bucket defines actions that you want S3 to take during an object's lifetime\. For example, you can transition objects to another storage class, archive them, or delete them after a specified period of time\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="s3-13-remediation"></a>

For information about configuring lifecycle policies on an Amazon S3 bucket, see [Setting lifecycle configuration on a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-set-lifecycle-configuration-intro.html) and see [Managing your storage lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html)in the *Amazon S3 User Guide*\.

## \[SageMaker\.1\] SageMaker notebook instances should not have direct internet access<a name="fsbp-sagemaker-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::SageMaker::NotebookInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/sagemaker-notebook-no-direct-internet-access.html](https://docs.aws.amazon.com/config/latest/developerguide/sagemaker-notebook-no-direct-internet-access.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether direct internet access is disabled for an SageMaker notebook instance\. To do this, it checks whether the `DirectInternetAccess` field is disabled for the notebook instance\. 

If you configure your SageMaker instance without a VPC, then by default direct internet access is enabled on your instance\. You should configure your instance with a VPC and change the default setting to **Disable — Access the internet through a VPC**\.

To train or host models from a notebook, you need internet access\. To enable internet access, make sure that your VPC has a NAT gateway and your security group allows outbound connections\. To learn more about how to connect a notebook instance to resources in a VPC, see [Connect a notebook instance to resources in a VPC](https://docs.aws.amazon.com/sagemaker/latest/dg/appendix-notebook-and-internet-access.html) in the *Amazon SageMaker Developer Guide*\.

You should also ensure that access to your SageMaker configuration is limited to only authorized users\. Restrict users' IAM permissions to modify SageMaker settings and resources\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
 AWS GovCloud \(US\-East\)

### Remediation<a name="sagemaker-1-remediation"></a>

Note that you cannot change the internet access setting after a notebook instance is created\. It must be stopped, deleted, and recreated\.

**To configure an SageMaker notebook instance to deny direct internet access**

1. Open the SageMaker console at [https://console.aws.amazon.com/sagemaker/](https://console.aws.amazon.com/sagemaker/)

1. Navigate to **Notebook instances**\.

1. Delete the instance that has direct internet access enabled\. Choose the instance, choose **Actions**, then choose stop\.

   After the instance is stopped, choose **Actions**, then choose **delete**\.

1. Choose **Create notebook instance**\. Provide the configuration details\.

1. Expand the network section, then choose a VPC, subnet, and security group\. Under **Direct internet access**, choose **Disable — Access the internet through a VPC**\.

1. Choose **Create notebook instance**\.

For more information, see [Connect a notebook instance to resources in a VPC](https://docs.aws.amazon.com/sagemaker/latest/dg/appendix-notebook-and-internet-access.html) in the *Amazon SageMaker Developer Guide*\.

## \[SecretsManager\.1\] Secrets Manager secrets should have automatic rotation enabled<a name="fsbp-secretsmanager-1"></a>

**Category:** Protect > Secure development

**Severity:** Medium

**Resource type:** `AWS::SecretsManager::Secret`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-rotation-enabled-check.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-rotation-enabled-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a secret stored in AWS Secrets Manager is configured with automatic rotation\.

Secrets Manager helps you improve the security posture of your organization\. Secrets include database credentials, passwords, and third\-party API keys\. You can use Secrets Manager to store secrets centrally, encrypt secrets automatically, control access to secrets, and rotate secrets safely and automatically\.

Secrets Manager can rotate secrets\. You can use rotation to replace long\-term secrets with short\-term ones\. Rotating your secrets limits how long an unauthorized user can use a compromised secret\. For this reason, you should rotate your secrets frequently\. To learn more about rotation, see [Rotating your AWS Secrets Manager secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html) in the *AWS Secrets Manager User Guide*\.

**Note**  
This control is not supported in Asia Pacific \(Jakarta\) or Asia Pacific \(Osaka\)\.

### Remediation<a name="secretsmanager-1-remediation"></a>

To remediate this issue, you enable automatic rotation for your secrets\.

**To enable automatic rotation for secrets**

1. Open the Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

1. To find the secret that requires rotating, enter the secret name in the search field\. 

1. Choose the secret you want to rotate, which displays the secrets details page\. 

1. Under **Rotation configuration**, choose **Edit rotation**\.

1. From **Edit rotation configuration**, choose **Enable automatic rotation**\.

1. For **Select Rotation Interval**, choose a rotation interval\.

1. Choose a Lambda function for rotation\. For information about customizing your Lambda rotation function, see [Understanding and customizing your Lambda rotation function](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets-lambda-function-customizing.html) in the *AWS Secrets Manager User Guide*\.

1. To configure the secret for rotation, choose **Next**\.

To learn more about Secrets Manager rotation, see [Rotating your AWS Secrets Manager secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html) in the *AWS Secrets Manager User Guide*\.

## \[SecretsManager\.2\] Secrets Manager secrets configured with automatic rotation should rotate successfully<a name="fsbp-secretsmanager-2"></a>

**Category:** Protect > Secure development

**Severity:** Medium

**Resource type:** `AWS::SecretsManager::Secret`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-scheduled-rotation-success-check.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-scheduled-rotation-success-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS Secrets Manager secret rotated successfully based on the rotation schedule\. The control fails if `RotationOccurringAsScheduled` is `false`\. The control does not evaluate secrets that do not have rotation configured\.

Secrets Manager helps you improve the security posture of your organization\. Secrets include database credentials, passwords, and third\-party API keys\. You can use Secrets Manager to store secrets centrally, encrypt secrets automatically, control access to secrets, and rotate secrets safely and automatically\.

Secrets Manager can rotate secrets\. You can use rotation to replace long\-term secrets with short\-term ones\. Rotating your secrets limits how long an unauthorized user can use a compromised secret\. For this reason, you should rotate your secrets frequently\.

In addition to configuring secrets to rotate automatically, you should ensure that those secrets rotate successfully based on the rotation schedule\.

To learn more about rotation, see [Rotating your AWS Secrets Manager secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html) in the *AWS Secrets Manager User Guide*\.

### Remediation<a name="secretsmanager-2-remediation"></a>

If the automatic rotation fails, then Secrets Manager might have encountered errors with the configuration\. 

To rotate secrets in Secrets Manager, you use a Lambda function that defines how to interact with the database or service that owns the secret\. 

For help on how to diagnose and fix common errors related to secrets rotation, see [Troubleshooting AWS Secrets Manager rotation of secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/troubleshoot_rotation.html) in the *AWS Secrets Manager User Guide*\.

## \[SecretsManager\.3\] Remove unused Secrets Manager secrets<a name="fsbp-secretsmanager-3"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::SecretsManager::Secret`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-unused.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-unused.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether your secrets have been accessed within a specified number of days\. The default value is 90 days\. If a secret was not accessed within the defined number of days, this control fails\.

Deleting unused secrets is as important as rotating secrets\. Unused secrets can be abused by their former users, who no longer need access to these secrets\. Also, as more users get access to a secret, someone might have mishandled and leaked it to an unauthorized entity, which increases the risk of abuse\. Deleting unused secrets helps revoke secret access from users who no longer need it\. It also helps to reduce the cost of using Secrets Manager\. Therefore, it is essential to routinely delete unused secrets\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="secretsmanager-3-remediation"></a>

You can delete inactive secrets from the Secrets Manager console\.

**To delete inactive secrets**

1. Open the Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

1. To locate the secret, enter the secret name in the search box\.

1. Choose the secret to delete\. 

1. Under **Secret details**, from **Actions**, choose **Delete secret**\.

1. Under **Schedule secret deletion**, enter the number of days to wait before the secret is deleted\.

1. Choose **Schedule deletion**\.

## \[SecretsManager\.4\] Secrets Manager secrets should be rotated within a specified number of days<a name="fsbp-secretsmanager-4"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource type:** `AWS::SecretsManager::Secret`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-periodic-rotation.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-periodic-rotation.html)

**Schedule type:** Periodic

**Parameters:**
+ **Rotation period:** 90 days by default

This control checks whether your secrets have been rotated at least once within 90 days\.

Rotating secrets can help you to reduce the risk of an unauthorized use of your secrets in your AWS account\. Examples include database credentials, passwords, third\-party API keys, and even arbitrary text\. If you do not change your secrets for a long period of time, the secrets are more likely to be compromised\.

As more users get access to a secret, it can become more likely that someone mishandled and leaked it to an unauthorized entity\. Secrets can be leaked through logs and cache data\. They can be shared for debugging purposes and not changed or revoked once the debugging completes\. For all these reasons, secrets should be rotated frequently\.

You can configure your secrets for automatic rotation in AWS Secrets Manager\. With automatic rotation, you can replace long\-term secrets with short\-term ones, significantly reducing the risk of compromise\.

Security Hub recommends that you enable rotation for your Secrets Manager secrets\. To learn more about rotation, see [Rotating your AWS Secrets Manager secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html) in the *AWS Secrets Manager User Guide*\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="secretsmanager-4-remediation"></a>

You can enable automatic secret rotation in the Secrets Manager console\.

**To enable secret rotation**

1. Open the Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

1. To locate the secret, enter the secret name in the search box\.

1. Choose the secret to display\.

1. Under **Rotation configuration**, choose **Edit rotation**\.

1. From **Edit rotation configuration**, choose **Enable automatic rotation**\.

1. From **Select Rotation Interval**, choose the rotation interval\.

1. Choose a Lambda function to use for rotation\.

1. Choose **Next**\.

1. After you configure the secret for automatic rotation, under **Rotation Configuration**, choose** Rotate secret immediately**\.

## \[SNS\.1\] SNS topics should be encrypted at rest using AWS KMS<a name="fsbp-sns-1"></a>

**Category:** Protect > Data protection > Encryption of data at rest 

**Severity:** Medium

**Resource type:** `AWS::SNS::Topic`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/sns-encrypted-kms.html](https://docs.aws.amazon.com/config/latest/developerguide/sns-encrypted-kms.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an SNS topic is encrypted at rest using AWS KMS\.

Encrypting data at rest reduces the risk of data stored on disk being accessed by a user not authenticated to AWS\. It also adds another set of access controls to limit the ability of unauthorized users to access the data\. For example, API permissions are required to decrypt the data before it can be read\. SNS topics should be encrypted at\-rest for an added layer of security\. For more information, see [Encryption at rest](https://docs.aws.amazon.com/sns/latest/dg/sns-server-side-encryption.html) in the *Amazon Simple Notification Service Developer Guide*\.

### Remediation<a name="sns-1-remediation"></a>

To remediate this issue, update your SNS topic to enable encryption\.

**To encrypt an unencrypted SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. In the navigation pane, choose **Topics**\.

1. Choose the name of the topic to encrypt\.

1. Choose **Edit**\.

1. Under **Encryption**, choose **Enable Encryption**\.

1. Choose the KMS key to use to encrypt the topic\.

1. Choose **Save changes**\.

## \[SNS\.2\] Logging of delivery status should be enabled for notification messages sent to a topic<a name="fsbp-sns-2"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::SNS::Topic`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/sns-topic-message-delivery-notification-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/sns-topic-message-delivery-notification-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether logging is enabled for the delivery status of notification messages sent to an Amazon SNS topic for the endpoints\. This control fails if the delivery status notification for messages is not enabled\.

Logging is an important part of maintaining the reliability, availability, and performance of services\. Logging message delivery status helps provide operational insights, such as the following:
+ Knowing whether a message was delivered to the Amazon SNS endpoint\.
+ Identifying the response sent from the Amazon SNS endpoint to Amazon SNS\.
+ Determining the message dwell time \(the time between the publish timestamp and the hand off to an Amazon SNS endpoint\)\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="sns-2-remediation"></a>

To configure delivery status logging for a topic, see [Amazon SNS message delivery status](https://docs.aws.amazon.com/sns/latest/dg/sns-topic-attributes.html) in the *Amazon Simple Notification Service Developer Guide*\.

## \[SQS\.1\] Amazon SQS queues should be encrypted at rest<a name="fsbp-sqs-1"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::SQS::Queue`

**AWS Config rule:** `sqs-queue-encrypted` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Amazon SQS queues are encrypted at rest\. The control passes if you use an Amazon SQS managed key \(SSE\-SQS\) or an AWS Key Management Service \(AWS KMS\) key \(SSE\-KMS\)\.

Server\-side encryption \(SSE\) allows you to transmit sensitive data in encrypted queues\. To protect the content of messages in queues, SSE uses KMS keys\. For more information, see [Encryption at rest](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html) in the *Amazon Simple Queue Service Developer Guide*\.

### Remediation<a name="sqs-1-remediation"></a>

For information about managing SSE using the AWS Management Console, see[ Configuring server\-side encryption \(SSE\) for a queue \(console\)](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-configure-sse-existing-queue.html) in the *Amazon Simple Queue Service Developer Guide*\.

## \[SSM\.1\] EC2 instances should be managed by AWS Systems Manager<a name="fsbp-ssm-1"></a>

**Category:** Identify > Inventory

**Severity:** Medium

**Resource type:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-managed-by-systems-manager.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-managed-by-systems-manager.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the stopped and running EC2 instances in your account are managed by AWS Systems Manager\. Systems Manager is an AWS service that you can use to view and control your AWS infrastructure\.

To help you to maintain security and compliance, Systems Manager scans your stopped and running managed instances\. A managed instance is a machine that is configured for use with Systems Manager\. Systems Manager then reports or takes corrective action on any policy violations that it detects\. Systems Manager also helps you to configure and maintain your managed instances\.

To learn more, see [https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)\.

### Remediation<a name="ssm-1-remediation"></a>

You can use the Systems Manager console to remediate this issue\.

**To ensure that EC2 instances are managed by Systems Manager**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation menu, choose **Quick setup**\.

1. Choose **Create**\.

1. Under **Configuration type**, choose **Host Management**, then choose **Next**\.

1. On the configuration screen, you can keep the default options\.

   You can optionally make the following changes:

   1. If you use CloudWatch to monitor EC2 instances, select **Install and configure the CloudWatch agent** and **Update the CloudWatch agent once every 30 days**\.

   1. Under **Targets**, choose the management scope to determine the accounts and Regions where this configuration is applied\.

   1. Under **Instance profile options**, select **Add required IAM policies to existing instance profiles attached to your instances**\.

1. Choose **Create**\.

To determine whether your instances support Systems Manager associations, see [Systems Manager prerequisites](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html) in the *AWS Systems Manager User Guide*\.

## \[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements<a name="fsbp-ssm-2"></a>

**Category:** Detect > Detection services 

**Severity:** High

**Resource type:** `AWS::SSM::PatchCompliance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the compliance status of the Amazon EC2 Systems Manager patch compliance is `COMPLIANT` or `NON_COMPLIANT` after the patch installation on the instance\. It only checks instances that are managed by Systems Manager Patch Manager\.

Having your EC2 instances fully patched as required by your organization reduces the attack surface of your AWS accounts\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(Bahrain\)

### Remediation<a name="ssm-2-remediation"></a>

To remediate this issue, install the required patches on your noncompliant instances\.

**To remediate noncompliant patches**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. Under **Node Management**, choose **Run Command** and then choose **Run command**\.

1. Choose the button next to **AWS\-RunPatchBaseline**\.

1. Change the **Operation** to **Install**\.

1. Choose **Choose instances manually** and then choose the noncompliant instances\.

1. At the bottom of the page, choose **Run**\.

1. After the command is complete, to monitor the new compliance status of your patched instances, in the navigation pane, choose **Compliance**\.

For more information about using Systems Manager documents to patch a managed instance, see[ About SSM documents for patching instances](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-ssm-documents.html) and [Running commands using Systems Manager Run command](https://docs.aws.amazon.com/systems-manager/latest/userguide/run-command.html) in the *AWS Systems Manager User Guide*\.

## \[SSM\.3\] Instances managed by Systems Manager should have an association compliance status of COMPLIANT<a name="fsbp-ssm-3"></a>

**Category:** Detect > Detection services

**Severity:** Low

**Resource type:** `AWS::SSM::AssociationCompliance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-association-compliance-status-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-association-compliance-status-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the status of the AWS Systems Manager association compliance is `COMPLIANT` or `NON_COMPLIANT` after the association is run on an instance\. The control passes if the association compliance status is `COMPLIANT`\.

A State Manager association is a configuration that is assigned to your managed instances\. The configuration defines the state that you want to maintain on your instances\. For example, an association can specify that antivirus software must be installed and running on your instances or that certain ports must be closed\. 

After you create one or more State Manager associations, compliance status information is immediately available to you\. You can view the compliance status in the console or in response to AWS CLI commands or corresponding Systems Manager API actions\. For associations, Configuration Compliance shows the compliance status \(`Compliant` or `Non-compliant`\)\. It also shows the severity level assigned to the association, such as `Critical` or `Medium`\.

To learn more about State Manager association compliance, see [About State Manager association compliance](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-compliance-about.html#sysman-compliance-about-association) in the *AWS Systems Manager User Guide*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="ssm-3-remediation"></a>

A failed association can be related to different things, including targets and SSM document names\. To remediate this issue, you must first identify and investigate the association\. You can then update the association to correct the specific issue\.

You can edit an association to specify a new name, schedule, severity level, or targets\. After you edit an association, AWS Systems Manager creates a new version\.

**To investigate and update a failed association**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation pane, under **Node Management**, choose **Fleet Manager**\.

1. Choose the instance ID that has an **Association status** of **Failed**\.

1. Choose **View details**\.

1. Choose **Associations**\.

1. Note the name of the association that has an **Association status** of **Failed**\. This is the association that you need to investigate\. You need to use the association name in the next step\.

1. In the navigation pane, under **Node Management**, choose **State Manager**\. Search for the association name, then select the association\.

1. After you determine the issue, edit the failed association to correct the problem\. For information on how to edit an association, see [Edit an association](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-state-assoc-edit.html)\.

For more information on creating and editing State Manager associations, see [Working with associations in Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-associations.html) in the *AWS Systems Manager User Guide*\.

## \[SSM\.4\] SSM documents should not be public<a name="fsbp-ssm-4"></a>

**Category:** Protect > Secure network configuration > Resources not publicly accessible

**Severity:** Critical

**Resource type:** `AWS::SSM::Document`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ssm-document-not-public.html](https://docs.aws.amazon.com/config/latest/developerguide/ssm-document-not-public.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether AWS Systems Manager documents that are owned by the account are public\. This control fails if SSM documents with the owner `Self` are public\.

SSM documents that are public might allow unintended access to your documents\. A public SSM document can expose valuable information about your account, resources, and internal processes\.

Unless your use case requires public sharing to be enabled, Security Hub recommends that you turn on the block public sharing setting for your Systems Manager documents that are owned by `Self`\.

**Note**  
This control is not supported in the following Regions:  
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ssm-4-remediation"></a>



For more information about disabling public access to SSM documents, see [Modify permissions for a shared SSM document](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-share-modify.html) and [Best practices for shared SSM documents](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-before-you-share.html) in the *AWS Systems Manager User Guide*\.

## \[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled<a name="fsbp-waf-1"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::WAF::WebACL`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-classic-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-classic-logging-enabled.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether logging is enabled for an AWS WAF global web ACL\. This control fails if logging is not enabled for the web ACL\.

Logging is an important part of maintaining the reliability, availability, and performance of AWS WAF globally\. It is a business and compliance requirement in many organizations, and allows you to troubleshoot application behavior\. It also provides detailed information about the traffic that is analyzed by the web ACL that is attached to AWS WAF\.

**Note**  
This control is not supported in the following Regions:  
US East \(Ohio\)
US West \(N\. California\)
US West \(Oregon\)
Africa \(Cape Town\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Mumbai\)
Asia Pacific \(Osaka\)
Asia Pacific \(Seoul\)
Asia Pacific \(Singapore\)
Asia Pacific \(Sydney\)
Asia Pacific \(Tokyo\)
Canada \(Central\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Frankfurt\)
Europe \(Ireland\)
Europe \(London\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
South America \(São Paulo\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="waf-1-remediation"></a>

You can enable logging for a web ACL from the Kinesis Data Firehose console\.

**To enable logging for a web ACL**

1. Open the Kinesis Data Firehose console at [https://console\.aws\.amazon\.com/firehose/](https://console.aws.amazon.com/firehose/)\.

1. Create a Kinesis Data Firehose delivery stream\.

   The name must start with the prefix `aws-waf-logs`\-\. For example, `aws-waf-logs-us-east-2-analytics`\.

   Create the Kinesis Data Firehose delivery stream with a `PUT` source and in the Region where you operate\. If you capture logs for Amazon CloudFront, create the delivery stream in US East \(N\. Virginia\)\. For more information, see [Creating an Amazon Kinesis Data Firehose delivery stream](https://docs.aws.amazon.com/firehose/latest/dev/basic-create.html) in the *Amazon Kinesis Data Firehose Developer Guide*\.

1. From **Services**, choose **WAF & Shield**\. Then choose **Switch to AWS WAF Classic**\.

1. From **Filter**, choose **Global \(CloudFront\)**\.

1. Choose the web ACL to enable logging for\.

1. Under **Logging**, choose **Enable logging**\.

1. Choose the Kinesis Data Firehose delivery stream that you created earlier\. You must choose a delivery stream that has a name that begins with `aws-waf-logs`\-\.

1. Choose **Enable logging**\.

## \[WAF\.2\] A WAF Regional rule should have at least one condition<a name="fsbp-waf-2"></a>

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAFRegional::Rule`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-rule-not-empty.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-rule-not-empty.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF Regional rule has at least one condition\. The control fails if no conditions are present within a rule\.

A WAF Regional rule can contain multiple conditions\. The rule's conditions allow for traffic inspection and take a defined action \(allow, block, or count\)\. Without any conditions, the traffic passes without inspection\. A WAF Regional rule with no conditions, but with a name or tag suggesting allow, block, or count, could lead to the wrong assumption that one of those actions is occurring\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="waf-2-remediation"></a>

To add a condition to an empty rule, see [Adding and removing conditions in a rule](https://docs.aws.amazon.com/waf/latest/developerguide/classic-web-acl-rules-editing.html) in the *AWS WAF Developer Guide*\.

## \[WAF\.3\] A WAF Regional rule group should have at least one rule<a name="fsbp-waf-3"></a>

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAFRegional::RuleGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-rulegroup-not-empty.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-rulegroup-not-empty.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF Regional rule group has at least one rule\. The control fails if no rules are present within a rule group\.

A WAF Regional rule group can contain multiple rules\. The rule's conditions allow for traffic inspection and take a defined action \(allow, block, or count\)\. Without any rules, the traffic passes without inspection\. A WAF Regional rule group with no rules, but with a name or tag suggesting allow, block, or count, could lead to the wrong assumption that one of those actions is occurring\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="waf-3-remediation"></a>

To add rules and rule conditions to an empty rule group, see [Adding and deleting rules from an AWS WAF Classic rule group](https://docs.aws.amazon.com/waf/latest/developerguide/classic-rule-group-editing.html) and [Adding and removing conditions in a rule](https://docs.aws.amazon.com/waf/latest/developerguide/classic-web-acl-rules-editing.html) in the *AWS WAF Developer Guide*\.

## \[WAF\.4\] A WAF Classic Regional web ACL should have at least one rule or rule group<a name="fsbp-waf-4"></a>

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAFRegional::WebACL`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-webacl-not-empty](https://docs.aws.amazon.com/config/latest/developerguide/waf-regional-webacl-not-empty)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF Classic Regional web ACL contains any WAF rules or WAF rule groups\. This control fails if a web ACL does not contain any WAF rules or rule groups\.

A WAF Regional web ACL can contain a collection of rules and rule groups that inspect and control web requests\. If a web ACL is empty, the web traffic can pass without being detected or acted upon by WAF depending on the default action\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="waf-4-remediation"></a>

**To add rules or rule groups to an empty web ACL**

1. Open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Switch to AWS WAF Classic**, and then choose **Web ACLs**\.

1. For **Filter**, choose the Region where the empty web ACL is located\.

1. Choose the name of the empty web ACL\.

1. Choose **Rules**, and then choose **Edit web ACL**\.

1. For **Rules**, choose a rule or rule group, and then choose **Add rule to web ACL**\.

1. At this point, you can modify the rule order within the web ACL if you are adding multiple rules or rule groups to the web ACL\.

1. Choose **Update**\.

## \[WAF\.6\] A WAF global rule should have at least one condition<a name="fsbp-waf-6"></a>

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAF::Rule`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-global-rule-not-empty.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-global-rule-not-empty.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF global rule contains any conditions\. The control fails if no conditions are present within a rule\.

A WAF global rule can contain multiple conditions\. A rule’s conditions allow for traffic inspection and take a defined action \(allow, block, or count\)\. Without any conditions, the traffic passes without inspection\. A WAF global rule with no conditions, but with a name or tag suggesting allow, block, or count, could lead to the wrong assumption that one of those actions is occurring\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="waf-6-remediation"></a>

For instructions on creating a rule and adding conditions, see [Creating a rule and adding conditions](https://docs.aws.amazon.com/waf/latest/developerguide/classic-web-acl-rules-creating.html) in the *AWS WAF Developer Guide*\.

## \[WAF\.7\] A WAF global rule group should have at least one rule<a name="fsbp-waf-7"></a>

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAF::RuleGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-global-rulegroup-not-empty.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-global-rulegroup-not-empty.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF global rule group has at least one rule\. The control fails if no rules are present within a rule group\.

A WAF global rule group can contain multiple rules\. The rule's conditions allow for traffic inspection and take a defined action \(allow, block, or count\)\. Without any rules, the traffic passes without inspection\. A WAF global rule group with no rules, but with a name or tag suggesting allow, block, or count, could lead to the wrong assumption that one of those actions is occurring\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="waf-7-remediation"></a>

For instructions on adding a rule to a rule group, see [Creating an AWS WAF Classic rule group](https://docs.aws.amazon.com/waf/latest/developerguide/classic-create-rule-group.html) in the *AWS WAF Developer Guide*\.

## \[WAF\.8\] A WAF global web ACL should have at least one rule or rule group<a name="fsbp-waf-8"></a>

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource type:** `AWS::WAF::WebACL`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-global-webacl-not-empty](https://docs.aws.amazon.com/config/latest/developerguide/waf-global-webacl-not-empty)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an AWS WAF global web ACL contains at least one WAF rule or WAF rule group\. The control fails if a web ACL does not contain any WAF rules or rule groups\.

A WAF global web ACL can contain a collection of rules and rule groups that inspect and control web requests\. If a web ACL is empty, the web traffic can pass without being detected or acted upon by WAF depending on the default action\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="waf-8-remediation"></a>

**To add rules or rule groups to an empty web ACL**

1. Open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Switch to AWS WAF Classic**, and then choose **Web ACLs**\.

1. For **Filter**, choose **Global \(CloudFront\)**\.

1. Choose the name of the empty web ACL\.

1. Choose **Rules**, and then choose **Edit web ACL**\.

1. For **Rules**, choose a rule or rule group, and then choose **Add rule to web ACL**\.

1. At this point, you can modify the rule order within the web ACL if you are adding multiple rules or rule groups to the web ACL\.

1. Choose **Update**\.