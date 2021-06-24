# Determining the security score for a security standard<a name="standards-security-score"></a>

On the **Security standards** page, each enabled standard displays a security score from 0–100%\. The standard details page also displays the overall security score\.

Security Hub updates the calculated security score every 24 hours\. Security Hub displays a timestamp to indicate when the current security score was last updated\.

When the standard is first enabled, Security Hub cannot calculate the initial security score until the standard status is `READY`\. The initial security score is available within 24 hours after that\. To see the current status of the standard, use the `GetEnabledStandards` API operation\.

## How the security score is calculated<a name="standard-security-score-calculation"></a>

The security score represents the proportion of **Passed** controls to enabled controls\. The score is displayed as a percentage\. For example, if 10 controls are enabled for a standard, and seven of those controls are in a **Passed** state, then the security score is 70%\.

The security score calculation omits enabled controls that do not have any findings \(overall status is **No data**\)\. For example, a standard has 12 controls enabled\. Six of those controls are in a **Passed** state\. Two controls have no data\. Because the calculation omits the controls without data, the security score is 60%\.

## Security score for administrator accounts<a name="standard-security-score-admin"></a>

For the administrator account, the security score for a standard is an aggregated score across both the administrator account and all of the member accounts\.

## Security scores on the Summary page<a name="standard-security-score-summary-page"></a>

On the **Summary** page, the **Security standards** card displays the security scores for each enabled standard\. It also displays a consolidated security score that represents the proportion of passed controls to enabled controls across all of the enabled standards\.