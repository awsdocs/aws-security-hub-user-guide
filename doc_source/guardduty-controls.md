# Amazon GuardDuty controls<a name="guardduty-controls"></a>

These controls are related to GuardDuty resources\.

## \[GuardDuty\.1\] GuardDuty should be enabled<a name="guardduty-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/11\.4, NIST\.800\-53\.r5 AC\-2\(12\), NIST\.800\-53\.r5 AU\-6\(1\), NIST\.800\-53\.r5 AU\-6\(5\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 CM\-8\(3\), NIST\.800\-53\.r5 RA\-3\(4\), NIST\.800\-53\.r5 SA\-11\(1\), NIST\.800\-53\.r5 SA\-11\(6\), NIST\.800\-53\.r5 SA\-15\(2\), NIST\.800\-53\.r5 SA\-15\(8\), NIST\.800\-53\.r5 SA\-8\(19\), NIST\.800\-53\.r5 SA\-8\(21\), NIST\.800\-53\.r5 SA\-8\(25\), NIST\.800\-53\.r5 SC\-5, NIST\.800\-53\.r5 SC\-5\(1\), NIST\.800\-53\.r5 SC\-5\(3\), NIST\.800\-53\.r5 SI\-20, NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4, NIST\.800\-53\.r5 SI\-4\(1\), NIST\.800\-53\.r5 SI\-4\(13\), NIST\.800\-53\.r5 SI\-4\(2\), NIST\.800\-53\.r5 SI\-4\(22\), NIST\.800\-53\.r5 SI\-4\(25\), NIST\.800\-53\.r5 SI\-4\(4\), NIST\.800\-53\.r5 SI\-4\(5\)

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
Middle East \(UAE\)
AWS GovCloud \(US\-East\)

### Remediation<a name="guardduty-1-remediation"></a>

To remediate this issue, you enable GuardDuty\.

For details on how to enable GuardDuty, including how to use AWS Organizations to manage multiple accounts, see [Getting started with GuardDuty](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_settingup.html) in the *Amazon GuardDuty User Guide*\.