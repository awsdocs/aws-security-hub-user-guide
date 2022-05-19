# Vulnerabilities<a name="asff-vulnerabilities"></a>

The `Vulnerabilities` object provides a list of vulnerabilities that are associated with the findings\.

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
                "Name": "openssl",
                "Release": "16.amzn2.0.3",
                "Version": "1.0.2k"
            }
        ]
    }
]
```

**Contents**
+ [Vulnerabilities attributes](#asff-vulnerabilities-attributes)
+ [Cvss](#asff-vulnerabilities-cvss)
  + [Adjustments](#asff-vulnerabilities-cvss-adjustments)
+ [Vendor](#asff-vulnerabilities-vendor)
+ [VulnerablePackages](#asff-vulnerabilities-vulnerablepackages)

## Vulnerabilities attributes<a name="asff-vulnerabilities-attributes"></a>

Each vulnerability can have the following attributes\.

**[`Cvss`](#asff-vulnerabilities-cvss)**  
Optional  
Common Vulnerability Scoring System \(CVSS\) scores from the advisory that are related to the vulnerability\.  
**Type:** Array of objects

**`Id`**  
Required  
The identifier of the vulnerability\.  
**Type:** String  
**Maximum length:** 128

**`ReferenceUrls`**  
Optional  
A list of URLs that provide additional information about the vulnerability\.  
**Type:** Array of strings

**`RelatedVulnerabilities`**  
Optional  
List of vulnerabilities that are related to this vulnerability\. For each vulnerability, provide the vulnerability ID\.  
**Type:** Array of strings

**[`Vendor`](#asff-vulnerabilities-vendor)**  
Optional  
Information about the vendor that generates the vulnerability report\.  
**Type:** Object

**[`VulnerablePackages`](#asff-vulnerabilities-vulnerablepackages)**  
Optional  
List of packages that have the vulnerability\.  
**Type:** Array of objects

## Cvss<a name="asff-vulnerabilities-cvss"></a>

The `Cvss` object provides a list of CVSS scores for the vulnerability\.

Each `CVSS` score can have the following attributes\.

**[`Adjustments`](#asff-vulnerabilities-cvss-adjustments)**  
Optional  
**Type:** Array of objects

**`BaseScore`**  
Optional  
The base CVSS score\.  
**Type:** Number

**`BaseVector`**  
Optional  
The base scoring vector for the CVSS score\.  
**Type:** String

**`Source`**  
Optional  
The origin of the original CVSS score and vector\.  
**Type:** String

**`Version`**  
Optional  
The version of CVSS for the CVSS score\.  
**Type:** String

### Adjustments<a name="asff-vulnerabilities-cvss-adjustments"></a>

`Adjustments` can have the following attributes\.

**`Metric`**  
Optional  
The metric to adjust\.  
Type: String

**`Reason`**  
Optional  
The reason for the adjustment\.  
**Type:** String  
**Minimum length:** 1  
**Maximum length:** 512

## Vendor<a name="asff-vulnerabilities-vendor"></a>

The `Vendor` object provides information about the vendor that generated the vulnerability advisory for the vulnerability\.

The `Vendor` object can have the following attributes\.

**`Name`**  
Required  
The name of the vendor\.  
**Type:** String  
**Maximum length:** 32

**`Url`**  
Optional  
The URL of the vulnerability advisory\.  
**Type:** String

**`VendorCreatedAt`**  
Optional  
Indicates when the vulnerability advisory was created\.  
**Type:** String  
**Format:** Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.

**`VendorSeverity`**  
Optional  
The severity that the vendor assigned to the vulnerability\.  
**Type:** String  
**Maximum length:** 32

**`VendorUpdatedAt`**  
Optional  
Indicates when the vulnerability advisory was last updated\.  
**Type:** String  
**Format:** Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.

## VulnerablePackages<a name="asff-vulnerabilities-vulnerablepackages"></a>

The `VulnerablePackages` object provides the list of packages that have the vulnerability\.

Each package can have the following attributes\.

**`Architecture`**  
Optional  
The architecture used for the vulnerable package\.  
**Type:** String

**`Epoch`**  
Optional  
The epoch for the vulnerable package\.  
**Type:** String

**`FilePath`**  
Optional  
The file system path to the package manager inventory file\.  
**Type:** String

**`Name`**  
Optional  
The name of the vulnerable package\.  
**Type:** String

**`PackageManager`**  
Optional  
The source of the package\.  
**Type:** String

**`Release`**  
Optional  
The release for the vulnerable package\.  
**Type:** String

**`Version`**  
Optional  
The version of the vulnerable package\.  
**Type:** String