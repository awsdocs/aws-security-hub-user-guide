# AwsEcrContainerImage<a name="asff-resourcedetails-awsecrcontainerimage"></a>

The `AwsEcrContainerImage` object provides information about an Amazon Elastic Container Registry image\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcrContainerImage` object\. To view descriptions of `AwsEcrContainerImage` attributes, see [AwsEcrContainerImageDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcrContainerImageDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEcrContainerImage": {
    "RegistryId": "123456789012",
    "RepositoryName": "repository-name",
    "Architecture": "amd64"
    "ImageDigest": "sha256:a568e5c7a953fbeaa2904ac83401f93e4a076972dc1bae527832f5349cd2fb10",
    "ImageTags": ["00000000-0000-0000-0000-000000000000"],
    "ImagePublishedAt": "2019-10-01T20:06:12Z"
}
```

The following is a list of valid value examples for `AwsEcrContainerImage` attributes:
+ `Architecture`

  Valid values: `i386` \| `x86_64` \| `arm64`