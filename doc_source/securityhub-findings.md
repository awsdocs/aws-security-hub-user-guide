# Findings in AWS Security Hub<a name="securityhub-findings"></a>

AWS Security Hub eliminates the complexity of addressing large volumes of findings from multiple providers\. It reduces the effort required to manage and improve the security of all of your AWS accounts, resources, and workloads\.

Security Hub receives findings from the following sources\.
+ Integrations with AWS security services that you enable\. See [Available AWS service integrations](securityhub-internal-providers.md)\.
+ Integrations with third\-party products that you enable\. See [Available third\-party partner product integrations](securityhub-partner-providers.md)\.
+ Custom integrations that you configure\. See [Using custom product integrations to send findings to AWS Security Hub](securityhub-custom-providers.md)\.
+ Security Hub checks against enabled controls\. See [Results of security checks](securityhub-standards-results.md)\.

Security Hub consumes findings using a standard findings format called the AWS Security Finding Format\. For more information about the finding format, see [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\.

Security Hub correlates the findings across integrated products to prioritize the most important ones\.

Finding providers can update findings to reflect additional instances of the finding\. You can update findings to provide details about your investigation and its results\.

**Topics**
+ [Creating and updating findings in AWS Security Hub](securityhub-findings-update-types.md)
+ [Viewing findings in AWS Security Hub](securityhub-findings-viewing.md)
+ [Taking action on findings in AWS Security Hub](securityhub-findings-taking-action.md)
+ [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)