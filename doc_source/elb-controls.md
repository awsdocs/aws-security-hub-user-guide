# Elastic Load Balancing controls<a name="elb-controls"></a>

These controls are related to Elastic Load Balancing resources\.

## \[ELB\.1\] Application Load Balancer should be configured to redirect all HTTP requests to HTTPS<a name="elb-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/2\.3,PCI DSS v3\.2\.1/4\.1, NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancingV2::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html](https://docs.aws.amazon.com/config/latest/developerguide/alb-http-to-https-redirection-check.html) 

**Schedule type:** Periodic

**Parameters:** None

This control checks whether HTTP to HTTPS redirection is configured on all HTTP listeners of Application Load Balancers\. The control fails if any of the HTTP listeners of Application Load Balancers do not have HTTP to HTTPS redirection configured\.

Before you start to use your Application Load Balancer, you must add one or more listeners\. A listener is a process that uses the configured protocol and port to check for connection requests\. Listeners support both the HTTP and HTTPS protocols\. You can use an HTTPS listener to offload the work of encryption and decryption to your load balancer\. To enforce encryption in transit, you should use redirect actions with Application Load Balancers to redirect client HTTP requests to an HTTPS request on port 443\.

To learn more, see [Listeners for your Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-listeners.html) in *User Guide for Application Load Balancers*\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="elb-1-remediation"></a>

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

## \[ELB\.2\] Classic Load Balancers with SSL/HTTPS listeners should use a certificate provided by AWS Certificate Manager<a name="elb-2"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(5\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

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

## \[ELB\.3\] Classic Load Balancer listeners should be configured with HTTPS or TLS termination<a name="elb-3"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

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

**Note**  
This control is not supported in Middle East \(UAE\)\.

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

## \[ELB\.4\] Application Load Balancer should be configured to drop http headers<a name="elb-4"></a>

**Related requirements:** NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8\(2\)

**Category:** Protect > Network security

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancingV2::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/alb-http-drop-invalid-header-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/alb-http-drop-invalid-header-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control evaluates AWS Application Load Balancers to ensure they are configured to drop invalid HTTP headers\. The control fails if the value of `routing.http.drop_invalid_header_fields.enabled` is set to `false`\.

By default, Application Load Balancers are not configured to drop invalid HTTP header values\. Removing these header values prevents HTTP desync attacks\.

Note that you can disable this control if [ELB\.12](#elb-12) is enabled\.

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

## \[ELB\.5\] Application and Classic Load Balancers logging should be enabled<a name="elb-5"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-7\(8\)

**Category:** Logging

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`, `AWS::ElasticLoadBalancingV2::LoadBalancer`

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

1. Choose an Application Load Balancer or Classic Load Balancer\.

1. From **Actions**, choose **Edit attributes**\.

1. Under **Access logs**, choose **Enable**\.

1. Enter your S3 location\. This location can exist or it can be created for you\. If you do not specify a prefix, the access logs are stored in the root of the S3 bucket\.

1. Choose **Save**\.

## \[ELB\.6\] Application Load Balancer deletion protection should be enabled<a name="elb-6"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\), NIST\.800\-53\.r5 CM\-3, NIST\.800\-53\.r5 SC\-5\(2\)

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

## \[ELB\.7\] Classic Load Balancers should have connection draining enabled<a name="elb-7"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Recover > Resilience

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Configrule:** `elb-connection-draining-enabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether Classic Load Balancers have connection draining enabled\.

Enabling connection draining on Classic Load Balancers ensures that the load balancer stops sending requests to instances that are de\-registering or unhealthy\. It keeps the existing connections open\. This is particularly useful for instances in Auto Scaling groups, to ensure that connections aren't severed abruptly\.

### Remediation<a name="elb-7-remediation"></a>

To enable connection draining on Classic Load Balancers, following the steps in [Configure connection draining for your Classic Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/config-conn-drain.html) in *User Guide for Classic Load Balancers*\.

## \[ELB\.8\] Classic Load Balancers with SSL listeners should use a predefined security policy that has strong AWS Configuration<a name="elb-8"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-17\(2\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 IA\-5\(1\), NIST\.800\-53\.r5 SC\-12\(3\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-23, NIST\.800\-53\.r5 SC\-23\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-8, NIST\.800\-53\.r5 SC\-8\(1\), NIST\.800\-53\.r5 SC\-8\(2\), NIST\.800\-53\.r5 SI\-7\(6\)

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

## \[ELB\.9\] Classic Load Balancers should have cross\-zone load balancing enabled<a name="elb-9"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

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
This control is not supported in Africa \(Cape Town\) or Middle East \(UAE\)\.

### Remediation<a name="elb-9-remediation"></a>

To enable cross\-zone load balancing in a Classic Load Balancer, see [Enable cross\-zone load balancing](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/enable-disable-crosszone-lb.html#enable-cross-zone) in the Elastic Load Balancing User Guide\.

## \[ELB\.10\] Classic Load Balancer should span multiple Availability Zones<a name="elb-10"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

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

## \[ELB\.12\] Application Load Balancer should be configured with defensive or strictest desync mitigation mode<a name="elb-12"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Data protect > Data integrity 

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancingV2::LoadBalancer`

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

## \[ELB\.13\] Application, Network and Gateway Load Balancers should span multiple Availability Zones<a name="elb-13"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

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

## \[ELB\.14\] Classic Load Balancer should be configured with defensive or strictest desync mitigation mode<a name="elb-14"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Data Protect > Data Integrity

**Severity:** Medium

**Resource type:** `AWS::ElasticLoadBalancing::LoadBalancer`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/clb-desync-mode-check.html](https://docs.aws.amazon.com/config/latest/developerguide/clb-desync-mode-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `desyncMode`: defensive, strictest

This control checks whether a Classic Load Balancer is configured with defensive or strictest desync mitigation mode\. The control fails if the Classic Load Balancer isn't configured with defensive or strictest desync mitigation mode\.

HTTP Desync issues can lead to request smuggling and make applications vulnerable to request queue or cache poisoning\. In turn, these vulnerabilities can lead to credential hijacking or execution of unauthorized commands\. Classic Load Balancers configured with defensive or strictest desync mitigation mode protect your application from security issues that may be caused by HTTP Desync\. 

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elb-14-remediation"></a>

To update desync mitigation mode on a Classic Load Balancer, see [Modify desync mitigation mode](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/config-desync-mitigation-mode.html#update-desync-mitigation-mode) in the *User Guide for Classic Load Balancers*\. 