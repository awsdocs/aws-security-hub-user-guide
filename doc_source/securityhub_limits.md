# Security Hub quotas<a name="securityhub_limits"></a>

The following are Security Hub quotas per AWS account per AWS Region\. 

## Maximum quotas<a name="maximum_quotas"></a>

The following Security Hub quotas are per AWS account per Region\.


|  Resource  |  Quota  |  Comments  | 
| --- | --- | --- | 
|  Number of Security Hub member accounts  |  11,000  |  The maximum number of Security Hub member accounts that can be added for each Security Hub administrator account in each Region\. To add more than 5,000 accounts, you must contact AWS Support to allow list your Organization\. This is a hard quota\. You cannot request an increase to the maximum allowed number of Security Hub member accounts\.  | 
|  Number of Security Hub outstanding invitations  |  1,000  |  The maximum number of outstanding Security Hub member account invitations that can be sent per administrator account per Region\. This is a hard quota\. You cannot request an increase to the allowed number of Security Hub outstanding invitations\.  | 
|  Number of custom actions  |  50  |  The maximum number of Security Hub custom actions that can be created\. This is a hard quota\. You cannot request an increase to the number of custom actions\.  | 
|  Number of custom insights  |  100  |  The maximum number of user\-defined custom insights that can be created\. This is a hard quota\. You cannot request an increase to the allowed number of Security Hub custom insights\.  | 
|  Number of insight results  |  100  |  The maximum number of aggregated results returned for the `GetInsightsResults` API operation\. This is a hard quota\. You cannot request an increase to the number of insight results\.  | 
|  Security Hub finding retention time  |  90 days  |  Findings are deleted 90 days after the most recent update or 90 days after the creation date if no update occurs\. To store findings for longer than 90 days, you can configure a rule in EventBridge that routes findings to your Amazon S3 bucket\.  | 

## Rate quotas<a name="rate_quotas"></a>

The following Security Hub quotas are per AWS account per Region\.


|  Request type  |  Rate limit quota \(per second\)  |  Burst limit quota \(per second\)  | 
| --- | --- | --- | 
|  `BatchEnableStandards`  |  1  |  1  | 
|  `GetFindings`  |  3  |  6  | 
|  `BatchImportFindings`  |  10  |  30  | 
|  `BatchUpdateFindings`  |  10  |  30  | 
|  `UpdateStandardsControl`  |  1  |  5  | 
|  All other request types  |  10  |  30  | 

If you have set up [Cross\-Region aggregation](finding-aggregation.md), one call to `BatchImportFindings` and `BatchUpdateFindings` impacts linked Regions and the aggregation Region\. The `GetFindings` operation retrieves findings from linked Regions and the aggregation Region\. However, the `BatchEnableStandards` and `UpdateStandardsControl` operations are Region\-specific\.