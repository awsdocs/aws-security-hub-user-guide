# Amazon API Gateway controls<a name="apigateway-controls"></a>

These controls are related to API Gateway resources\.

## \[APIGateway\.1\] API Gateway REST and WebSocket API execution logging should be enabled<a name="apigateway-1"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-7\(8\)

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
Middle East \(UAE\)

### Remediation<a name="apigateway-1-remediation"></a>

To enable logging for REST and WebSocket API operations, see [Set up CloudWatch API logging using the API Gateway console](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-logging.html#set-up-access-logging-using-console) in the *API Gateway Developer Guide*\.

## \[APIGateway\.2\] API Gateway REST API stages should be configured to use SSL certificates for backend authentication<a name="apigateway-2"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

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

## \[APIGateway\.3\] API Gateway REST API stages should have AWS X\-Ray tracing enabled<a name="apigateway-3"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-7

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
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="apigateway-3-remediation"></a>

For detailed instructions on how to enable X\-Ray active tracing for API Gateway REST API operations, see [Amazon API Gateway active tracing support for AWS X\-Ray](https://docs.aws.amazon.com/xray/latest/devguide/xray-services-apigateway.html) in the *AWS X\-Ray Developer Guide*\. 

## \[APIGateway\.4\] API Gateway should be associated with a WAF Web ACL<a name="apigateway-4"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(21\)

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

## \[APIGateway\.5\] API Gateway REST API cache data should be encrypted at rest<a name="apigateway-5"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

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

## \[APIGateway\.8\] API Gateway routes should specify an authorization type<a name="apigateway-8"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\)

**Category:** Protect > Secure Access Management

**Severity:** Medium

**Resource type:** `AWS::ApiGatewayV2::Route`

AWS Config rule: `api-gwv2-authorization-type-configured`

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon API Gateway routes have an authorization type\. The control fails if the API Gateway route does not specify an authorization type\.

API Gateway supports multiple mechanisms for controlling and managing access to your API\. By specifying an authorization type, you can restrict access to your API to only authorized users or processes\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="apigateway-8-remediation"></a>

To set an authorization type for HTTP APIs, see [Controlling and managing access to an HTTP API in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-access-control.html) in the *API Gateway Developer Guide*\. To set an authorization type for WebSocket APIs, see [Controlling and managing access to a WebSocket API in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-control-access.html) in the *API Gateway Developer Guide*\.

## \[APIGateway\.9\] Access logging should be configured for API Gateway V2 Stages<a name="apigateway-9"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-7\(8\)

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::ApiGatewayV2::Stage`

AWS Config rule: `api-gwv2-access-logs-enabled`

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon API Gateway V2 stages have access logging configured\. This control fails if access log settings aren't defined\.

API Gateway access logs provide detailed information about who has accessed your API and how the caller accessed the API\. These logs are useful for applications such as security and access audits and forensics investigation\. Enable these access logs to analyze traffic patterns and to troubleshoot issues\.

For additional best practices, see [Monitoring REST APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/rest-api-monitor.html) in the *API Gateway Developer Guide*\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="apigateway-9-remediation"></a>

To set up access logging, see [Set up CloudWatch API logging using the API Gateway console](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-logging.html#set-up-access-logging-using-console) in the *API Gateway Developer Guide*\. 