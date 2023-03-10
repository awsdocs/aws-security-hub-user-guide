# AWS CloudFormation controls<a name="cloudformation-controls"></a>

These controls are related to CloudFormation resources\.

## \[CloudFormation\.1\] CloudFormation stacks should be integrated with Simple Notification Service \(SNS\)<a name="cloudformation-1"></a>

**Related requirements:** NIST\.800\-53\.r5 SI\-4\(12\), NIST\.800\-53\.r5 SI\-4\(5\)

**Category:** Detect > Detection services > Application monitoring

**Severity:** Low

**Resource type:** `AWS::CloudFormation::Stack`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloudformation-stack-notification-check.html](https://docs.aws.amazon.com/config/latest/developerguide/cloudformation-stack-notification-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `SNSTopic1`: 30
+ `SNSTopic2`: 30
+ `SNSTopic3`: 30
+ `SNSTopic4`: 30
+ `SNSTopic5`: 30
+ `(Optional): SNS topic ARN`: 30

This control checks whether an Amazon Simple Notification Service notification is integrated with a CloudFormation stack\. The control fails for a CloudFormation stack if there is no SNS notification associated with it\. 

Configuring an SNS notification with your CloudFormation stack helps immediately notify stakeholders of any events or changes occurring with the stack\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Asia Pacific \(Hong Kong\)
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
Europe \(Paris\)
Europe \(Stockholm\)
Middle East \(Bahrain\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="cloudformation-1-remediation"></a>

For information about how to update a CloudFormation stack, see [AWS CloudFormation stack updates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks) in the AWS CloudFormation User Guide\.