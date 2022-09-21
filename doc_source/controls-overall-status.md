# Determining the overall status of a control from its findings<a name="controls-overall-status"></a>

Security Hub uses the `Compliance.Status` value from each control's findings to determine the overall control status\. The overall status is displayed in the control list for a standard and on the control details page\.

For administrator accounts, the control status reflects the aggregated status across both the administrator account and all of the member accounts\. If you have set an aggregation Region, control statuses in the aggregation Region reflect control statuses across all of your linked Regions\. Specifically, the overall status of a control appears as **Failed** if the control has one or more failed findings in at least one account and one linked Region\.

Security Hub typically generates the initial control status within 30 minutes after your first visit to the **Summary** page or **Security standards** page on the Security Hub console\. Statuses are only available for controls that are enabled when you visit those pages\. Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateStandardsControl.html) API operation to enable or disable a control\. In addition, AWS Config resource recording must be configured for the control status to appear\. After control statuses are generated for the first time, Security Hub updates the control status every 24 hours based on the findings from the previous 24 hours\. On the control details page, Security Hub displays a timestamp to indicate when the status of a control was last updated\.

**Note**  
It can take up to 24 hours after enabling a control for first\-time control statuses to be generated in the China Regions and AWS GovCloud \(US\) Region\.

## Values for Compliance\.Status<a name="controls-overall-status-compliance-status"></a>

The `Compliance.Status` for each finding is assigned one of the following values\.
+ `PASSED` – Automatically sets the Security Hub `Workflow.Status` to `RESOLVED`\.

  If `Compliance.Status` for a finding changes from `PASSED` to `FAILED`, `WARNING`, or `NOT_AVAILABLE`; and `Workflow.Status` was either `NOTIFIED` or `RESOLVED`; then Security Hub automatically sets `Workflow.Status` to `NEW`\.
+ `FAILED` – Indicates that the control did not pass the security check for this finding\.
+ `WARNING` – Indicates that the check was completed, but Security Hub cannot determine whether the resource is in a `PASSED` or `FAILED` state\.
+ `NOT_AVAILABLE` – Indicates that the check cannot be completed because a server failed, the resource was deleted, or the result of the AWS Config evaluation was `NOT_APPLICABLE`\.

  If the AWS Config evaluation result was `NOT_APPLICABLE`, then Security Hub automatically archives the finding\.

## Values for the control status<a name="controls-overall-status-values"></a>

Security Hub uses the compliance status of the control findings to calculate an overall control status\. When it calculates the overall control status, Security Hub ignores findings that have a `Workflow.Status` of `SUPPRESSED`\.

The available values for the overall control status are as follows:
+ **Passed** – Indicates that all findings have a `Compliance.Status` of `PASSED`\.
+ **Failed** – Indicates that at least one finding has a `Compliance.Status` of `FAILED`\.
+ **Unknown** – Indicates that at least one finding has a `Compliance.Status` of `WARNING` or `NOT_AVAILABLE`\. No findings are `FAILED`\.
+ **No data** – Indicates that there are no findings for the control\. For example, a new control has this status until it begins to generate findings\. A control also has this status if all of the findings are `SUPPRESSED`\.
+ **Disabled** – Indicates that the control is deactivated in the current account and Region\. This means that no security checks are currently being performed for this control is this account and Region\. However, a disabled control may have a value for `Compliance.Status` for up to 24 hours after disablement\.