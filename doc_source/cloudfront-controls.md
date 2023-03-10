# Amazon CloudFront controls<a name="cloudfront-controls"></a>

These controls are related to CloudFront resources\.

## \[CloudFront\.1\] CloudFront distributions should have a default root object configured<a name="cloudfront-1"></a>

**Related requirements:** NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\)

**Category:** Protect > Secure access management > Resources not publicly accessible

**Severity:** Critical

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-default-root-object-configured.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudfront-default-root-object-configured.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon CloudFront distribution is configured to return a specific object that is the default root object\. The control fails if the CloudFront distribution does not have a default root object configured\.

A user might sometimes request the distribution's root URL instead of an object in the distribution\. When this happens, specifying a default root object can help you to avoid exposing the contents of your web distribution\.

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-1-remediation"></a>

For detailed instructions on how to specify a default root object for your distribution, see [How to specify a default root object](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/DefaultRootObject.html#DefaultRootObjectHowToDefine) in the *Amazon CloudFront Developer Guide*\.

## \[CloudFront\.2\] CloudFront distributions should have origin access identity enabled<a name="cloudfront-2"></a>

**Related requirements:** NIST\.800\-53\.r5 SC\-7\(11\)

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

## \[CloudFront\.3\] CloudFront distributions should require encryption in transit<a name="cloudfront-3"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

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

## \[CloudFront\.4\] CloudFront distributions should have origin failover configured<a name="cloudfront-4"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

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

## \[CloudFront\.5\] CloudFront distributions should have logging enabled<a name="cloudfront-5"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(4\), NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AC\-6\(9\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4\(20\), NIST\.800\-53\.r5 SI\-7\(8\)

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

## \[CloudFront\.6\] CloudFront distributions should have WAF enabled<a name="cloudfront-6"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(21\)

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

## \[CloudFront\.7\] CloudFront distributions should use custom SSL/TLS certificates<a name="cloudfront-7"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

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

## \[CloudFront\.8\] CloudFront distributions should use SNI to serve HTTPS requests<a name="cloudfront-8"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

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

## \[CloudFront\.9\] CloudFront distributions should encrypt traffic to custom origins<a name="cloudfront-9"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

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

## \[CloudFront\.10\] CloudFront distributions should not use deprecated SSL protocols between edge locations and custom origins<a name="cloudfront-10"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

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

## \[CloudFront\.12\] CloudFront distributions should not point to non\-existent S3 origins<a name="cloudfront-12"></a>

**Related requirements:** NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\)

**Category:** Identify > Resource configuration

**Severity:** High

**Resource type:** `AWS::CloudFront::Distribution`

**AWS Config rule:** `cloudfront-s3-origin-non-existent-bucket`

**Schedule type:** Periodic

**Parameters:** None

This control checks whether Amazon CloudFront distributions are pointing to non\-existent Amazon S3 origins\. The control fails for a CloudFront distribution if the origin is configured to point to a non\-existent bucket\. This control only applies to CloudFront distributions where an S3 bucket without static website hosting is the S3 origin\.

When a CloudFront distribution in your account is configured to point to a non\-existent bucket, a malicious third party can create the referenced bucket and serve their own content through your distribution\. We recommend checking all origins regardless of routing behavior to ensure that your distributions are pointing to appropriate origins\. 

**Note**  
This control is only supported in US East \(N\. Virginia\)\.

### Remediation<a name="cloudfront-12-remediation"></a>

To modify your CloudFront distribution to point to a new origin, see [Updating a distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowToUpdateDistribution.html) in the *Amazon CloudFront Developer Guide*\.