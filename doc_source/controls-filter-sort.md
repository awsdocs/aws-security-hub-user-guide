# Filtering and sorting the list of controls<a name="controls-filter-sort"></a>

On the **Controls** page, you can see a list of your controls\. You can filter and sort the list to focus on a specific subset of controls\. 
+ **Enabled** \(controls that are enabled in at least one enabled standard\)
+ **Failed** \(controls with a `Failed` status\)
+ **Unknown** \(controls with an `Unknown` status\)
+ **Passed** \(controls with a `Passed` status\)
+ **Disabled** \(controls that are disabled in all standards\)
+ **No data** \(controls with no findings\)
+ **All** \(all controls, both enabled and disabled, and without regard to control status or findings count\)

For more information about control status, see [Determining the overall status of a control from its findings](controls-overall-status.md)\.

If you're using the integration with AWS Organizations and are logged in to the AWS Security Hub administrator account, the **Enabled** tab includes controls that are enabled in at least one member account\. If you have set an aggregation Region, the **Enabled** tab includes controls that are enabled in at least one linked Region\.

The **Failed** tab is displayed by default\. On each tab, the controls are by default sorted by severity, from **Critical** to **Low**\. You can also sort controls by control ID, compliance status, workflow status, or other specific ASFF fields as filters\.

Choosing the option next to the control brings up a side panel which displays the standards in which the control is currently enabled\. You can also see the standards in which the control is currently disabled\. From this panel, you can disable a control by disabling it in all standards\. For more information about enabling and disabling controls across standards, see [Enabling and disabling controls in all standards](securityhub-standards-enable-disable-controls.md)\. For administrator accounts, the information presented in the side panel reflects all member accounts\.

On the Security Hub API, run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListSecurityControlDefinitions.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ListSecurityControlDefinitions.html) to get back a list of control IDs\. Once you have the control IDs you are interested in, run [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchGetSecurityControls.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchGetSecurityControls.html) to get data about that subset of controls for the current AWS account and AWS Region\.