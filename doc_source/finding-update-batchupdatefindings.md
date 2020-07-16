# Using BatchUpdateFindings to update a finding<a name="finding-update-batchupdatefindings"></a>

[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) is used to update information related to a customer's processing of findings from finding providers\. It can be used by a customer or by a SIEM, ticketing, incident management, or SOAR tool that works on behalf of a customer\. [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) cannot be used to create new findings\. It can be used to update up to 100 findings at a time\.

[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) does not change the `UpdatedAt` field for the finding\. `UpdatedAt` only reflects the most recent update from the finding provider\.

## Available fields for BatchUpdateFindings<a name="batchupdatefindings-fields"></a>

Master accounts can use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update findings for their account or for their member accounts\. For those accounts, they can only use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update the following fields and objects\.
+ `Confidence`
+ `Criticality`
+ `Note`
+ `RelatedFindings`
+ `Severity`
+ `Types`
+ `UserDefinedFields`
+ `VerificationState`
+ `Workflow`

Member accounts can only use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update the `Note` object on their findings\.

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