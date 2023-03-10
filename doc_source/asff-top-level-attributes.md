# Optional top\-level attributes<a name="asff-top-level-attributes"></a>

These top\-level attributes are optional in the AWS Security Finding Format\. For more information about these attributes, see [AwsSecurityFinding](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsSecurityFinding.html) in the *AWS Security Hub API Reference*\.

## Action<a name="asff-action"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Action.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Action.html) object provides details about an action that affects or that was taken on a resource\.

**Example**

```
"Action": {
    "ActionType": "PORT_PROBE",
    "PortProbeAction": {
        "PortProbeDetails": [
            {
                "LocalPortDetails": {
                    "Port": 80,
                    "PortName": "HTTP"
                  },
                "LocalIpDetails": {
                     "IpAddressV4": "192.0.2.0"
                 },
                "RemoteIpDetails": {
                    "Country": {
                        "CountryName": "Example Country"
                    },
                    "City": {
                        "CityName": "Example City"
                    },
                   "GeoLocation": {
                       "Lon": 0,
                       "Lat": 0
                   },
                   "Organization": {
                       "AsnOrg": "ExampleASO",
                       "Org": "ExampleOrg",
                       "Isp": "ExampleISP",
                       "Asn": 64496
                   }
                }
            }
        ],
        "Blocked": false
    }
}
```

## CompanyName<a name="asff-companyname"></a>

The name of the company for the product that generated the finding\. For control\-based findings, the company is AWS\.

Security Hub populates this attribute automatically for each finding\. You cannot update it using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) or [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. The exception to this is when you use a custom integration\. See [Using custom product integrations to send findings to AWS Security Hub](securityhub-custom-providers.md)\.

When you use the Security Hub console to filter findings by company name, you use this attribute\.When you use the Security Hub API to filter findings by company name, you use the `aws/securityhub/CompanyName` attribute under `ProductFields`\. Security Hub does not synchronize those two attributes\.

**Example**

```
"CompanyName": "AWS"
```

## Compliance<a name="asff-compliance"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Compliance.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Compliance.html) object provides finding details related to a control\. This attribute is returned for findings generated from a Security Hub control and for findings that AWS Config sends to Security Hub\.

**Example**

```
"Compliance": {
    "AssociatedStandards": [
       {"StandardsId": "standards/aws-foundational-security-best-practices/v/1.0.0"},
       {"StandardsId": "standards/pci-dss/v/3.2.1"},
       {"StandardsId": "ruleset/cis-aws-foundations-benchmark/v/1.2.0"},
       {"StandardsId": "standards/cis-aws-foundations-benchmark/v/1.4.0"},
       {"StandardsId": "standards/service-managed-aws-control-tower/v/1.0.0"}
    ],
    "RelatedRequirements": [
       "PCI DSS v3.2.1/3.4",
       "CIS AWS Foundations Benchmark v1.2.0/2.7",
       "CIS AWS Foundations Benchmark v1.4.0/3.7"
    ],
    "SecurityControlId": "CloudTrail.2",
    "Status": "PASSED",
    "StatusReasons": [
        {
            "ReasonCode": "CLOUDWATCH_ALARMS_NOT_PRESENT",
            "Description": "CloudWatch alarms do not exist in the account"
        }
    ]
}
```

## Confidence<a name="asff-confidence"></a>

The likelihood that a finding accurately identifies the behavior or issue that it was intended to identify\.

`Confidence` should only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

Finding providers who want to provide a value for `Confidence` should use the `Confidence` attribute under `FindingProviderFields`\. See [Using FindingProviderFields](finding-update-batchimportfindings.md#batchimportfindings-findingproviderfields)\.

`Confidence` is scored on a 0–100 basis using a ratio scale\. 0 means 0 percent confidence, and 100 means 100 percent confidence\. For example, a data exfiltration detection based on a statistical deviation of network traffic has low confidence because an actual exfiltration hasn't been verified\.

**Example**

```
"Confidence": 42
```

## Criticality<a name="asff-criticality"></a>

The level of importance that is assigned to the resources that are associated with a finding\.

`Criticality` should only be updated by calling the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) API operation\. Don't update this object with [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html)\.

Finding providers who want to provide a value for `Criticality` should use the `Criticality` attribute under `FindingProviderFields`\. See [Using FindingProviderFields](finding-update-batchimportfindings.md#batchimportfindings-findingproviderfields)\.

`Criticality` is scored on a 0–100 basis, using a ratio scale that supports only full integers\. A score of 0 means that the underlying resources have no criticality, and a score of 100 is reserved for the most critical resources\.

For each resource, consider the following when assigning `Criticality`:
+ Does the affected resource contain sensitive data \(for example, an S3 bucket with PII\)? 
+ Does the affected resource enable an adversary to deepen their access or extend their capabilities to carry out additional malicious activity \(for example, a compromised sysadmin account\)?
+ Is the resource a business\-critical asset \(for example, a key business system that if compromised could have significant revenue impact\)?

You can use the following guidelines:
+ A resource powering mission\-critical systems or containing highly sensitive data can be scored in the 75–100 range\.
+ A resource powering important \(but not critical systems\) or containing moderately important data can be scored in the 25–74 range\.
+ A resource powering unimportant systems or containing nonsensitive data should be scored in the 0–24 range\.

**Example**

```
"Criticality": 99
```

## FindingProviderFields<a name="asff-findingproviderfields"></a>

`FindingProviderFields` includes the following attributes:
+ `Confidence`
+ `Criticality`
+ `RelatedFindings`
+ `Severity`
+ `Types`

You can update`FindingProviderFields` by using the[https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) API operation\. You cannot update it with [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

For details on how Security Hub handles updates from [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) to `FindingProviderFields` and to the corresponding top\-level attributes, see [Using FindingProviderFields](finding-update-batchimportfindings.md#batchimportfindings-findingproviderfields)\.

**Example**

```
"FindingProviderFields": {
    "Confidence": 42,
    "Criticality": 99,
    "RelatedFindings":[
      { 
        "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", 
        "Id": "123e4567-e89b-12d3-a456-426655440000" 
      }
    ],
    "Severity": {
        "Label": "MEDIUM", 
        "Original": "MEDIUM"
    },
    "Types": [ "Software and Configuration Checks/Vulnerabilities/CVE" ]
}
```

## FirstObservedAt<a name="asff-firstobservedat"></a>

Indicates when the potential security issue captured by a finding was first observed\.

This timestamp reflects the time of when the event or vulnerability was first observed\. Consequently, it can differ from the `CreatedAt` timestamp, which reflects the time this finding record was created\. 

This timestamp should be immutable between updates of the finding record but can be updated if a more accurate timestamp is determined\.

**Example**

```
"FirstObservedAt": "2017-03-22T13:22:13.933Z"
```

## LastObservedAt<a name="asff-lastobservedat"></a>

Indicates when the potential security issue that was captured by a finding was most recently observed by the security findings product\.

This timestamp reflects the time when the event or vulnerability was last or most recently observed\. Consequently, it can differ from the `UpdatedAt` timestamp, which reflects when this finding record was last or most recently updated\. 

You can provide this timestamp, but it isn't required upon first observation\. If you provide this field upon first observation, the timestamp should be the same as the `FirstObservedAt` timestamp\. You should update this field to reflect the last or most recently observed timestamp each time a finding is observed\.

**Example**

```
"LastObservedAt": "2017-03-23T13:22:13.933Z"
```

## Malware<a name="asff-malware"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Malware.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Malware.html) object provides a list of malware related to a finding\.

**Example**

```
"Malware": [
    {
        "Name": "Stringler",
        "Type": "COIN_MINER",
        "Path": "/usr/sbin/stringler",
        "State": "OBSERVED"
    }
]
```

## Network \(Retired\)<a name="asff-network"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Network.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Network.html) object provides network\-related information about a finding\.

This object is retired\. To provide this data, you can either map the data to a resource in `Resources`, or use the `Action` object\.

**Example**

```
"Network": {
    "Direction": "IN",
    "OpenPortRange": {
        "Begin": 443,
        "End": 443
    },
    "Protocol": "TCP",
    "SourceIpV4": "1.2.3.4",
    "SourceIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",
    "SourcePort": "42",
    "SourceDomain": "example1.com",
    "SourceMac": "00:0d:83:b1:c0:8e",
    "DestinationIpV4": "2.3.4.5",
    "DestinationIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",
    "DestinationPort": "80",
    "DestinationDomain": "example2.com"
}
```

## NetworkPath<a name="asff-networkpath"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_NetworkPathComponent.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_NetworkPathComponent.html) object provides information about a network path that is related to a finding\. Each entry in `NetworkPath` represents a component of the path\.

**Example**

```
"NetworkPath" : [
    {
        "ComponentId": "abc-01a234bc56d8901ee",
        "ComponentType": "AWS::EC2::InternetGateway",
        "Egress": {
            "Destination": {
                "Address": [ "192.0.2.0/24" ],
                "PortRanges": [
                    {
                        "Begin": 443,
                        "End": 443
                    }
                ]
            },
            "Protocol": "TCP",
            "Source": {
                "Address": ["203.0.113.0/24"]
            }
        },
        "Ingress": {
            "Destination": {
                "Address": [ "198.51.100.0/24" ],
                "PortRanges": [
                    {
                        "Begin": 443,
                        "End": 443
                    }
                 ]
            },
            "Protocol": "TCP",
            "Source": {
                "Address": [ "203.0.113.0/24" ]
            }
        }
     }
]
```

## Note<a name="asff-note"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Note.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Note.html) object specifies a user\-defined note that you can add to a finding\.

A finding provider can provide an initial note for a finding, but cannot add notes after that\. You can only update a note using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

**Example**

```
"Note": {
    "Text": "Don't forget to check under the mat.",
    "UpdatedBy": "jsmith",
    "UpdatedAt": "2018-08-31T00:15:09Z"
}
```

## PatchSummary<a name="asff-patchsummary"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_PatchSummary.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_PatchSummary.html) object provides a summary of the patch compliance status for an instance against a selected compliance standard\.

**Example**

```
"PatchSummary" : {
    "FailedCount" : 0,
    "Id" : "pb-123456789098",
    "InstalledCount" : 100,
    "InstalledOtherCount" : 1023,
    "InstalledPendingReboot" : 0,
    "InstalledRejectedCount" : 0,
    "MissingCount" : 100,
    "Operation" : "Install",
    "OperationEndTime" : "2018-09-27T23:39:31Z",
    "OperationStartTime" : "2018-09-27T23:37:31Z",
    "RebootOption" : "RebootIfNeeded"
}
```

## Process<a name="asff-process"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ProcessDetails.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ProcessDetails.html) object provides process\-related details about a finding\.

Example:

```
"Process": {
    "LaunchedAt": "2018-09-27T22:37:31Z",
    "Name": "syslogd",
    "ParentPid": 56789,
    "Path": "/usr/sbin/syslogd",
    "Pid": 12345,
    "TerminatedAt": "2018-09-27T23:37:31Z"
}
```

## ProductFields<a name="asff-productfields"></a>

A data type where security findings products can include additional solution\-specific details that are not part of the defined AWS Security Finding Format\.

For findings generated by Security Hub controls, `ProductFields` includes information about the control\. See [Generating and updating control findings](controls-findings-create-update.md)\.

This field should not contain redundant data and must not contain data that conflicts with AWS Security Finding Format fields\.

The "`aws/`" prefix represents a reserved namespace for AWS products and services only and must not be submitted with findings from third\-party integrations\.

Although not required, products should format field names as `company-id/product-id/field-name`, where the `company-id` and `product-id` match those supplied in the `ProductArn` of the finding\.

The fields referencing `Archival` are used when Security Hub archives an existing finding\. For example, Security Hub archives existing findings when you disable a control or standard and when you turn [consolidated control findings](controls-findings-create-update.md#consolidated-control-findings) on or off\.

This field may also include information about the standard that includes the control which produced the finding\.

**Example**

```
"ProductFields": {
    "API", "DeleteTrail",
    "ArchivalReasons:0/Description": "The finding is in an ARCHIVED state because consolidated control findings has been turned on or off. This causes findings in the previous state to be archived when new findings are being generated.",
    "ArchivalReasons:0/ReasonCode": "CONSOLIDATED_CONTROL_FINDINGS_UPDATE",
    "aws/inspector/AssessmentTargetName": "My prod env",
    "aws/inspector/AssessmentTemplateName": "My daily CVE assessment",
    "aws/inspector/RulesPackageName": "Common Vulnerabilities and Exposures",
    "generico/secure-pro/Action.Type", "AWS_API_CALL",
    "generico/secure-pro/Count": "6",
    "Service_Name": "cloudtrail.amazonaws.com"
}
```

## ProductName<a name="asff-productname"></a>

Provides the name of the product that generated the finding\. For control\-based findings, the product name is Security Hub\.

Security Hub populates this attribute automatically for each finding\. You cannot update it using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) or [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. The exception to this is when you use a custom integration\. See [Using custom product integrations to send findings to AWS Security Hub](securityhub-custom-providers.md)\.

When you use the Security Hub console to filter findings by product name, you use this attribute\.

When you use the Security Hub API to filter findings by product name, you use the `aws/securityhub/ProductName` attribute under `ProductFields`\.

Security Hub does not synchronize those two attributes\.

## RecordState<a name="asff-recordstate"></a>

Provides the record state of a finding\. 

By default, when initially generated by a service, findings are considered `ACTIVE`\.

The `ARCHIVED` state indicates that a finding should be hidden from view\. Archived findings are not immediately deleted\. You can search, review, and report on them\. Security Hub automatically archives control\-based findings if the associated resource is deleted, the resource does not exist, or the control is disabled\.

`RecordState` is intended for finding providers, and can only be updated by [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html)\. You cannot update it using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

To track the status of your investigation into a finding, use [`Workflow`](#asff-workflow) instead of `RecordState`\.

If the record state changes from `ARCHIVED` to `ACTIVE`, and the workflow status of the finding is either `NOTIFIED` or `RESOLVED`, then Security Hub automatically sets the workflow status to `NEW`\.

**Example**

```
"RecordState": "ACTIVE"
```

## Region<a name="asff-region"></a>

Specifies the AWS Region from which the finding was generated\.

Security Hub populates this attribute automatically for each finding\. You cannot update it using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) or [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

**Example**

```
"Region": "us-west-2"
```

## RelatedFindings<a name="asff-relatedfindings"></a>

Provides a list of findings that are related to the current finding\.

`RelatedFindings` should only be updated with the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) API operation\. You should not update this object with [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html)\.

For [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) requests, finding providers should use the `RelatedFindings` object under [`FindingProviderFields`](#asff-findingproviderfields)\.

To view descriptions of `RelatedFindings` attributes, see [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_RelatedFinding.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_RelatedFinding.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"RelatedFindings": [
    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", 
      "Id": "123e4567-e89b-12d3-a456-426655440000" },
    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", 
      "Id": "AcmeNerfHerder-111111111111-x189dx7824" }
]
```

## Remediation<a name="asff-remediation"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Remediation.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Remediation.html) object provides information about recommended remediation steps to address the finding\.

**Example**

```
"Remediation": {
    "Recommendation": {
        "Text": "For instructions on how to fix this issue, see the AWS Security Hub documentation for EC2.2.",
        "Url": "https://docs.aws.amazon.com/console/securityhub/EC2.2/remediation"
    }
}
```

## Sample<a name="asff-sample"></a>

Specifies whether the finding is a sample finding\.

```
"Sample": true
```

## SourceUrl<a name="asff-sourceurl"></a>

The `SourceUrl` object provides a URL that links to a page about the current finding in the finding product\.

```
"SourceUrl": "http://sourceurl.com"
```

## ThreatIntelIndicators<a name="asff-threatintelindicators"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ThreatIntelIndicator.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ThreatIntelIndicator.html) object provides threat intelligence details that are related to a finding\.

**Example**

```
"ThreatIntelIndicators": [
  {
    "Category": "BACKDOOR",
    "LastObservedAt": "2018-09-27T23:37:31Z",
    "Source": "Threat Intel Weekly",
    "SourceUrl": "http://threatintelweekly.org/backdoors/8888",
    "Type": "IPV4_ADDRESS",
    "Value": "8.8.8.8",
  }
]
```

## Threats<a name="asff-threats"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Threat.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Threat.html) object provides details about the threat detected by a finding\.

**Example**

```
"Threats": [{
    "FilePaths": [{
        "FileName": "b.txt",
        "FilePath": "/tmp/b.txt",
        "Hash": "sha256",
        "ResourceId": "arn:aws:ec2:us-west-2:123456789012:volume/vol-032f3bdd89aee112f"
    }],
    "ItemCount": 3,
    "Name": "Iot.linux.mirai.vwisi",
    "Severity": "HIGH"
}]
```

## UserDefinedFields<a name="asff-userdefinedfields"></a>

Provides a list of name\-value string pairs that are associated with the finding\. These are custom, user\-defined fields that are added to a finding\. These fields can be generated automatically through your specific configuration\.

Finding providers should not use this field for data that the product generates\. Instead, finding providers can use the `ProductFields` field for data that does not map to any standard AWS Security Finding Format field\.

These fields can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

**Example**

```
"UserDefinedFields": {
    "reviewedByCio": "true",
    "comeBackToLater": "Check this again on Monday"
}
```

## VerificationState<a name="asff-verificationstate"></a>

Provides the veracity of a finding\. Findings products can provide a value of `UNKNOWN` for this field\. A findings product should provide a value for this field if there is a meaningful analog in the findings product's system\. This field is typically populated by a user determination or action after investigating a finding\.

A finding provider can provide an initial value for this attribute, but cannot update it after that\. You can only update this attribute by using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

```
"VerificationState": "Confirmed"
```

## Vulnerabilities<a name="asff-vulnerabilities"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Vulnerability.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Vulnerability.html) object provides a list of vulnerabilities that are associated with a finding\.

**Example**

```
"Vulnerabilities" : [
    {
        "Cvss": [
            {
                "BaseScore": 4.7,
                "BaseVector": "AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N",
                "Version": "V3"
            },
            {
                "BaseScore": 4.7,
                "BaseVector": "AV:L/AC:M/Au:N/C:C/I:N/A:N",
                "Version": "V2"
            }
        ],
        "FixAvailable": "YES",
        "Id": "CVE-2020-12345",
        "ReferenceUrls":[
           "http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-12418",
            "http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-17563"
        ],
        "RelatedVulnerabilities": ["CVE-2020-12345"],
        "Vendor": {
            "Name": "Alas",
            "Url":"https://alas.aws.amazon.com/ALAS-2020-1337.html",
            "VendorCreatedAt":"2020-01-16T00:01:43Z",
            "VendorSeverity":"Medium",
            "VendorUpdatedAt":"2020-01-16T00:01:43Z"
        },
        "VulnerablePackages": [
            {
                "Architecture": "x86_64",
                "Epoch": "1",
                "FilePath": "/tmp",
                "FixedInVersion": "0.14.0",
                "Name": "openssl",
                "PackageManager": "OS",
                "Release": "16.amzn2.0.3",
                "Remediation": "Update aws-crt to 0.14.0",
                "SourceLayerArn": "arn:aws:lambda:us-west-2:123456789012:layer:id",
                "SourceLayerHash": "sha256:c1962c35b63a6ff6ce7df6e042ee82371a605ca9515569edec46ff14f926f001",
                "Version": "1.0.2k"
            }
        ]
    }
]
```

## Workflow<a name="asff-workflow"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Workflow.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Workflow.html) object provides information about the status of the investigation into a finding\.

This field is intended for customers to use with remediation, orchestration, and ticketing tools\. It is not intended for finding providers\.

You can only update the `Workflow` field with [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Customers can also update it from the console\. See [Setting the workflow status for findings](finding-workflow-status.md)\.

**Example**

```
"Workflow": {
    "Status": "NEW"
}
```

## WorkflowState \(Retired\)<a name="asff-workflowstate"></a>

This object is retired and has been replaced by the `Status` field of the `Workflow` object\.

This field provides the workflow state of a finding\. Findings products can provide the value of `NEW` for this field\. A findings product can provide a value for this field if there is a meaningful analog in the findings product's system\.

**Example**

```
"WorkflowState": "NEW"
```