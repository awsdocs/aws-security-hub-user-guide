# Elasticsearch controls<a name="es-controls"></a>

These controls are related to Elasticsearch resources\.

## \[ES\.1\] Elasticsearch domains should have encryption at\-rest enabled<a name="es-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/3\.4, NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SC\-7\(10\), NIST\.800\-53\.r5 SI\-7\(6\)

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

## \[ES\.2\] Elasticsearch domains should be in a VPC<a name="es-2"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1,PCI DSS v3\.2\.1/1\.3\.1,PCI DSS v3\.2\.1/1\.3\.2,PCI DSS v3\.2\.1/1\.3\.4,PCI DSS v3\.2\.1/1\.3\.6, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

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

## \[ES\.3\] Elasticsearch domains should encrypt data sent between nodes<a name="es-3"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\)

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

## \[ES\.4\] Elasticsearch domain error logging to CloudWatch Logs should be enabled<a name="es-4"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(4\), NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AC\-6\(9\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4\(20\), NIST\.800\-53\.r5 SI\-7\(8\)

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

## \[ES\.5\] Elasticsearch domains should have audit logging enabled<a name="es-5"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(4\), NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AC\-6\(9\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4\(20\), NIST\.800\-53\.r5 SI\-7\(8\)

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

## \[ES\.6\] Elasticsearch domains should have at least three data nodes<a name="es-6"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

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

1. Open the Amazon OpenSearch Service console at [https://console\.aws\.amazon\.com/aos/](https://console.aws.amazon.com/aos/)\.

1. Under **My domains**, choose the name of the domain to edit\.

1. Choose **Edit domain**\.

1. Under **Data nodes**, set **Number of nodes** to a number greater than or equal to `3`\.

   For three Availability Zone deployments, set to a multiple of three to ensure equal distribution across Availability Zones\.

1. Choose **Submit**\.

## \[ES\.7\] Elasticsearch domains should be configured with at least three dedicated master nodes<a name="es-7"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

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

1. Open the Amazon OpenSearch Service console at [https://console\.aws\.amazon\.com/aos/](https://console.aws.amazon.com/aos/)\.

1. Under **My domains**, choose the name of the domain to edit\.

1. Choose **Edit domain**\.

1. Under **Dedicated master nodes**, set **Instance type** to the desired instance type\.

1. Set **Number of master nodes** equal to three or greater\.

1. Choose **Submit**\.

## \[ES\.8\] Connections to Elasticsearch domains should be encrypted using TLS 1\.2<a name="es-8"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

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