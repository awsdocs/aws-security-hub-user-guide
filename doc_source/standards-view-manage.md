# Viewing and managing security standards<a name="standards-view-manage"></a>

Security standards include a set of requirements to determine compliance with regulatory frameworks, industry best practices, or company policies\. AWS Security Hub maps these requirements to controls and runs security checks on controls to assess whether the requirements of a standard are being met\. A control may be enabled in one or more standards\. If you turn on consolidated control findings, Security Hub generates a single finding per security check even when a control is part of multiple enabled standards\. For more information, see [Consolidated control findings](controls-findings-create-update.md#consolidated-control-findings)\.

 For a list of available standards and the controls that apply to them, see [Standards reference](standards-reference.md)\. The **Security standards** page on the Security Hub console also shows all of the supported security standards in Security Hub and their enablement status\. For each enabled security standard, you can view a list of controls that are currently enabled in the standard and the status of those controls\. You can also view a list of controls that apply to the standard but are currently disabled\.

Security Hub generates a security score for each standard\. Administrator accounts see aggregated security scores and control statuses across their member accounts\. If you have set an aggregation Region, your security scores reflect the compliance status of controls across all linked Regions\. For more information, see [How security scores are calculated](standards-security-score.md#standard-security-score-calculation)\.

**Topics**
+ [Enabling and disabling security standards](securityhub-standards-enable-disable.md)
+ [Viewing details for a standard](securityhub-standards-view-controls.md)
+ [Enabling and disabling controls in specific standards](controls-configure.md)