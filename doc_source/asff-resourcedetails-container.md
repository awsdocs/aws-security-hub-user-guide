# Container<a name="asff-resourcedetails-container"></a>

Container details that are related to a finding\. 

The following example shows the AWS Security Finding Format \(ASFF\) for the `Container` object\. To view descriptions of `Container` attributes, see [ContainerDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ContainerDetails.html) in the *AWS Security Hub API Reference*\.

Type: Object

Example:

```
"Container": {
    "Name": "Secret Service Container",
    "ImageId": "image12",
    "ImageName": "SecSvc v1.2 Image",
    "LaunchedAt": "2018-09-29T01:25:54Z"
}
```