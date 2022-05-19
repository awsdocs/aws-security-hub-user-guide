# AwsEc2NetworkInterface<a name="asff-resourcedetails-awsec2networkinterface"></a>

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