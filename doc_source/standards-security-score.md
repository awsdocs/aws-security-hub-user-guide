# Determining the security score for a security standard<a name="standards-security-score"></a>

On the **Security standards** page, Security Hub displays a security score from 0–100% for each enabled standard\. The **Summary** page also displays the overall security score across all enabled standards\.

When you enable Security Hub, Security Hub calculates the initial security score for a standard within 30 minutes after your first visit to the **Summary** page or **Security standards** page on the Security Hub console\. Scores are only generated for standards that are enabled when you visit those pages\. To view a list of standards that are currently enabled, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetEnabledStandards.html) API operation\. In addition, AWS Config resource recording must be configured for scores to appear\. The overall security score is the average of the standard security scores\.

After first\-time score generation, Security Hub updates the security score every 24 hours\. Security Hub displays a timestamp to indicate when a security score was last updated\.

**Note**  
It can take up to 24 hours for first\-time security scores to be generated in the China Regions and AWS GovCloud \(US\) Region\.

## How security scores are calculated<a name="standard-security-score-calculation"></a>

Security scores represent the proportion of **Passed** controls to enabled controls\. The score is displayed as a percentage\. For example, if 10 controls are enabled for a standard, and seven of those controls are in a **Passed** state, then the security score for the standard is 70%\.

If your account is an administrator account, security scores account for control findings in all member accounts\.

If you have set an aggregation Region, the overall security score is an aggregated score  that accounts for findings in all linked Regions\. Similarly,  the security score for each standard is an aggregated score that accounts for findings associated  with that standard in all linked Regions\. Note that if your account is an administrator  account, the security scores account for all member accounts and all Regions\.

Security score calculation omits enabled controls that do not have any findings \(overall status is **No data**\)\. For example, a standard has 12 controls enabled\. Six of those controls are in a **Passed** state\. Two controls have no data\. Because the calculation omits the controls without data, the security score is 60%\.

## Security scores for administrator accounts<a name="standard-security-score-admin"></a>

For the administrator account, the overall security score and security scores for specific standards are aggregated scores across both the administrator account and all of the member accounts\.

## Security scores if you have set an aggregation Region<a name="standard-security-aggregation-region"></a>

If you have set an aggregation Region, the overall security score and the security scores for each standard reflect  findings from all linked Regions\. If your account is an administrator account, the security scores also account for all member accounts\.

## Security scores on the Summary page<a name="standard-security-score-summary-page"></a>

On the **Summary** page, the **Security standards** card displays the security scores for each enabled standard\. It also displays a consolidated security score that represents the proportion of passed controls to enabled controls across all of the enabled standards\.