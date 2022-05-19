# AwsAutoScalingAutoScalingGroup<a name="asff-resourcedetails-awsautoscalingautoscalinggroup"></a>

The `AwsAutoScalingAutoScalingGroup` object provides details about an automatic scaling group\.

The following is an example `AwsAutoScalingAutoScalingGroup` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsAutoScalingAutoScalingGroup` attributes, see [AwsAutoScalingAutoScalingGroupDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsAutoScalingAutoScalingGroupDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsAutoScalingAutoScalingGroup": {
        "CreatedTime": "2017-10-17T14:47:11Z",
        "HealthCheckGracePeriod": 300,
        "HealthCheckType": "EC2",
        "LaunchConfigurationName": "mylaunchconf",
        "LoadBalancerNames": [],
        "LaunchTemplate": {                            
            "LaunchTemplateId": "string",
            "LaunchTemplateName": "string",
            "Version": "string"
        },
        "MixedInstancesPolicy": {
            "InstancesDistribution": {
                "OnDemandAllocationStrategy": "prioritized",
                "OnDemandBaseCapacity": number,
                "OnDemandPercentageAboveBaseCapacity": number,
                "SpotAllocationStrategy": "lowest-price",
                "SpotInstancePools": number,
                "SpotMaxPrice": "string"
            },
            "LaunchTemplate": {
                "LaunchTemplateSpecification": {
                    "LaunchTemplateId": "string",
                    "LaunchTemplateName": "string",
                    "Version": "string"
                 },
                "CapacityRebalance": true,
                "Overrides": [
                    {
                       "InstanceType": "string",
                       "WeightedCapacity": "string"
                    }
                ]
            }
        }
    }
}
```

The following is a list of valid value examples for `AwsAutoScalingAutoScalingGroup` attributes:
+ `HealthCheckType`

  Valid values: `EC2` \| `ELB`
+ `OnDemandAllocationStrategy`

  Valid values: `prioritized`
+ `SpotAllocationStrategy`

  Valid values: `lowest-price` \| `capacity-optimized` \| `capacity-optimized-prioritized`