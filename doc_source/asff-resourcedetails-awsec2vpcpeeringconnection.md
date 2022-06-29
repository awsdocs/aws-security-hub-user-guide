# AwsEc2VpcPeeringConnection<a name="asff-resourcedetails-awsec2vpcpeeringconnection"></a>

The `AwsCloudFormationStack` object provides details about the networking connection between two VPCs\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2VpcPeeringConnection` object\. To view descriptions of `AwsEc2VpcPeeringConnection` attributes, see [AwsEc2VpcPeeringConnectionDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2VpcPeeringConnectionDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2VpcPeeringConnection": { 
	"AccepterVpcInfo": {
		"CidrBlock": "10.0.0.0/28",
		"CidrBlockSet": [{
			"CidrBlock": "10.0.0.0/28"
		}],
		"Ipv6CidrBlockSet": [{
			"Ipv6CidrBlock": "2002::1234:abcd:ffff:c0a8:101/64"
		}],
		"OwnerId": "012345678910",
		"PeeringOptions": {
			"AllowDnsResolutionFromRemoteVpc": true,
			"AllowEgressFromLocalClassicLinkToRemoteVpc": false,
			"AllowEgressFromLocalVpcToRemoteClassicLink": true
		},
		"Region": "us-west-2",
		"VpcId": "vpc-i123456"
	},
	"ExpirationTime": "2022-02-18T15:31:53.161Z",
	"RequesterVpcInfo": {
		"CidrBlock": "192.168.0.0/28",
		"CidrBlockSet": [{
			"CidrBlock": "192.168.0.0/28"
		}],
		"Ipv6CidrBlockSet": [{
			"Ipv6CidrBlock": "2002::1234:abcd:ffff:c0a8:101/64"
		}],
		"OwnerId": "012345678910",
		"PeeringOptions": {
			"AllowDnsResolutionFromRemoteVpc": true,
			"AllowEgressFromLocalClassicLinkToRemoteVpc": false,
			"AllowEgressFromLocalVpcToRemoteClassicLink": true
		},
		"Region": "us-west-2",
		"VpcId": "vpc-i123456"
	},
	"Status": {
		"Code": "initiating-request",
		"Message": "Active"
	},
	"VpcPeeringConnectionId": "pcx-1a2b3c4d"
}
```