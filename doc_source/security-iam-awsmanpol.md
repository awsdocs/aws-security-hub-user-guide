# AWS managed policies for AWS Security Hub<a name="security-iam-awsmanpol"></a>

To add permissions to users, groups, and roles, it is easier to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need\. To get started quickly, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the **ReadOnlyAccess** AWS managed policy provides read\-only access to all AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.



## AWS managed policy: AWSSecurityHubFullAccess<a name="security-iam-awsmanpol-awssecurityhubfullaccess"></a>

You can attach the `AWSSecurityHubFullAccess` policy to your IAM identities\.

This policy grants administrative permissions that allow a principal full access to all Security Hub actions\. This policy must be attached to a principal before they enable Security Hub manually for their account\. For example, principals with these permissions can both view and update the status of findings\. They can configure custom insights, and enable integrations\. They can enable and disable standards and controls\. Principals for an administrator account can also manage member accounts\.

**Permissions details**

This policy includes the following permissions\.
+ `securityhub` – Allows principals full access to all Security Hub actions\.
+ `iam` – Allows principals to create a service\-linked role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "securityhub:*",
            "Resource": "*" 
        },
        {
            "Effect": "Allow",
            "Action": "iam:CreateServiceLinkedRole",
            "Resource": "*",
            "Condition": {
                "StringLike": {
                    "iam:AWSServiceName": "securityhub.amazonaws.com"
                }
            }
        }
    ]
}
```

## Security Hub managed policy: AWSSecurityHubReadOnlyAccess<a name="security-iam-awsmanpol-awssecurityhubreadonlyaccess"></a>

You can attach the `AWSSecurityHubReadOnlyAccess` policy to your IAM identities\.

This policy grants read\-only permissions that allow users to view information in Security Hub\. Principals with this policy attached cannot make any updates in Security Hub\. For example, principals with these permissions can view the list of findings associated with their account, but cannot change the status of a finding\. They can view the results of insights, but cannot create or configure custom insights\. They cannot configure controls or product integrations\.

**Permissions details**

This policy includes the following permissions\.
+ `securityhub` – Allows users to perform actions that return either a list of items or details about an item\. This includes API operations that start with `Get`, `List`, or `Describe`\.

```
{
    "Version": "2012-10-17",
    "Statement": [ 
        {
            "Effect": "Allow",
            "Action": [
                "securityhub:Get*",
                "securityhub:List*",
                "securityhub:Describe*"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSSecurityHubOrganizationsAccess<a name="security-iam-awsmanpol-awssecurityhuborganizationsaccess"></a>

You can attach the `AWSSecurityHubOrganizationsAccess` policy to your IAM identities\.

This policy grants administrative permissions in AWS Organizations that are required to support the Security Hub integration with Organizations\.

These permissions allow the organization management account to designate the delegated administrator account for Security Hub\. They also allow the delegated Security Hub administrator account to enable organization accounts as member accounts\.

This policy only provides the permissions for Organizations\. The organization management account and delegated Security Hub administrator account also require permissions for the associated actions in Security Hub\. These permissions can be granted using the `AWSSecurityHubFullAccess` managed policy\.

**Permissions details**

This policy includes the following permissions\.
+ `organizations:ListAccounts` – Allows principals to retrieve the list of accounts that belong to an organization\.
+ `organizations:DescribeOrganization` – Allows principals to retrieve information about the organization configuration\.
+ `organizations:EnableAWSServiceAccess` – Allows principals to enable the Security Hub integration with Organizations\.
+ `organizations:RegisterDelegatedAdministrator` – Allows principals to designate the delegated administrator account for Security Hub\.
+ `organizations:DeregisterDelegatedAdministrator` – Allows principals to remove the delegated administrator account for Security Hub\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "organizations:ListAccounts",
                "organizations:DescribeOrganization"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "organizations:EnableAWSServiceAccess",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "organizations:ServicePrincipal": "securityhub.amazonaws.com"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "organizations:RegisterDelegatedAdministrator",
                "organizations:DeregisterDelegatedAdministrator"
            ],
            "Resource": "arn:aws:organizations::*:account/o-*/*",
            "Condition": {
            "StringEquals": {
                "organizations:ServicePrincipal": "securityhub.amazonaws.com"
                }
            }
        }
    ]
}
```

## AWS managed policy: AWSSecurityHubServiceRolePolicy<a name="security-iam-awsmanpol-awssecurityhubservicerolepolicy"></a>

You can't attach `AWSSecurityHubServiceRolePolicy` to your IAM entities\. This policy is attached to a service\-linked role that allows Security Hub to perform actions on your behalf\. For more information, see [Using service\-linked roles for AWS Security Hub](using-service-linked-roles.md)\.

This policy grants administrative permissions that allow the service\-linked role to perform the security checks for Security Hub controls\.

**Permissions details**

This policy includes permissions to do the following:
+ `cloudtrail` – Retrieve information about CloudTrail trails\.
+ `cloudwatch` – Retrieve the current CloudWatch alarms\.
+ `logs` – Retrieve the metric filters for CloudWatch logs\.
+ `sns` – Retrieve the list of subscriptions to an SNS topic\.
+ `config` – Retrieve information about configuration recorders, resources, and AWS Config rules\. Also allows the service\-linked role to create and delete AWS Config rules, and to run evaluations against the rules\.
+ `iam` – Get and generate credential reports for accounts\.
+ `organizations` – Retrieve account information for an organization\.

```
{
    "Version": "2012-10-17",
    "Statement": [ 
        {
            "Effect": "Allow",
            "Action": [
                "cloudtrail:DescribeTrails",
                "cloudtrail:GetTrailStatus",
                "cloudtrail:GetEventSelectors",
                "cloudwatch:DescribeAlarms",
                "logs:DescribeMetricFilters",
                "sns:ListSubscriptionsByTopic",
                "config:DescribeConfigurationRecorders",
                "config:DescribeConfigurationRecorderStatus",
                "config:DescribeConfigRules",
                "config:BatchGetResourceConfig",
                "config:PutEvaluations",
                "config:SelectResourceConfig",
                "iam:GenerateCredentialReport",
                "iam:GetCredentialReport",
                "organizations:ListAccounts",
                "organizations:DescribeAccount",
                "organizations:DescribeOrganization"
            ],
            "Resource": "*"
        }
        {
            "Effect": "Allow",
            "Action": [
                "config:PutConfigRule",
                "config:DeleteConfigRule",
                "config:GetComplianceDetailsByConfigRule",
                "config:DescribeConfigRuleEvaluationStatus"
            ],
            "Resource": "arn:aws:config:*:*:config-rule/aws-service-rule/*securityhub*"
        }
    ]
}
```

## Security Hub updates to AWS managed policies<a name="security-iam-awsmanpol-updates"></a>

View details about updates to AWS managed policies for Security Hub since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the Security Hub [Document history](doc-history.md) page\.








| Change | Description | Date | 
| --- | --- | --- | 
|  `AWSSecurityHubServiceRolePolicy` – Update to an existing policy  |  Security Hub moved the existing `config:PutEvaluations` permission to a different statement within the policy\. The `config:PutEvaluations` permission is now applied to all resources\.  | July 14, 2021 | 
|  [`AWSSecurityHubServiceRolePolicy`](#security-iam-awsmanpol-awssecurityhubservicerolepolicy) – Update to an existing policy  |  Security Hub added a new permission to allow the service\-linked role to deliver evaluation results to AWS Config\.  | June 29, 2021 | 
|  [`AWSSecurityHubServiceRolePolicy`](#security-iam-awsmanpol-awssecurityhubservicerolepolicy) – Added to the list of managed policies  |  Added information about the managed policy `AWSSecurityHubServiceRolePolicy`, which is used by the Security Hub service\-linked role\.  | June 11, 2021 | 
|  [`AWSSecurityHubOrganizationsAccess` ](#security-iam-awsmanpol-awssecurityhuborganizationsaccess) – New policy  |  Security Hub added a new policy that grants permissions that are needed for the Security Hub integration with Organizations\.  | March 15, 2021 | 
|  Security Hub started tracking changes  |  Security Hub started tracking changes for its AWS managed policies\.  | March 15, 2021 | 