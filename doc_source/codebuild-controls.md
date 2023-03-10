# AWS CodeBuild controls<a name="codebuild-controls"></a>

These controls are related to CodeBuild resources\.

## \[CodeBuild\.1\] CodeBuild GitHub or Bitbucket source repository URLs should use OAuth<a name="codebuild-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/8\.2\.1, NIST\.800\-53\.r5 SA\-3

**Category:** Protect > Secure development

**Severity:** Critical

**Resource type:** `AWS::CodeBuild::Project`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-source-repo-url-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-source-repo-url-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the GitHub or Bitbucket source repository URL contains either personal access tokens or a user name and password\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

Sign\-in credentials should never be stored or transmitted in clear text or appear in the repository URL\. Instead of personal access tokens or sign\-in credentials, you should use OAuth to grant authorization for accessing GitHub or Bitbucket repositories\. Using personal access tokens or sign\-in credentials could expose your credentials to unintended data exposure and unauthorized access\.

### Remediation<a name="codebuild-1-remediation"></a>

You can update your CodeBuild project to use OAuth\.

**To remove basic authentication / \(GitHub\) Personal Access Token from CodeBuild project source**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Choose the build project that contains personal access tokens or a user name and password\.

1. From **Edit**, choose **Source**\.

1. Choose **Disconnect from GitHub / Bitbucket**\.

1. Choose **Connect using OAuth**, then choose **Connect to GitHub / Bitbucket**\.

1. When prompted, choose **authorize as appropriate**\.

1. Reconfigure your repository URL and additional configuration settings, as needed\.

1. Choose **Update source**\.

For more information, refer to [CodeBuild use case\-based samples](https://docs.aws.amazon.com/codebuild/latest/userguide/use-case-based-samples.html) in the *AWS CodeBuild User Guide*\.

## \[CodeBuild\.2\] CodeBuild project environment variables should not contain clear text credentials<a name="codebuild-2"></a>

**Related requirements:** PCI DSS v3\.2\.1/8\.2\.1, NIST\.800\-53\.r5 IA\-5\(7\), NIST\.800\-53\.r5 SA\-3

**Category:** Protect > Secure development

**Severity:** Critical

**Resource type:** `AWS::CodeBuild::Project`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-envvar-awscred-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-envvar-awscred-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether the project contains the environment variables `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`\.

Authentication credentials `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` should never be stored in clear text, as this could lead to unintended data exposure and unauthorized access\.

**Note**  
This control is not supported in the following Regions:  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="codebuild-2-remediation"></a>

To remediate this issue, update your CodeBuild project to remove the environment variable\.

**To remove environment variables from a CodeBuild project**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Expand **Build**\.

1. Choose **Build project**, and then choose the build project that contains plaintext credentials\.

1. From **Edit**, choose **Environment**\.

1. Expand **Additional configuration**\.

1. Choose **Remove** next to the environment variables\.

1. Choose **Update environment**\.

**To store sensitive values in the AWS Systems Manager Parameter Store and then retrieve them from your build spec**

1. Open the CodeBuild console at [https://console\.aws\.amazon\.com/codebuild/](https://console.aws.amazon.com/codebuild/)\.

1. Expand **Build**\.

1. Choose **Build project**, and then choose the build project that contains plaintext credentials\.

1. From **Edit**, choose **Environment**\.

1. Expand **Additional configuration** and scroll to **Environment variables**\.

1. Follow [this tutorial](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-paramstore-console.html) to create a Systems Manager parameter that contains your sensitive data\.

1. After you create the parameter, copy the parameter name\.

1. Back in the CodeBuild console, choose **Create environmental variable**\.

1. Enter the name of your variable as it appears in your build spec\.

1. For **Value**, paste the name of your parameter\.

1. For **Type**, choose **Parameter**\.

1. To remove your noncompliant environmental variable that contains plaintext credentials, choose **Remove**\.

1. Choose **Update environment**\.

For more information, see [Environment variables in build environments](https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-env-vars.html) in the *AWS CodeBuild User Guide*\.

## \[CodeBuild\.3\] CodeBuild S3 logs should be encrypted<a name="codebuild-3"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-3\(6\), NIST\.800\-53\.r5 SC\-13, NIST\.800\-53\.r5 SC\-28, NIST\.800\-53\.r5 SC\-28\(1\), NIST\.800\-53\.r5 SI\-7\(6\)

**Category:** Protect > Data protection > Encryption of data\-at\-rest

**Severity:** Low

**Resource type:** `AWS::CodeBuild::Project`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-s3-logs-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-s3-logs-encrypted.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon S3 logs for an AWS CodeBuild project are encrypted\. The control fails if encryption is deactivated for S3 logs for a CodeBuild project\.

Encryption of data at rest is a recommended best practice to add a layer of access management around your data\. Encrypting the logs at rest reduces the risk that a user not authenticated by AWS will access the data stored on disk\. It adds another set of access controls to limit the ability of unauthorized users to access the data\. 

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="codebuild-3-remediation"></a>

To change the encryption settings for CodeBuild project S3 logs, see [Change a build project's settings in AWS CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/change-project.html) in the *AWS CodeBuild User Guide*\.

## \[CodeBuild\.4\] CodeBuild project environments should have a logging AWS Configuration<a name="codebuild-4"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(12\), NIST\.800\-53\.r5 AC\-2\(4\), NIST\.800\-53\.r5 AC\-4\(26\), NIST\.800\-53\.r5 AC\-6\(9\), NIST\.800\-53\.r5 AU\-10, NIST\.800\-53\.r5 AU\-12, NIST\.800\-53\.r5 AU\-2, NIST\.800\-53\.r5 AU\-3, NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 AU\-9\(7\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SC\-7\(9\), NIST\.800\-53\.r5 SI\-3\(8\), NIST\.800\-53\.r5 SI\-4, NIST\.800\-53\.r5 SI\-4\(20\), NIST\.800\-53\.r5 SI\-7\(8\)

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::CodeBuild::Project`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-logging-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-logging-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a CodeBuild project environment has at least one log option, either to S3 or CloudWatch logs enabled\. This control fails if a CodeBuild project environment does not have at least one log option enabled\. 

From a security perspective, logging is an important feature to enable for future forensics efforts in the case of any security incidents\. Correlating anomalies in CodeBuild projects with threat detections can increase confidence in the accuracy of those threat detections\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="codebuild-4-remediation"></a>

For more information on how to configure CodeBuild project log settings, see [Create a build project \(console\)](https://docs.aws.amazon.com/codebuild/latest/userguide/create-project-console.html#create-project-console-logs) in the CodeBuild User Guide\.

## \[CodeBuild\.5\] CodeBuild project environments should not have privileged mode enabled<a name="codebuild-5"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-5, NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 AC\-6\(10\), NIST\.800\-53\.r5 AC\-6\(2\)

**Category:** Protect > Secure Access Management

**Severity:** High

**Resource type:** `AWS::CodeBuild::Project`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-environment-privileged-check.html](https://docs.aws.amazon.com/config/latest/developerguide/codebuild-project-environment-privileged-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if an AWS CodeBuild project environment has privileged mode enabled\. This control fails when an AWS CodeBuild project environment has privileged mode enabled\.

By default, Docker containers do not allow access to any devices\. Privileged mode grants a build project's Docker container access to all devices\. Setting `privilegedMode` with value `true` enables running the Docker daemon inside a Docker container\. The Docker daemon listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes\. This parameter should only be set to true if the build project is used to build Docker images\. Otherwise, this setting should be disabled to prevent unintended access to Docker APIs as well as the container's underlying hardware as unintended access to `privilegedMode` may risk malicious tampering or deletion of critical resources\.

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="codebuild-5-remediation"></a>

For more information on how to configure CodeBuild project environment settings, see [Create a build project \(console\)](https://docs.aws.amazon.com/codebuild/latest/userguide/create-project-console.html#create-project-console-environment) in the CodeBuild User Guide