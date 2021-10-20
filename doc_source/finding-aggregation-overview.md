# How finding aggregation works<a name="finding-aggregation-overview"></a>

Finding aggregation is configured by standalone accounts and by administrator accounts\. Member accounts inherit the finding aggregation configuration from their administrator account\.

When a member account is disassociated from the administrator account, then finding aggregation is stopped for the member account\. This is true even if the account had enabled finding aggregation before it became a member account\.

Finding aggregation is based on an aggregation Region and linked Regions\.

## Aggregating new findings and replicating updates to findings<a name="finding-aggregation-overview-replication"></a>

When finding aggregation is enabled, Security Hub aggregates new findings from the linked Regions to the aggregation Region\.

Security Hub also replicates finding updates between the linked Regions and the aggregation Region\. Updates that occur in a linked Region are replicated to the aggregation Region\. Updates that occur in the aggregation Region are replicated back to the original linked Region\.

![\[This diagram shows how new findings are replicated from linked Regions to the aggregation Region, and how finding updates are replicated to and from linked Regions and the aggregation Region.\]](http://docs.aws.amazon.com/securityhub/latest/userguide/images/diagram-finding-aggregation.png)

If there are conflicting updates in the aggregation Region and the linked Region, then the most recent update is used\.

Finding aggregation does not add to the cost of Security Hub\. You are not charged when Security Hub replicates findings or finding updates\.

## Determining the accounts to aggregate findings from<a name="finding-aggregation-overview-accounts"></a>

Security Hub only aggregates findings from Regions where an account has Security Hub enabled\. Security Hub is not automatically enabled for an account based on the finding aggregation configuration\.

When an administrator account configures finding aggregation, Security Hub identifies the member accounts for that administrator account in the linked Regions\.

In each linked Region, every member account for that administrator account inherits the finding aggregation configuration\. Security Hub aggregates their findings to the aggregation Region\.

If a member account from the aggregation Region is not a member account in a linked Region, then Security Hub does not aggregate findings for that account from that Region\.

If you plan to use cross\-Region finding aggregation, then Security Hub recommends the following best practices:
+ Each administrator account has the same member accounts in all Regions\.
+ Each administrator account has a different set of member accounts\.
+ Each administrator account uses a different aggregation Region\.