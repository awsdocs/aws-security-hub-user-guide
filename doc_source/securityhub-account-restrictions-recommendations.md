# Restrictions and recommendations<a name="securityhub-account-restrictions-recommendations"></a>

## Restrictions on master and member accounts<a name="securityhub-master-member-restrictions"></a>

Security Hub supports up to 1,000 member accounts per master account per Region\.

The master\-member account association is created only in the Region that the invitation was sent from\. You must enable Security Hub in each Region that you want to use it in\. Then invite each account to associate as a member account in each Region\.

An account cannot be a Security Hub master account and member account at the same time\.

An account can accept only one Security Hub membership invitation\. Accepting a membership invitation is optional\.

## Coordinating master accounts across services<a name="securityhub-coordinate-masters"></a>

Security Hub aggregates findings from various AWS services, such as Amazon GuardDuty, Amazon Inspector, and Amazon Macie\. Security Hub also allows users to pivot from a GuardDuty finding to start an investigation in Amazon Detective\.

However, the master\-member relationships that you set up in these other services do not automatically apply to Security Hub\. Security Hub recommends that you use the same account as the master account for all of these services\. This master account should be an account that is responsible for security tools\. The same account should also be the aggregator account for AWS Config\.

For example, a user from GuardDuty master account A can see findings for GuardDuty member accounts B and C on the GuardDuty console\. If account A then enables Security Hub, users from account A do *not* automatically see GuardDuty findings for accounts B and C in Security Hub\. A Security Hub master\-member relationship is also required for these accounts\. To do this, first enable Security Hub in all three accounts \(A, B, and C\)\. Next, make account A the Security Hub master account and invite accounts B and C to become Security Hub member accounts\.