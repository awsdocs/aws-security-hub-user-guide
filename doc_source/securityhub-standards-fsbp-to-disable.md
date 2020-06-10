# AWS Foundational Best Practices controls that you might want to disable<a name="securityhub-standards-fsbp-to-disable"></a>

To save on the cost of AWS Config, you can disable recording of global resources in all but one Region, and then disable these controls that deal with global resources in all Regions except for the Region that runs global recording\.
+ [\[IAM\.1\] IAM policies should not allow full "\*" administrative privileges](securityhub-standards-fsbp-controls.md#fsbp-iam-1)
+ [\[IAM\.2\] IAM users should not have IAM policies attached](securityhub-standards-fsbp-controls.md#fsbp-iam-2)
+ [\[IAM\.3\] IAM users' access keys should be rotated every 90 days or less](securityhub-standards-fsbp-controls.md#fsbp-iam-3)
+ [\[IAM\.4\] IAM root user access key should not exist](securityhub-standards-fsbp-controls.md#fsbp-iam-4)
+ [\[IAM\.5\] MFA should be enabled for all IAM users that have a console password](securityhub-standards-fsbp-controls.md#fsbp-iam-5)
+ [\[IAM\.6\] Hardware MFA should be enabled for the root user](securityhub-standards-fsbp-controls.md#fsbp-iam-6)
+ [\[IAM\.7\] Password policies for IAM users should have strong configurations](securityhub-standards-fsbp-controls.md#fsbp-iam-7)

If you disable these controls and disable recording of global resources in a particular Region, you should also disable [\[Config\.1\] AWS Config should be enabled](securityhub-standards-fsbp-controls.md#fsbp-config-1)\. This is because [\[Config\.1\] AWS Config should be enabled](securityhub-standards-fsbp-controls.md#fsbp-config-1) requires recording of global resources in order to pass\.