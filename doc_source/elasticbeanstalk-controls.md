# AWS Elastic Beanstalk controls<a name="elasticbeanstalk-controls"></a>

These controls are related to Elastic Beanstalk resources\.

## \[ElasticBeanstalk\.1\] Elastic Beanstalk environments should have enhanced health reporting enabled<a name="elasticbeanstalk-1"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-7,NIST\.800\-53\.r5 SI\-2

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
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticbeanstalk-1-remediation"></a>

For instructions on how to enable enhanced health reporting, see [Enabling enhanced health reporting using the Elastic Beanstalk console](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/health-enhanced-enable.html#health-enhanced-enable-console) in the *AWS Elastic Beanstalk Developer Guide*\.

## \[ElasticBeanstalk\.2\] Elastic Beanstalk managed platform updates should be enabled<a name="elasticbeanstalk-2"></a>

**Related requirements:** NIST\.800\-53\.r5 SI\-2,NIST\.800\-53\.r5 SI\-2\(2\),NIST\.800\-53\.r5 SI\-2\(4\),NIST\.800\-53\.r5 SI\-2\(5\)

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
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="elasticbeanstalk-2-remediation"></a>

For instructions on how to enable managed platform updates, see [To configure managed platform updates under Managed platform updates](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environment-platform-update-managed.html) in the *AWS Elastic Beanstalk Developer Guide*\.