# Amazon Elastic Container Registry controls<a name="ecr-controls"></a>

These controls are related to ecr\.

## \[ECR\.1\] ECR private repositories should have image scanning configured<a name="ecr-1"></a>

**Related requirements:** NIST\.800\-53\.r5 RA\-5

**Category:** Identify > Vulnerability, patch, and version management

**Severity:** High

**Resource type:** `AWS::ECR::Repository`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-image-scanning-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-image-scanning-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a private ECR repository has image scanning configured\. This control fails if a private ECR repository doesn't have image scanning configured\. Note that you must also configure [scan on push](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html#image-scanning-filters) for each repository to pass this control\.

ECR image scanning helps in identifying software vulnerabilities in your container images\. ECR uses the Common Vulnerabilities and Exposures \(CVEs\) database from the [open\-source Clair project ](https://github.com/quay/clair) and provides a list of scan findings\. Enabling image scanning on ECR repositories adds a layer of verification for the integrity and safety of the images being stored\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecr-1-remediation"></a>

To configure image scanning for an ECR repository, see [Image scanning](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html) in the *Amazon Elastic Container Registry User Guide*\.

## \[ECR\.2\] ECR private repositories should have tag immutability configured<a name="ecr-2"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-8\(1\)

**Category:** Identify > Inventory > Tagging

**Severity:** Medium

**Resource type:** `AWS::ECR::Repository`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-tag-immutability-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-tag-immutability-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a private ECR repository has tag immutability enabled\. This control fails if a private ECR repository has tag immutability disabled\. This rule passes if tag immutability is enabled and has the value `IMMUTABLE`\.

Amazon ECR Tag Immutability enables customers to rely on the descriptive tags of an image as a reliable mechanism to track and uniquely identify images\. An immutable tag is static, which means each tag refers to a unique image\. This improves reliability and scalability as the use of a static tag will always result in the same image being deployed\. When configured, tag immutability prevents the tags from being overridden, which reduces the attack surface\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecr-2-remediation"></a>

To create a repository with immutable tags configured or to update the image tag mutability settings for an existing repository, see [Image tag mutability](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-tag-mutability.html) in the *Amazon Elastic Container Registry User Guide*\.

## \[ECR\.3\] ECR repositories should have at least one lifecycle policy configured<a name="ecr-3"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\)

**Category:** Identify > Resource configuration

**Severity:** Medium

**Resource type:** `AWS::ECR::Repository`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-lifecycle-policy-configured.html](https://docs.aws.amazon.com/config/latest/developerguide/ecr-private-lifecycle-policy-configured.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon ECR repository has at least one lifecycle policy configured\. This control fails if an ECR repository does not have any lifecycle policies configured\.

Amazon ECR lifecycle policies enable you to specify the lifecycle management of images in a repository\. By configuring lifecycle policies, you can automate the cleanup of unused images and the expiration of images based on age or count\. Automating these tasks can help you avoid unintentionally using outdated images in your repository\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecr-3-remediation"></a>

To configure a lifecycle policy, see [Creating a lifecycle policy preview](https://docs.aws.amazon.com/AmazonECR/latest/userguide/lpp_creation.html) in the *Amazon Elastic Container Registry User Guide*\.