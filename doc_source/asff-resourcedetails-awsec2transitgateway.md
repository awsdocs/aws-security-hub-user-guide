# AwsEc2TransitGateway<a name="asff-resourcedetails-awsec2transitgateway"></a>

The `AwsEc2TransitGateway` object provides details about virtual private clouds \(VPCs\) and on\-premises networks\.

The following is an example `AwsEc2TransitGateway` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsEc2TransitGateway` attributes, see [AwsEc2TransitGatewayDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2TransitGatewayDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2TransitGateway": {
	"AmazonSideAsn": 65000,
	"AssociationDefaultRouteTableId": "tgw-rtb-099ba47cbbea837cc",
	"AutoAcceptSharedAttachments": "disable",
	"DefaultRouteTableAssociation": "enable",
	"DefaultRouteTablePropagation": "enable",
	"Description": "sample transit gateway",
	"DnsSupport": "enable",
	"Id": "tgw-042ae6bf7a5c126c3",
	"MulticastSupport": "disable",
	"PropagationDefaultRouteTableId": "tgw-rtb-099ba47cbbea837cc",
	"TransitGatewayCidrBlocks": ["10.0.0.0/16"],
	"VpnEcmpSupport": "enable"
}
```