# Service\-Managed Standard: AWS Control Tower<a name="service-managed-standard-aws-control-tower"></a>

## What is Service\-Managed Standard: AWS Control Tower?<a name="aws-control-tower-standard-summary"></a>

If you use AWS Control Tower and create this standard, you can configure the preventive controls of AWS Control Tower alongside the detective controls of Security Hub in the AWS Control Tower console\.

Preventive controls help ensure that your AWS accounts maintain compliance because they flag actions that may lead to policy violations or misconfigurations\. Detective controls, such as those offered by Security Hub, detect noncompliance of resources \(for example, misconfigurations\) within your AWS accounts\. By enabling preventive and detective controls for your AWS environment, you can enhance your security posture at different stages of development\.

**Tip**  
Service\-managed standards differ from standards that AWS Security Hub manages\. For example, you must create and delete a service\-managed standard in the managing service\. However, you may configure controls for the standard in both the managing service and Security Hub\. For more information about service\-managed standards, see [Service\-managed standards](service-managed-standards.md)\.

In the Security Hub console and API, you can view Service\-Managed Standard: AWS Control Tower alongside other Security Hub standards\.

## Creating the standard<a name="aws-control-tower-standard-creation"></a>

This standard is available only for AWS Control Tower customers who have created the standard in the AWS Control Tower console\. AWS Control Tower creates the standard for you when you enable the first Security Hub control in the AWS Control Tower console\. At this time, if you haven’t already enabled Security Hub, AWS Control Tower also enables Security Hub for you\.

If you haven't set up AWS Control Tower, you won't be able to view or access this standard in the Security Hub console, Security Hub API, or AWS CLI\. Even if you have set up AWS Control Tower, you won't be able to access this standard in the Security Hub console, Security Hub API, or AWS CLI without first creating the standard in the AWS Control Tower console\.

This standard is only available in the [AWS Regions where AWS Control Tower is available](https://docs.aws.amazon.com/controltower/latest/userguide/region-how.html), including AWS GovCloud \(US\)\.

## Enabling and disabling controls for the standard<a name="aws-control-tower-standard-managing-controls"></a>

After you've created the standard in the AWS Control Tower console, you can begin enabling and disabling controls for it in either service\. You can also view your created standard in the Security Hub console, Security Hub API, and AWS CLI\.

After you first create the standard, it doesn't have any controls that are automatically enabled\. In addition, when Security Hub adds new controls, they aren't automatically enabled for Service\-Managed Standard: AWS Control Tower\. Instead, you can enable and disable individual controls from AWS Control Tower or Security Hub\. When you change the enablement status of a control in AWS Control Tower, the change is also reflected in Security Hub\.

As with other Security Hub standards, you enable and disable controls in this standard separately in each AWS account and Region\. Enabling or disabling a control in one account or Region doesn't affect other accounts and Regions\.

## Viewing control status<a name="aws-control-tower-standard-control-status"></a>

You can view control status only in the Security Hub console, Security Hub API, and AWS CLI\. Security Hub calculates control status based on the workflow and compliance status of the control findings\. For more information about control status, see [Determining the overall status of a control from its findings](controls-overall-status.md)\.

A control that you disable in AWS Control Tower has a control status of `Disabled` in Security Hub unless you explicitly enable that control in Security Hub\.

Based on control statuses, Security Hub calculates a [security score](standards-security-score.md) for Service\-Managed Standard: AWS Control Tower\. This score is only available in Security Hub\. In addition, you can only view [control findings](controls-findings-create-update.md) in Security Hub\. The control status, standard security score, and control findings aren't available in AWS Control Tower\.

**Note**  
When you enable controls for Service\-Managed Standard: AWS Control Tower, Security Hub may take up to 18 hours to generate findings for controls that use an existing AWS Config service\-linked rule\. You may have existing service\-linked rules if you've enabled other standards and controls in Security Hub\. For more information, see [Schedule for running security checks](securityhub-standards-schedule.md)\.

## Deleting the standard<a name="aws-control-tower-standard-deletion"></a>

You can delete this standard in the AWS Control Tower console by disabling all controls in the standard\. This deletes the standard for all managed accounts and governed Regions in AWS Control Tower\. Deleting the standard in AWS Control Tower removes it from the **Standards** page of the Security Hub console, and it's no longer accessible by the Security Hub API or AWS CLI\.

**Note**  
 Disabling all controls from the standard in Security Hub doesn't disable or delete the standard\. 

Disabling the Security Hub service removes Service\-Managed Standard: AWS Control Tower and any other standards that you’ve enabled\.

## Finding field format for Service\-Managed Standard: AWS Control Tower<a name="aws-control-tower-standard-finding-fields"></a>

When you create Service\-Managed Standard: AWS Control Tower and enable controls for it, you'll start to receive control findings in Security Hub\. Security Hub reports control findings in the [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\. These are the ASFF values for this standard's Amazon Resource Name \(ARN\) and `GeneratorId`:
+ **Standard ARN** – `arn:aws:us-east-1:securityhub:::standards/service-managed-aws-control-tower/v/1.0.0`
+ **GeneratorId** – `service-managed-aws-control-tower/v/1.0.0/CodeBuild.1`

**Sample finding for Service\-Managed Standard: AWS Control Tower:**

```
{
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:securityhub:us-east-1:123456789012:subscription/service-managed-aws-control-tower/v/1.0.0/CodeBuild.1/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
  "ProductArn": "arn:aws:securityhub:us-east-1::product/aws/securityhub",
  "ProductName": "Security Hub",
  "CompanyName": "AWS",
  "Region": "us-east-1",
  "GeneratorId": "service-managed-aws-control-tower/v/1.0.0/CodeBuild.1",
  "AwsAccountId": "123456789012",
  "Types": [
    "Software and Configuration Checks/Industry and Regulatory Standards"
  ],
  "FirstObservedAt": "2022-11-17T01:25:30.296Z",
  "LastObservedAt": "2022-11-17T01:25:45.805Z",
  "CreatedAt": "2022-11-17T01:25:30.296Z",
  "UpdatedAt": "2022-11-17T01:25:30.296Z",
  "Severity": {
    "Product": 0,
    "Label": "INFORMATIONAL",
    "Normalized": 0,
    "Original": "INFORMATIONAL"
  },
  "Title": "CT.CodeBuild.1 CodeBuild GitHub or Bitbucket source repository URLs should use OAuth",
  "Description": "This AWS control checks whether the GitHub or Bitbucket source repository URL contains either personal access tokens or user name and password.",
  "Remediation": {
    "Recommendation": {
      "Text": "For information on how to correct this issue, consult the AWS Security Hub controls documentation.",
      "Url": "https://docs.aws.amazon.com/console/securityhub/CodeBuild.1/remediation"
    }
  },
  "ProductFields": {
    "StandardsArn": "arn:aws:securityhub:::standards/service-managed-aws-control-tower/v/1.0.0",
    "StandardsSubscriptionArn": "arn:aws:securityhub:us-east-1:123456789012:subscription/service-managed-aws-control-tower/v/1.0.0",
    "ControlId": "CT.CodeBuild.1",
    "RecommendationUrl": "https://docs.aws.amazon.com/console/securityhub/CodeBuild.1/remediation",
    "RelatedAWSResources:0/name": "securityhub-codebuild-project-source-repo-url-check-3e1a9c7d",
    "RelatedAWSResources:0/type": "AWS::Config::ConfigRule",
    "StandardsControlArn": "arn:aws:securityhub:us-east-1:123456789012:control/service-managed-aws-control-tower/v/1.0.0/CodeBuild.1",
    "aws/securityhub/ProductName": "Security Hub",
    "aws/securityhub/CompanyName": "AWS",
    "aws/securityhub/annotation": "AWS Config evaluated your resources against the rule. The rule did not apply to the AWS resources in its scope, the specified resources were deleted, or the evaluation results were deleted.",
    "Resources:0/Id": "arn:aws:iam::123456789012:root",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-1::product/aws/securityhub/arn:aws:securityhub:us-east-1:123456789012:subscription/service-managed-aws-control-tower/v/1.0.0/CodeBuild.1/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "Resources": [
    {
      "Type": "AwsAccount",
      "Id": "AWS::::Account:123456789012",
      "Partition": "aws",
      "Region": "us-east-1"
    }
  ],
  "Compliance": {
    "Status": "PASSED",
    "StatusReasons": [
      {
        "ReasonCode": "CONFIG_EVALUATIONS_EMPTY",
        "Description": "AWS Config evaluated your resources against the rule. The rule did not apply to the AWS resources in its scope, the specified resources were deleted, or the evaluation results were deleted."
      }
    ]
  },
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "RESOLVED"
  },
  "RecordState": "ACTIVE",
  "FindingProviderFields": {
    "Severity": {
      "Label": "INFORMATIONAL",
      "Original": "INFORMATIONAL"
    },
    "Types": [
      "Software and Configuration Checks/Industry and Regulatory Standards"
    ]
  }
}
```

## Service\-Managed Standard: AWS Control Tower controls<a name="aws-control-tower-standard-controls"></a>

Service\-Managed Standard: AWS Control Tower supports a subset of controls in the AWS Foundational Security Best Practices \(FSBP\) standard\. Choose a control from the following table to view information about it, including remediation steps for failed findings\. For this standard, control IDs in the AWS Control Tower console are formatted as **SH\.ControlID**\. For this standard, control IDs in the Security Hub console, Security Hub API, and AWS CLI are formatted as **CT\.ControlID**\. For example, CodeBuild\.1 is SH\.CodeBuild\.1 in the AWS Control Tower console and CT\.CodeBuild\.1 in Security Hub\.

Here's a list of available controls for Service\-Managed Standard: AWS Control Tower in all Regions except the AWS GovCloud \(US\) Region\.


| Security Hub control ID | AWS Control Tower control ID | 
| --- | --- | 
|  [CT\.ACM\.1](securityhub-standards-fsbp-controls.md#fsbp-acm-1)  |  SH\.ACM\.1  | 
|  [CT\.APIGateway\.1](securityhub-standards-fsbp-controls.md#fsbp-apigateway-1)  |  SH\.APIGateway\.1  | 
|  [CT\.APIGateway\.2](securityhub-standards-fsbp-controls.md#fsbp-apigateway-2)  |  SH\.APIGateway\.2  | 
|  [CT\.APIGateway\.3](securityhub-standards-fsbp-controls.md#fsbp-apigateway-3)  |  SH\.APIGateway\.3  | 
|  [CT\.APIGateway\.4](securityhub-standards-fsbp-controls.md#fsbp-apigateway-4)  |  SH\.APIGateway\.4  | 
|  [CT\.APIGateway\.5](securityhub-standards-fsbp-controls.md#fsbp-apigateway-5)  |  SH\.APIGateway\.5  | 
|  [CT\.AutoScaling\.1](securityhub-standards-fsbp-controls.md#fsbp-autoscaling-1)  |  SH\.AutoScaling\.1  | 
|  [CT\.AutoScaling\.2](securityhub-standards-fsbp-controls.md#fsbp-autoscaling-2)  |  SH\.AutoScaling\.2  | 
|  [CT\.AutoScaling\.3](securityhub-standards-fsbp-controls.md#fsbp-autoscaling-3)  |  SH\.AutoScaling\.3  | 
|  [CT\.AutoScaling\.4](securityhub-standards-fsbp-controls.md#fsbp-autoscaling-4)  |  SH\.AutoScaling\.4  | 
|  [CT\.Autoscaling\.5](securityhub-standards-fsbp-controls.md#fsbp-autoscaling-5)  |  SH\.Autoscaling\.5  | 
|  [CT\.AutoScaling\.6](securityhub-standards-fsbp-controls.md#fsbp-autoscaling-6)  |  SH\.AutoScaling\.6  | 
|  [CT\.AutoScaling\.9](securityhub-standards-fsbp-controls.md#fsbp-autoscaling-9)  |  SH\.AutoScaling\.9  | 
|  [CT\.CloudTrail\.1](securityhub-standards-fsbp-controls.md#fsbp-cloudtrail-1)  |  SH\.CloudTrail\.1  | 
|  [CT\.CloudTrail\.2](securityhub-standards-fsbp-controls.md#fsbp-cloudtrail-2)  |  SH\.CloudTrail\.2  | 
|  [CT\.CloudTrail\.4](securityhub-standards-fsbp-controls.md#fsbp-cloudtrail-4)  |  SH\.CloudTrail\.4  | 
|  [CT\.CloudTrail\.5](securityhub-standards-fsbp-controls.md#fsbp-cloudtrail-5)  |  SH\.CloudTrail\.5  | 
|  [CT\.CodeBuild\.1](securityhub-standards-fsbp-controls.md#fsbp-codebuild-1)  |  SH\.CodeBuild\.1  | 
|  [CT\.CodeBuild\.2](securityhub-standards-fsbp-controls.md#fsbp-codebuild-2)  |  SH\.CodeBuild\.2  | 
|  [CT\.CodeBuild\.4](securityhub-standards-fsbp-controls.md#fsbp-codebuild-4)  |  SH\.CodeBuild\.4  | 
|  [CT\.CodeBuild\.5](securityhub-standards-fsbp-controls.md#fsbp-codebuild-5)  |  SH\.CodeBuild\.5  | 
|  [CT\.DMS\.1](securityhub-standards-fsbp-controls.md#fsbp-dms-1)  |  SH\.DMS\.1  | 
|  [CT\.DynamoDB\.1](securityhub-standards-fsbp-controls.md#fsbp-dynamodb-1)  |  SH\.DynamoDB\.1  | 
|  [CT\.DynamoDB\.2](securityhub-standards-fsbp-controls.md#fsbp-dynamodb-2)  |  SH\.DynamoDB\.2  | 
|  [CT\.EC2\.1](securityhub-standards-fsbp-controls.md#fsbp-ec2-1)  |  SH\.EC2\.1  | 
|  [CT\.EC2\.2](securityhub-standards-fsbp-controls.md#fsbp-ec2-2)  |  SH\.EC2\.2  | 
|  [CT\.EC2\.3](securityhub-standards-fsbp-controls.md#fsbp-ec2-3)  |  SH\.EC2\.3  | 
|  [CT\.EC2\.4](securityhub-standards-fsbp-controls.md#fsbp-ec2-4)  |  SH\.EC2\.4  | 
|  [CT\.EC2\.6](securityhub-standards-fsbp-controls.md#fsbp-ec2-6)  |  SH\.EC2\.6  | 
|  [CT\.EC2\.7](securityhub-standards-fsbp-controls.md#fsbp-ec2-7)  |  SH\.EC2\.7  | 
|  [CT\.EC2\.8](securityhub-standards-fsbp-controls.md#fsbp-ec2-8)  |  SH\.EC2\.8  | 
|  [CT\.EC2\.9](securityhub-standards-fsbp-controls.md#fsbp-ec2-9)  |  SH\.EC2\.9  | 
|  [CT\.EC2\.10](securityhub-standards-fsbp-controls.md#fsbp-ec2-10)  |  SH\.EC2\.10  | 
|  [CT\.EC2\.15](securityhub-standards-fsbp-controls.md#fsbp-ec2-15)  |  SH\.EC2\.15  | 
|  [CT\.EC2\.16](securityhub-standards-fsbp-controls.md#fsbp-ec2-16)  |  SH\.EC2\.16  | 
|  [CT\.EC2\.17](securityhub-standards-fsbp-controls.md#fsbp-ec2-17)  |  SH\.EC2\.17  | 
|  [CT\.EC2\.18](securityhub-standards-fsbp-controls.md#fsbp-ec2-18)  |  SH\.EC2\.18  | 
|  [CT\.EC2\.19](securityhub-standards-fsbp-controls.md#fsbp-ec2-19)  |  SH\.EC2\.19  | 
|  [CT\.EC2\.20](securityhub-standards-fsbp-controls.md#fsbp-ec2-20)  |  SH\.EC2\.20  | 
|  [CT\.EC2\.21](securityhub-standards-fsbp-controls.md#fsbp-ec2-21)  |  SH\.EC2\.21  | 
|  [CT\.EC2\.22](securityhub-standards-fsbp-controls.md#fsbp-ec2-22)  |  SH\.EC2\.22  | 
|  [CT\.ECR\.1](securityhub-standards-fsbp-controls.md#fsbp-ecr-1)  |  SH\.ECR\.1  | 
|  [CT\.ECR\.2](securityhub-standards-fsbp-controls.md#fsbp-ecr-2)  |  SH\.ECR\.2  | 
|  [CT\.ECR\.3](securityhub-standards-fsbp-controls.md#fsbp-ecr-3)  |  SH\.ECR\.3  | 
|  [CT\.ECS\.1](securityhub-standards-fsbp-controls.md#fsbp-ecs-1)  |  SH\.ECS\.1  | 
|  [CT\.ECS\.2](securityhub-standards-fsbp-controls.md#fsbp-ecs-2)  |  SH\.ECS\.2  | 
|  [CT\.ECS\.3](securityhub-standards-fsbp-controls.md#fsbp-ecs-3)  |  SH\.ECS\.3  | 
|  [CT\.ECS\.4](securityhub-standards-fsbp-controls.md#fsbp-ecs-4)  |  SH\.ECS\.4  | 
|  [CT\.ECS\.5](securityhub-standards-fsbp-controls.md#fsbp-ecs-5)  |  SH\.ECS\.5  | 
|  [CT\.ECS\.8](securityhub-standards-fsbp-controls.md#fsbp-ecs-8)  |  SH\.ECS\.8  | 
|  [CT\.ECS\.10](securityhub-standards-fsbp-controls.md#fsbp-ecs-10)  |  SH\.ECS\.10  | 
|  [CT\.ECS\.12](securityhub-standards-fsbp-controls.md#fsbp-ecs-12)  |  SH\.ECS\.12  | 
|  [CT\.EFS\.1](securityhub-standards-fsbp-controls.md#fsbp-efs-1)  |  SH\.EFS\.1  | 
|  [CT\.EFS\.2](securityhub-standards-fsbp-controls.md#fsbp-efs-2)  |  SH\.EFS\.2  | 
|  [CT\.EFS\.3](securityhub-standards-fsbp-controls.md#fsbp-efs-3)  |  SH\.EFS\.3  | 
|  [CT\.EFS\.4](securityhub-standards-fsbp-controls.md#fsbp-efs-4)  |  SH\.EFS\.4  | 
|  [CT\.EKS\.2](securityhub-standards-fsbp-controls.md#fsbp-eks-2)  |  SH\.EKS\.2  | 
|  [CT\.ELB\.2](securityhub-standards-fsbp-controls.md#fsbp-elb-2)  |  SH\.ELB\.2  | 
|  [CT\.ELB\.3](securityhub-standards-fsbp-controls.md#fsbp-elb-3)  |  SH\.ELB\.3  | 
|  [CT\.ELB\.4](securityhub-standards-fsbp-controls.md#fsbp-elb-4)  |  SH\.ELB\.4  | 
|  [CT\.ELB\.5](securityhub-standards-fsbp-controls.md#fsbp-elb-5)  |  SH\.ELB\.5  | 
|  [CT\.ELB\.6](securityhub-standards-fsbp-controls.md#fsbp-elb-6)  |  SH\.ELB\.6  | 
|  [CT\.ELB\.7](securityhub-standards-fsbp-controls.md#fsbp-elb-7)  |  SH\.ELB\.7  | 
|  [CT\.ELB\.8](securityhub-standards-fsbp-controls.md#fsbp-elb-8)  |  SH\.ELB\.8  | 
|  [CT\.ELB\.9](securityhub-standards-fsbp-controls.md#fsbp-elb-9)  |  SH\.ELB\.9  | 
|  [CT\.ELB\.10](securityhub-standards-fsbp-controls.md#fsbp-elb-10)  |  SH\.ELB\.10  | 
|  [CT\.ELB\.12](securityhub-standards-fsbp-controls.md#fsbp-elb-12)  |  SH\.ELB\.12  | 
|  [CT\.ELB\.13](securityhub-standards-fsbp-controls.md#fsbp-elb-13)  |  SH\.ELB\.13  | 
|  [CT\.ELB\.14](securityhub-standards-fsbp-controls.md#fsbp-elb-14)  |  SH\.ELB\.14  | 
|  [CT\.ELBv2\.1](securityhub-standards-fsbp-controls.md#fsbp-elbv2-1)  |  SH\.ELBv2\.1  | 
|  [CT\.EMR\.1](securityhub-standards-fsbp-controls.md#fsbp-emr-1)  |  SH\.EMR\.1  | 
|  [CT\.ES\.1](securityhub-standards-fsbp-controls.md#fsbp-es-1)  |  SH\.ES\.1  | 
|  [CT\.ES\.2](securityhub-standards-fsbp-controls.md#fsbp-es-2)  |  SH\.ES\.2  | 
|  [CT\.ES\.3](securityhub-standards-fsbp-controls.md#fsbp-es-3)  |  SH\.ES\.3  | 
|  [CT\.ES\.4](securityhub-standards-fsbp-controls.md#fsbp-es-4)  |  SH\.ES\.4  | 
|  [CT\.ES\.5](securityhub-standards-fsbp-controls.md#fsbp-es-5)  |  SH\.ES\.5  | 
|  [CT\.ES\.6](securityhub-standards-fsbp-controls.md#fsbp-es-6)  |  SH\.ES\.6  | 
|  [CT\.ES\.7](securityhub-standards-fsbp-controls.md#fsbp-es-7)  |  SH\.ES\.7  | 
|  [CT\.ES\.8](securityhub-standards-fsbp-controls.md#fsbp-es-8)  |  SH\.ES\.8  | 
|  [CT\.ElasticBeanstalk\.1](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-1)  |  SH\.ElasticBeanstalk\.1  | 
|  [CT\.ElasticBeanstalk\.2](securityhub-standards-fsbp-controls.md#fsbp-elasticbeanstalk-2)  |  SH\.ElasticBeanstalk\.2  | 
|  [CT\.GuardDuty\.1](securityhub-standards-fsbp-controls.md#fsbp-guardduty-1)  |  SH\.GuardDuty\.1  | 
|  [CT\.IAM\.1](securityhub-standards-fsbp-controls.md#fsbp-iam-1)  |  SH\.IAM\.1  | 
|  [CT\.IAM\.2](securityhub-standards-fsbp-controls.md#fsbp-iam-2)  |  SH\.IAM\.2  | 
|  [CT\.IAM\.3](securityhub-standards-fsbp-controls.md#fsbp-iam-3)  |  SH\.IAM\.3  | 
|  [CT\.IAM\.4](securityhub-standards-fsbp-controls.md#fsbp-iam-4)  |  SH\.IAM\.4  | 
|  [CT\.IAM\.5](securityhub-standards-fsbp-controls.md#fsbp-iam-5)  |  SH\.IAM\.5  | 
|  [CT\.IAM\.6](securityhub-standards-fsbp-controls.md#fsbp-iam-6)  |  SH\.IAM\.6  | 
|  [CT\.IAM\.7](securityhub-standards-fsbp-controls.md#fsbp-iam-7)  |  SH\.IAM\.7  | 
|  [CT\.IAM\.8](securityhub-standards-fsbp-controls.md#fsbp-iam-8)  |  SH\.IAM\.8  | 
|  [CT\.IAM\.21](securityhub-standards-fsbp-controls.md#fsbp-iam-21)  |  SH\.IAM\.21  | 
|  [CT\.Kinesis\.1](securityhub-standards-fsbp-controls.md#fsbp-kinesis-1)  |  SH\.Kinesis\.1  | 
|  [CT\.KMS\.1](securityhub-standards-fsbp-controls.md#fsbp-kms-1)  |  SH\.KMS\.1  | 
|  [CT\.KMS\.2](securityhub-standards-fsbp-controls.md#fsbp-kms-2)  |  SH\.KMS\.2  | 
|  [CT\.KMS\.3](securityhub-standards-fsbp-controls.md#fsbp-kms-3)  |  SH\.KMS\.3  | 
|  [CT\.Lambda\.1](securityhub-standards-fsbp-controls.md#fsbp-lambda-1)  |  SH\.Lambda\.1  | 
|  [CT\.Lambda\.2](securityhub-standards-fsbp-controls.md#fsbp-lambda-2)  |  SH\.Lambda\.2  | 
|  [CT\.Lambda\.5](securityhub-standards-fsbp-controls.md#fsbp-lambda-5)  |  SH\.Lambda\.5  | 
|  [CT\.NetworkFirewall\.3](securityhub-standards-fsbp-controls.md#fsbp-networkfirewall-3)  |  SH\.NetworkFirewall\.3  | 
|  [CT\.NetworkFirewall\.4](securityhub-standards-fsbp-controls.md#fsbp-networkfirewall-4)  |  SH\.NetworkFirewall\.4  | 
|  [CT\.NetworkFirewall\.5](securityhub-standards-fsbp-controls.md#fsbp-networkfirewall-5)  |  SH\.NetworkFirewall\.5  | 
|  [CT\.NetworkFirewall\.6](securityhub-standards-fsbp-controls.md#fsbp-networkfirewall-6)  |  SH\.NetworkFirewall\.6  | 
|  [CT\.OpenSearch\.1](securityhub-standards-fsbp-controls.md#fsbp-opensearch-1)  |  SH\.OpenSearch\.1  | 
|  [CT\.OpenSearch\.2](securityhub-standards-fsbp-controls.md#fsbp-opensearch-2)  |  SH\.OpenSearch\.2  | 
|  [CT\.OpenSearch\.3](securityhub-standards-fsbp-controls.md#fsbp-opensearch-3)  |  SH\.OpenSearch\.3  | 
|  [CT\.OpenSearch\.4](securityhub-standards-fsbp-controls.md#fsbp-opensearch-4)  |  SH\.OpenSearch\.4  | 
|  [CT\.OpenSearch\.5](securityhub-standards-fsbp-controls.md#fsbp-opensearch-5)  |  SH\.OpenSearch\.5  | 
|  [CT\.OpenSearch\.6](securityhub-standards-fsbp-controls.md#fsbp-opensearch-6)  |  SH\.OpenSearch\.6  | 
|  [CT\.OpenSearch\.7](securityhub-standards-fsbp-controls.md#fsbp-opensearch-7)  |  SH\.OpenSearch\.7  | 
|  [CT\.OpenSearch\.8](securityhub-standards-fsbp-controls.md#fsbp-opensearch-8)  |  SH\.OpenSearch\.8  | 
|  [CT\.RDS\.1](securityhub-standards-fsbp-controls.md#fsbp-rds-1)  |  SH\.RDS\.1  | 
|  [CT\.RDS\.2](securityhub-standards-fsbp-controls.md#fsbp-rds-2)  |  SH\.RDS\.2  | 
|  [CT\.RDS\.3](securityhub-standards-fsbp-controls.md#fsbp-rds-3)  |  SH\.RDS\.3  | 
|  [CT\.RDS\.4](securityhub-standards-fsbp-controls.md#fsbp-rds-4)  |  SH\.RDS\.4  | 
|  [CT\.RDS\.5](securityhub-standards-fsbp-controls.md#fsbp-rds-5)  |  SH\.RDS\.5  | 
|  [CT\.RDS\.6](securityhub-standards-fsbp-controls.md#fsbp-rds-6)  |  SH\.RDS\.6  | 
|  [CT\.RDS\.8](securityhub-standards-fsbp-controls.md#fsbp-rds-8)  |  SH\.RDS\.8  | 
|  [CT\.RDS\.9](securityhub-standards-fsbp-controls.md#fsbp-rds-9)  |  SH\.RDS\.9  | 
|  [CT\.RDS\.10](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  |  SH\.RDS\.10  | 
|  [CT\.RDS\.11](securityhub-standards-fsbp-controls.md#fsbp-rds-11)  |  SH\.RDS\.11  | 
|  [CT\.RDS\.13](securityhub-standards-fsbp-controls.md#fsbp-rds-13)  |  SH\.RDS\.13  | 
|  [CT\.RDS\.17](securityhub-standards-fsbp-controls.md#fsbp-rds-17)  |  SH\.RDS\.17  | 
|  [CT\.RDS\.18](securityhub-standards-fsbp-controls.md#fsbp-rds-18)  |  SH\.RDS\.18  | 
|  [CT\.RDS\.19](securityhub-standards-fsbp-controls.md#fsbp-rds-19)  |  SH\.RDS\.19  | 
|  [CT\.RDS\.20](securityhub-standards-fsbp-controls.md#fsbp-rds-20)  |  SH\.RDS\.20  | 
|  [CT\.RDS\.21](securityhub-standards-fsbp-controls.md#fsbp-rds-21)  |  SH\.RDS\.21  | 
|  [CT\.RDS\.22](securityhub-standards-fsbp-controls.md#fsbp-rds-22)  |  SH\.RDS\.22  | 
|  [CT\.RDS\.23](securityhub-standards-fsbp-controls.md#fsbp-rds-23)  |  SH\.RDS\.23  | 
|  [CT\.RDS\.25](securityhub-standards-fsbp-controls.md#fsbp-rds-25)  |  SH\.RDS\.25  | 
|  [CT\.Redshift\.1](securityhub-standards-fsbp-controls.md#fsbp-redshift-1)  |  SH\.Redshift\.1  | 
|  [CT\.Redshift\.2](securityhub-standards-fsbp-controls.md#fsbp-redshift-2)  |  SH\.Redshift\.2  | 
|  [CT\.Redshift\.4](securityhub-standards-fsbp-controls.md#fsbp-redshift-4)  |  SH\.Redshift\.4  | 
|  [CT\.Redshift\.6](securityhub-standards-fsbp-controls.md#fsbp-redshift-6)  |  SH\.Redshift\.6  | 
|  [CT\.Redshift\.7](securityhub-standards-fsbp-controls.md#fsbp-redshift-7)  |  SH\.Redshift\.7  | 
|  [CT\.Redshift\.8](securityhub-standards-fsbp-controls.md#fsbp-redshift-8)  |  SH\.Redshift\.8  | 
|  [CT\.Redshift\.9](securityhub-standards-fsbp-controls.md#fsbp-redshift-9)  |  SH\.Redshift\.9  | 
|  [CT\.S3\.1](securityhub-standards-fsbp-controls.md#fsbp-s3-1)  |  SH\.S3\.1  | 
|  [CT\.S3\.2](securityhub-standards-fsbp-controls.md#fsbp-s3-2)  |  SH\.S3\.2  | 
|  [CT\.S3\.3](securityhub-standards-fsbp-controls.md#fsbp-s3-3)  |  SH\.S3\.3  | 
|  [CT\.S3\.4](securityhub-standards-fsbp-controls.md#fsbp-s3-4)  |  SH\.S3\.4  | 
|  [CT\.S3\.5](securityhub-standards-fsbp-controls.md#fsbp-s3-5)  |  SH\.S3\.5  | 
|  [CT\.S3\.6](securityhub-standards-fsbp-controls.md#fsbp-s3-6)  |  SH\.S3\.6  | 
|  [CT\.S3\.8](securityhub-standards-fsbp-controls.md#fsbp-s3-8)  |  SH\.S3\.8  | 
|  [CT\.S3\.9](securityhub-standards-fsbp-controls.md#fsbp-s3-9)  |  SH\.S3\.9  | 
|  [CT\.S3\.10](securityhub-standards-fsbp-controls.md#fsbp-s3-10)  |  SH\.S3\.10  | 
|  [CT\.S3\.11](securityhub-standards-fsbp-controls.md#fsbp-s3-11)  |  SH\.S3\.11  | 
|  [CT\.S3\.12](securityhub-standards-fsbp-controls.md#fsbp-s3-12)  |  SH\.S3\.12  | 
|  [CT\.S3\.13](securityhub-standards-fsbp-controls.md#fsbp-s3-13)  |  SH\.S3\.13  | 
|  [CT\.SageMaker\.1](securityhub-standards-fsbp-controls.md#fsbp-sagemaker-1)  |  SH\.SageMaker\.1  | 
|  [CT\.SecretsManager\.1](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-1)  |  SH\.SecretsManager\.1  | 
|  [CT\.SecretsManager\.2](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-2)  |  SH\.SecretsManager\.2  | 
|  [CT\.SecretsManager\.3](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-3)  |  SH\.SecretsManager\.3  | 
|  [CT\.SecretsManager\.4](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-4)  |  SH\.SecretsManager\.4  | 
|  [CT\.SNS\.1](securityhub-standards-fsbp-controls.md#fsbp-sns-1)  |  SH\.SNS\.1  | 
|  [CT\.SNS\.2](securityhub-standards-fsbp-controls.md#fsbp-sns-2)  |  SH\.SNS\.2  | 
|  [CT\.SQS\.1](securityhub-standards-fsbp-controls.md#fsbp-sqs-1)  |  SH\.SQS\.1  | 
|  [CT\.SSM\.1](securityhub-standards-fsbp-controls.md#fsbp-ssm-1)  |  SH\.SSM\.1  | 
|  [CT\.SSM\.2](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)  |  SH\.SSM\.2  | 
|  [CT\.SSM\.3](securityhub-standards-fsbp-controls.md#fsbp-ssm-3)  |  SH\.SSM\.3  | 
|  [CT\.SSM\.4](securityhub-standards-fsbp-controls.md#fsbp-ssm-4)  |  SH\.SSM\.4  | 
|  [CT\.WAF\.2](securityhub-standards-fsbp-controls.md#fsbp-waf-2)  |  SH\.WAF\.2  | 
|  [CT\.WAF\.3](securityhub-standards-fsbp-controls.md#fsbp-waf-3)  |  SH\.WAF\.3  | 
|  [CT\.WAF\.4](securityhub-standards-fsbp-controls.md#fsbp-waf-4)  |  SH\.WAF\.4  | 

Here's a list of available controls for Service\-Managed Standard: AWS Control Tower in the AWS GovCloud \(US\) Region\.


| Security Hub control ID | AWS Control Tower control ID | 
| --- | --- | 
|  [CT\.ACM\.1](securityhub-standards-fsbp-controls.md#fsbp-acm-1)  |  SH\.ACM\.1  | 
|  [CT\.APIGateway\.1](securityhub-standards-fsbp-controls.md#fsbp-apigateway-1)  |  SH\.APIGateway\.1  | 
|  [CT\.APIGateway\.5](securityhub-standards-fsbp-controls.md#fsbp-apigateway-5)  |  SH\.APIGateway\.5  | 
|  [CT\.AutoScaling\.1](securityhub-standards-fsbp-controls.md#fsbp-autoscaling-1)  |  SH\.AutoScaling\.1  | 
|  [CT\.CloudTrail\.1](securityhub-standards-fsbp-controls.md#fsbp-cloudtrail-1)  |  SH\.CloudTrail\.1  | 
|  [CT\.CloudTrail\.2](securityhub-standards-fsbp-controls.md#fsbp-cloudtrail-2)  |  SH\.CloudTrail\.2  | 
|  [CT\.CloudTrail\.4](securityhub-standards-fsbp-controls.md#fsbp-cloudtrail-4)  |  SH\.CloudTrail\.4  | 
|  [CT\.CloudTrail\.5](securityhub-standards-fsbp-controls.md#fsbp-cloudtrail-5)  |  SH\.CloudTrail\.5  | 
|  [CT\.DMS\.1](securityhub-standards-fsbp-controls.md#fsbp-dms-1)  |  SH\.DMS\.1  | 
|  [CT\.DynamoDB\.2](securityhub-standards-fsbp-controls.md#fsbp-dynamodb-2)  |  SH\.DynamoDB\.2  | 
|  [CT\.EC2\.1](securityhub-standards-fsbp-controls.md#fsbp-ec2-1)  |  SH\.EC2\.1  | 
|  [CT\.EC2\.2](securityhub-standards-fsbp-controls.md#fsbp-ec2-2)  |  SH\.EC2\.2  | 
|  [CT\.EC2\.3](securityhub-standards-fsbp-controls.md#fsbp-ec2-3)  |  SH\.EC2\.3  | 
|  [CT\.EC2\.4](securityhub-standards-fsbp-controls.md#fsbp-ec2-4)  |  SH\.EC2\.4  | 
|  [CT\.EC2\.6](securityhub-standards-fsbp-controls.md#fsbp-ec2-6)  |  SH\.EC2\.6  | 
|  [CT\.EC2\.7](securityhub-standards-fsbp-controls.md#fsbp-ec2-7)  |  SH\.EC2\.7  | 
|  [CT\.EC2\.8](securityhub-standards-fsbp-controls.md#fsbp-ec2-8)  |  SH\.EC2\.8  | 
|  [CT\.EC2\.9](securityhub-standards-fsbp-controls.md#fsbp-ec2-9)  |  SH\.EC2\.9  | 
|  [CT\.EC2\.10](securityhub-standards-fsbp-controls.md#fsbp-ec2-10)  |  SH\.EC2\.10  | 
|  [CT\.EC2\.18](securityhub-standards-fsbp-controls.md#fsbp-ec2-18)  |  SH\.EC2\.18  | 
|  [CT\.EC2\.19](securityhub-standards-fsbp-controls.md#fsbp-ec2-19)  |  SH\.EC2\.19  | 
|  [CT\.EC2\.20](securityhub-standards-fsbp-controls.md#fsbp-ec2-20)  |  SH\.EC2\.20  | 
|  [CT\.ECS\.2](securityhub-standards-fsbp-controls.md#fsbp-ecs-2)  |  SH\.ECS\.2  | 
|  [CT\.EFS\.1](securityhub-standards-fsbp-controls.md#fsbp-efs-1)  |  SH\.EFS\.1  | 
|  [CT\.ELB\.3](securityhub-standards-fsbp-controls.md#fsbp-elb-3)  |  SH\.ELB\.3  | 
|  [CT\.ELB\.4](securityhub-standards-fsbp-controls.md#fsbp-elb-4)  |  SH\.ELB\.4  | 
|  [CT\.ELB\.5](securityhub-standards-fsbp-controls.md#fsbp-elb-5)  |  SH\.ELB\.5  | 
|  [CT\.ELB\.6](securityhub-standards-fsbp-controls.md#fsbp-elb-6)  |  SH\.ELB\.6  | 
|  [CT\.ELBv2\.1](securityhub-standards-fsbp-controls.md#fsbp-elbv2-1)  |  SH\.ELBv2\.1  | 
|  [CT\.ELB\.7](securityhub-standards-fsbp-controls.md#fsbp-elb-7)  |  SH\.ELB\.7  | 
|  [CT\.ELB\.9](securityhub-standards-fsbp-controls.md#fsbp-elb-9)  |  SH\.ELB\.9  | 
|  [CT\.EMR\.1](securityhub-standards-fsbp-controls.md#fsbp-emr-1)  |  SH\.EMR\.1  | 
|  [CT\.ES\.1](securityhub-standards-fsbp-controls.md#fsbp-es-1)  |  SH\.ES\.1  | 
|  [CT\.ES\.2](securityhub-standards-fsbp-controls.md#fsbp-es-2)  |  SH\.ES\.2  | 
|  [CT\.ES\.3](securityhub-standards-fsbp-controls.md#fsbp-es-3)  |  SH\.ES\.3  | 
|  [CT\.ES\.5](securityhub-standards-fsbp-controls.md#fsbp-es-5)  |  SH\.ES\.5  | 
|  [CT\.ES\.6](securityhub-standards-fsbp-controls.md#fsbp-es-6)  |  SH\.ES\.6  | 
|  [CT\.ES\.7](securityhub-standards-fsbp-controls.md#fsbp-es-7)  |  SH\.ES\.7  | 
|  [CT\.ES\.8](securityhub-standards-fsbp-controls.md#fsbp-es-8)  |  SH\.ES\.8  | 
|  [CT\.IAM\.1](securityhub-standards-fsbp-controls.md#fsbp-iam-1)  |  SH\.IAM\.1  | 
|  [CT\.IAM\.2](securityhub-standards-fsbp-controls.md#fsbp-iam-2)  |  SH\.IAM\.2  | 
|  [CT\.IAM\.3](securityhub-standards-fsbp-controls.md#fsbp-iam-3)  |  SH\.IAM\.3  | 
|  [CT\.IAM\.4](securityhub-standards-fsbp-controls.md#fsbp-iam-4)  |  SH\.IAM\.4  | 
|  [CT\.IAM\.5](securityhub-standards-fsbp-controls.md#fsbp-iam-5)  |  SH\.IAM\.5  | 
|  [CT\.IAM\.7](securityhub-standards-fsbp-controls.md#fsbp-iam-7)  |  SH\.IAM\.7  | 
|  [CT\.IAM\.8](securityhub-standards-fsbp-controls.md#fsbp-iam-8)  |  SH\.IAM\.8  | 
|  [CT\.KMS\.1](securityhub-standards-fsbp-controls.md#fsbp-kms-1)  |  SH\.KMS\.1  | 
|  [CT\.KMS\.2](securityhub-standards-fsbp-controls.md#fsbp-kms-2)  |  SH\.KMS\.2  | 
|  [CT\.KMS\.3](securityhub-standards-fsbp-controls.md#fsbp-kms-3)  |  SH\.KMS\.3  | 
|  [CT\.Lambda\.1](securityhub-standards-fsbp-controls.md#fsbp-lambda-1)  |  SH\.Lambda\.1  | 
|  [CT\.Lambda\.2](securityhub-standards-fsbp-controls.md#fsbp-lambda-2)  |  SH\.Lambda\.2  | 
|  [CT\.RDS\.1](securityhub-standards-fsbp-controls.md#fsbp-rds-1)  |  SH\.RDS\.1  | 
|  [CT\.RDS\.2](securityhub-standards-fsbp-controls.md#fsbp-rds-2)  |  SH\.RDS\.2  | 
|  [CT\.RDS\.3](securityhub-standards-fsbp-controls.md#fsbp-rds-3)  |  SH\.RDS\.3  | 
|  [CT\.RDS\.4](securityhub-standards-fsbp-controls.md#fsbp-rds-4)  |  SH\.RDS\.4  | 
|  [CT\.RDS\.5](securityhub-standards-fsbp-controls.md#fsbp-rds-5)  |  SH\.RDS\.5  | 
|  [CT\.RDS\.6](securityhub-standards-fsbp-controls.md#fsbp-rds-6)  |  SH\.RDS\.6  | 
|  [CT\.RDS\.7](securityhub-standards-fsbp-controls.md#fsbp-rds-7)  |  SH\.RDS\.7  | 
|  [CT\.RDS\.8](securityhub-standards-fsbp-controls.md#fsbp-rds-8)  |  SH\.RDS\.8  | 
|  [CT\.RDS\.9](securityhub-standards-fsbp-controls.md#fsbp-rds-9)  |  SH\.RDS\.9  | 
|  [CT\.RDS\.10](securityhub-standards-fsbp-controls.md#fsbp-rds-10)  |  SH\.RDS\.10  | 
|  [CT\.RDS\.11](securityhub-standards-fsbp-controls.md#fsbp-rds-11)  |  SH\.RDS\.11  | 
|  [CT\.RDS\.16](securityhub-standards-fsbp-controls.md#fsbp-rds-16)  |  SH\.RDS\.16  | 
|  [CT\.RDS\.17](securityhub-standards-fsbp-controls.md#fsbp-rds-17)  |  SH\.RDS\.17  | 
|  [CT\.RDS\.18](securityhub-standards-fsbp-controls.md#fsbp-rds-18)  |  SH\.RDS\.18  | 
|  [CT\.RDS\.19](securityhub-standards-fsbp-controls.md#fsbp-rds-19)  |  SH\.RDS\.19  | 
|  [CT\.RDS\.20](securityhub-standards-fsbp-controls.md#fsbp-rds-20)  |  SH\.RDS\.20  | 
|  [CT\.RDS\.21](securityhub-standards-fsbp-controls.md#fsbp-rds-21)  |  SH\.RDS\.21  | 
|  [CT\.RDS\.22](securityhub-standards-fsbp-controls.md#fsbp-rds-22)  |  SH\.RDS\.22  | 
|  [CT\.RDS\.23](securityhub-standards-fsbp-controls.md#fsbp-rds-23)  |  SH\.RDS\.23  | 
|  [CT\.Redshift\.1](securityhub-standards-fsbp-controls.md#fsbp-redshift-1)  |  SH\.Redshift\.1  | 
|  [CT\.Redshift\.2](securityhub-standards-fsbp-controls.md#fsbp-redshift-2)  |  SH\.Redshift\.2  | 
|  [CT\.Redshift\.3](securityhub-standards-fsbp-controls.md#fsbp-redshift-3)  |  SH\.Redshift\.3  | 
|  [CT\.Redshift\.4](securityhub-standards-fsbp-controls.md#fsbp-redshift-4)  |  SH\.Redshift\.4  | 
|  [CT\.Redshift\.6](securityhub-standards-fsbp-controls.md#fsbp-redshift-6)  |  SH\.Redshift\.6  | 
|  [CT\.S3\.2](securityhub-standards-fsbp-controls.md#fsbp-s3-2)  |  SH\.S3\.2  | 
|  [CT\.S3\.3](securityhub-standards-fsbp-controls.md#fsbp-s3-3)  |  SH\.S3\.3  | 
|  [CT\.S3\.4](securityhub-standards-fsbp-controls.md#fsbp-s3-4)  |  SH\.S3\.4  | 
|  [CT\.S3\.5](securityhub-standards-fsbp-controls.md#fsbp-s3-5)  |  SH\.S3\.5  | 
|  [CT\.S3\.6](securityhub-standards-fsbp-controls.md#fsbp-s3-6)  |  SH\.S3\.6  | 
|  [CT\.S3\.9](securityhub-standards-fsbp-controls.md#fsbp-s3-9)  |  SH\.S3\.9  | 
|  [CT\.SNS\.1](securityhub-standards-fsbp-controls.md#fsbp-sns-1)  |  SH\.SNS\.1  | 
|  [CT\.SQS\.1](securityhub-standards-fsbp-controls.md#fsbp-sqs-1)  |  SH\.SQS\.1  | 
|  [CT\.SSM\.1](securityhub-standards-fsbp-controls.md#fsbp-ssm-1)  |  SH\.SSM\.1  | 
|  [CT\.SSM\.2](securityhub-standards-fsbp-controls.md#fsbp-ssm-2)  |  SH\.SSM\.2  | 
|  [CT\.SSM\.3](securityhub-standards-fsbp-controls.md#fsbp-ssm-3)  |  SH\.SSM\.3  | 
|  [CT\.SecretsManager\.1](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-1)  |  SH\.SecretsManager\.1  | 
|  [CT\.SecretsManager\.2](securityhub-standards-fsbp-controls.md#fsbp-secretsmanager-2)  |  SH\.SecretsManager\.2  | 

For more information about this standard, see [Security Hub controls](https://docs.aws.amazon.com/controltower/latest/userguide/security-hub-controls.html) in the *AWS Control Tower User Guide*\.