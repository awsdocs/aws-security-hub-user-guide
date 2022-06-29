# AwsEcsContainer<a name="asff-resourcedetails-awsecscontainer"></a>

The `AwsEcsContainer` object contains details about an Amazon ECS container\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcsContainer` object\. To view descriptions of `AwsEcsContainer` attributes, see [AwsEcsContainerDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcsContainerDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEcsContainer": {
    "Image": "1111111/knotejs@sha256:356131c9fef111111111111115f4ed8de5f9dce4dc3bd34bg21846588a3",
    "MountPoints": [{
        "ContainerPath": "/mnt/etc",
        "SourceVolume": "vol-03909e9"
    }],
    "Name": "knote",
    "Privileged": true 
}
```