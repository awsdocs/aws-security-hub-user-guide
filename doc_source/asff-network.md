# Network \(Deprecated\)<a name="asff-network"></a>

An example of network\-related information about a finding\.

This object is deprecated\. To provide this data, you can either map it to a resource in `Resources`, or use the `Action` object\.

To view descriptions of `Network` attributes, see [Network](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Network.html) in the *AWS Security Hub API Reference*\.

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