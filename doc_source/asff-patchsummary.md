# PatchSummary<a name="asff-patchsummary"></a>

The `PatchSummary` object provides an overview of the patch compliance status for an instance against a selected compliance standard\.

To view descriptions of `PatchSummary` attributes, see [PatchSummary](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_PatchSummary.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"PatchSummary" : {
    "Id" : "pb-123456789098"
    "InstalledCount" : "100",
    "MissingCount" : "100",
    "FailedCount" : "0",
    "InstalledOtherCount" : "1023",
    "InstalledRejectedCount" : "0",
    "InstalledPendingReboot" : "0",
    "OperationStartTime" : "2018-09-27T23:37:31Z",
    "OperationEndTime" : "2018-09-27T23:39:31Z",
    "RebootOption" : "RebootIfNeeded",
    "Operation" : "Install"
}
```