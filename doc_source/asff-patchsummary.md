# PatchSummary<a name="asff-patchsummary"></a>

The `PatchSummary` object provides an overview of the patch compliance status for an instance against a selected compliance standard\.

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

The `PatchSummary` object can have the following attributes\.

**`FailedCount`**  
Optional  
The number of patches from the compliance standard with installation failures\.  
**Type:** Number  
**Minimum value:** 0  
**Maximum value:** 100,000

**`Id`**  
Required  
The identifier of the compliance standard that was used to determine the patch compliance status\.  
**Type:** String  
**Minimum length:** 20  
**Maximum length:** 128

**`InstalledCount`**  
Optional  
The number of patches from the compliance standard that were installed successfully\.  
**Type:** Number  
**Minimum value:** 0  
**Maximum value:** 100,000

**`InstalledOtherCount`**  
Optional  
The number of installed patches that are not part of the compliance standard\.  
**Type:** Number  
**Minimum value:** 0  
**Maximum value:** 100,000

**`InstalledPendingReboot`**  
Optional  
The number of patches that were applied but that require the instance to be rebooted in order to be marked as installed\.  
**Type:** Number  
**Minimum value:** 0  
**Maximum value:** 100,000

**`InstalledRejectedCount`**  
Optional  
The number of patches that are installed but are also on a list of patches that the customer rejected\.  
**Type:** Number  
**Minimum value:** 0  
**Maximum value:** 100,000

**`MissingCount`**  
Optional  
The number of patches that are part of the compliance standard but are not installed\. The count includes patches with installation failures\.  
**Type:** Number  
**Minimum value:** 0  
**Maximum value:** 100,000

**`Operation`**  
Optional  
The type of patch operation that was performed\.  
For Patch Manager, the values are `SCAN` and `INSTALL`\.  
**Type:** String  
**Maximum length:** 256

**`OperationEndTime`**  
Optional  
Indicates when the operation was completed\.  
**Type:** String  
**Format:** Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  
**Example**  

```
"OperationEndTime": "2020-06-22T17:40:12.322Z"
```

**`OperationStartTime`**  
Optional  
Indicates when the operation started\.  
**Type:** String  
**Format:** Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  
**Example**  

```
"OperationStartTime": "2020-06-22T17:40:12.322Z"
```

**`RebootOption`**  
Optional  
The reboot option specified for the instance\.  
**Type:** String  
**Maximum length:** 256  
**Valid values:** `NoReboot` \| `RebootIfNeeded`\.