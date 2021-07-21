# CIS AWS Foundations Benchmark controls that you might want to disable<a name="securityhub-standards-cis-to-disable"></a>

For the CIS AWS Foundations Benchmark standard, below are some specific controls that you might want to disable\. You might want to disable them because they are related to resources that only exist in specific accounts or Regions\. The controls would then produce `WARNING` statuses if the relevant resource cannot be found\.

**CIS AWS Foundations Benchmark 2\.7 control**  
This control deals with using AWS KMS to encrypt CloudTrail trail logs\. If you log these trails in a centralized logging account, you only need to run this control in the account and Region where centralized logging takes place\.

**CIS AWS Foundations Benchmark 1\.2\-1\.14, 1\.16, 1\.20, 1\.22, and 2\.5 controls**  
To save on the cost of AWS Config, you can disable recording of global resources in all but one Region, and then disable these controls that deal with global resources in all Regions except for the Region that runs global recording\.  
If you disable these 1\.x controls and disable recording of global resources in a particular Region, you should also disable 2\.5\. This is because 2\.5 requires recording of global resources in order to pass\.