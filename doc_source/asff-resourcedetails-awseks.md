# AwsEks<a name="asff-resourcedetails-awseks"></a>

The following are examples of the AWS Security Finding Format for `AwsEks` resources\.

## AwsEksCluster<a name="asff-resourcedetails-awsekscluster"></a>

The `AwsEksCluster` object provides details about an Amazon EKS cluster\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEksCluster` object\. To view descriptions of `AwsEksCluster` attributes, see [AwsEksClusterDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEksClusterDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
{
  "AwsEksCluster": {
    "Name": "example",
    "Arn": "arn:aws:eks:us-west-2:222222222222:cluster/example",
    "CreatedAt": 1565804921.901,
    "Version": "1.12",
    "RoleArn": "arn:aws:iam::222222222222:role/example-cluster-ServiceRole-1XWBQWYSFRE2Q",
    "ResourcesVpcConfig": {
      "SubnetIds": [
        "subnet-021345abcdef6789",
        "subnet-abcdef01234567890",
        "subnet-1234567890abcdef0"
      ],
      "SecurityGroupIds": [
        "sg-abcdef01234567890"
      ]
    },
    "Logging": {
      "ClusterLogging": [
        {
          "Types": [
            "api",
            "audit",
            "authenticator",
            "controllerManager",
            "scheduler"
          ],
          "Enabled": true
        }
      ]
    },
    "Status": "CREATING",
    "CertificateAuthorityData": {},
  }
}
```