# AWS Foundational Security Best Practices controls<a name="securityhub-standards-fsbp-controls"></a>

The AWS Foundational Security Best Practices standard contains the following controls\. For each control, the information includes the following information\.
+ The category and subcategory that the control applies to
+ The severity
+ The applicable resource
+ The required AWS Config rule, and any specific parameter values set by AWS Security Hub
+ Remediation steps

Note that gaps in the control numbers indicate controls that are not yet released\.

## \[ACM\.1\] Imported ACM certificates should be renewed after a specified time period<a name="fsbp-acm-1"></a>

**Category:** Protect > Data protection > Encryption of data in transit

**Severity:** Medium

**Resource:** ACM certificate

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/acm-certificate-expiration-check.html](https://docs.aws.amazon.com/config/latest/developerguide/acm-certificate-expiration-check.html)

**Parameters:**
+ `daysToExpiration`: 30

This control checks whether ACM certificates in your account are marked for expiration within 30 days\. It checks both imported certificates and certificates provided by AWS Certificate Manager\.

Certificates provided by ACM are automatically renewed\. If you're using certificates provided by ACM, you do not need to rotate SSL/TLS certificates\. ACM manages certificate renewals for you\.

ACM does not automatically renew certificates that you import\. You must renew imported certificates manually\.

For more information, see [Managed renewal](https://docs.aws.amazon.com/acm/latest/userguide/managed-renewal.html) in the *AWS Certificate Manager User Guide*\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\) 
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)

### Remediation<a name="acm-1-remediation"></a>

ACM provides managed renewal for your Amazon issued SSL/TLS certificates\. This includes both public and private certificates issued by using ACM\. If possible, ACM renews your certificates automatically with no action required from you\. A certificate is eligible for renewal if it is associated with another AWS service, such as Elastic Load Balancing or Amazon CloudFront\. It can also be renewed if it has been exported since being issued or last renewed\.

If ACM cannot automatically validate one or more domain names in a certificate, ACM notifies the domain owner that the domain must be validated manually\. A domain can require manual validation for the following reasons\.
+ ACM cannot establish an HTTPS connection with the domain\.
+ The certificate that is returned in the response to the HTTPS requests does not match the one that ACM is renewing\.

When a certificate is 45 days from expiration and one or more domain names in the certificate requires manual validation, ACM notifies the domain owner:

**By email \(for email\-validated certificates\)**  
If the certificate was last validated by email, ACM sends to the domain owner an email for each domain name that requires manual validation\. To ensure that this email can be received, the domain owner must correctly configure email for each domain\.  
For more information, see [\(Optional\) Configure email for your domain](https://docs.aws.amazon.com/acm/latest/userguide/setup-email.html)\. The email contains a link that performs the validation\. This link expires after 72 hours\. If necessary, you can use the ACM console, AWS CLI, or API to request that ACM resend the domain validation email\. For more information, see [Request a domain validation email for certificate renewal](https://docs.aws.amazon.com/acm/latest/userguide/request-domain-validation-email-for-renewal.html)\.  
Email\-validated certificates are automatically renewed up to 825 days after their last manual validation date\. After 825 days, to proceed with the renewal, the domain owner or an authorized representative must manually revalidate ownership of the domain\. To avoid this issue, Security Hub recommends that you create a new certificate and use DNS validation if possible\. If they are properly configured, DNS\-validated certificates are revalidated indefinitely\.

**By notification in your AWS Personal Health Dashboard**  
ACM sends notifications to your AWS Personal Health Dashboard to notify you that one or more domain names in the certificate require validation before the certificate can be renewed\. ACM sends these notifications when your certificate is 45 days, 30 days, 15 days, 7 days, 3 days, and 1 day from expiration\. These notifications are informational only\.

## \[APIGateway\.1\] API Gateway REST and WebSocket API logging should be enabled<a name="fsbp-apigateway-1"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource:** Stage \(v1\), Stage \(v2\)

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/api-gw-execution-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/api-gw-execution-logging-enabled.html)

**Parameters:** None

This control checks whether all stages of an Amazon API Gateway REST or WebSocket API have logging enabled\. The control fails if logging is not enabled for all methods of a stage or if `loggingLevel` is neither `ERROR` nor `INFO`\.

API Gateway REST or WebSocket API stages should have relevant logs enabled\. API Gateway REST and WebSocket API execution logging provides detailed records of requests made to API Gateway REST and WebSocket API stages\. The stages include API integration backend responses, Lambda authorizer responses, and the `requestId` for AWS integration endpoints\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Europe \(Milan\)

### Remediation<a name="apigateway1-remediation"></a>

To enable logging for REST and WebSocket API operations, see [Set up CloudWatch API logging using the API Gateway console](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-logging.html#set-up-access-logging-using-console) in the *API Gateway Developer Guide*\.

## \[APIGateway\.2\] API Gateway REST API stages should be configured to use SSL certificates for backend authentication<a name="fsbp-apigateway-2"></a>

**Category:** Protect > Data protection

**Severity:** Medium

**Resource type:** Stage \(v1\)

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/api-gw-ssl-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/api-gw-ssl-enabled.html)

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

**Resource type:** Stage \(v1\)

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/api-gw-xray-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/api-gw-xray-enabled.html)

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

**Resource:** `AWS::ApiGateway::Stage`

**AWS Configrule:** [https://docs.aws.amazon.com/config/latest/developerguide/api-gw-associated-with-waf.html](https://docs.aws.amazon.com/config/latest/developerguide/api-gw-associated-with-waf.html)

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
This control is still in the release process\. It might not yet be available in all of the Regions where it is supported\.

### Remediation<a name="apigateway-4-remediation"></a>

For information on how to use the API Gateway console to associate an AWS WAF Regional web ACL with an existing API Gateway API stage, see [Using AWS WAF to protect your APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-control-access-aws-waf.html) in the *API Gateway Developer Guide*\.

## \[AutoScaling\.1\] Auto Scaling groups associated with a load balancer should use load balancer health checks<a name="fsbp-autoscaling-1"></a>

**Category:** Identify > Inventory

**Severity:** Low

**Resource type:** AutoScaling AutoScalingGroup

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-group-elb-healthcheck-required.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-group-elb-healthcheck-required.html)

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

## \[CloudFront\.1\] CloudFront distributions should have a default root object configured<a name="fsbp-cloudfront-1"></a>

**Category:** Protect > Secure access management > Resources not publicly accessible

**Severity:** Critical

**Resource:** Distribution

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-default-root-object-configured.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-default-root-object-configured.html)

**Parameters:** None

This control checks whether an Amazon CloudFront distribution is configured to return a specific object that is the default root object\. The control fails if the CloudFront distribution does not have a default root object configured\.

A user might sometimes request the distribution’s root URL instead of an object in the distribution\. When this happens, specifying a default root object can help you to avoid exposing the contents of your web distribution\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\. It is not supported in the following Regions:  
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

### Remediation<a name="cloudfront-1-remediation"></a>

For detailed instructions on how to specify a default root object for your distribution, see [How to specify a default root object](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/DefaultRootObject.html#DefaultRootObjectHowToDefine) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.2\] CloudFront distributions should have origin access identity enabled<a name="fsbp-cloudfront-2"></a>

**Category:** Protect > Secure access management > Resource policy configuration

**Severity:** Medium

**Resource:** Distribution

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-origin-access-identity-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-origin-access-identity-enabled.html)

**Parameters:** None

This control checks whether an Amazon CloudFront distribution with Amazon S3 Origin type has Origin Access Identity \(OAI\) configured\. The control fails if OAI is not configured\.

CloudFront OAI prevents users from accessing S3 bucket content directly\. When users access an S3 bucket directly, they effectively bypass the CloudFront distribution and any permissions that are applied to the underlying S3 bucket content\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\. It is not supported in the following Regions:  
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

### Remediation<a name="cloudfront-2-remediation"></a>

For detailed remediation instructions, see [Creating a CloudFront OAI and adding it to your distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html#private-content-creating-oai) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.3\] CloudFront distributions should require encryption in transit<a name="fsbp-cloudfront-3"></a>

**Category:** Protect > Data protection > Encryption of data in transit

**Severity:** Medium

**Resource:** Distribution

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-viewer-policy-https.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-viewer-policy-https.html)

**Parameters:** None

This control checks whether an Amazon CloudFront distribution requires viewers to use HTTPS directly or whether it uses redirection\. The control fails if `ViewerProtocolPolicy` is set to `allow-all` for `defaultCacheBehavior` or for `cacheBehaviors`\.

HTTPS \(TLS\) can be used to help prevent potential attackers from using person\-in\-the\-middle or similar attacks to eavesdrop on or manipulate network traffic\. Only encrypted connections over HTTPS \(TLS\) should be allowed\. Encrypting data in transit can affect performance\. You should test your application with this feature to understand the performance profile and the impact of TLS\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\. It is not supported in the following Regions:  
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

### Remediation<a name="cloudfront-3-remediation"></a>

For detailed remediation instructions, see [Requiring HTTPS for communication between viewers and CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-viewers-to-cloudfront.html) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.4\] CloudFront distributions should have origin failover configured<a name="fsbp-cloudfront-4"></a>

**Category:** Recover > Resilience > High availability

**Severity:** Low

**Resource:** Distribution

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-origin-failover-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-origin-failover-enabled.html)

**Parameters:** None

This control checks whether an Amazon CloudFront distribution is configured with an origin group that has two or more origins\.

CloudFront origin failover can increase availability\. Origin failover automatically redirects traffic to a secondary origin if the primary origin is unavailable or if it returns specific HTTP response status codes\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\. It is not supported in the following Regions:  
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

### Remediation<a name="cloudfront-4-remediation"></a>

For detailed remediation instructions, see [Creating an origin group](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html#concept_origin_groups.creating) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.5\] CloudFront distributions should have logging enabled<a name="fsbp-cloudfront-5"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-accesslogs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-accesslogs-enabled.html)

**Parameters:**
+ `S3BucketName` \(Optional\) – The S3 bucket to send the logs to

This control checks whether server access logging is enabled on CloudFront distributions\. The control fails if access logging is not enabled for a distribution\.

CloudFront access logs provide detailed information about every user request that CloudFront receives\. Each log contains information such as the date and time the request was received, the IP address of the viewer that made the request, the source of the request, and the port number of the request from the viewer\.

These logs are useful for applications such as security and access audits and forensics investigation\. For additional guidance on how to analyze access logs, see [Querying Amazon CloudFront logs](https://docs.aws.amazon.com/athena/latest/ug/cloudfront-logs.html) in the *Amazon Athena User Guide*\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\. It is not supported in the following Regions:  
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
This control is still in the release process\. It might not yet be available in all of the Regions where it is supported\.

### Remediation<a name="cloudfront-5-remediation"></a>

For information on how to configure access logging for a CloudFront distribution, see [Configuring and using standard logs \(access logs\)](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/AccessLogs.html) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.6\] CloudFront distributions should have AWS WAF enabled<a name="fsbp-cloudfront-6"></a>

**Category:** Protect > Protective services

**Severity:** Medium

**Resource:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-associated-with-waf.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-associated-with-waf.html)

**Parameters:**
+ `wafWebAclIds` \(Optional\) \- A comma\-separated list of web ACL IDs \(for AWS WAF\) or web ACL ARNs \(for AWS WAFv2\)\.

This control checks whether CloudFront distributions are associated with either AWS WAF or AWS WAFv2 web ACLs\. The control fails if the distribution is not associated with a web ACL\.

AWS WAF is a web application firewall that helps protect web applications and APIs from attacks\. It allows you to configure a set of rules, called a web access control list \(web ACL\), that allow, block, or count web requests based on customizable web security rules and conditions that you define\. Ensure your CloudFront distribution is associated with an AWS WAF web ACL to help protect it from malicious attacks\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\. It is not supported in the following Regions:  
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
This control is still in the release process\. It might not yet be available in all of the Regions where it is supported\.

### Remediation<a name="cloudfront-6-remediation"></a>

For information on how to associate a web ACL with a CloudFront distribution, see [Using AWS WAF to control access to your content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-awswaf.html) in the *Amazon CloudFront Developer Guide*\.

## \[CloudTrail\.1\] CloudTrail should be enabled and configured with at least one multi\-Region trail<a name="fsbp-cloudtrail-1"></a>

**Category:** Identify > Logging

**Severity:** High

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloudtrail-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloudtrail-enabled.html)

**Parameters:**
+ `readWriteType`: `ALL`

This control checks that there is at least one multi\-Region CloudTrail trail\.

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

**Resource:** CloudTrail trail

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html)

**Parameters:** None

This control checks whether CloudTrail is configured to use the server\-side encryption \(SSE\) AWS Key Management Service customer master key \(CMK\) encryption\. The check passes if the `KmsKeyId` is defined\.

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

   You might need to modify the policy for CloudTrail to successfully interact with your CMK\. For more information, see [Encrypting CloudTrail log files with AWS KMS–managed keys \(SSE\-KMS\)](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html) in the *AWS CloudTrail User Guide*\.

## \[CloudTrail\.4\] Ensure CloudTrail log file validation is enabled<a name="fsbp-cloudtrail-4"></a>

**Category:** Data protection > Data integrity

**Severity:** Low

**Resource type:** `AWS::CloudTrail::Trail`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html)

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

Security Hub recommends that you send CloudTrail logs to CloudWatch Logs\. Note that this recommendation is intended to ensure that account activity is captured, monitored, and has appropriately alarms\. You can use CloudWatch Logs to set this up with your AWS services\. This recommendation does not preclude the use of a different solution\.

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

**Resource:** CodeBuild project

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-envvar-awscred-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-envvar-awscred-check.html)

**Parameters:** None

This control checks whether the project contains the environment variables `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`\.

Authentication credentials `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` should never be stored in clear text, as this could lead to unintended data exposure and unauthorized access\.

**Note**  
This control is not supported in the following Regions\.  
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

## \[Config\.1\] AWS Config should be enabled<a name="fsbp-config-1"></a>

**Category:** Identify > Inventory

**Severity:** Medium

**Resource:** Account

**AWS Config rule:** None

**Parameters:** None

This control checks whether AWS Config is enabled in the account for the local Region and is recording all resources\.

The AWS Config service performs configuration management of supported AWS resources in your account and delivers log files to you\. The recorded information includes the configuration item \(AWS resource\), relationships between configuration items, and any configuration changes between resources\. 

Security Hub recommends that you enable AWS Config in all Regions\. The AWS configuration item history that AWS Config captures enables security analysis, resource change tracking, and compliance auditing\. 

**Note**  
Because Security Hub is a Regional service, the check performed for this control checks only the current Region for the account\. It does not check all Regions\.   
To allow security checks against global resources in each Region, you also must record global resources\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

To learn more, see [Getting started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.

### Remediation<a name="config-1-remediation"></a>

After you enable AWS Config, configure it to record all resources\.

**To configure AWS Config settings**

1. Open the AWS Config console at [https://console\.aws\.amazon\.com/config/](https://console.aws.amazon.com/config/)\.

1. Choose the Region to configure AWS Config in\.

1. If you have not used AWS Config before, choose **Get started**\.

1. On the **Settings** page, do the following:

   1. Under **Resource types to record**, choose **Record all resources supported in this region** and **Include global resources \(e\.g\. AWS IAM resources\)**\. 

   1. Under **AWS Config role**, either choose **Create AWS Config service\-linked role** or **Choose a role from your account** and then choose the role to use\.

   1. Under **Amazon S3 bucket**, specify the bucket to use or create a bucket and optionally include a prefix\. 

   1. Under **Amazon SNS topic**, choose an Amazon SNS topic from your account or create one\. For more information about Amazon SNS, see the [https://docs.aws.amazon.com/sns/latest/gsg/](https://docs.aws.amazon.com/sns/latest/gsg/)\. 

1. Choose **Next**\.

1. On the **AWS Config rules** page, choose **Next**\. 

1. Choose **Confirm**\.

For more information about using AWS Config from the AWS CLI, see [Turning on AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/gs-cli-subscribe.html) in the *AWS Config Developer Guide*\. 

You can also use an AWS CloudFormation template to automate this process\. For more information, see the [AWS CloudFormation StackSets sample template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html) in the *AWS CloudFormation User Guide*\. 

## \[DMS\.1\] AWS Database Migration Service replication instances should not be public<a name="fsbp-dms-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource:** DMS:ReplicationInstance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dms-replication-not-public.html](https://docs.aws.amazon.com/config/latest/developerguide/dms-replication-not-public.html)

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

**Resource:** Table

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-autoscaling-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-autoscaling-enabled.html)

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

**Resource:** Table

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-pitr-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/dynamodb-pitr-enabled.html)

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

**Resource:** Cluster

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/dax-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/dax-encryption-enabled.html)

**Parameters:** None

This control checks whether a DAX cluster is encrypted at rest\. 

Encrypting data at rest reduces the risk of data stored on disk being accessed by a user not authenticated to AWS\. The encryption adds another set of access controls to limit the ability of unauthorized users to access to the data\. For example, API permissions are required to decrypt the data before it can be read\.

### Remediation<a name="dynamodb-3-remediation"></a>

You cannot enable or disable encryption at rest after a cluster is created\. You must recreate the cluster in order to enable encryption at rest\. For detailed instructions on how to create a DAX cluster with encryption at rest enabled, see[ Enabling encryption at rest using the AWS Management Console](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DAXEncryptionAtRest.html#dax.encryption.tutorial-console) in the *Amazon DynamoDB Developer Guide*\.

## \[EC2\.1\] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone<a name="fsbp-ec2-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical 

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ebs-snapshot-public-restorable-check.html)

**Parameters:** None

This control checks that Amazon Elastic Block Store snapshots are not public, as determined by the ability to be restorable by anyone\.

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

**Resource:** EC2 security group

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html)

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

**Resource:** EC2 volume

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/encrypted-volumes.html](https://docs.aws.amazon.com/config/latest/developerguide/encrypted-volumes.html)

**Parameters:** None

This control checks whether the EBS volumes that are in an attached state are encrypted\. To pass this check, EBS volumes must be in use and encrypted\. If the EBS volume is not attached, then it is not subject to this check\.

For an added layer of security of your sensitive data in EBS volumes, you should enable EBS encryption at rest\. Amazon EBS encryption offers a straightforward encryption solution for your EBS resources that doesn't require you to build, maintain, and secure your own key management infrastructure\. It uses AWS KMS customer master keys \(CMK\) when creating encrypted volumes and snapshots\.

To learn more about Amazon EBS encryption, see [Amazon EBS encryption](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html) in the *Amazon EC2 User Guide for Linux Instances*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

### Remediation<a name="ec2-3-remediation"></a>

There is no direct way to encrypt an existing unencrypted volume or snapshot\. You can only encrypt a new volume or snapshot when you create it\.

If you enabled encryption by default, Amazon EBS encrypts the resulting new volume or snapshot using your default key for Amazon EBS encryption\. Even if you have not enabled encryption by default, you can enable encryption when you create an individual volume or snapshot\. In both cases, you can override the default key for Amazon EBS encryption and choose a symmetric customer managed CMK\.

For more information, see [Creating an Amazon EBS volume](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-creating-volume.html) and [Copying an Amazon EBS snapshot](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-copy-snapshot.html) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.4\] Stopped EC2 instances should be removed after a specified time period<a name="fsbp-ec2-4"></a>

**Category:** Identify > Inventory

**Severity:** Medium

**Resource:** EC2 Instance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-stopped-instance.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-stopped-instance.html)

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

**Resource:** EC2 VPC

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html)

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

**Resource type:** AWS Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-ebs-encryption-by-default.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-ebs-encryption-by-default.html)

**Parameters:** None

This control checks whether account\-level encryption is enabled by default for Amazon Elastic Block Store\(Amazon EBS\)\. The control fails if the account level encryption is not enabled\. 

When encryption is enabled for your account, Amazon EBS volumes and snapshot copies are encrypted at rest\. This adds an additional layer of protection for your data\. For more information, see [Encryption by default](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html#encryption-by-default) in the *Amazon EC2 User Guide for Linux Instances*\.

Note that following instance types do not support encryption: R1, C1, and M1\.

### Remediation<a name="ec2-7-remediation"></a>

You can use the Amazon EC2 console to enable default encryption for Amazon EBS volumes\.

**To configure the default encryption for Amazon EBS encryption for a Region**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the navigation pane, select **EC2 Dashboard**\.

1. In the upper\-right corner of the page, choose **Account Attributes, EBS encryption**\.

1. Choose **Manage**\.

1. Select **Enable**\. You can keep the AWS managed CMK with the alias `alias/aws/ebs` created on your behalf as the default encryption key, or choose a symmetric customer managed CMK\.

1. Choose **Update EBS encryption**\.

## \[EC2\.8\] EC2 instances should use IMDSv2<a name="fsbp-ec2-8"></a>

**Category:** Protect > Network security

**Severity:** High

**Resource type:** EC2 Instance 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-imdsv2-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-imdsv2-check.html)

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

1. Choose **Launch instance** and then choose **Launch instance**\.

1. In the **Configure Instance Details** step, under **Advanced Details**, for **Metadata version**, choose **V2 \(token required\)**\.

1. Choose **Review and Launch**\.

If your software uses IMDSv1, you can reconfigure your software to use IMDSv2\. For details, see [Transitioning to using Instance Metadata Service Version 2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html#instance-metadata-transition-to-version-2) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[EC2\.9\] EC2 instances should not have a public IP address<a name="fsbp-ec2-9"></a>

**Category:** Protect > Secure network configuration > Public IP addresses

**Severity:** High

**Resource:** EC2 instance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-no-public-ip.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-no-public-ip.html)

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

## \[EC2\.10\] Amazon EC2 should be configured to use VPC endpoints<a name="fsbp-ec2-10"></a>

**Category:** Protect \- Secure network configuration > API private access

**Severity:** Medium

**Resource:** EC2 VPC

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/service-vpc-endpoint-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/service-vpc-endpoint-enabled.html)

**Parameters:** 
+ `serviceName`: `ec2`

This control checks whether a service endpoint for Amazon EC2 is created for each VPC\. The control fails if a VPC does not have a VPC endpoint created for the Amazon EC2 service\. 

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

**Resource type:** Amazon EC2 subnet

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/subnet-auto-assign-public-ip-disabled.html](https://docs.aws.amazon.com/config/latest/developerguide/subnet-auto-assign-public-ip-disabled.html)

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

For instructions on how to delete an unused network ACL, see [Deleting a network ACL](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html#DeleteNetworkACL) in the *Amazon VPC User Guide*\.

## \[EC2\.17\] EC2 instances should not use multiple ENIs<a name="fsbp-ec2-17"></a>

**Category:** Network security 

**Severity:** Low

**Resource:** `AWS::EC2::Instance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-multiple-eni-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-multiple-eni-check.html)

**Parameters:**
+ `Adapterids` \(Optional\) – A list of network interface IDs that are attached to EC2 instances

This control checks whether an EC2 instance uses multiple Elastic Network Interfaces \(ENIs\) or Elastic Fabric Adapters \(EFAs\)\. This control passes if a single network adapter is used\. The control includes an optional parameter list to identify the allowed ENIs\.

Multiple ENIs can cause dual\-homed instances, meaning instances that have multiple subnets\. This can add network security complexity and introduce unintended network paths and access\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)
This control is still in the release process\. It might not yet be available in all of the Regions where it is supported\.

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

**Resource:** `AWS::EC2::SecurityGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-sg-open-only-to-authorized-ports.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-sg-open-only-to-authorized-ports.html)

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
This control is still in the release process\. It might not yet be available in all of the Regions where it is supported\.

### Remediation<a name="ecs-18-remediation"></a>

For information on how to modify a security group, see [Add, remove, or update rules](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#AddRemoveRules) in the *Amazon VPC User Guide*\.

## \[ECS\.1\] Amazon ECS task definitions should have secure networking modes and user definitions<a name="fsbp-ecs-1"></a>

**Category:** Protect > Secure access management

**Severity:** High

**Resource:** `AWS::ECS::TaskDefinition`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecs-task-definition-user-for-host-mode-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ecs-task-definition-user-for-host-mode-check.html)

**Parameters:** None

This control checks whether an Amazon ECS task definition that has host networking mode also has 'privileged' or 'user' container definitions\. The control fails for task definitions that have host network mode and container definitions where privileged=false or is empty and user=root or is empty\.

If a task definition has elevated privileges, it is because the customer has specifically opted in to that configuration\. This control checks for unexpected privilege escalation when a task definition has host networking enabled but the customer has not opted in to elevated privileges\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)
This control is still in the release process\. It might not yet be available in all of the Regions where it is supported\.

### Remediation<a name="ecs-1-remediation"></a>

For information on how to update a task definition, see [Updating a task definition](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/update-task-definition.html) in the *Amazon Elastic Container Service Developer Guide*\.

Note that when you update a task definition, it does not update running tasks that were launched from the previous task definition\. To update a running task, you must redeploy the task with the new task definition\.

## \[EFS\.1\] Amazon EFS should be configured to encrypt file data at rest using AWS KMS<a name="fsbp-efs-1"></a>

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource:** EFS file system

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-encrypted-check.html)

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

**Resource type:** EFS FileSystem

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/efs-in-backup-plan.html](https://docs.aws.amazon.com/config/latest/developerguide/efs-in-backup-plan.html)

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

## \[ElasticBeanstalk\.1\] Elastic Beanstalk environments should have enhanced health reporting enabled<a name="fsbp-elasticbeanstalk-1"></a>

**Category:** Detect > Detection services > Application monitoring

**Severity:** Low

**Resource type:** Environment

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/beanstalk-enhanced-health-reporting-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/beanstalk-enhanced-health-reporting-enabled.html)

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

**Resource type:** Environment

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elastic-beanstalk-managed-updates-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/elastic-beanstalk-managed-updates-enabled.html)

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

## \[ELB\.3\] Classic Load Balancer listeners should be configured with HTTPS or TLS termination<a name="fsbp-elb-3"></a>

**Category:** Protect > Data protection > Encryption of data in transit 

**Severity:** Medium

**Resource:** ELB load balancer

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elb-tls-https-listeners-only.html](https://docs.aws.amazon.com/config/latest/developerguide/elb-tls-https-listeners-only.html)

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

1. For all listeners where Load Balancer Protocol is not set to HTTPS or SSL, change the setting to HTTPS or SSL\.

1. For all modified listeners, under **SSL Certificate**, choose **Change**\.

1. For all modified listeners, select **Choose a certificate from ACM**\.

1. Select the certificate from the **Certificates** drop\-down list\. Then choose **Save**\.

1. After you update all of the listeners, choose **Save**\.

## \[ELB\.4\] Application load balancers should be configured to drop HTTP headers<a name="fsbp-elb-4"></a>

**Category:** Protect > Network security

**Severity:** Medium

**Resource type:** ELB load balancer

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/alb-http-drop-invalid-header-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/alb-http-drop-invalid-header-enabled.html)

**Parameters:** None

This control evaluates AWS Application Load Balancers \(ALB\) to ensure they are configured to drop invalid HTTP headers\. The control fails if the value of `routing.http.drop_invalid_header_fields.enabled` is set to `false`\.

By default, ALBs are not configured to drop invalid HTTP header values\. Removing these header values prevents HTTP desync attacks\.

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

**Resource:** ELB load balancer

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elb-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/elb-logging-enabled.html)

**Parameters:** None

This control checks whether the Application Load Balancer and the Classic Load Balancer have logging enabled\. The control fails if `access_logs.s3.enabled` is `false`\.

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

**Resource:** Elbv2 load balancer

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elb-deletion-protection-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/elb-deletion-protection-enabled.html)

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

## \[ELBv2\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS<a name="fsbp-elbv2-1"></a>

**Category:** Protect > Data protection > Encryption of data in transit

**Severity:** Medium

**Resource:** Elbv2 load balancer

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html](https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html)

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

**Resource type:** EMR:Cluster

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/emr-master-no-public-ip.html](https://docs.aws.amazon.com/config/latest/developerguide/emr-master-no-public-ip.html)

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

**Resource:** Elasticsearch domain

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-encrypted-at-rest.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-encrypted-at-rest.html)

**Parameters:** None

This control checks whether Amazon Elasticsearch Service \(Amazon ES\) domains have encryption\-at\-rest configuration enabled\. The check fails if encryption at rest is not enabled\.

For an added layer of security for your sensitive data in Elasticsearch, you should configure your Elasticsearch to be encrypted at rest\. Elasticsearch domains offer encryption of data at rest\. The feature uses AWS KMS to store and manage your encryption keys\. To perform the encryption, it uses the Advanced Encryption Standard algorithm with 256\-bit keys \(AES\-256\)\.

To learn more about Elasticsearch encryption at rest, see [Encryption of data at rest for Amazon Elasticsearch Service](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/encryption-at-rest.html) in the *Amazon Elasticsearch Service Developer Guide*\.

**Note**  
Certain instance types, such as t\.small and t\.medium, do not support encryption of data at rest\. For details, see [Supported instance types](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/aes-supported-instance-types.html) in the *Amazon Elasticsearch Service Developer Guide*\.

### Remediation<a name="es-1-remediation"></a>

By default, domains do not encrypt data at rest, and you cannot configure existing domains to use the feature\.

To enable the feature, you must create another domain and migrate your data\. For information about creating domains, see the [https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createupdatedomains.html#es-createdomains](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createupdatedomains.html#es-createdomains)\.

Encryption of data at rest requires Amazon ES 5\.1 or later\. For more information about encrypting data at rest for Amazon ES, see the [https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/encryption-at-rest.html](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/encryption-at-rest.html)\.

## \[ES\.2\] Amazon Elasticsearch Service domains should be in a VPC<a name="fsbp-es-2"></a>

**Category:** Protect > Secure network configuration > Resources within VPC 

**Severity:** Critical

**Resource type:** Elasticsearch domain

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-in-vpc-only.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-in-vpc-only.html)

**Parameters:** None

This control checks whether Amazon Elasticsearch Service domains are in a VPC\. It does not evaluate the VPC subnet routing configuration to determine public access\. You should ensure that Amazon ES domains are not attached to public subnets\. See [Resource\-based policies](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-ac.html#es-ac-types-resource) in the *Amazon Elasticsearch Service Developer Guide*\. You should also ensure that your VPC is configured according to the recommended best practices\. See [Security best practices for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html) in the *Amazon VPC User Guide*\.

Amazon ES domains deployed within a VPC can communicate with VPC resources over the private AWS network, without the need to traverse the public internet\. This configuration increases the security posture by limiting access to the data in transit\. VPCs provide a number of network controls to secure access to Amazon ES domains, including network ACL and security groups\. Security Hub recommends that you migrate public Amazon ES domains to VPCs to take advantage of these controls\.

### Remediation<a name="es-2-remediation"></a>

If you create a domain with a public endpoint, you cannot later place it within a VPC\. Instead, you must create a new domain and migrate your data\. The reverse is also true\. If you create a domain within a VPC, it cannot have a public endpoint\. Instead, you must either[ create another domain](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createupdatedomains.html#es-createdomains) or disable this control\.

See [Migrating from public access to VPC access](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-vpc.html#es-migrating-public-to-vpc) in the *Amazon Elasticsearch Service Developer Guide*\.

## \[ES\.3\] Amazon Elasticsearch Service domains should encrypt data sent between nodes<a name="fsbp-es-3"></a>

**Category:** Protect > Data protection > Encryption of data in transit 

**Severity:** Medium

**Resource type:** Elasticsearch domain

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-node-to-node-encryption-check.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-node-to-node-encryption-check.html)

**Parameters:** None

This control checks whether Amazon ES domains have node\-to\-node encryption enabled\.

HTTPS \(TLS\) can be used to help prevent potential attackers from eavesdropping on or manipulating network traffic using person\-in\-the\-middle or similar attacks\. Only encrypted connections over HTTPS \(TLS\) should be allowed\. Enabling node\-to\-node encryption for Amazon ES domains ensures that intra\-cluster communications are encrypted in transit\.

There can be a performance penalty associated with this configuration\. You should be aware of and test the performance trade\-off before enabling this option\. 

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)

### Remediation<a name="es-3-remediation"></a>

Node\-to\-node encryption can only be enabled on a new domain\. To remediate this finding, first [create a new domain](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createupdatedomains.html#es-createdomains) with the **Node\-to\-node encryption** check box selected\. Then follow [Using a snapshot to migrate data](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-version-migration.html#snapshot-based-migration) to migrate your data to the new domain\.

## \[ES\.4\] Amazon Elasticsearch Service domain error logging to CloudWatch Logs should be enabled<a name="fsbp-es-4"></a>

**Category:** Identify \- Logging

**Severity:** Medium

**Resource type:** `AWS::Elasticsearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-logs-to-cloudwatch.html](https://docs.aws.amazon.com/config/latest/developerguide/elasticsearch-logs-to-cloudwatch.html)

**Parameters:**
+ `logtype = 'error'`

This control checks whether Amazon ES domains are configured to send error logs to CloudWatch Logs\.

You should enable error logs for Amazon ES domains and send those logs to CloudWatch Logs for retention and response\. Domain error logs can assist with security and access audits, and can help to diagnose availability issues\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)
This control is still in the release process\. It might not yet be available in all of the Regions where it is supported\.

### Remediation<a name="es-4-remediation"></a>

For information on how to enable log publishing, see [Enabling log publishing \(console\)](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-createdomain-configure-slow-logs.html#es-createdomain-configure-slow-logs-console) in the *Amazon Elasticsearch Service Developer Guide*\.

## \[GuardDuty\.1\] GuardDuty should be enabled<a name="fsbp-guardduty-1"></a>

**Category:** Detect > Detection services 

**Severity:** High

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html](https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html)

**Parameters:** None

This control checks whether Amazon GuardDuty is enabled in your GuardDuty account and Region\.

It is highly recommended that you enable GuardDuty in all supported AWS Regions\. Doing so allows GuardDuty to generate findings about unauthorized or unusual activity, even in Regions that you do not actively use\. This also allows GuardDuty to monitor CloudTrail events for global AWS services such as IAM\.

**Note**  
This control is not supported in the following Regions\.  
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

**Resource:** IAM policy

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html)

**Parameters:** None

This control checks whether the default version of IAM policies \(also known as customer managed policies\) has administrator access that includes a statement with "Effect": "Allow" with "Action": "\*" over "Resource": "\*"\.

The control only checks the customer managed policies that you create\. It does not check inline and AWS managed policies\.

IAM policies define a set of privileges that are granted to users, groups, or roles\. Following standard security advice, AWS recommends that you grant least privilege, which means to grant only the permissions that are required to perform a task\. When you provide full administrative privileges instead of the minimum set of permissions that the user needs, you expose the resources to potentially unwanted actions\.

Instead of allowing full administrative privileges, determine what users need to do and then craft policies that let the users perform only those tasks\. It is more secure to start with a minimum set of permissions and grant additional permissions as necessary\. Do not start with permissions that are too lenient and then try to tighten them later\.

You should remove IAM policies that have a statement with `"Effect": "Allow" `with `"Action": "*"` over `"Resource": "*"`\.

### Remediation<a name="iam-1-remediation"></a>

To remediate this issue, update your IAM policies so that they do not allow full "\*" administrative privileges\.

**To modify an IAM policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Policies**\.

1. Choose the button next to the policy to remove\.

1. From **Policy actions**, choose **Detach**\.

1. For each user to detach the policy from, choose the button next to the user, then choose **Detach policy**\.

Confirm that the user that you detached the policy from can still access AWS services and resources as expected\.

## \[IAM\.2\] IAM users should not have IAM policies attached<a name="fsbp-iam-2"></a>

**Category:** Protect > Secure access management

**Severity:** Low

**Resource:** IAM user

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-no-policies-check.html)

**Parameters:** None

This control checks that none of your IAM users have policies attached\. Instead, IAM users must inherit permissions from IAM groups or roles\.

By default, IAM users, groups, and roles have no access to AWS resources\. IAM policies grant privileges to users, groups, or roles\. We recommend that you apply IAM policies directly to groups and roles but not to users\. Assigning privileges at the group or role level reduces the complexity of access management as the number of users grows\. Reducing access management complexity might in turn reduce the opportunity for a principal to inadvertently receive or retain excessive privileges\. 

### Remediation<a name="iam-2-remediation"></a>

To resolve this issue, create an IAM group, assign the policy to the group, and then add the users to the group\. The policy is applied to each user in the group\.

**To create an IAM group**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Groups** and then choose **Create New Group**\.

1. Enter a name for the group to create and then choose **Next Step**\.

1. Select each policy to assign to the group and then choose **Next Step**\. The policies that you choose should include any policies currently attached directly to a user account\.

1. Add users to a group and then assign the policies to that group\. Each user in the group is then assigned the policies that are assigned to the group\.

1. Confirm the details on the **Review** page and then choose **Create Group**\.

For more information about creating groups, see [Creating IAM groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_create.html) in the *IAM User Guide*\.

**To add users to an IAM group**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Groups**\.

1. Choose **Group Actions** and then choose **Add Users to Group**\.

1. Select the users to add to the group and then choose **Add Users**\.

For more information about adding users to groups, see [Adding and removing users in an IAM group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_manage_add-remove-users.html) in the *IAM User Guide*\.

**To remove a policy attached directly to a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. For the user to detach a policy from, choose the name in the **User name** column\.

1. For each policy listed under **Attached directly**, choose the **X** on the right side of the page to remove the policy from the user and then choose **Remove**\.

1. Confirm that the user can still use AWS services as expected\.

## \[IAM\.3\] IAM users' access keys should be rotated every 90 days or less<a name="fsbp-iam-3"></a>

**Category:** Protect > Secure access management

**Severity:** Medium 

**Resource:** IAM user

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html](https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html)

**Parameters:**
+ `maxAccessKeyAge`: 90

This control checks whether the active access keys are rotated within 90 days\.

We highly recommend that you do not generate and remove all access keys in your account\. Instead, the recommended best practice is to either create one or more IAM roles or to use [federation](http://aws.amazon.com/identity/federation/)\. You can use these methods to allow your users to use their existing corporate credentials to log into the AWS Management Console and AWS CLI\.

Each approach has its use cases\. Federation is generally better for enterprises that have an existing central directory or plan to need more than the current limit IAM users\. Applications that run outside of an AWS environment need access keys for programmatic access to AWS resources\.

However, if the resources that need programmatic access run inside AWS, the best practice is to use IAM roles\. Roles allow you to grant a resource access without hardcoding an access key ID and secret access key into the configuration\.

To learn more about protecting your access keys and account, see [Best practices for managing AWS access keys](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html) in the *AWS General Reference*\. Also see the blog post [Guidelines for protecting your AWS account while using programmatic access](http://aws.amazon.com/blogs/security/guidelines-for-protecting-your-aws-account-while-using-programmatic-access/)\.

If you already have an access key, Security Hub recommends that you rotate the access keys every 90 days\. Rotating access keys reduces the chance that an access key that is associated with a compromised or terminated account is used\. It also ensures that data cannot be accessed with an old key that might have been lost, cracked, or stolen\. Always update your applications after you rotate access keys\. 

Access keys consist of an access key ID and a secret access key\. They are used to sign programmatic requests that you make to AWS\. AWS users need their own access keys to make programmatic calls to AWS from the AWS CLI, Tools for Windows PowerShell, the AWS SDKs, or direct HTTP calls using the API operations for individual AWS services\.

If your organization uses AWS Single Sign\-On \(AWS SSO\), your users can sign in to Active Directory, a built\-in AWS SSO directory, or [another identity provider \(IdP\) connected to AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-idp.html)\. They can then be mapped to an IAM role that enables them to run AWS CLI commands or call AWS API operations without the need for IAM user access keys\. To learn more, see [Configuring the AWS CLI to use AWS Single Sign\-On](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html) in the *AWS Command Line Interface User Guide*\.

**Note**  
This control is not supported in Africa \(Cape Town\) or Europe \(Milan\)\.

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

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html)

**Parameters:** None

This control checks whether the root user access key is present\. 

The root account is the most privileged user in an AWS account\. AWS access keys provide programmatic access to a given account\.

Security Hub recommends that you remove all access keys that are associated with the root account\. This limits that vectors that can be used to compromise the account\. It also encourages the creation and use of role\-based accounts that are least privileged\. 

**Note**  
This control is not supported in Africa \(Cape Town\)\.

### Remediation<a name="iam-4-remediation"></a>

To remediate this issue, delete the root user access key\.

**To delete access keys**

1. Log in to your account using the AWS account root user credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\. 

1. Choose **Access keys \(access key ID and secret access key\)**\. 

1. To permanently delete the key, choose **Delete** and then choose **Yes**\. You cannot recover deleted keys\.

1. If there is more than one root user access key, then repeat steps 4 and 5 for each key\.

## \[IAM\.5\] MFA should be enabled for all IAM users that have a console password<a name="fsbp-iam-5"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource:** IAM user

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html](https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html)

**Parameters:** None

This control checks whether AWS multi\-factor authentication \(MFA\) is enabled for all IAM users that use a console password\.

Multi\-factor authentication \(MFA\) adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they are prompted for their user name and password\. In addition, they are prompted for an authentication code from their AWS MFA device\.

We recommend that you enable MFA for all accounts that have a console password\. MFA is designed to provide increased security for console access\. The authenticating principal must possess a device that emits a time\-sensitive key and must have knowledge of a credential\. 

### Remediation<a name="iam-5-remediation"></a>

To remediate this issue, add MFA to users that do not yet have it\. 

**To configure MFA for a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the **User name** of the user to configure MFA for\.

1. Choose **Security credentials**\.

1. Next to **Assigned MFA Device**, choose **Manage**\.

1. Follow the **Manage MFA Device** wizard to assign the type of device appropriate for your environment\. 

To learn how to delegate MFA setup to users, see the blog post [How to delegate management of multi\-factor authentication to AWS IAM users](http://aws.amazon.com/blogs/security/how-to-delegate-management-of-multi-factor-authentication-to-aws-iam-users/)\.

## \[IAM\.6\] Hardware MFA should be enabled for the root user<a name="fsbp-iam-6"></a>

**Category:** Protect > Secure access management

**Severity:** Critical

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html)

**Parameters:** None

This control checks whether your AWS account is enabled to use a hardware multi\-factor authentication \(MFA\) device to sign in with root user credentials\.

Virtual MFA might not provide the same level of security as hardware MFA devices\. We recommend that you use only a virtual MFA device while you wait for hardware purchase approval or for your hardware to arrive\. To learn more, see[ Enabling a virtual multi\-factor authentication \(MFA\) device \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html) in the *IAM User Guide*\.

**Note**  
This control is not supported in the following Regions\.  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)\.

### Remediation<a name="iam-6-remediation"></a>

To remediate this issue, add hardware\-based MFA to the root account\.

**To enable hardware\-based MFA for the root account**

1. Log in to your account using the root user credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Multi\-Factor Authentication \(MFA\)**\.

1. Choose **Activate MFA**\.

1. Choose a hardware\-based \(not virtual\) device to use for MFA and then choose **Continue**\.

1. Complete the steps to configure the device type appropriate to your selection\.

## \[IAM\.7\] Password policies for IAM users should have strong configurations<a name="fsbp-iam-7"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Parameters:**
+ `RequireUppercaseCharacters`: `true`
+ `RequireLowercaseCharacters`: `true`
+ `RequireSymbols`: `true`
+ `RequireNumbers`: `true`
+ `MinimumPasswordLength`: `8`

This control checks whether the account password policy for IAM users uses the following recommended configurations\.
+ `RequireUppercaseCharacters`: `true`
+ `RequireLowercaseCharacters`: `true`
+ `RequireSymbols`: `true`
+ `RequireNumbers`: `true`
+ `MinimumPasswordLength`: `8`

To access the AWS Management Console, IAM users need passwords\. As a best practice, Security Hub highly recommends that instead of creating IAM users, you use federation\. Federation allows users to use their existing corporate credentials to log into the AWS Management Console\. Use AWS Single Sign\-On \(AWS SSO\) to create or federate the user, and then assume an IAM role into an account\.

To learn more about identity providers and federation, see [Identity providers and federation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html) in the *IAM User Guide*\. To learn more about AWS SSO, see the [https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)\.

 If you need to use IAM users, Security Hub recommends that you enforce the creation of strong user passwords\. You can set a password policy on your AWS account to specify complexity requirements and mandatory rotation periods for passwords\. When you create or change a password policy, most of the password policy settings are enforced the next time users change their passwords\. Some of the settings are enforced immediately\. To learn more, see [Setting an account password policy for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html) in the *IAM User Guide*\.

### Remediation<a name="iam-7-remediation"></a>

To remediate this issue, update your password policy to use the recommended configuration\.

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Requires at least one uppercase letter**\.

1. Select **Requires at least one lowercase letter**\.

1. Select **Requires at least one non\-alphanumeric character**\.

1. Select **Requires at least one number**\.

1. For **Minimum password length**, enter **8**\.

1. Choose **Apply password policy**\.

## \[IAM\.8\] Unused IAM user credentials should be removed<a name="fsbp-iam-8"></a>

**Category:** Protect > Secure access management 

**Severity:** Medium 

**Resource:** IAM User

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html)

**Parameters:**
+ `maxCredentialUsageAge`: 90 

This control checks whether your IAM users have passwords or active access keys that have not been used for 90 days\.

IAM users can access AWS resources using different types of credentials, such as passwords or access keys\. 

Security Hub recommends that you remove or deactivate all credentials that were unused for 90 days or more\. Disabling or removing unnecessary credentials reduces the window of opportunity for credentials associated with a compromised or abandoned account to be used\.

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

**Resource:** IAM Policy

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-full-access.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-full-access.html)

**Parameters:** None

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
This control is still in the release process\. It might not yet be available in all of the Regions where it is supported\.

### Remediation<a name="iam-21-remediation"></a>

To remediate this issue, update your IAM policies so that they do not allow full "\*" administrative privileges\.

For details on how to edit an IAM policy, see [Editing IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-edit.html) in the *IAM User Guide*\.

## \[KMS\.1\] IAM customer managed policies should not allow decryption actions on all KMS keys<a name="fsbp-kms-1"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource:** IAM policy

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-customer-policy-blocked-kms-actions.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-customer-policy-blocked-kms-actions.html)

**Parameters:** 
+ `kms:ReEncryptFrom, kms:Decrypt`

Checks whether the default version of IAM customer managed policies allow principals to use the AWS KMS decryption actions on all resources\. This control uses [Zelkova](http://aws.amazon.com/blogs/security/protect-sensitive-data-in-the-cloud-with-automated-reasoning-zelkova/), an automated reasoning engine, to validate and warn you about policies that may grant broad access to your secrets across AWS accounts\.

This control fails if the `kms:Decrypt` or `kms:ReEncryptFrom` actions are allowed on all KMS keys\. The control evaluates both attached and unattached customer managed policies\. It does not check inline policies or AWS managed policies\.

With AWS KMS, you control who can use your customer master keys \(CMKs\) and gain access to your encrypted data\. IAM policies define which actions an identity \(user, group, or role\) can perform on which resources\. Following security best practices, AWS recommends that you allow least privilege\. In other words, you should grant to identities only the `kms:Decrypt` or `kms:ReEncryptFrom` permissions and only for the keys that are required to perform a task\. Otherwise, the user might use keys that are not appropriate for your data\.

Instead of granting permissions for all keys, determine the minimum set of keys that users need to access encrypted data\. Then design policies that allow users to use only those keys\. For example, do not allow `kms:Decrypt` permission on all KMS keys\. Instead, allow `kms:Decrypt` only on keys in a particular Region for your account\. By adopting the principle of least privilege, you can reduce the risk of unintended disclosure of your data\.

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

## \[KMS\.2\] IAM principals should not have IAM inline policies that allow decryption actions on all KMS keys<a name="fsbp-kms-2"></a>

**Category:** Protect > Secure access management

**Severity:** Medium

**Resource:**
+ IAM role
+ IAM user
+ IAM group

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-inline-policy-blocked-kms-actions.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-inline-policy-blocked-kms-actions.html) 

**Parameters:**
+ `kms:ReEncryptFrom, kms:Decrypt`

Checks whether the inline policies that are embedded in your IAM identities \(role, user, or group\) allow the AWS KMS decryption actions on all KMS keys\. This control uses [Zelkova](http://aws.amazon.com/blogs/security/protect-sensitive-data-in-the-cloud-with-automated-reasoning-zelkova/), an automated reasoning engine, to validate and warn you about policies that may grant broad access to your secrets across AWS accounts\.

This control fails if `kms:Decrypt` or `kms:ReEncryptFrom` actions are allowed on all KMS keys in an inline policy\. 

With AWS KMS, you control who can use your customer master keys \(CMKs\) and gain access to your encrypted data\. IAM policies define which actions an identity \(user, group, or role\) can perform on which resources\. Following security best practices, AWS recommends that you allow least privilege\. In other words, you should grant to identities only the permissions they need and only for keys that are required to perform a task\. Otherwise, the user might use keys that are not appropriate for your data\.

Instead of granting permission for all keys, determine the minimum set of keys that users need to access encrypted data\. Then design policies that allow the users to use only those keys\. For example, do not allow `kms:Decrypt` permission on all KMS keys\. Instead, allow them only on keys in a particular Region for your account\. By adopting the principle of least privilege, you can reduce the risk of unintended disclosure of your data\.

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

**Resource type:** KMS key

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/kms-cmk-not-scheduled-for-deletion.html](https://docs.aws.amazon.com/config/latest/developerguide/kms-cmk-not-scheduled-for-deletion.html)

**Parameters:** None

This control checks whether AWS KMS customer managed keys \(CMK\) are scheduled for deletion\. The control fails if a CMK is scheduled for deletion\.

CMKs cannot be recovered once deleted\. Data encrypted under a KMS CMK is also permanently unrecoverable if the CMK is deleted\. If meaningful data has been encrypted under a CMK scheduled for deletion, consider decrypting the data or re\-encrypting the data under a new CMK unless you are intentionally performing a *cryptographic erasure*\.

When a CMK is scheduled for deletion, a mandatory waiting period is enforced to allow time to reverse the deletion, if it was scheduled in error\. The default waiting period is 30 days, but it can be reduced to as short as 7 days when the KMS CMK is scheduled for deletion\. During the waiting period, the scheduled deletion can be canceled and the KMS CMK will not be deleted\.

For additional information regarding deleting CMKs, see [Deleting customer master keys](https://docs.aws.amazon.com/kms/latest/developerguide/deleting-keys.html) in the *AWS Key Management Service Developer Guide*\.

**Note**  
This control is not supported in the Europe \(Milan\) Region\.

### Remediation<a name="kms-3-remediation"></a>

For detailed remediation instructions to cancel a scheduled KMS CMK deletion, see **To cancel key deletion** under [Scheduling and canceling key deletion \(console\)](https://docs.aws.amazon.com/kms/latest/developerguide/deleting-keys.html#deleting-keys-scheduling-key-deletion) in the AWS Key Management Service Developer Guide\. 

## \[Lambda\.1\] Lambda function policies should prohibit public access<a name="fsbp-lambda-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource:** Lambda function

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-public-access-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-public-access-prohibited.html)

**Parameters:** None

This control checks whether the Lambda function resource\-based policy prohibits public access outside of your account\.

The Lambda function should not be publicly accessible, as this may allow unintended access to your code stored in the function\.

**Note**  
This control is not supported in the China \(Beijing\) or China \(Ningxia\) Regions\.

### Remediation<a name="lambda-1-remediation"></a>

If a Lambda function fails this control, it indicates that the resource\-based policy statement for the Lambda function allows public access\.

To remediate the issue, you must update the policy\. You can only update the resource\-based policy from the Lambda API\. These instructions use the console to review the policy and the AWS Command Line Interface to remove the permissions\.

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

**Resource:** Lambda function

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-settings-check.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-settings-check.html)

**Parameters:** 
+ `runtime`: `nodejs14.x, nodejs12.x, nodejs10.x, python3.8, python3.7, python3.6, ruby2.7, ruby2.5, java11, java8, java8.al2, go1.x, dotnetcore3.1, dotnetcore2.1`

This control checks that the Lambda function settings for runtimes match the expected values set for the supported runtimes for each language\. This control checks for the following runtimes: `nodejs14.x`, `nodejs12.x`, `nodejs10.x`, `python3.8`, `python3.7`, `python3.6`, `ruby2.7`, `ruby2.5`, `java11`, `java8`, `java8.al2`, `go1.x`, `dotnetcore3.1`, `dotnetcore2.1`

[Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) are built around a combination of operating system, programming language, and software libraries that are subject to maintenance and security updates\. When a runtime component is no longer supported for security updates, Lambda deprecates the runtime\. Even though you cannot create functions that use the deprecated runtime, the function is still available to process invocation events\. Make sure that your Lambda functions are current and do not use out\-of\-date runtime environments\.

To learn more about the supported runtimes that this control checks for the supported languages, see [AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) in the *AWS Lambda Developer Guide*\.

**Note**  
This control is not supported in the China \(Beijing\) or China \(Ningxia\) Regions\.

### Remediation<a name="lambda-2-remediation"></a>

For more information on supported runtimes and deprecation schedules, see the [Runtime support policy](https://docs.aws.amazon.com/lambda/latest/dg/runtime-support-policy.html) section of the *AWS Lambda Developer Guide*\. When you migrate your runtimes to the latest version, follow the syntax and guidance from the publishers of the language\.

## \[Lambda\.4\] Lambda functions should have a dead\-letter queue configured<a name="fsbp-lambda-4"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::Lambda::Function`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-dlq-check.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-dlq-check.html)

**Parameters:**
+ `dlqArns` \(Optional\) – Comma\-separated list of Amazon SQS and Amazon SNS ARNs that must be configured as the Lambda function dead\-letter queue target\.

This control checks whether a Lambda function is configured with a dead\-letter queue\. The control fails if the Lambda function is not configured with a dead\-letter queue\.

As an alternative to an on\-failure destination, you can configure your function with a dead\-letter queue to save discarded events for further processing\. A dead\-letter queue acts the same as an on\-failure destination\. It is used when an event fails all processing attempts or expires without being processed\.

A dead\-letter queue allows you to look back at errors or failed requests to your Lambda function to debug or identify unusual behavior\.

From a security perspective, it is important to understand why your function failed and to ensure that your function does not drop data or compromise data security as a result\. For example, if your function cannot communicate to an underlying resource, that could be a symptom of a denial of service \(DoS\) attack elsewhere in the network\.

**Note**  
This control is not supported in the Asia Pacific \(Osaka\) orChina \(Ningxia\) Regions\.

### Remediation<a name="lambda-4-remediation"></a>

You can configure a dead\-letter queue from the AWS Lambda console\.

**To configure a dead\-letter queue**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. In the navigation pane, choose **Functions**\.

1. Choose a function\.

1. Choose **Configuration** and then choose **Asynchronous invocation**\.

1. Under **Asynchronous invocation**, choose **Edit**\.

1. Set **DLQ resource** to Amazon SQS or Amazon SNS\.

1. Choose the target queue or topic\.

1. Choose **Save**\.

## \[RDS\.1\] RDS snapshots should be private<a name="fsbp-rds-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource:** RDS DB snapshot

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshots-public-prohibited.html)

**Parameters:** None

This control checks whether Amazon RDS snapshots are public\.

This control is intended for RDS instances\. It can also return findings for snapshots of Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters, even though they are not evaluated for public accessibility\. If these findings are not useful, you can suppress them\.

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

## \[RDS\.2\] RDS DB instances should prohibit public access, determined by the PubliclyAccessible configuration<a name="fsbp-rds-2"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource:** RDS DB instance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-public-access-check.html)

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

**Resource:** RDS DB instance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html)

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

**Resource type:** DBClusterSnapshot, DBSnapshot

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshot-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-snapshot-encrypted.html)

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

**Resource type:** DBInstance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-multi-az-support.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-multi-az-support.html)

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

**Resource type:** DBInstance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-enhanced-monitoring-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-enhanced-monitoring-enabled.html)

**Parameters:** None

This control checks whether enhanced monitoring is enabled for your RDS DB instances\.

In Amazon RDS, Enhanced Monitoring enables a more rapid response to performance changes in underlying infrastructure\. These performance changes could result in a lack of availability of the data\. Enhanced Monitoring provides real\-time metrics of the operating system that your RDS DB instance runs on\. An agent is installed on the instance\. The agent can obtain metrics more accurately than is possible from the hypervisor layer\.

Enhanced Monitoring metrics are useful when you want to see how different processes or threads on a DB instance use the CPU\. For more information, see [Enhanced Monitoring](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="rds-6-remediation"></a>

For detailed instructions on how to enable Enhanced Monitoring for your DB instance, see [Setting up for and enabling Enhanced Monitoring](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.html#USER_Monitoring.OS.Enabling) in the *Amazon RDS User Guide*\.

## \[RDS\.7\] RDS clusters should have deletion protection enabled<a name="fsbp-rds-7"></a>

**Category:** Protect > Data protection > Data deletion protection

**Severity:** Low

**Resource type:** DBCluster

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-deletion-protection-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-deletion-protection-enabled.html)

**Parameters:** None

This control checks whether RDS clusters have deletion protection enabled\. 

This control is intended for RDS DB instances\. However, it can also generate findings for Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters\. If these findings are not useful, then you can suppress them\.

Enabling cluster deletion protection is an additional layer of protection against accidental database deletion or deletion by an unauthorized entity\.

When deletion protection is enabled, an RDS cluster cannot be deleted\. Before a deletion request can succeed, deletion protection must be disabled\.

**Note**  
This control is not supported in the following Regions\.  
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

**Resource type:** DBInstance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-deletion-protection-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-deletion-protection-enabled.html)

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

**Resource:** DBInstance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-logging-enabled.html)

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

**Resource:** DBInstance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-iam-authentication-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-instance-iam-authentication-enabled.html)

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

1. Under **Database options**, choose **Enable IAM DB authentication**\.

1. Choose **Continue**\.

1. Under **Scheduling of modifications**, choose when to apply modifications\. The options are **Apply during the next scheduled maintenance window** or **Apply immediately**\.

1. For clusters, choose **Modify DB Instance**\.

## \[RDS\.12\] IAM authentication should be configured for RDS clusters<a name="fsbp-rds-12"></a>

**Category:** Protect > Secure access management > Passwordless authentication

**Severity:** Medium

**Resource type:** `DBCluster`, `DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-iam-authentication-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-iam-authentication-enabled.html)

**Parameters:** None

This control checks whether an RDS DB cluster has IAM database authentication enabled\.

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

**Resource type:** `DBInstance`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-automatic-minor-version-upgrade-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-automatic-minor-version-upgrade-enabled.html)

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

**Resource type:** `DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/aurora-mysql-backtracking-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/aurora-mysql-backtracking-enabled.html)

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

**Resource type:** `DBCluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-multi-az-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-cluster-multi-az-enabled.html)

**Parameters:** None

This control checks whether high availability is enabled for your RDS DB clusters\.

RDS DB clusters should be configured for multiple Availability Zones to ensure availability of the data that is stored\. Deployment to multiple Availability Zones allows for automated failover in the event of an Availability Zone availability issue and during regular RDS maintenance events\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(Bahrain\)
South America \(São Paulo\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)
This control is still in the release process\. It might not yet be available in all of the Regions where it is supported\.

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

## \[Redshift\.1\] Amazon Redshift clusters should prohibit public access<a name="fsbp-redshift-1"></a>

**Category:** Protect > Secure network configuration > Resources not publicly accessible

**Severity:** Critical

**Resource:** Cluster

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-public-access-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-public-access-check.html)

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

**Resource:** Cluster

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-require-tls-ssl.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-require-tls-ssl.html)

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

**Resource:** Cluster

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-backup-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-backup-enabled.html)

**Parameters:**
+ `MinRetentionPeriod = 7`

This control checks whether Amazon Redshift clusters have automated snapshots enabled\. It also checks whether the snapshot retention period is greater than or equal to seven\.

Backups help you to recover more quickly from a security incident\. They strengthen the resilience of your systems\. Amazon Redshift takes periodic snapshots by default\. This control checks whether automatic snapshots are enabled and retained for at least seven days\. For more details on Amazon Redshift automated snapshots, see [Automated snapshots](https://docs.aws.amazon.com/redshift/latest/mgmt/working-with-snapshots.html#about-automated-snapshots) in the *Amazon Redshift Cluster Management Guide*\.

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

## \[Redshift\.6\] Amazon Redshift should have automatic upgrades to major versions enabled<a name="fsbp-redshift-6"></a>

**Category:** Detect > Vulnerability and patch management

**Severity:** Medium

**Resource:** Cluster

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-maintenancesettings-check.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-cluster-maintenancesettings-check.html)

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

**Severity:** High

**Resource type:** Cluster

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/redshift-enhanced-vpc-routing-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/redshift-enhanced-vpc-routing-enabled.html)

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

For detailed remediation instructions, see [Enabling enhanced VPC routing](https://docs.aws.amazon.com/redshift/latest/mgmt/enhanced-vpc-enabling-cluster.html) in the *Amazon Redshift Cluster Management Guide*\.

## \[S3\.1\] S3 Block Public Access setting should be enabled<a name="fsbp-s3-1"></a>

**Category:** Protect > Secure network configuration

**Severity:** Medium

**Resource:** Account

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks.html) 

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

The control fails if any of the settings are set to `false`, or if any of the settings are not configured\. When the settings do not have a value, the AWS Config rule cannot complete its evaluation\.

Amazon S3 public access block is designed to provide controls across an entire AWS account or at the individual S3 bucket level to ensure that objects never have public access\. Public access is granted to buckets and objects through access control lists \(ACLs\), bucket policies, or both\.

Unless you intend to have your S3 buckets be publicly accessible, you should configure the account level Amazon S3 Block Public Access feature\.

To learn more, see [Using Amazon S3 Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service Developer Guide*\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(Bahrain\)

### Remediation<a name="s3-1-remediation"></a>

To remediate this issue, enable Amazon S3 Block Public Access\.

**To enable Amazon S3 Block Public Access**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Block public access \(account settings\)**\.

1. Choose **Edit**\.

1. Select **Block *all* public access**\.

1. Choose **Save changes**\.

For more information, see [Using Amazon S3 block public access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service Developer Guide*\.

## \[S3\.2\] S3 buckets should prohibit public read access<a name="fsbp-s3-2"></a>

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource:** S3 bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited)

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

**Resource:** S3 bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html) 

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

**Resource:** S3 bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html)

**Parameters:** None

This control checks that your S3 bucket either has Amazon S3 default encryption enabled or that the S3 bucket policy explicitly denies put\-object requests without server\-side encryption\.

For an added layer of security for your sensitive data in S3 buckets, you should configure your buckets with server\-side encryption to protect your data at rest\. Amazon S3 encrypts each object with a unique key\. As an additional safeguard, it encrypts the key itself with a master key that it rotates regularly\. Amazon S3 server\-side encryption uses one of the strongest block ciphers available to encrypt your data, 256\-bit Advanced Encryption Standard \(AES\-256\)\.

To learn more, see [Protecting data using server\-side encryption with Amazon S3\-managed encryption keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html) in the *Amazon Simple Storage Service Developer Guide*\.

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
   + Choose **AWS\-KMS** to use keys that are managed by AWS KMS for default encryption\. Then choose a master key from the list of the AWS KMS master keys that you have created\.

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

**Resource:** S3 Bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-ssl-requests-only.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-ssl-requests-only.html)

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

**Resource type:** AWS::S3::Bucket

**AWS Config** rule: [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-blacklisted-actions-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-blacklisted-actions-prohibited.html)

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

**Resource:** AWS::S3::Bucket

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-level-public-access-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-level-public-access-prohibited.html)

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
This control is still in the release process\. It might not yet be available in all of the Regions where it is supported\.

### Remediation<a name="s3-8-remediation"></a>

For information on how to remove public access at a bucket level, see [Blocking public access to your Amazon S3 storage](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon S3 User Guide*\.

## \[SageMaker\.1\] SageMaker notebook instances should not have direct internet access<a name="fsbp-sagemaker-1"></a>

**Category:** Protect > Secure network configuration

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

**Resource:** Secrets Manager secret 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-rotation-enabled-check.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-rotation-enabled-check.html)

**Parameters:** None

This control checks whether a secret stored in AWS Secrets Manager is configured with automatic rotation\.

Secrets Manager helps you improve the security posture of your organization\. Secrets include database credentials, passwords, and third\-party API keys\. You can use Secrets Manager to store secrets centrally, encrypt secrets automatically, control access to secrets, and rotate secrets safely and automatically\.

Secrets Manager can rotate secrets\. You can use rotation to replace long\-term secrets with short\-term ones\. Rotating your secrets limits how long an unauthorized user can use a compromised secret\. For this reason, you should rotate your secrets frequently\. To learn more about rotation, see [Rotating your AWS Secrets Manager secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html) in the *AWS Secrets Manager User Guide*\.

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

**Resource:** Secrets Manager secret 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-scheduled-rotation-success-check.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-scheduled-rotation-success-check.html)

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

**Resource type:** Secrets Manager Secret

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-unused.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-unused.html)

**Parameters:** None

This control checks whether your secrets have been accessed within a specified number of days\. The default value is 90 days\. If a secret was accessed even once within the defined number of days, this control fails\.

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

**Resource:** Secrets Manager Secret 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-periodic-rotation.html](https://docs.aws.amazon.com/config/latest/developerguide/secretsmanager-secret-periodic-rotation.html)

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

**Resource:** Amazon SNS Topic

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/sns-encrypted-kms.html](https://docs.aws.amazon.com/config/latest/developerguide/sns-encrypted-kms.html)

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

## \[SSM\.1\] EC2 instances should be managed by AWS Systems Manager<a name="fsbp-ssm-1"></a>

**Category:** Identify > Inventory

**Severity:** Medium

**Resource:** EC2 instance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-managed-by-ssm.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-instance-managed-by-ssm.html)

**Parameters:** None

This control checks whether the EC2 instances in your account are managed by AWS Systems Manager\. Systems Manager is an AWS service that you can use to view and control your AWS infrastructure\.

To help you to maintain security and compliance, Systems Manager scans your managed instances\. A managed instance is a machine that is configured for use with Systems Manager\. Systems Manager then reports or takes corrective action on any policy violations that it detects\. Systems Manager also helps you to configure and maintain your managed instances\.

To learn more, see [https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)\.

### Remediation<a name="ssm-1-remediation"></a>

You can use the Systems Manager console to remediate this issue\.

**To ensure that EC2 instances are managed by Systems Manager**

1. Open the AWS Systems Manager console at [https://console\.aws\.amazon\.com/systems\-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. Choose **Quick setup**\.

1. On the configuration screen, keep the default options\.

1. Choose **Enable**\.

To determine whether your instances support Systems Manager associations, see [Systems Manager prerequisites](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html) in the *AWS Systems Manager User Guide*\.

## \[SSM\.2\] All EC2 instances managed by Systems Manager should be compliant with patching requirements<a name="fsbp-ssm-2"></a>

**Category:** Detect > Detection services 

**Severity:** High

**Resource:** SSM patch compliance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-patch-compliance-status-check.html)

**Parameters:** None

This control checks whether the compliance status of the Amazon EC2 Systems Manager patch compliance is `COMPLIANT` or `NON_COMPLIANT` after the patch installation on the instance\. It only checks instances that are managed by Systems Manager Patch Manager\.

Having your EC2 instances fully patched as required by your organization reduces the attack surface of your AWS accounts\. 

**Note**  
This control is not supported in the following Regions\.  
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

**Resource:** AwsSSMAssociationCompliance

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-association-compliance-status-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-managedinstance-association-compliance-status-check.html)

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

## \[WAF\.1\] AWS WAF Classic global web ACL logging should be enabled<a name="fsbp-waf-1"></a>

**Category:** Identify > Logging

**Severity:** Medium

**Resource:** `AWS::WAF::WebACL`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/waf-classic-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/waf-classic-logging-enabled.html)

**Parameters:** None

This control checks whether logging is enabled for an AWS WAF global Web ACL\. This control fails if logging is not enabled for the web ACL\.

Logging is an important part of maintaining the reliability, availability, and performance of AWS WAF globally\. It is a business and compliance requirement in many organizations, and allows you to troubleshoot application behavior\. It also provides detailed information about the traffic that is analyzed by the web ACL that is attached to AWS WAF\.

NOTE

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