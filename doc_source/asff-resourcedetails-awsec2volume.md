# AwsEc2Volume<a name="asff-resourcedetails-awsec2volume"></a>

The `AwsEc2Volume` object provides details about an Amazon Elastic Compute Cloud volume\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEc2Volume` object\. To view descriptions of `AwsEc2Volume` attributes, see [AwsEc2VolumeDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEc2VolumeDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEc2Volume": {
    "Attachments": [{
        "AttachTime": "2017-10-17T14:47:11Z",
        "DeleteOnTermination": true,
        "InstanceId": "i-123abc456def789g",
        "Status": "attached"
    }],
    "CreateTime": "2020-02-24T15:54:30Z",
    "DeviceName": "/dev/sda2",
    "Encrypted": true,
    "KmsKeyId": "arn:aws:kms:us-east-1:111122223333:key/wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY", 
    "Size": 80,
    "SnapshotId": "snap-014f23111111fadfb",
    "Status": "available",
    "VolumeId": "vol-111111111aee112f",
    "VolumeScanStatus": "scanned",
    "VolumeType": "gp2"
}
```

The following is a list of valid value examples for `AwsEc2Volume` attributes:
+ `Attachments Status`

  Valid values: `attaching` \| `attached` \| `detaching` \| `detached` \| `busy`
+ `Status`

  Valid values: `creating` \| `available` \| `in-use` \| `deleting` \| `deleted` \| `error`
+ `VolumeScanStatus`

  Valid values: `scanned` \| `skipped`