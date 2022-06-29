# Control categories<a name="control-categories"></a>

Each control in AWS Security Hub is assigned a category\. The category for a control reflects the security function that the control applies to\.

The category value contains the category, the subcategory within the category, and, optionally, a classifier within the subcategory\. For example:
+ Detect > Detection services > Application monitoring
+ Identify > Inventory
+ Protect > Data protection > Encryption of data in transit

Here are descriptions of the categories, subcategories, and classifiers that apply to currently available Security Hub controls\.

## Detect<a name="control-category-detect"></a>

Develop and implement the appropriate activities to identify the occurrence of a cybersecurity event\.

**Detection services**  
Are the correct detection services in place with the right amount of coverage?  
Examples of AWS detection services include Amazon CloudWatch Alarms, Amazon Detective, Amazon GuardDuty, Amazon Inspector, AWS IoT Device Defender, AWS Security Hub, and AWS Trusted Advisor\.  
+ **Application monitoring** – Is application health monitored to maintain availability?

## Identify<a name="control-category-identify"></a>

Develop the organizational understanding to manage cybersecurity risk to systems, assets, data, and capabilities\.

**Inventory**  
What resources are being used, and are they approved resources for this service?  
+ **Tagging** – Are the correct resource tagging strategies implemented for the service, including the resource owner?

**Logging**  
Have you securely enabled all relevant logging for the service? Examples of log files include the following:  
+ Amazon VPC Flow Logs
+ Elastic Load Balancing access logs
+ Amazon CloudFront logs
+ Amazon CloudWatch logs
+ Amazon Relational Database Service logs
+ Amazon OpenSearch Service slow index logs
+ X\-Ray tracing
+ AWS Directory Service logs
+ AWS Config items

**Resource configuration**  
Do you understand how your resources are configured so that you can reduce your attack surface?

**Vulnerability, patch, and version management**  
Do you have resources that need to be patched or resources with unacceptable vulnerabilities? Are you using the latest versions of software?

## Protect<a name="control-category-protect"></a>

Develop and implement the appropriate safeguards to ensure delivery of critical infrastructure services and secure coding practices\.

**Secure access management**  
Are there strong authentication and authorization policies in place for the service?  
+ **Access control** – Do IAM or resource policies for the service align to least privilege practices?
+ **Passwordless authentication** – Are federated identities or SSO used to authenticate users instead of IDs, passwords, and access keys? Is Kerberos used to eliminate the need to transmit passwords over the network?
+ **Root user access restrictions** – Is usage of the root user being avoided?
+ **Sensitive API actions restricted** – Are sensitive API actions for a service properly restricted, especially those leading to privilege escalation or resource\-sharing? This could apply to IAM or resource\-based policies\.

**Secure network configuration**  
Are public and insecure remote network access avoided for the service?  
+ **API private access** – Are VPC endpoints enabled for private access to AWS APIs?
+ **Resources not publicly accessible** – Are resources properly segmented and isolated?
+ **Resources within VPC** – Is there proper usage of VPCs, such as requiring jobs to run in VPCs?
+ **Security group configuration** – Are security groups securely configured?

**Data protection**  
Do you have mechanisms to protect data that your service consumes, sends, or stores?  
+ **Encryption of data at rest** – Does the service encrypt data at rest?
+ **Encryption of data in transit** – Does the service encrypt data in transit?
+ **Data integrity** – Does the service validate data for integrity?
+ **Data deletion protection** – Does the service protect data from accidental deletion?

**API protection**  
Does the service use AWS PrivateLink to protect the service API operations?

**Protective services**  
Are the correct protective services in place? Do they provide the correct amount of coverage?  
Protective services help you deflect attacks and compromises that are directed at the service\. Examples of protective services in AWS include AWS Control Tower, AWS WAF, AWS Shield Advanced, AWS Network Firewall, AWS Secrets Manager, AWS Identity and Access Management Access Analyzer, and AWS Resource Access Manager\.

**Secure development**  
Do you use secure coding practices?  
+ **Credentials not hardcoded** – Do you have credentials hardcoded into your code?

## Recover<a name="control-category-recover"></a>

Develop and implement the appropriate activities to maintain plans for resilience and to restore any capabilities or services that were impaired due to a cybersecurity event\.

**Resilience**  
Can your workloads quickly recover from a security event?  
+ **Backups enabled** – Have you established and tested backups?
+ **High availability** – Does the configuration of the service allow for graceful failovers, elastic scaling, and high availability?