# Using service\-linked roles for AWS Security Hub<a name="using-service-linked-roles"></a>

AWS Security Hub uses AWS Identity and Access Management \(IAM\) [service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to Security Hub\. Service\-linked roles are predefined by Security Hub and include all the permissions that Security Hub requires to call other AWS services on your behalf\. 

A service\-linked role makes setting up Security Hub easier because you don't have to manually add the necessary permissions\. Security Hub defines the permissions of its service\-linked role, and unless the permissions are defined otherwise, only Security Hub can assume the role\. The defined permissions include the trust policy and the permissions policy, and you can't attach that permissions policy to any other IAM entity\.

Security Hub supports using service\-linked roles in all of the Regions where Security Hub is available\. For more information, see [Supported Regions](securityhub-regions.md)\.

You can delete the Security Hub service\-linked role only after first disabling Security Hub in all Regions where it's enabled\. This protects your Security Hub resources because you can't inadvertently remove permissions to access them\.

For information about other services that support service\-linked roles, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide* and locate the services that have **Yes** in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-linked role permissions for Security Hub<a name="slr-permissions"></a>

Security Hub uses the service\-linked role named `AWSServiceRoleForSecurityHub`\. It's a service\-linked role required for AWS Security Hub to access your resources\.

The `AWSServiceRoleForSecurityHub` service\-linked role trusts the following services to assume the role:
+ `securityhub.amazonaws.com`

The role permissions policy allows Security Hub to complete the following actions on the specified resources:
+ Action: `cloudtrail:DescribeTrails` 
+ Action: `cloudtrail:GetTrailStatus` 
+ Action: `cloudtrail:GetEventSelectors` 
+ Action: `cloudwatch:DescribeAlarms` 
+ Action: `logs:DescribeMetricFilters` 
+ Action: `sns:ListSubscriptionsByTopic` 
+ Action: `config:DescribeConfigurationRecorders` 
+ Action: `config:DescribeConfigurationRecorderStatus` 
+ Action: `config:DescribeConfigRules` 
+ Action: `config:BatchGetResourceConfig` 
+ Resources: `*` 

And:
+ Action: `config:PutConfigRule`
+ Action: `config:DeleteConfigRule`
+ Action: `config:GetComplianceDetailsByConfigRule`
+ Action: `config:DescribeConfigRuleEvaluationStatus`
+ Resources: `arn:aws:config:*:*:config-rule/aws-service-rule/*securityhub*`

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For the `AWSServiceRoleForSecurityHub` service\-linked role to be successfully created, the IAM identity that you use Security Hub with must have the required permissions\. To grant the required permissions, attach the following policy to this IAM user, group, or role\.

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

## Creating a service\-linked role for Security Hub<a name="create-slr"></a>

The `AWSServiceRoleForSecurityHub` service\-linked role is automatically created when you enable Security Hub for the first time or enable Security Hub in a supported Region where you previously didn't have it enabled\. You can also create the `AWSServiceRoleForSecurityHub` service\-linked role manually using the IAM console, the IAM CLI, or the IAM API\. 

**Important**  
The service\-linked role that is created for the Security Hub master account doesn't apply to the Security Hub member accounts\.

For more information about creating the role manually, see [Creating a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide*\.

## Editing a service\-linked role for Security Hub<a name="edit-slr"></a>

Security Hub doesn't allow you to edit the `AWSServiceRoleForSecurityHub` service\-linked role\. After you create a service\-linked role, you can't change the name of the role because various entities might reference the role\. However, you can edit the description of the role by using IAM\. For more information, see [Editing a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting a service\-linked role for Security Hub<a name="delete-slr"></a>

If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way, you don't have an unused entity that isn't actively monitored or maintained\. 

**Important**  
To delete the `AWSServiceRoleForSecurityHub` service\-linked role, you must first disable Security Hub in all Regions where it's enabled\.  
If Security Hub isn't disabled when you try to delete the service\-linked role, the deletion fails\. For more information, see [Disabling AWS Security Hub](securityhub-disable.md)\.

When you disable Security Hub, the `AWSServiceRoleForSecurityHub` service\-linked role is *not* automatically deleted\. If you enable Security Hub again, it starts using the existing `AWSServiceRoleForSecurityHub` service\-linked role\.

**To manually delete the service\-linked role using IAM**

Use the IAM console, the IAM CLI, or the IAM API to delete the `AWSServiceRoleForSecurityHub` service\-linked role\. For more information, see [Deleting a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.