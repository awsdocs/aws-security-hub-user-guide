# Restrictions and recommendations<a name="securityhub-account-restrictions-recommendations"></a>

## Maximum number of member accounts<a name="admin-maximum-member-accounts"></a>

Security Hub supports up to 5,000 member accounts per administrator account in each Region\.

## Accounts and Regions<a name="securityhub-accounts-regions"></a>

### Membership by organization<a name="accounts-regions-orgs"></a>

If you are enrolled in AWS Organizations, the organization management account can designate a Security Hub administrator account in each Region\.

The Security Hub administrator account for a Region also becomes that Region's delegated administrator account for Security Hub in Organizations\. The exception is if the organization management account designates itself as the Security Hub administrator account\. The organization management account cannot be a delegated administrator in Organizations\.

Once the delegated administrator account for a Region is set in Organizations, the organization management account can choose either the delegated administrator account or itself as the Security Hub administrator account in that Region\. We recommend that you choose the same delegated administrator account in all Regions\.

The Security Hub administrator account manages member accounts separately in each Region\.

### Membership by invitation<a name="accounts-regions-invitation"></a>

For member accounts created by invitation, the administrator\-member account association is created only in the Region that the invitation is sent from\. The administrator account must enable Security Hub in each Region that you want to use it in\. The administrator account then invites each account to associate as a member account in that Region\.

## Restrictions on administrator\-member relationships<a name="account-relationship-restrictions"></a>

An account cannot be an administrator account and a member account at the same time\.

A member account can only be associated with one administrator account\. If an organization account is enabled by the Security Hub administrator account, the account cannot accept an invitation from another account\. If an account has accepted an invitation, the account cannot be enabled by the Security Hub administrator account for the organization\. It also cannot receive invitations from other accounts\.

For the manual invitation process, accepting a membership invitation is optional\.

## Coordinating administrator accounts across services<a name="securityhub-coordinate-admins"></a>

Security Hub aggregates findings from various AWS services, such as Amazon GuardDuty, Amazon Inspector, and Amazon Macie\. Security Hub also allows users to pivot from a GuardDuty finding to start an investigation in Amazon Detective\.

However, the administrator\-member relationships that you set up in these other services do not automatically apply to Security Hub\. Security Hub recommends that you use the same account as the administrator account for all of these services\. This administrator account should be an account that is responsible for security tools\. The same account should also be the aggregator account for AWS Config\.

For example, a user from the GuardDuty administrator account A can see findings for GuardDuty member accounts B and C on the GuardDuty console\. If account A then enables Security Hub, users from account A do *not* automatically see GuardDuty findings for accounts B and C in Security Hub\. A Security Hub administrator\-member relationship is also required for these accounts\.

To do this, make account A the Security Hub administrator account and enable accounts B and C to become Security Hub member accounts\.