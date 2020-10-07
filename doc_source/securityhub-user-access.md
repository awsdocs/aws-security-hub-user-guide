# Using IAM policies to delegate Security Hub access to IAM identities<a name="securityhub-user-access"></a>

By default, access to the Security Hub resources is restricted to the owner of the account that the resources were created in\.

If you're the owner, you can choose to grant full or limited access to Security Hub to the various IAM identities in your account\. For more information about creating IAM access policies, see [Controlling access using policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_controlling.html)\.

## AWS managed \(predefined\) policies for Security Hub<a name="securityhub-managedpolicies"></a>

AWS addresses many common use cases by providing standalone IAM policies that AWS creates and administers\. These *managed policies* grant necessary permissions for common use cases so that you don't have to investigate which permissions are needed\. For more information, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to users in your account, are specific to Security Hub:
+ `AWSSecurityHubFullAccess` – Provides access to all Security Hub functionality
+ `AWSSecurityHubReadOnlyAccess` – Provides read\-only access to Security Hub

## Resources defined by Security Hub<a name="resources"></a>

The following resource types are defined by this service and can be used in the `Resource` element of IAM permission policy statements\.


|  Resource type  |  ARN  | 
| --- | --- | 
|   hub  |  `arn:${Partition}:securityhub:${Region}:${Account}:hub/default`  | 
|   product  |  `arn:${Partition}:securityhub:${Region}:${Account}:product/${Company}/${ProductId}`  | 

## Condition keys defined by Security Hub<a name="conditions"></a>

Security Hub defines the following condition keys that you can use in the `Condition` element of an IAM policy\.

You can use these keys to further refine the conditions under which the policy statement applies\.


|  Condition keys  |  Description  |  Type  | 
| --- | --- | --- | 
|   securityhub:TargetAccount  |  The ID of the AWS account associated with a finding\. In the AWS Security Finding Format \(ASFF\), this the `AwsAccountId` field\.  |  String  | 
|  securityhub:ASFFSyntaxPath/$\{ASFFSyntaxPath\}  |  The path to an ASFF field for which to restrict updates from [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.  |  String  | 