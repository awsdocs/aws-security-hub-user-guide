# Using BatchUpdateFindings to update a finding<a name="finding-update-batchupdatefindings"></a>

[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) is used to update information related to a customer's processing of findings from finding providers\. It can be used by a customer or by a SIEM, ticketing, incident management, or SOAR tool that works on behalf of a customer\. [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) cannot be used to create new findings\. It can be used to update up to 100 findings at a time\.

[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) does not change the `UpdatedAt` field for the finding\. `UpdatedAt` only reflects the most recent update from the finding provider\.

## Available fields for BatchUpdateFindings<a name="batchupdatefindings-fields"></a>

Master accounts can use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update findings for their account or for their member accounts\. Member accounts can use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update findings for their account\.

Customers can only use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update the following fields and objects\.
+ `Confidence`
+ `Criticality`
+ `Note`
+ `RelatedFindings`
+ `Severity`
+ `Types`
+ `UserDefinedFields`
+ `VerificationState`
+ `Workflow`

By default, master and member accounts have access to all of the above fields and field values\. Security Hub also provides context keys to allow you to restrict access to fields and field values\.

For example, you might only allow member accounts to set `Workflow.Status` to `RESOLVED`\. Or you might not want to allow member accounts to change `Severity.Label`\.

## Configuring access to BatchUpdateFindings<a name="batchupdatefindings-configure-access"></a>

You can configure IAM policies to restrict access to using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update fields and field values\.

In a statement to restrict access to [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html), use the following values\.
+ `Action` is `securityhub:BatchUpdateFindings`
+ `Effect` is `Deny`
+ For `Condition`, you can deny a [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) request based on the following:
  + The finding includes a specific field\.
  + The finding includes a specific field value\.

### Context keys<a name="batchupdatefindings-configure-access-context-keys"></a>

These are the context keys for restricting access to [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

**ASFF field**  
The context key for an ASFF field is as follows\.  

```
securityhub:ASFFSyntaxPath/<fieldName>
```
Replace `<fieldName>` with the ASFF field\.  
For example, to restrict access to the `Workflow.Status` field, use` securityhub:ASFFSyntaxPath/Workflow.Status`\.

### Disallowing all updates to a field<a name="batchupdatefindings-configure-access-block-field"></a>

To prevent a user from making any update to a specific field, use a condition like this:

```
 "Condition": {
                "Null": {
                    "securityhub:ASFFSyntaxPath/<fieldName>": "false"
               }
}
```

For example, the following statement indicates that [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) cannot be used to update the workflow status\.

```
{
    "Sid": "VisualEditor0",
    "Effect": "Deny",
    "Action": "securityhub:BatchUpdateFindings",
    "Resource": "*",
    "Condition": {
        "Null": {
            "securityhub:ASFFSyntaxPath/Workflow.Status": "false"
        }
    }
}
```

### Disallowing specific field values<a name="batchupdatefindings-configure-access-block-field-values"></a>

To prevent a user from setting a field to a specific value, use a condition like this:

```
"Condition": {
                "StringEquals": {
                    "securityhub:ASFFSyntaxPath/<fieldName>": "<fieldValue>"
               }
}
```

For example, the following statement indicates that [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) cannot be used to set `Workflow.Status` to `SUPPRESSED`\.

```
{
    "Sid": "VisualEditor0",
    "Effect": "Deny",
    "Action": "securityhub:BatchUpdateFindings",
    "Resource": "*",
    "Condition": {
    "StringEquals": {
        "securityhub:ASFFSyntaxPath/Workflow.Status": "SUPPRESSED"
    }
}
```

You can also provide a list of values that are not permitted\.

```
 "Condition": {
                "ForAnyValue:StringEquals": {
                    "securityhub:ASFFSyntaxPath/<fieldName>": [ "<fieldValue1>", "<fieldValue2>", "<fieldValuen>" ]
               }
}
```

For example, the following statement indicates that [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) cannot be used to set `Workflow.Status` to either `RESOLVED` or `SUPPRESSED`\.

```
{
    "Sid": "VisualEditor0",
    "Effect": "Deny",
    "Action": "securityhub:BatchUpdateFindings",
    "Resource": "*",
    "Condition": {
    "ForAnyValue:StringEquals": {
        "securityhub:ASFFSyntaxPath/Workflow.Status": [
            "RESOLVED",
            "NOTIFIED"
        ]
    }
}
```

## Using the batch\-update\-findings command from the AWS CLI<a name="batchupdatefindings-command-line"></a>

In the AWS Command Line Interface, you use the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-update-findings.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-update-findings.html) command to update the findings\.

For each finding to update, you provide both the finding ID and the ARN of the product that generated the finding\.

```
--finding-identifiers ID="<findingID1>",ProductArn="<productARN>" ID="<findingID2>",ProductArn="<productARN2>"
```

When you provide the attributes to update, you can either use a JSON format or a shortcut format\.

Here is an example of an update to the `Note` object that uses the JSON format:

```
--note '{"Text": "Known issue that is not a risk.", "UpdatedBy": "user1"}'
```

Here is the same update that uses the shortcut format:

```
--note Text="Known issue that is not a risk.",UpdatedBy="user1"
```

The AWS CLI Command Reference provides the JSON and shortcut syntax for each field\.

The following [https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-update-findings.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/batch-update-findings.html) example updates two findings to add a note, change the severity label, and resolve them\.

```
aws securityhub batch-update-findings --finding-identifiers Id="arn:aws:securityhub:us-west-1:123456789012:subscription/pci-dss/v/3.2.1/PCI.Lambda.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",ProductArn="arn:aws:securityhub:us-west-2::product/aws/securityhub" Id="arn:aws:securityhub:us-west-1:123456789012:subscription/pci-dss/v/3.2.1/PCI.Lambda.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE22222",ProductArn="arn:aws:securityhub:us-west-1::product/aws/securityhub" --note '{"Text": "Known issue that is not a risk.", "UpdatedBy": "user1"}' --severity '{"Label": "LOW"}' --workflow '{"Status": "RESOLVED"}'
```

This is the same example, but uses the shortcuts instead of JSON\.

```
aws securityhub batch-update-findings --finding-identifiers Id="arn:aws:securityhub:us-west-1:123456789012:subscription/pci-dss/v/3.2.1/PCI.Lambda.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",ProductArn="arn:aws:securityhub:us-west-1::product/aws/securityhub" Id="arn:aws:securityhub:us-west-1:123456789012:subscription/pci-dss/v/3.2.1/PCI.Lambda.2/finding/a1b2c3d4-5678-90ab-cdef-EXAMPLE22222",ProductArn="arn:aws:securityhub:us-west-1::product/aws/securityhub" --note Text="Known issue that is not a risk.",UpdatedBy="user1" --severity Label="LOW" --workflow Status="RESOLVED"
```