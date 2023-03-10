# Amazon OpenSearch Service controls<a name="opensearch-controls"></a>

These controls are related to OpenSearch Service resources\.

## \[Opensearch\.1\] OpenSearch domains should have encryption at rest enabled<a name="opensearch-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.4, PCI DSS v3\.2\.1/7\.2\.1, NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data at rest

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-encrypted-at-rest.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-encrypted-at-rest.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether OpenSearch domains have encryption\-at\-rest configuration enabled\. The check fails if encryption at rest is not enabled\.

For an added layer of security for sensitive data, you should configure your OpenSearch Service domain to be encrypted at rest\. When you configure encryption of data at rest, AWS KMS stores and manages your encryption keys\. To perform the encryption, AWS KMS uses the Advanced Encryption Standard algorithm with 256\-bit keys \(AES\-256\)\.

To learn more about OpenSearch Service encryption at rest, see [Encryption of data at rest for Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/encryption-at-rest.html) in the *Amazon OpenSearch Service* *Developer Guide*\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="opensearch-1-remediation"></a>

By default, domains do not encrypt data at rest, and you cannot configure existing domains to use the feature\. To enable the feature, you must create another domain and migrate your data\.

For information about creating domains, see [Creating and managing Amazon OpenSearch Service domains](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createupdatedomains.html#es-createdomains) in the Amazon OpenSearch Service Developer Guide\.

Encryption of data at rest requires Amazon OpenSearch 1\.0 or later\. For more information about encrypting data at rest for Amazon OpenSearch, see [Encryption of data at rest for Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/encryption-at-rest.html) in the *Amazon OpenSearch Service Developer Guide*\.

## \[Opensearch\.2\] OpenSearch domains should be in a VPC<a name="opensearch-2"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.2, PCI DSS v3\.2\.1/1\.3\.4, PCI DSS v3\.2\.1/1\.3\.6, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration > Resources within VPC

**Severity:** Critical

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-in-vpc-only.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-in-vpc-only.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether OpenSearch domains are in a VPC\. It does not evaluate the VPC subnet routing configuration to determine public access\.

You should ensure that OpenSearch domains are not attached to public subnets\. See [Resource\-based policies](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/ac.html#ac-types-resource) in the Amazon OpenSearch Service Developer Guide\. You should also ensure that your VPC is configured according to the recommended best practices\. See [Security best practices for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html) in the Amazon VPC User Guide\.

OpenSearch domains deployed within a VPC can communicate with VPC resources over the private AWS network, without the need to traverse the public internet\. This configuration increases the security posture by limiting access to the data in transit\. VPCs provide a number of network controls to secure access to OpenSearch domains, including network ACL and security groups\. Security Hub recommends that you migrate public OpenSearch domains to VPCs to take advantage of these controls\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="opensearch-2-remediation"></a>

If you create a domain with a public endpoint, you cannot later place it within a VPC\. Instead, you must create a new domain and migrate your data\. The reverse is also true\. If you create a domain within a VPC, it cannot have a public endpoint\.

Instead, you must either [create another domain](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createupdatedomains.html#es-createdomains) or disable this control\.

See [Launching your Amazon OpenSearch Service domains within a VPC](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/vpc.html) in the Amazon OpenSearch Service Developer Guide\.

## \[Opensearch\.3\] OpenSearch domains should encrypt data sent between nodes<a name="opensearch-3"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\)

**Category:** Protect > Data protection > Encryption of data in transit

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-node-to-node-encryption-check.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-node-to-node-encryption-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether OpenSearch domains have node\-to\-node encryption enabled\. This control fails if node\-to\-node encryption is disabled on the domain\.

HTTPS \(TLS\) can be used to help prevent potential attackers from eavesdropping on or manipulating network traffic using person\-in\-the\-middle or similar attacks\. Only encrypted connections over HTTPS \(TLS\) should be allowed\. Enabling node\-to\-node encryption for OpenSearch domains ensures that intra\-cluster communications are encrypted in transit\.

There can be a performance penalty associated with this configuration\. You should be aware of and test the performance trade\-off before enabling this option\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="opensearch-3-remediation"></a>

Node\-to\-node encryption can only be enabled on a new domain\. To remediate this finding, create a new domain with **Node\-to\-node encryption** enabled and migrate your data to the new domain\. Follow the instructions to [create a new domain](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createupdatedomains.html#es-createdomains) in the Amazon OpenSearch Service Developer Guide and ensure that you select the **Node\-to\-node encryption** option when creating the new domain\. Then follow [Using a snapshot to migrate data](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/version-migration.html#snapshot-based-migration) to migrate your data to the new domain\.

## \[Opensearch\.4\] OpenSearch domain error logging to CloudWatch Logs should be enabled<a name="opensearch-4"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(4\), NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AC\-6\(9\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4\(20\), NIST\.800\-53\.r5 SI\-7\(8\)

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-logs-to-cloudwatch.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-logs-to-cloudwatch.html)

**Schedule type:** Change triggered

**Parameters:**
+ `logtype = 'error'`

This control checks whether OpenSearch domains are configured to send error logs to CloudWatch Logs\. This control fails if error logging to CloudWatch is not enabled for a domain\.

You should enable error logs for OpenSearch domains and send those logs to CloudWatch Logs for retention and response\. Domain error logs can assist with security and access audits, and can help to diagnose availability issues\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="opensearch-4-remediation"></a>

For information on how to enable log publishing, see [Enabling log publishing \(console\)](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/createdomain-configure-slow-logs.html#createdomain-configure-slow-logs-console) in the Amazon OpenSearch Service Developer Guide\.

## \[Opensearch\.5\] OpenSearch domains should have audit logging enabled<a name="opensearch-5"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(4\), NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AC\-6\(9\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4\(20\), NIST\.800\-53\.r5 SI\-7\(8\)

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

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="opensearch-5-remediation"></a>

For detailed instructions on enabling audit logs, see [Enabling audit logs](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/audit-logs.html#audit-log-enabling) in the Amazon OpenSearch Service Developer Guide\.

## \[Opensearch\.6\] OpenSearch domains should have at least three data nodes<a name="opensearch-6"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > High availability

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-data-node-fault-tolerance.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-data-node-fault-tolerance.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether OpenSearch domains are configured with at least three data nodes and `zoneAwarenessEnabled` is `true`\. This control fails for an OpenSearch domain if `instanceCount` is less than 3 or `zoneAwarenessEnabled` is `false`\.

An OpenSearch domain requires at least three data nodes for high availability and fault\-tolerance\. Deploying an OpenSearch domain with at least three data nodes ensures cluster operations if a node fails\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="opensearch-6-remediation"></a>

**To modify the number of data nodes in an OpenSearch domain**

1. Sign in to the AWS console and open the Amazon OpenSearch Service console at [https://console\.aws\.amazon\.com/es/](https://console.aws.amazon.com/es/)\.

1. Under **My domains**, choose the name of the domain to edit, and choose **Edit**\.

1. Under **Data nodes** set **Number of nodes** to a number greater than `3`\. If you are deploying to three Availability Zone, set the number to a multiple of three to ensure equal distribution across Availability Zones\. 

1. Choose **Submit**\.

## \[Opensearch\.7\] OpenSearch domains should have fine\-grained access control enabled<a name="opensearch-7"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-5, NIST\.800\-53\.r5 AC\-6

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
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="opensearch-7-remediation"></a>

To enable fine\-grained access control, see [Fine\-grained access control in Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/fgac.html) in the *Amazon OpenSearch Service Developer Guide*\.

## \[Opensearch\.8\] Connections to OpenSearch domains should be encrypted using TLS 1\.2<a name="opensearch-8"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data\-in\-transit

**Severity:** Medium

**Resource type:** `AWS::OpenSearch::Domain`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/opensearch-https-required.html](https://docs.aws.amazon.com/config/latest/developerguide/opensearch-https-required.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether connections to OpenSearch domains are required to use TLS 1\.2\. The check fails if the OpenSearch domain `TLSSecurityPolicy` is not `Policy-Min-TLS-1-2-2019-07`\.

HTTPS \(TLS\) can be used to help prevent potential attackers from using person\-in\-the\-middle or similar attacks to eavesdrop on or manipulate network traffic\. Only encrypted connections over HTTPS \(TLS\) should be allowed\. Encrypting data in transit can affect performance\. You should test your application with this feature to understand the performance profile and the impact of TLS\. TLS 1\.2 provides several security enhancements over previous versions of TLS\. 

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="opensearch-8-remediation"></a>

To enable TLS encryption, use the [UpdateDomainConfig](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/configuration-api.html#configuration-api-actions-updatedomainconfig) API operation to configure the [DomainEndpointOptions](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/configuration-api.html#configuration-api-datatypes-domainendpointoptions) in order to set the `TLSSecurityPolicy`\. For more information, see [Node\-to\-node encryption](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/ntn.html) in the Amazon OpenSearch Service Developer Guide\.