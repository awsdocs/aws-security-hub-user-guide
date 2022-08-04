# Container<a name="asff-resourcedetails-container"></a>

Container details that are related to a finding\. 

The following example shows the AWS Security Finding Format \(ASFF\) for the `Container` object\. To view descriptions of `Container` attributes, see [ContainerDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ContainerDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"Container": {
    "ContainerRuntime": "docker",
    "ImageId": "image12",
    "ImageName": "1111111/knotejs@sha256:372131c9fef111111111111115f4ed3ea5f9dce4dc3bd34ce21846588a3",
    "LaunchedAt": "2018-09-29T01:25:54Z",
    "Name": "knote",
    "Privileged": true,
    "VolumeMounts": [{
        "Name": "vol-03909e9",
        "MountPath": "/mnt/etc"
    }]
}
```