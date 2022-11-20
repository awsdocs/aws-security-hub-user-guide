# CIS AWS Foundations Benchmark<a name="securityhub-standards-cis"></a>

AWS Security Hub supports versions 1\.2\.0 and 1\.4\.0 of the Center for Internet Security \(CIS\) AWS Foundations Benchmark\.

**Note**  
We recommend upgrading to CIS AWS Foundations Benchmark v1\.4\.0 to stay current on security best practices, but you may have both v1\.4\.0 and v1\.2\.0 enabled at the same time\. For more information, see [Disabling or enabling a security standard](securityhub-standards-enable-disable.md)\. If you want to upgrade to v1\.4\.0, it's best to enable v1\.4\.0 first before disabling v1\.2\.0\. If you use the Security Hub integration with AWS Organizations to centrally manage multiple accounts and wish to batch enable v1\.4\.0 across all accounts \(and disable v1\.2\.0 if you wish\), you can use a [Security Hub multi\-account script](https://github.com/awslabs/aws-securityhub-multiaccount-scripts)\. 

Security Hub has satisfied the requirements of CIS Security Software Certification and has been awarded CIS Security Software Certification for the following CIS Benchmarks:
+ CIS Benchmark for CIS Amazon Web Services Foundations Benchmark, v1\.2\.0, Level 1
+ CIS Benchmark for CIS Amazon Web Services Foundations Benchmark, v1\.2\.0, Level 2

CIS considers Level 1 to be a basic set of requirements that most organizations can implement fairly quickly to lower their attack surface\. Level 2 is designed for environments where security is paramount\.

**Topics**
+ [AWS Config resources required for CIS controls](securityhub-standards-cis-config-resources.md)
+ [CIS AWS Foundations Benchmark v1\.2\.0](securityhub-cis-controls.md)
+ [CIS AWS Foundations Benchmark v1\.4\.0](securityhub-cis-controls-1.4.0.md)
+ [CIS AWS Foundations Benchmark v1\.2\.0 compared to v1\.4\.0](securityhub-standards-cis1.4-vs-cis1.2.md)
+ [CIS AWS Foundations Benchmark controls that you might want to disable](securityhub-standards-cis-to-disable.md)
+ [CIS AWS Foundations Benchmark security checks that are not supported in Security Hub](securityhub-standards-cis-checks-not-supported.md)