# Action<a name="asff-action"></a>

The `Action` object provides details about an action that affects or that was taken on a resource\. The action can be one of the following:
+ A remote IP address issued an AWS API call\.
+ A DNS request was received\.
+ A remote IP address attempted to connect to an EC2 instance\.
+ A remote IP address attempted a port probe on an EC2 instance\.

To view descriptions of `Action` attributes, see [Action](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Action.html) in the *AWS Security Hub API Reference*\.

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