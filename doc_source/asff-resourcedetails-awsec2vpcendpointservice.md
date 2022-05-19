# AwsEc2VpcEndpointService<a name="asff-resourcedetails-awsec2vpcendpointservice"></a>

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

The following is a list of valid value examples for `AwsEc2VpcEndpointService` attributes:
+ `ServiceState`

  Valid values: `Pending` \| `Available` \| `Deleting` \| `Deleted` \| `Failed`