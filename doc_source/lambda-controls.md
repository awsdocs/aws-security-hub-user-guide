# AWS Lambda controls<a name="lambda-controls"></a>

These controls are related to Lambda resources\.

## \[Lambda\.1\] Lambda function policies should prohibit public access<a name="lambda-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.2, PCI DSS v3\.2\.1/1\.3\.4, PCI DSS v3\.2\.1/7\.2\.1, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration

**Severity:** Critical

**Resource type:** `AWS::Lambda::Function`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-public-access-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-public-access-prohibited.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the Lambda function resource\-based policy prohibits public access outside of your account\.

The control also fails if a Lambda function is invoked from Amazon S3 and the policy does not include a condition for `AWS:SourceAccount`\.

The Lambda function should not be publicly accessible, as this may allow unintended access to your code stored in the function\.

**Note**  
This control is not supported in the China \(Beijing\) or China \(Ningxia\) Regions\.

### Remediation<a name="lambda-1-remediation"></a>

If a Lambda function fails this control, it indicates that the resource\-based policy statement for the Lambda function allows public access\.

To remediate the issue, you must update the policy to remove the permissions or to add the `AWS:SourceAccount` condition\. You can only update the resource\-based policy from the Lambda API\.

The following instructions use the console to review the policy and the AWS Command Line Interface to remove the permissions\.

**To view the resource\-based policy for a Lambda function**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. In the navigation pane, choose **Functions**\.

1. Choose the function\.

1. Choose **Permissions**\. The resource\-based policy shows the permissions that are applied when another account or AWS service attempts to access the function\. 

1. Examine the resource\-based policy\. Identify the policy statement that has `Principal` field values that make the policy public\. For example, allowing `"*"` or `{ "AWS": "*" }`\.

   You cannot edit the policy from the console\. To remove permissions from the function, you use the `remove-permission` command from the AWS CLI\.

   Note the value of the statement ID \(`Sid`\) for the statement that you want to remove\.

To use the AWS CLI to remove permissions from a Lambda function, issue the [https://docs.aws.amazon.com/cli/latest/reference/lambda/remove-permission.html](https://docs.aws.amazon.com/cli/latest/reference/lambda/remove-permission.html) command\.

```
$ aws lambda remove-permission --function-name <function-name> --statement-id <statement-id>
```

Replace `<function-name>` with the name of the Lambda function, and `<statement-id>` with the statement ID of the statement to remove\.

**To verify that the permissions are updated**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. In the navigation pane, choose **Functions**\.

1. Choose the function that you updated\.

1. Choose **Permissions**\.

   The resource\-based policy should be updated\. If there was only one statement in the policy, then the policy is empty\.

For more information, see [Using resource\-based policies for AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html) in the *AWS Lambda Developer Guide*\.

## \[Lambda\.2\] Lambda functions should use supported runtimes<a name="lambda-2"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 SI\-2, NIST\.800\-53\.r5 SI\-2\(2\), NIST\.800\-53\.r5 SI\-2\(4\), NIST\.800\-53\.r5 SI\-2\(5\)

**Category:** Protect > Secure development

**Severity:** Medium

**Resource type:** `AWS::Lambda::Function`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-settings-check.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-function-settings-check.html)

**Schedule type:** Change triggered

**Parameters:** 
+ `runtime`: `nodejs18.x, nodejs16.x, nodejs14.x, nodejs12.x, python3.9, python3.8, python3.7, ruby2.7, java11, java8, java8.al2, go1.x, dotnetcore3.1, dotnet6`

This control checks that the Lambda function settings for runtimes match the expected values set for the supported runtimes for each language\. This control checks function settings for the following runtimes: `nodejs18.x,`, `nodejs16.x`, `nodejs14.x`, `nodejs12.x`, `python3.9`, `python3.8`, `python3.7`, `ruby2.7`, `java11`, `java8`, `java8.al2`, `go1.x`, `dotnetcore3.1`, and `dotnet6`\.

The AWS Config rule ignores functions that have a package type of `Image`\.

[Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) are built around a combination of operating system, programming language, and software libraries that are subject to maintenance and security updates\. When a runtime component is no longer supported for security updates, Lambda deprecates the runtime\. Even though you cannot create functions that use the deprecated runtime, the function is still available to process invocation events\. Make sure that your Lambda functions are current and do not use out\-of\-date runtime environments\.

To learn more about the supported runtimes that this control checks for the supported languages, see [AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) in the *AWS Lambda Developer Guide*\.

**Note**  
This control is not supported in Asia Pacific \(Osaka\)or China \(Ningxia\)\.

### Remediation<a name="lambda-2-remediation"></a>

For more information on supported runtimes and deprecation schedules, see the [Runtime support policy](https://docs.aws.amazon.com/lambda/latest/dg/runtime-support-policy.html) section of the *AWS Lambda Developer Guide*\. When you migrate your runtimes to the latest version, follow the syntax and guidance from the publishers of the language\.

## \[Lambda\.3\] Lambda functions should be in a VPC<a name="lambda-3"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1, PCI DSS v3\.2\.1/1\.3\.1, PCI DSS v3\.2\.1/1\.3\.2, PCI DSS v3\.2\.1/1\.3\.4, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Severity: ** Low

**Resource type: ** `AWS::Lambda::Function`

**AWS Config rule: ** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-inside-vpc.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-inside-vpc.html) 

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a Lambda function is in a VPC\. You might see failed findings for Lambda@Edge resources\.

It does not evaluate the VPC subnet routing configuration to determine public reachability\. 

**Note**  
This control is not supported in the following Regions\.  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)

### Remediation<a name="lambda-3-remediation"></a>

**To configure a function to connect to private subnets in a virtual private cloud \(VPC\) in your account**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. Navigate to **Functions** and then select your Lambda function\.

1. Scroll to **Network** and then select a VPC with the connectivity requirements of the function\.

1. To run your functions in high availability mode, Security Hub recommends that you choose at least two subnets\.

1. Choose at least one security group that has the connectivity requirements of the function\.

1. Choose **Save**\.

For more information see the section on configuring a Lambda function to access resources in a VPC in the [https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html)\.

## \[Lambda\.5\] VPC Lambda functions should operate in more than one Availability Zone<a name="lambda-5"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > High Availability

**Severity:** Medium

**Resource type:** `AWS::Lambda::Function`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/lambda-vpc-multi-az-check.html](https://docs.aws.amazon.com/config/latest/developerguide/lambda-vpc-multi-az-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Lambda has more than one availability zone associated\. The rule fails if only one availability zone is associated with Lambda\. 

Deploying resources across multiple Availability Zones is an AWS best practice to ensure high availability within your architecture\. Availability is a core pillar in the confidentiality, integrity, and availability triad security model\. All Lambda functions should have a multi\-Availability Zone deployment to ensure that a single zone of failure does not cause a total disruption of operations\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="lambda-5-remediation"></a>

**To deploy a Lambda function in multiple Availability Zones through console:**

1. Open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)

1. From the **Functions** page on the Lambda console choose a function\.

1. Choose **Configuration** and then choose **VPC**\.

1. Choose **Edit**\.

1. If the function was not originally connected to a VPC, select a VPC from the dropdown menu\. If the function was not originally connected to a VPC, choose at least one security group to attach to the function\.
**Note**  
The function execution role must have permissions to call `CreateNetworkInterface` on EC2\.

1. Choose **Save**\.