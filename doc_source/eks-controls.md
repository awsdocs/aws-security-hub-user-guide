# Amazon Elastic Kubernetes Service controls<a name="eks-controls"></a>

These controls are related to Amazon EKS resources\.

## \[EKS\.2\] EKS clusters should run on a supported Kubernetes version<a name="eks-2"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 SI\-2, NIST\.800\-53\.r5 SI\-2\(2\), NIST\.800\-53\.r5 SI\-2\(4\), NIST\.800\-53\.r5 SI\-2\(5\)

**Category:** Identify > Vulnerability, patch, and version management

**Severity:** High

**Resource type:** `AWS::EKS::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/eks-cluster-supported-version.html](https://docs.aws.amazon.com/config/latest/developerguide/eks-cluster-supported-version.html)

**Schedule type:** Change triggered

**Parameters:**
+ `eks:oldestVersionSupported` \(Current oldest supported version is 1\.22\)

This control checks whether an Amazon EKS cluster is running on a supported Kubernetes version\. The control fails if the EKS cluster is running on an unsupported version\. For more information about supported versions, see [Amazon EKS Kubernetes release calendar](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html#kubernetes-release-calendar) in the **Amazon EKS User Guide**\.

If your application doesn't require a specific version of Kubernetes, we recommend that you use the latest available Kubernetes version that's supported by EKS for your clusters\. For more information about supported Kubernetes versions for Amazon EKS, see [Amazon EKS Kubernetes release calendar](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html#kubernetes-release-calendar) and [Amazon EKS version support and FAQ](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html#version-deprecation)/para> in the **Amazon EKS User Guide**\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="eks-2-remediation"></a>

To update an EKS cluster, [Updating an Amazon EKS cluster Kubernetes version](https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html) in the **Amazon EKS User Guide**\. 