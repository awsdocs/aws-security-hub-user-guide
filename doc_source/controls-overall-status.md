# Determining the overall status of a control from its findings<a name="controls-overall-status"></a>

Security Hub uses the `Compliance.Status` value from each control's findings to determine the overall status of the control\. The overall status is displayed in the control list for a standard and on the control details page\.

For administrator accounts, the status for each control is the aggregated status across both the administrator account and all of the member accounts\.

Security Hub calculates the control status every 24 hours\. The calculation uses the findings from the previous 24 hours\. On the standard details page and the control details page, Security Hub displays a timestamp to indicate when the status was last updated\.

## Values for Compliance\.Status<a name="controls-overall-status-compliance-status"></a>

`Compliance.Status` is assigned one of the following values\.
+ `PASSED` – Automatically sets the Security Hub `Workflow.Status` to `RESOLVED`\.

  If `Compliance.Status` for a finding changes from `PASSED` to `FAILED`, `WARNING`, or `NOT_AVAILABLE`; and `Workflow.Status` was either `NOTIFIED` or `RESOLVED`; then Security Hub automatically sets `Workflow.Status` to `NEW`\.
+ `FAILED`
+ `WARNING` – Indicates that the check was completed, but Security Hub cannot determine whether the resource is in a `PASSED` or `FAILED` state\.
+ `NOT_AVAILABLE` – Indicates that the check cannot be completed because a server failed, the resource was deleted, or the result of the AWS Config evaluation was `NOT_APPLICABLE`\.

  If the AWS Config evaluation result was `NOT_APPLICABLE`, then Security Hub automatically archives the finding\.

## Values for the control status<a name="controls-overall-status-values"></a>

When it calculates the overall status, Security Hub ignores findings that have a `Workflow.Status` of `SUPPRESSED`\.

The available values for the overall status are as follows:
+ **Passed** – Indicates that all findings have a `Compliance.Status` of `PASSED`\.
+ **Failed** – Indicates that at least one finding has a `Compliance.Status` of `FAILED`\.
+ **Unknown** – Indicates that at least one finding has a `Compliance.Status` of `WARNING` or `NOT_AVAILABLE`\. No findings are `FAILED`\.
+ **No data** – Indicates that there are no findings for the control\. For example, a new control has this status until it begins to generate findings\. A control also has this status if all of the findings are `SUPPRESSED`\.