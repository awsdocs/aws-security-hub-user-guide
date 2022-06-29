# AwsElbv2LoadBalancer<a name="asff-resourcedetails-awselbv2loadbalancer"></a>

The `AwsElbv2LoadBalancer` object provides information about an Application Load Balancer, a Network Load Balancer, or a Gateway Load Balancer\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsElbv2LoadBalancer` object\. To view descriptions of `AwsElbv2LoadBalancer` attributes, see [AwsElbv2LoadBalancerDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsElbv2LoadBalancerDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsElbv2LoadBalancer": {
                        "AvailabilityZones": {
                            "SubnetId": "string",
                            "ZoneName": "string"
                        },
                        "CanonicalHostedZoneId": "string",
                        "CreatedTime": "string",
                        "DNSName": "string",
                        "IpAddressType": "string",
                        "LoadBalancerAttributes": [
                            {
                                "Key": "string",
                                "Value": "string"
                            }
                        ],
                        "Scheme": "string",
                        "SecurityGroups": [ "string" ],
                        "State": {
                            "Code": "string",
                            "Reason": "string"
                        },
                        "Type": "string",
                        "VpcId": "string"
                    }
```