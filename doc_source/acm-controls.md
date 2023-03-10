# AWS Certificate Manager controls<a name="acm-controls"></a>

These controls are related to ACM resources\.

## \[ACM\.1\] Imported and ACM\-issued certificates should be renewed after a specified time period<a name="acm-1"></a>

**Related requirements:** NIST\.800\-53\.r5 SC\-28\(3\), NIST\.800\-53\.r5 SC\-7\(16\)

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
This control is not supported in the following Regions:  
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