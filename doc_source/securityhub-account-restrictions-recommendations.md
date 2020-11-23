# Restrictions and recommendations<a name="securityhub-account-restrictions-recommendations"></a>

## Maximum number of member accounts<a name="master-maximum-member-accounts"></a>

Security Hub supports up to 5,000 member accounts per master account in each Region\.

## Accounts and Regions<a name="securityhub-accounts-regions"></a>

If you use AWS Organizations to manage accounts, the organization management account designates the Security Hub administrator account\. The Security Hub administrator account must be the same in all Regions\. However, the organization management account must designate the Security Hub administrator account separately in each Region\. The Security Hub administrator account also manages member accounts separately for each Region\.

For member accounts created by invitation, the master\-member account association is created only in the Region that the invitation is sent from\. The master account must enable Security Hub in each Region that you want to use it in\. The master account then invites each account to associate as a member account in that Region\.

## Restrictions on master\-member relationships<a name="account-relationship-restrictions"></a>

An account cannot be a Security Hub master account and member account at the same time\.

A member account can only be associated with one master account\. If an organization account is enabled by the Security Hub administrator account, the account cannot accept an invitation from another account\. If an account has accepted an invitation, the account cannot be enabled by the Security Hub administrator account\. It also cannot receive invitations from other accounts\.

For the manual invitation process, accepting a membership invitation is optional\.

## Coordinating master accounts across services<a name="securityhub-coordinate-masters"></a>

Security Hub aggregates findings from various AWS services, such as Amazon GuardDuty, Amazon Inspector, and Amazon Macie\. Security Hub also allows users to pivot from a GuardDuty finding to start an investigation in Amazon Detective\.

However, the master\-member relationships that you set up in these other services do not automatically apply to Security Hub\. Security Hub recommends that you use the same account as the master account for all of these services\. This master account should be an account that is responsible for security tools\. The same account should also be the aggregator account for AWS Config\.

For example, a user from GuardDuty master account A can see findings for GuardDuty member accounts B and C on the GuardDuty console\. If account A then enables Security Hub, users from account A do *not* automatically see GuardDuty findings for accounts B and C in Security Hub\. A Security Hub master\-member relationship is also required for these accounts\.

To do this, make account A the Security Hub master account and enable accounts B and C to become Security Hub member accounts\.