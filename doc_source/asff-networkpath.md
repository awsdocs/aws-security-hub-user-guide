# NetworkPath<a name="asff-networkpath"></a>

The `NetworkPath` object provides information about a network path that is relevant to a finding\. Each entry under `NetworkPath` represents a component of that path\.

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

## NetworkPath attributes<a name="asff-networkpath-attributes"></a>

Each component of the network path can have the following attributes\.

**`ComponentId`**  
Required  
The identifier of a component in the network path\.  
**Type:** String

**`ComponentType`**  
Required  
The type of component\.  
**Type:** String

**[`Egress`](#asff-networkpath-egress)**  
Optional  
Information about the component that comes after the current component in the network path\.  
**Type:** Object

**[`Ingress`](#asff-networkpath-ingress)**  
Optional  
Information about the component that comes before the current component in the network path\.  
**Type:** Object

## Egress<a name="asff-networkpath-egress"></a>

The `Egress` object contains information about the component that comes after the current component in the network path\. It can have the following attributes\.

**[`Destination`](#asff-networkpath-egress-ingress-destination)**  
Optional  
Information about the destination of the component\.  
**Type:** Object

**`Protocol`**  
Optional  
The protocol used for the component\.  
Type: String

**[`Source`](#asff-networkpath-egress-ingress-source)**  
Optional  
Information about the origin of the component\.  
**Type:** Object

## Ingress<a name="asff-networkpath-ingress"></a>

The `Ingress` object contains information about the previous component in the network path\. It can have the following attributes\.

**[`Destination`](#asff-networkpath-egress-ingress-destination)**  
Optional  
Information about the destination for the previous component\.  
**Type:** Object

**`Protocol`**  
Optional  
The protocol used by the previous component\.  
**Type:** String

**[`Source`](#asff-networkpath-egress-ingress-source)**  
Optional  
Information about the origin of the previous component\.  
**Type:** Object

## Destination<a name="asff-networkpath-egress-ingress-destination"></a>

The `Destination` object in `Egress` or `Ingress` contains the destination information for the previous or next component\. It can have the following attributes\.

**`Address`**  
Optional  
IP addresses of the previous or next component\.  
**Type:** Array of strings

**`PortRanges`**  
Optional  
List of open port ranges for the destination of the previous or next component\.  
**Type:** Array of objects

**`PortRanges.Begin`**  
Optional  
For an open port range, the beginning of the range\.  
**Type:** Integer

**`PortRanges.End`**  
Optional  
For an open port range, the end of the range\.  
**Type:** Number

## Source<a name="asff-networkpath-egress-ingress-source"></a>

The `Source` object under `Egress` or `Ingress` contains information about the origin of the previous or next component\. It can have the following attributes\.

**`Address`**  
Optional  
IP addresses for the origin of the previous or next component\.  
**Type:** Array of strings

**`PortRanges`**  
Optional  
List of open port ranges for the origin of the previous or next component\.  
**Type: **Array of objects

**`PortRanges.Begin`**  
Optional  
For an open port range, the beginning of the range\.  
**Type:** Integer

**`PortRanges.End`**  
Optional  
For an open port range, the end of the range\.  
**Type:** Number