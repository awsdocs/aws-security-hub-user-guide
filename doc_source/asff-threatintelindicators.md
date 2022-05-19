# ThreatIntelIndicators<a name="asff-threatintelindicators"></a>

Threat intelligence details that are related to a finding\.

Type: Array of up to five threat intelligence indicator objects

**Example**

```
"ThreatIntelIndicators": [
  {
    "Type": "IPV4_ADDRESS",
    "Value": "8.8.8.8",
    "Category": "BACKDOOR",
    "LastObservedAt": "2018-09-27T23:37:31Z",
    "Source": "Threat Intel Weekly",
    "SourceUrl": "http://threatintelweekly.org/backdoors/8888"
  }
]
```

Each threat intelligence indicator object can have the following attributes\.

**`Category`**  
Optional  
The category of a threat intel indicator\.  
**Type:** Enum  
**Valid values:** `BACKDOOR` \| `CARD_STEALER` \| `COMMAND_AND_CONTROL` \| `DROP_SITE` \| `EXPLOIT_SITE` \| `KEYLOGGER`

**`LastObservedAt`**  
Optional  
Indicates when the threat intelligence indicator was last observed\.  
**Type:** String  
**Format:** Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.

**`Source`**  
Optional  
The source of the threat intelligence\.  
**Type:** String  
**Maximum length:** 64

**`SourceUrl`**  
Optional  
The URL for more details from the source of the threat intelligence\.  
**Type:** URL

**`Type`**  
Optional  
The type of a threat intelligence indicator\.  
**Type:** Enum  
**Valid values:** `DOMAIN` \| `EMAIL_ADDRESS` \| `HASH_MD5` \| `HASH_SHA1` \| `HASH_SHA256` \|` HASH_SHA512` \| `IPV4_ADDRESS` \| `IPV6_ADDRESS` \| `MUTEX` \| `PROCESS` \| `URL`

**`Value`**  
Optional  
The value of a threat intelligence indicator\.  
**Type:** String  
**Maximum length:** 512