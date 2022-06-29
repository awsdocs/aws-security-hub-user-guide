# Vulnerabilities<a name="asff-vulnerabilities"></a>

The `Vulnerabilities` object provides a list of vulnerabilities that are associated with the findings\.

To view descriptions of `Vulnerabilities` attributes, see [Vulnerability](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Vulnerability.html) in the *AWS Security Hub API Reference*\.

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