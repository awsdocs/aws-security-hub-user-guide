# Action<a name="asff-action"></a>

The `Action` object provides details about an action that affects or that was taken on a resource\. The action can be one of the following:
+ A remote IP address issued an AWS API call\.
+ A DNS request was received\.
+ A remote IP address attempted to connect to an EC2 instance\.
+ A remote IP address attempted a port probe on an EC2 instance\.

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

**Contents**
+ [Action attributes](#asff-action-attributes)
+ [AwsApiCallAction](#asff-action-awsapicallaction)
  + [DomainDetails](#asff-action-awsapicallaction-domaindetails)
+ [DnsRequestAction](#asff-action-dnsrequestaction)
+ [NetworkConnectionAction](#asff-action-networkconnectionaction)
  + [RemotePortDetails](#asff-action-networkconnectionaction-remoteportdetails)
+ [PortProbeAction](#asff-action-portprobeaction)
  + [PortProbeDetails](#asff-action-portprobeaction-portprobedetails)
+ [LocalPortDetails](#asff-action-localportdetails)
+ [RemoteIpDetails](#asff-action-remoteipdetails)
  + [City](#asff-action-remoteipdetails-city)
  + [Country](#asff-action-remoteipdetails-country)
  + [Geolocation](#asff-action-remoteipdetails-geolocation)
  + [Organization](#asff-action-remoteipdetails-organization)

## Action attributes<a name="asff-action-attributes"></a>

`Action` can have the following attributes\.

`ActionType`  
Optional  
The type of action that was detected\. The action type determines which of the other objects is provided in the `Action` object\.  
**Type:** String  
**Valid values:** `NETWORK_CONNECTION` \| `AWS_API_CALL` \| `DNS_REQUEST` \| `PORT_PROBE`

[`AwsApiCallAction`](#asff-action-awsapicallaction)  
Optional  
Included if `ActionType` is `AWS_API_CALL`\.  
Provides details about the API call that was detected\.  
**Type:** Object

[`DnsRequestAction`](#asff-action-dnsrequestaction)  
Optional  
Included if `ActionType` is `DNS_REQUEST`\.  
Provides details about the DNS request that was detected\.  
**Type: **Object

[`NetworkConnectionAction`](#asff-action-networkconnectionaction)  
Optional  
Included if `ActionType` is `NETWORK_CONNECTION`\.  
Provides details about the network connection that was detected\.  
**Type:** Object

[`PortProbeAction`](#asff-action-portprobeaction)  
Optional  
Included if `ActionType` is `PORT_PROBE`\.  
Provides details about the port probe that was detected\.  
**Type:** Object

## AwsApiCallAction<a name="asff-action-awsapicallaction"></a>

`AwsApiCallAction` is provided if `ActionType` is `AWS_API_CALL`\. It provides details about the API call that was detected\.

`AwsApiCallAction` can have the following attributes\.

`AffectedResources`  
Optional  
Identifies the resources that were affected by the API call\.  
**Type:** Map of key\-value pairs

`Api`  
Optional  
The name of the API method that was issued\.  
**Type:** String

`CallerType`  
Optional  
Indicates whether the API call originated from a remote IP address or from a DNS domain\.  
**Type:** String  
**Valid values:** `domain` \| `remoteIp`

[`DomainDetails`](#asff-action-awsapicallaction-domaindetails)  
Optional  
Provided if `CallerType` is `domain`\. Provides information about the DNS domain that the API call originated from\.  
Type: Object

`FirstSeen`  
Optional  
Indicates when the API call was first observed\.  
**Type:** String  
**Format:** Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.

`LastSeen`  
Optional  
Indicates when the API call was most recently observed\.  
**Type:** String  
**Format:** Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.

[`RemoteIpDetails`](#asff-action-remoteipdetails)  
Optional  
Provided if `CallerType` is `remoteIp`\. Provides information about the remote IP address that the API call originated from\.  
**Type:** Object

`ServiceName`  
Optional  
The name of the AWS service that the API call belongs to\.  
**Type:** String

### DomainDetails<a name="asff-action-awsapicallaction-domaindetails"></a>

`DomainDetails` is provided if `AwsApiCallAction.CallerType` is `domain`\. It provides information about the DNS domain that issued the API call\.

`DomainDetails` can have the following attributes\.

`Domain`  
Optional  
The name of the DNS domain that issued the API call\.  
**Type:** String

## DnsRequestAction<a name="asff-action-dnsrequestaction"></a>

`DnsRequestAction` is provided if `ActionType` is `DNS_REQUEST`\. It provides details about the DNS request that was detected\.

`DnsRequestAction` can have the following attributes\.

`Blocked`  
Optional  
Indicates whether the DNS request was blocked\.  
**Type:** Boolean

`Domain`  
Optional  
The DNS domain that is associated with the DNS request\.  
**Type:** String

`Protocol`  
Optional  
The protocol that was used for the DNS request\.  
**Type:** String

## NetworkConnectionAction<a name="asff-action-networkconnectionaction"></a>

`NetworkConnectionAction` is provided if `ActionType` is `NETWORK_CONNECTION`\. It provides details about the attempted network connection that was detected\.

`NetworkConnectionAction` can have the following attributes\.

`Blocked`  
Optional  
Indicates whether the network connection attempt was blocked\.  
**Type:** Boolean

`ConnectionDirection`  
Optional  
The direction of the network connection request\.  
**Type:** String  
**Valid values:** `IN` \| `OUT`

[`LocalPortDetails`](#asff-action-localportdetails)  
Optional  
Information about the port on the EC2 instance\.  
**Type:** Object

`Protocol`  
Optional  
The protocol used to make the network connection request\.  
**Type:** String

[`RemoteIpDetails`](#asff-action-remoteipdetails)  
Optional  
Information about the remote IP address that issued the network connection request\.  
**Type:** Object

[`RemotePortDetails`](#asff-action-networkconnectionaction-remoteportdetails)  
Optional  
Information about the port on the remote IP address\.  
**Type:** Object

### RemotePortDetails<a name="asff-action-networkconnectionaction-remoteportdetails"></a>

`RemotePortDetails` provides information about the remote port that was involved in the attempted network connection\.

`RemotePortDetails` can have the following attributes\.

`Port`  
Optional  
The number of the port\.  
**Type:** Integer

`PortName`  
Optional  
The port name of the remote connection\.  
Type: String

## PortProbeAction<a name="asff-action-portprobeaction"></a>

`PortProbeAction` is provided if `ActionType` is `PORT_PROBE`\. It provides details about the attempted port probe that was detected\.

`PortProbeAction` can have the following attributes\.

`Blocked`  
Optional  
Whether the port probe was blocked\.  
**Type:** Boolean

[`PortProbeDetails`](#asff-action-portprobeaction-portprobedetails)  
Optional  
Information about the ports affected by the port probe\.  
**Type:** Array of objects

### PortProbeDetails<a name="asff-action-portprobeaction-portprobedetails"></a>

`PortProbeDetails` contains a list of port scans that were part of the port probe\. For each scan, `PortProbeDetails` provides information about the local IP address and port that were scanned as well as the remote IP address that the scan originated from\.

`PortProbeDetails` can have the following attributes\.

`LocalIpDetails`  
Optional  
Provides information about the IP address where the scanned port is located\.  
**Type:** Object

[`LocalPortDetails`](#asff-action-localportdetails)  
Optional  
Provides information about the port that was scanned\.  
**Type:** Object

[`RemoteIpDetails`](#asff-action-remoteipdetails)  
Optional  
Provides information about the remote IP address that performed the scan\.  
**Type:** Object

`LocalIpDetails` can have the following attributes\.

`IpAddressV4`  
Optional  
The IP address\.  
**Type:** String

## LocalPortDetails<a name="asff-action-localportdetails"></a>

For `NetworkConnectionAction` and `PortProbeDetails`, `LocalPortDetails` provides information about the local port that was involved in the action\.

`LocalPortDetails` can have the following attributes\.

`Port`  
Optional  
The number of the port\.  
**Type:** Integer

`PortName`  
Optional  
The port name of the local connection\.  
**Type:** String

## RemoteIpDetails<a name="asff-action-remoteipdetails"></a>

In the details for `AwsApiCallAction`, `NetworkConnectionAction`, and `PortProbeAction`, the `RemoteIpDetails` object provides information about the remote IP address that was involved in the action\.

`RemoteIpDetails` can have the following attributes\.

[`City`](#asff-action-remoteipdetails-city)  
Optional  
The city where the remote IP address is located\.  
**Type:** Object

[`Country`](#asff-action-remoteipdetails-country)  
Optional  
The country where the remote IP address is located\.  
**Type:** Object

[`Geolocation`](#asff-action-remoteipdetails-geolocation)  
Optional  
The coordinates of the location of the remote IP address\.  
**Type:** Object

`IpAddressV4`  
Optional  
The IP address\.  
**Type:** String

[`Organization`](#asff-action-remoteipdetails-organization)  
Optional  
The internet service provider \(ISP\) organization that is associated with the remote IP address\.  
**Type:** Object

### City<a name="asff-action-remoteipdetails-city"></a>

`City` contains information about the city where the remote IP address is located\.

`City` can have the following attributes\.

`CityName`  
Optional  
The name of the city where the remote IP address is located\.  
**Type:** String

### Country<a name="asff-action-remoteipdetails-country"></a>

`Country` identifies the country where the remote IP address is located\.

`Country` can have the following attributes\.

`CountryCode`  
Optional  
The 2\-letter ISO 3166 country code for the country where the remote IP address is located\.  
**Type:** String

`CountryName`  
Optional  
The name of the country where the remote IP address is located\.  
**Type:** String

### Geolocation<a name="asff-action-remoteipdetails-geolocation"></a>

`Geolocation` provides the latitude and longitude coordinates of the remote IP address location\.

`Geolocation` can have the following attributes\.

`Lat`  
Optional  
The latitude of the location of the remote IP address\.  
**Type:** Double

`Lon`  
Optional  
The longitude of the location of the remote IP address\.  
**Type:** Double

### Organization<a name="asff-action-remoteipdetails-organization"></a>

`Organization` identifies the ISP organization that is associated with the remote IP address\.

`Organization` can have the following attributes\.

`Asn`  
Optional  
The Autonomous System Number \(ASN\) of the internet provider of the remote IP address\.  
**Type:** String

`AsnOrg`  
Optional  
The name of the organization that registered the ASN\.  
**Type:** String

`Isp`  
Optional  
The ISP information for the internet provider\.  
**Type:** String

`Org`  
Optional  
The name of the internet provider\.  
**Type:** String