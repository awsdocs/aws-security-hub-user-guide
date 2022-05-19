# Network \(Deprecated\)<a name="asff-network"></a>

The details of network\-related information about a finding\.

This object is deprecated\. To provide this data, you can either map it to a resource in `Resources`, or use the `Action` object\.

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

## Network attributes<a name="asff-network-attributes"></a>

The `Network` object can have the following attributes\.

**`DestinationDomain`**  
Optional  
The destination domain of network\-related information about a finding\.  
**Type:** String  
**Maximum length:** 128  
**Example**  

```
"DestinationDomain": "there.com"
```

**`DestinationIpV4`**  
Optional  
The destination IPv4 address of network\-related information about a finding\.  
**Type:** IPv4  
**Example**  

```
"DestinationIpV4": "2.3.4.5"
```

**`DestinationIpV6`**  
Optional  
The destination IPv6 address of network\-related information about a finding\.   
**Type:** IPv6  
**Example**  

```
"DestinationIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C"
```

**`DestinationPort`**  
Optional  
The destination port of network\-related information about a finding\.  
**Type:** Number  
**Valid values:** Range of 0–65535  
**Example**  

```
"DestinationPort": "80"
```

**`Direction`**  
Optional  
The direction of network traffic that is associated with a finding\.  
**Type:** Enum  
**Valid values:** `IN` \| `OUT`  
**Example**  

```
"Direction": "IN"
```

**[`OpenPortRange`](#asff-network-openportrange)**  
Optional  
The range of open ports that is present in the network\.  
**Type:** Object

**`Protocol`**  
Optional  
The protocol of network\-related information about a finding\.  
**Type:** String  
**Maximum length:** 16  
The name should be the [IANA registered name](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml) for the associated port except in the case where the finding product can determine a more accurate protocol\.  
**Example**  

```
"Protocol": "TCP"
```

**`SourceDomain`**  
Optional  
The source domain of network\-related information about a finding\.   
**Type:** String  
**Maximum length:** 128  
**Example**  

```
"SourceDomain": "here.com"
```

**`SourceIpV4`**  
Optional  
The source IPv4 address of network\-related information about a finding\.   
**Type:** IPv4  
**Example**  

```
"SourceIpV4": "1.2.3.4"
```

**`SourceIpV6`**  
Optional  
The source IPv6 address of network\-related information about a finding\.  
**Type:** IPv6  
**Example**  

```
"SourceIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C"
```

**`SourceMac`**  
Optional  
The source media access control \(MAC\) address of network\-related information about a finding\.  
**Type:** String  
**Format:** Must match `MM:MM:MM:SS:SS:SS`  
**Example**  

```
"SourceMac": "00:0d:83:b1:c0:8e"
```

**`SourcePort`**  
Optional  
The source port of network\-related information about a finding\.  
**Type:** Number  
**Valid values:** Range of 0–65535  
**Example**  

```
"SourcePort": "80"
```

## OpenPortRange<a name="asff-network-openportrange"></a>

Provides the beginning and end ports of the open port range\.

`OpenPortRange` can have the following attributes\.

**`Begin`**  
Optional  
The first port in the port range\.  
**Type:** Integer

**`End`**  
Optional  
The last port in the port range\.  
**Type:** Integer