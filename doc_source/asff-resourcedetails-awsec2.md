# AwsEc2<a name="asff-resourcedetails-awsec2"></a>

The following are examples of the AWS Security Finding Format for `AwsEc2` resources\.

## AwsEc2Eip<a name="asff-resourcedetails-awsec2eip"></a>

The `AwsEc2Eip` object provides information about an Elastic IP address\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Eip` object\. To view descriptions of `AwsEc2Eip` attributes, see [AwsEc2EipDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2EipDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2Eip": {
    "InstanceId": "instance1",
    "PublicIp": "192.0.2.04",
    "AllocationId": "eipalloc-example-id-1",
    "AssociationId": "eipassoc-example-id-1",
    "Domain": "vpc",
    "PublicIpv4Pool": "anycompany",
    "NetworkBorderGroup": "eu-central-1",
    "NetworkInterfaceId": "eni-example-id-1",
    "NetworkInterfaceOwnerId": "777788889999",
    "PrivateIpAddress": "192.0.2.03"
}
```

## AwsEc2Instance<a name="asff-resourcedetails-awsec2instance"></a>

The `AwsEc2Instance` object provides details about an Amazon EC2 instance\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Instance` object\. To view descriptions of `AwsEc2Instance` attributes, see [AwsEc2InstanceDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2InstanceDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2Instance": { 
    "IamInstanceProfileArn": "string",
    "ImageId": "string",
    "IpV4Addresses": [ "string" ],
    "IpV6Addresses": [ "string" ],
    "KeyName": "string",
    "LaunchedAt": "string",
    "NetworkInterfaces": [
      {
         "NetworkInterfaceId": "string"
      }
    ],
    "SubnetId": "string",
    "Type": "string",
    "VpcId": "string"
}
```

## AwsEc2LaunchTemplate<a name="asff-resourcedetails-awsec2launchtemplate"></a>

The `AwsEc2LaunchTemplate` object contains details about an Amazon Elastic Compute Cloud launch template that specifies instance configuration information\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2LaunchTemplate` object\. To view descriptions of `AwsEc2LaunchTemplate` attributes, see [AwsEc2LaunchTemplateDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2LaunchTemplateDetals.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2LaunchTemplate": {
    "DefaultVersionNumber": "1",
    "ElasticGpuSpecifications": ["string"],
    "ElasticInferenceAccelerators": ["string"],
    "Id": "lt-0a16e9802800bdd85",
    "ImageId": "ami-0d5eff06f840b45e9",
    "LatestVersionNumber": "1",
    "LaunchTemplateData": {
    	"BlockDeviceMappings": [{
    		"DeviceName": "/dev/xvda",
    		"Ebs": {
    			"DeleteonTermination": true,
    			"Encrypted": true,
    			"SnapshotId": "snap-01047646ec075f543",
    			"VolumeSize": 8,
    			"VolumeType:" "gp2"
    		}
    	}],
    	"MetadataOptions": {
    		"HttpTokens": "enabled",
    		"HttpPutResponseHopLimit" : 1
    	},
    	"Monitoring": {
    		"Enabled": true,
    	"NetworkInterfaces": [{
    		"AssociatePublicIpAddress" : true,
    	}],
    "LaunchTemplateName": "string",
    "LicenseSpecifications": ["string"],
    "SecurityGroupIds": ["sg-01fce87ad6e019725"],
    "SecurityGroups": ["string"],
    "TagSpecifications": ["string"]
}
```

## AwsEc2NetworkAcl<a name="asff-resourcedetails-awsec2networkacl"></a>

The `AwsEc2NetworkAcl` object contains details about an Amazon EC2 network access control list \(ACL\)\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2NetworkAcl` object\. To view descriptions of `AwsEc2NetworkAcl` attributes, see [AwsEc2NetworkAclDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2NetworkAclDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2NetworkAcl": {
    "IsDefault": false,
    "NetworkAclId": "acl-1234567890abcdef0",
    "OwnerId": "123456789012",
    "VpcId": "vpc-1234abcd",
    "Associations": [{
        "NetworkAclAssociationId": "aclassoc-abcd1234",
        "NetworkAclId": "acl-021345abcdef6789",
        "SubnetId": "subnet-abcd1234"
   }],
   "Entries": [{
        "CidrBlock": "10.24.34.0/23",
        "Egress": true,
        "IcmpTypeCode": {
            "Code": 10,
            "Type": 30
        },
        "Ipv6CidrBlock": "2001:DB8::/32",
        "PortRange": {
            "From": 20,
            "To": 40
        },
        "Protocol": "tcp",
        "RuleAction": "allow",
        "RuleNumber": 100
   }]
}
```

## AwsEc2NetworkInterface<a name="asff-resourcedetails-awsec2networkinterface"></a>

The `AwsEc2NetworkInterface` object provides information about an Amazon EC2 network interface\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2NetworkInterface` object\. To view descriptions of `AwsEc2NetworkInterface` attributes, see [AwsEc2NetworkInterfaceDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2NetworkInterfaceDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2NetworkInterface": {
    "Attachment": {
        "AttachTime": "2019-01-01T03:03:21Z",
        "AttachmentId": "eni-attach-43348162",
        "DeleteOnTermination": true,
        "DeviceIndex": 123,
        "InstanceId": "i-1234567890abcdef0",
        "InstanceOwnerId": "123456789012",
        "Status": 'ATTACHED'
    },
    "SecurityGroups": [
        {
            "GroupName": "my-security-group",
            "GroupId": "sg-903004f8"
        },
    ],
    "NetworkInterfaceId": 'eni-686ea200',
    "SourceDestCheck": false
}
```

## AwsEc2SecurityGroup<a name="asff-resourcedetails-awsec2securitygroup"></a>

The `AwsEc2SecurityGroup` object describes an Amazon EC2 security group\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2SecurityGroup` object\. To view descriptions of `AwsEc2SecurityGroup` attributes, see [AwsEc2SecurityGroupDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2SecurityGroupDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2SecurityGroup": {
    "GroupName": "MySecurityGroup",
    "GroupId": "sg-903004f8",
    "OwnerId": "123456789012",
    "VpcId": "vpc-1a2b3c4d",
    "IpPermissions": [
        {
            "IpProtocol": "-1",
            "IpRanges": [],
            "UserIdGroupPairs": [
                {
                    "UserId": "123456789012",
                    "GroupId": "sg-903004f8"
                }
            ],
            "PrefixListIds": [
                {"PrefixListId": "pl-63a5400a"}
            ]
        },
        {
            "PrefixListIds": [],
            "FromPort": 22,
            "IpRanges": [
                {
                    "CidrIp": "203.0.113.0/24"
                }
            ],
            "ToPort": 22,
            "IpProtocol": "tcp",
            "UserIdGroupPairs": []
        }
    ]
}
```

## AwsEc2Subnet<a name="asff-resourcedetails-awsec2subnet"></a>

The `AwsEc2Subnet` object provides information about a subnet in Amazon EC2\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Subnet` object\. To view descriptions of `AwsEc2Subnet` attributes, see [AwsEc2SubnetDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2SubnetDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
AwsEc2Subnet: {
    "AssignIpv6AddressOnCreation": false,
    "AvailabilityZone": "us-west-2c",
    "AvailabilityZoneId": "usw2-az3",
    "AvailableIpAddressCount": 8185,
    "CidrBlock": "10.0.0.0/24",
    "DefaultForAz": false,
    "MapPublicIpOnLaunch": false,
    "OwnerId": "123456789012",
    "State": "available",
    "SubnetArn": "arn:aws:ec2:us-west-2:123456789012:subnet/subnet-d5436c93",
    "SubnetId": "subnet-d5436c93",
    "VpcId": "vpc-153ade70",
    "Ipv6CidrBlockAssociationSet": [{
        "AssociationId": "subnet-cidr-assoc-EXAMPLE",
        "Ipv6CidrBlock": "2001:DB8::/32",
        "CidrBlockState": "associated"
   }]
}
```

## AwsEc2TransitGateway<a name="asff-resourcedetails-awsec2transitgateway"></a>

The `AwsEc2TransitGateway` object provides details about an Amazon EC2 transit gateway that interconnects your virtual private clouds \(VPCs\) and on\-premises networks\.

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

## AwsEc2Volume<a name="asff-resourcedetails-awsec2volume"></a>

The `AwsEc2Volume` object provides details about an Amazon EC2 volume\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Volume` object\. To view descriptions of `AwsEc2Volume` attributes, see [AwsEc2VolumeDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2VolumeDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2Volume": {
    "Attachments": [
      {
        "AttachTime": "2017-10-17T14:47:11Z",
        "DeleteOnTermination": true,
        "InstanceId": "i-123abc456def789g",
        "Status": "attached"
      }
     ],
    "CreateTime": "2020-02-24T15:54:30Z",
    "Encrypted": true,
    "KmsKeyId": "arn:aws:kms:us-east-1:111122223333:key/wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY",
    "Size": 80,
    "SnapshotId": "",
    "Status": "available"
}
```

## AwsEc2Vpc<a name="asff-resourcedetails-awsec2vpc"></a>

The `AwsEc2Vpc` object provides details about an Amazon EC2 VPC\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Vpc` object\. To view descriptions of `AwsEc2Vpc` attributes, see [AwsEc2VpcDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2VpcDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2Vpc": {
    "CidrBlockAssociationSet": [
        {
            "AssociationId": "vpc-cidr-assoc-0dc4c852f52abda97",
            "CidrBlock": "192.0.2.0/24",
            "CidrBlockState": "associated"
        }
    ],
    "DhcpOptionsId": "dopt-4e42ce28",
    "Ipv6CidrBlockAssociationSet": [
        {
            "AssociationId": "vpc-cidr-assoc-0dc4c852f52abda97",
            "CidrBlockState": "associated",
            "Ipv6CidrBlock": "192.0.2.0/24"
       }

    ],
    "State": "available"
}
```

## AwsEc2VpcEndpointService<a name="asff-resourcedetails-awsec2vpcendpointservice"></a>

The `AwsEc2VpcEndpointService` object contains details about the service configuration for a VPC endpoint service\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2VpcEndpointService` object\. To view descriptions of `AwsEc2VpcEndpointService` attributes, see [AwsEc2VpcEndpointServiceDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2VpcEndpointServiceDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2VpcEndpointService": {
    "ServiceType": [
      {
        "ServiceType": "Interface"
      }
    ],
    "ServiceId": "vpce-svc-example1",
    "ServiceName": "com.amazonaws.vpce.us-east-1.vpce-svc-example1",
    "ServiceState": "Available",
    "AvailabilityZones": [
      "us-east-1"
    ],
    "AcceptanceRequired": true,
    "ManagesVpcEndpoints": false,
    "NetworkLoadBalancerArns": [
      "arn:aws:elasticloadbalancing:us-east-1:444455556666:loadbalancer/net/my-network-load-balancer/example1"
    ],
    "GatewayLoadBalancerArns": [],
    "BaseEndpointDnsNames": [
      "vpce-svc-04eec859668b51c34.us-east-1.vpce.amazonaws.com"
    ],
    "PrivateDnsName": "my-private-dns"
}
```

## AwsEc2VpcPeeringConnection<a name="asff-resourcedetails-awsec2vpcpeeringconnection"></a>

The `AwsEc2VpcPeeringConnection` object provides details about the networking connection between two VPCs\.

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

## AwsEc2VpnConnection<a name="asff-resourcedetails-awsec2vpnconnection"></a>

The `AwsEc2VpnConnection` object provides details about an Amazon EC2 VPN connection\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2VpnConnection` object\. To view descriptions of `AwsEc2VpnConnection` attributes, see [AwsEc2VpnConnectionDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2VpnConnectionDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2VpnConnection": {
    "VpnConnectionId": "vpn-205e4f41",
    "State": "available",
    "CustomerGatewayConfiguration": "",
    "CustomerGatewayId": "cgw-5699703f",
    "Type": "ipsec.1",
    "VpnGatewayId": "vgw-2ccb2245",
    "Category": "VPN"
    "TransitGatewayId": "tgw-09b6f3a659e2b5elf", 
    "VgwTelemetry": [
        {
            "OutsideIpAddress": "92.0.2.11",
            "Status": "DOWN",
            "LastStatusChange": "2016-11-11T23:09:32.000Z",
            "StatusMessage": "IPSEC IS DOWN",
            "AcceptedRouteCount": 0
        },
        {
            "OutsideIpAddress": "92.0.2.12",
            "Status": "DOWN",
            "LastStatusChange": "2016-11-11T23:10:51.000Z",
            "StatusMessage": "IPSEC IS DOWN",
            "AcceptedRouteCount": 0
        }
    ],
    "Routes": [{
        "DestinationCidrBlock": "10.24.34.0/24",
        "State": "available"
   }],
    "Options": {
        "StaticRoutesOnly": true
        "TunnelOptions": [{
            "DpdTimeoutSeconds": 30,
            "IkeVersions": ["ikev1", "ikev2"],
            "Phase1DhGroupNumbers": [14, 15, 16, 17, 18},
            "Phase1EncryptionAlgorithms": ["AES128", "AES256"],
            "Phase1IntegrityAlgorithms": ["SHA1", "SHA2-256"],
            "Phase1LifetimeSeconds": 28800,
            "Phase2DhGroupNumbers": [14, 15, 16, 17, 18],
            "Phase2EncryptionAlgorithms": ["AES128", "AES256"],
            "Phase2IntegrityAlgorithms": ["SHA1", "SHA2-256"],
            "Phase2LifetimeSeconds": 28800,
            "PreSharedKey": "RltXC3REhTw1RAdiM2s1uMfkkSDLyGJoe1QEWeGxqkQ=",
            "RekeyFuzzPercentage": 100,
            "RekeyMarginTimeSeconds": 540,
            "ReplayWindowSize": 1024,
            "TunnelInsideCidr": "10.24.34.0/23"
        }]
   }
}
```