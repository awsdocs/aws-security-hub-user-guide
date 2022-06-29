# AwsAutoScalingLaunchConfiguration<a name="asff-resourcedetails-awsautoscalinglaunchconfiguration"></a>

The `AwsAutoScalingLaunchConfiguration` object provides details about an Amazon EC2 Auto Scaling launch configuration\.

The following is an example `AwsAutoScalingLaunchConfiguration` finding in the AWS Security Finding Format \(ASFF\)\.

To view descriptions of `AwsAutoScalingLaunchConfiguration` attributes, see [AwsAutoScalingLaunchConfigurationDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsAutoScalingLaunchConfigurationDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
AwsAutoScalingLaunchConfiguration: {
    "LaunchConfigurationName": "newtest",
    "ImageId": "ami-058a3739b02263842",
    "KeyName": "55hundredinstance",
    "SecurityGroups": [ "sg-01fce87ad6e019725" ],
    "ClassicLinkVpcSecurityGroups": [],
    "UserData": "...Base64-Encoded user data..."
    "InstanceType": "a1.metal",
    "KernelId": "",
    "RamdiskId": "ari-a51cf9cc",
    "BlockDeviceMappings": [
        {
            "DeviceName": "/dev/sdh",
            "Ebs": {
                "VolumeSize": 30,
                "VolumeType": "gp2",
                "DeleteOnTermination": false,
                "Encrypted": true,
                "SnapshotId": "snap-ffaa1e69",
                "VirtualName": "ephemeral1"
            }
        },
        {
            "DeviceName": "/dev/sdb",
            "NoDevice": true
        },
        {
            "DeviceName": "/dev/sda1",
            "Ebs": {
                "SnapshotId": "snap-02420cd3d2dea1bc0",
                "VolumeSize": 8,
                "VolumeType": "gp2",
                "DeleteOnTermination": true,
                "Encrypted": false
            }
        },
        {
            "DeviceName": "/dev/sdi",
            "Ebs": {
                "VolumeSize": 20,
                "VolumeType": "gp2",
                "DeleteOnTermination": false,
                "Encrypted": true
            }
        },
        {
            "DeviceName": "/dev/sdc",
            "NoDevice": true
        }
    ],
    "InstanceMonitoring": {
        "Enabled": false
    },
    "CreatedTime": 1620842933453,
    "EbsOptimized": false,
    "AssociatePublicIpAddress": true,
    "SpotPrice": "0.045"
}
```

The following is a list of valid value examples for `AwsAutoScalingLaunchConfiguration` attributes:
+ `VolumeType`

  Valid values: `standard` \| `io1` \| `gp2` \| `st1` \| `sc1` \| `gp3`