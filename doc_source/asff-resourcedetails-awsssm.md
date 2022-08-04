# AwsSsm<a name="asff-resourcedetails-awsssm"></a>

The following are examples of the AWS Security Finding Format for `AwsSsm` resources\.

## AwsSsmPatchCompliance<a name="asff-resourcedetails-awsssmpatchcompliance"></a>

The `AwsSsmPatchCompliance` object provides information about the state of a patch on an instance based on the patch baseline that was used to patch the instance\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsSsmPatchCompliance` object\. To view descriptions of `AwsSsmPatchCompliance` attributes, see [AwsSsmPatchComplianceDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsSsmPatchComplianceDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsSsmPatchCompliance": {
    "Patch": {
        "ComplianceSummary": {
            "ComplianceType": "Patch",
            "CompliantCriticalCount": 0,
            "CompliantHighCount": 0,
            "CompliantInformationalCount": 0,
            "CompliantLowCount": 0,
            "CompliantMediumCount": 0,
            "CompliantUnspecifiedCount": 461,
            "ExecutionType": "Command",
            "NonCompliantCriticalCount": 0,
            "NonCompliantHighCount": 0,
            "NonCompliantInformationalCount": 0,
            "NonCompliantLowCount": 0,
            "NonCompliantMediumCount": 0,
            "NonCompliantUnspecifiedCount": 0,
            "OverallSeverity": "UNSPECIFIED",
            "PatchBaselineId": "pb-0c5b2769ef7cbe587",
            "PatchGroup": "ExamplePatchGroup",
            "Status": "COMPLIANT"
        }
    }
}
```