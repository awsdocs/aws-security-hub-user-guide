# Effects of an administrator\-member relationship<a name="accounts-admin-member-relationship"></a>

An administrator account is granted permission to view the findings that are associated with their member accounts\. This also allows the administrator account to view insight results and control statuses from across their member accounts\. Administrator accounts can also take action on their member accounts' findings\.

Security Hub does not copy member account findings into the administrator account\. Administrator accounts also cannot change the Security Hub configuration for member accounts\. For more information, see [Allowed actions for accounts](securityhub-accounts-allowed-actions.md)\.

In Security Hub, all findings are ingested into a specific Region for a specific account\.

In each Region, the administrator account can view and manage findings for their member accounts in that Region\.

In an aggregation Region, the administrator account can view and manage member account findings from linked Regions that are replicated to the aggregation Region\. For more information about cross\-Region aggregation, see [Cross\-Region aggregation](finding-aggregation.md)\.