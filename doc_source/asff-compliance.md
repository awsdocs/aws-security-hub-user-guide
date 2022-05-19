# Compliance<a name="asff-compliance"></a>

Contains finding details related to a control\. Only returned for findings that are generated as the result of a check that is run on a control\.

**Example**

```
"Compliance": {
    "RelatedRequirements": ["Req1", "Req2"],
    "Status": "FAILED",
    "StatusReasons": [
        {
            "ReasonCode": "CLOUDWATCH_ALARMS_NOT_PRESENT",
            "Description": "CloudWatch alarms do not exist in the account"
        }
    ]
}
```

## Compliance attributes<a name="asff-compliance-attributes"></a>

The `Compliance` object can have the following attributes\.

**`RelatedRequirements`**  
Optional  
For a Security Hub control, the industry or regulatory framework requirements that are related to the control\. The check for that control is aligned with those requirements\.  
You can provide up to 32 related requirements\.  
To identify a requirement, use its identifier\.  
**Type:** Array of strings

**`Status`**  
Optional  
The result of a security check\.  
**Type:** Enum  
**Valid values:**  
+ `PASSED` – Security check passed for all evaluated resources\. If` Compliance.Status` is `PASSED`, then Security Hub automatically sets `Workflow.Status` to `RESOLVED`\.

  If `Compliance.Status` for a finding changes from `PASSED` to `FAILED`, `WARNING`, or `NOT_AVAILABLE`, and `Workflow.Status` was either `NOTIFIED` or `RESOLVED`, then Security Hub automatically sets `Workflow.Status` to `NEW`\.
+ `WARNING` – Some information is missing, or this check is not supported given your configuration\.
+ `FAILED` – Security check failed for at least one evaluated resource\.
+ `NOT_AVAILABLE` – Check could not be performed due to a service outage or API error\. The `NOT_AVAILABLE` status can also indicate that the result of the AWS Config evaluation was `NOT_APPLICABLE`\. In that case, after three to five days, Security Hub automatically archives the finding on a best effort basis\.
**Example**  

```
"Status": "PASSED"
```

**[`StatusReasons`](#asff-compliance-statusreasons)**  
Optional  
For findings generated from controls, a list of reasons behind the value of `Compliance.Status`\.  
For the list of status codes and their meanings, see [Generating and updating control findings](controls-findings-create-update.md)\.  
Type: String  
Example:  

```
"StatusReasons": [
    {

        "Description": "CloudWatch alarms do not exist in the account",
        "ReasonCode": "CW_ALARMS_NOT_PRESENT"
    }
]
```

## StatusReasons<a name="asff-compliance-statusreasons"></a>

For findings generated from controls, a list of reasons for the value of `Compliance.Status`\.

```
"StatusReasons": [
    {
        "Description": "CloudWatch alarms do not exist in the account",
        "ReasonCode": "CW_ALARMS_NOT_PRESENT"
    }
]
```

Each reason in the `StatusReasons` object can have the following attributes\.

**`Description`**  
Optional  
The corresponding description for the reason\.  
**Type:** String

**`ReasonCode`**  
Required  
A code that represents a reason for the current control status\.  
**Type:** String  
For the list of available status codes and their meanings, see [Generating and updating control findings](controls-findings-create-update.md)\.