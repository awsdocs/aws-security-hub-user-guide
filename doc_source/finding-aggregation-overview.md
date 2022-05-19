# How cross\-Region aggregation works<a name="finding-aggregation-overview"></a>

Cross\-Region aggregation is configured by standalone accounts and by administrator accounts\. Member accounts inherit the cross\-Region aggregation configuration from their administrator account\.

When a member account is disassociated from the administrator account, then cross\-Region aggregation is stopped for the member account\. This is true even if the account had enabled cross\-Region aggregation before it became a member account\.

Cross\-Region aggregation is based on an aggregation Region and linked Regions\.

## Aggregating new data and replicating updates to data<a name="finding-aggregation-overview-replication"></a>

When cross\-Region aggregation is enabled, Security Hub aggregates new findings, insights, control compliance statuses, and security scores from the linked Regions to the aggregation Region\.

Security Hub also replicates updates to this data between the linked Regions and the aggregation Region\. Updates that occur in a linked Region are replicated to the aggregation Region\. Updates that occur in the aggregation Region are replicated back to the original linked Region\.

![\[As an example, this diagram shows how new findings are replicated from linked Regions to the aggregation Region, and how finding updates are replicated to and from linked Regions and the aggregation Region.\]](http://docs.aws.amazon.com/securityhub/latest/userguide/images/diagram-finding-aggregation.png)

If there are conflicting updates in the aggregation Region and the linked Region, then the most recent update is used\.

Cross\-Region aggregation does not add to the cost of Security Hub\. You are not charged when Security Hub replicates new data or updates\.

## Determining the accounts to aggregate data from<a name="finding-aggregation-overview-accounts"></a>

Security Hub only aggregates data from Regions where an account has Security Hub enabled\. Security Hub is not automatically enabled for an account based on the cross\-Region aggregation configuration\.

When an administrator account configures cross\-Region aggregation, Security Hub identifies the member accounts for that administrator account in the linked Regions\.

In each linked Region, every member account for that administrator account inherits the cross\-Region aggregation configuration\. Security Hub aggregates their findings, insights, control statuses, and security scores to the aggregation Region\.

If a member account from the aggregation Region is not a member account in a linked Region, then Security Hub does not aggregate data for that account from that Region\.

If you plan to use cross\-Region aggregation, and have multiple administrator accounts, then Security Hub recommends the following best practices:
+ Each administrator account has the same member accounts across Regions\.
+ Each administrator account has different member accounts\.
+ Each administrator account uses a different aggregation Region\.