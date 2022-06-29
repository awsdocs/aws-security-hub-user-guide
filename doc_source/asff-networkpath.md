# NetworkPath<a name="asff-networkpath"></a>

The `NetworkPath` object provides information about a network path that is relevant to a finding\. Each entry under `NetworkPath` represents a component of that path\.

To view descriptions of `NetworkPath` attributes, see [NetworkPathComponent](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_NetworkPathComponent.html) in the *AWS Security Hub API Reference*\.

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