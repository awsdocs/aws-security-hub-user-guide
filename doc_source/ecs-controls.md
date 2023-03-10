# Amazon ECS controls<a name="ecs-controls"></a>

These controls are related to Amazon ECS resources\.

## \[ECS\.1\] Amazon ECS task definitions should have secure networking modes and user definitions\.<a name="ecs-1"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-5, NIST\.800\-53\.r5 AC\-6

**Category:** Protect > Secure access management

**Severity:** High

**Resource type:** `AWS::ECS::TaskDefinition`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecs-task-definition-user-for-host-mode-check.html](https://docs.aws.amazon.com/config/latest/developerguide/ecs-task-definition-user-for-host-mode-check.html)

**Schedule type:** Change triggered

**Parameters:**
+ `SkipInactiveTaskDefinitions`: `true`

This control checks whether an active Amazon ECS task definition that has host networking mode also has `privileged` or `user` container definitions\. The control fails for task definitions that have host network mode and container definitions where `privileged=false` or is empty and `user=root` or is empty\. This control only evaluates the latest active revision of an Amazon ECS task definition\.

If a task definition has elevated privileges, it is because the customer has specifically opted in to that configuration\. This control checks for unexpected privilege escalation when a task definition has host networking enabled but the customer has not opted in to elevated privileges\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Middle East \(UAE\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-1-remediation"></a>

For information on how to update a task definition, see [Updating a task definition](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/update-task-definition.html) in the *Amazon Elastic Container Service Developer Guide*\.

Note that when you update a task definition, it does not update running tasks that were launched from the previous task definition\. To update a running task, you must redeploy the task with the new task definition\.

## \[ECS\.2\] ECS services should not have public IP addresses assigned to them automatically<a name="ecs-2"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration > Resources not publicly accessible

**Severity:** High

**Resource type:** `AWS::ECS::Service`

**AWS Configrule:** `ecs-service-assign-public-ip-disabled` \(Custom rule developed by Security Hub\)

**Schedule type:** Change triggered

**Parameters:**
+ `exemptEcsServiceArns` \(Optional\)\. Security Hub does not populate this parameter\. Comma\-separated list of ARNs of Amazon ECS services that are exempt from this rule\.

  This rule is `COMPLIANT` if an Amazon ECS service has `AssignPublicIP` set to `ENABLED` and is specified in this parameter list\.

  This rule is `NON_COMPLIANT` if an Amazon ECS service has `AssignPublicIP` set to `ENABLED` and is not specified in this parameter list\.

This control checks whether Amazon ECS services are configured to automatically assign public IP addresses\. This control fails if `AssignPublicIP` is `ENABLED`\. This control passes if `AssignPublicIP` is `DISABLED`\.

A public IP address is an IP address that is reachable from the internet\. If you launch your Amazon ECS instances with a public IP address, then your Amazon ECS instances are reachable from the internet\. Amazon ECS services should not be publicly accessible, as this may allow unintended access to your container application servers\.

**Note**  
This control is not supported in the Asia Pacific \(Osaka\) Region\.

### Remediation<a name="ecs-2-remediation"></a>

To disable automatic public IP assignment, see [To configure VPC and security group settings for your service](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-configure-network.html) in the *Amazon Elastic Container Service Developer Guide*\.

## \[ECS\.3\] ECS task definitions should not share the host's process namespace<a name="ecs-3"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Identify > Resource configuration

**Severity:** High

**Resource type:** `AWS::ECS::TaskDefinition`

**AWS Configrule:** [ecs\-task\-definition\-pid\-mode\-check](https://docs.aws.amazon.com/config/latest/developerguide/ecs-task-definition-pid-mode-check.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon ECS task definitions are configured to share a host's process namespace with its containers\. The control fails if the task definition shares the host's process namespace with the containers running on it\. This control only evaluates the latest active revision of an Amazon ECS task definition\.

A process ID \(PID\) namespace provides separation between processes\. It prevents system processes from being visible, and allows PIDs to be reused, including PID 1\. If the host's PID namespace is shared with containers, it would allow containers to see all of the processes on the host system\. This reduces the benefit of process level isolation between the host and the containers\. These circumstances could lead to unauthorized access to processes on the host itself, including the ability to manipulate and terminate them\. Customers shouldn't share the host's process namespace with containers running on it\.

### Remediation<a name="ecs-3-remediation"></a>

To configure the `pidMode` on a task definition, see [Task definition parameters](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definition_parameters.html#task_definition_pidmode) in the Amazon Elastic Container Service Developer Guide\.

## \[ECS\.4\] ECS containers should run as non\-privileged<a name="ecs-4"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-5, NIST\.800\-53\.r5 AC\-6

**Category:** Protect > Secure access management > Root user access restrictions

**Severity:** High

**Resource type:** `AWS::ECS::TaskDefinition`

**AWS Configrule:** [ecs\-containers\-nonprivileged](https://docs.aws.amazon.com/config/latest/developerguide/ecs-containers-nonprivileged.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if the `privileged` parameter in the container definition of Amazon ECS Task Definitions is set to `true`\. The control fails if this parameter is equal to `true`\. This control only evaluates the latest active revision of an Amazon ECS task definition\.

We recommend that you remove elevated privileges from your ECS task definitions\. When the privilege parameter is `true`, the container is given elevated privileges on the host container instance \(similar to the root user\)\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-4-remediation"></a>

To configure the `privileged` parameter on a task definition, see [Advanced container definition parameters](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definition_parameters.html#container_definition_security) in the Amazon Elastic Container Service Developer Guide\.

## \[ECS\.5\] ECS containers should be limited to read\-only access to root filesystems<a name="ecs-5"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-2\(1\), NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-5, NIST\.800\-53\.r5 AC\-6

**Category:** Protect > Secure access management

**Severity:** High

**Resource type:** `AWS::ECS::TaskDefinition`

**AWS Configrule:** [ecs\-containers\-readonly\-access](https://docs.aws.amazon.com/config/latest/developerguide/ecs-containers-readonly-access.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon ECS containers are limited to read\-only access to mounted root filesystems\. This control fails if the `ReadonlyRootFilesystem` parameter in the container definition of Amazon ECS task definitions is set to `false`\. This control only evaluates the latest active revision of an Amazon ECS task definition\.

Enabling this option reduces security attack vectors since the container instance's filesystem cannot be tampered with or written to unless it has explicit read\-write permissions on its filesystem folder and directories\. This control also adheres to the principle of least privilege\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-5-remediation"></a>

**To limit container definitions to read\-only access to root filesystems \(classic Amazon ECS console\)**

1. Open the Amazon ECS console at [https://console\.aws\.amazon\.com/ecs/](https://console.aws.amazon.com/ecs/)\.

   Use the classic Amazon ECS console\.

1. In the left navigation pane, choose **Task Definitions**\.

1. For each task definition that has container definitions that need to be updated, do the following:
   + Select the container definition that needs to be updated\.
   + Choose **Edit Container**\. For **Storage and Logging**, select **Read only root file system**\.
   + Choose **Update** at the bottom of the **Edit Container** tab\.
   + Choose **Create**\.

## \[ECS\.8\] Secrets should not be passed as container environment variables<a name="ecs-8"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure development > Credentials not hard\-coded

**Severity:** High

**Resource type:** `AWS::ECS::TaskDefinition`

**AWS Configrule:** [ecs\-no\-environment\-secrets](https://docs.aws.amazon.com/config/latest/developerguide/ecs-no-environment-secrets.html) 

**Schedule type:** Change triggered

**Parameters:** 
+  secretKeys = `AWS_ACCESS_KEY_ID`,`AWS_SECRET_ACCESS_KEY`,`ECS_ENGINE_AUTH_DATA` 

This control checks if the key value of any variables in the `environment` parameter of container definitions includes `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, or `ECS_ENGINE_AUTH_DATA`\. This control fails if a single environment variable in any container definition equals `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, or `ECS_ENGINE_AUTH_DATA`\. This control does not cover environmental variables passed in from other locations such as Amazon S3\. This control only evaluates the latest active revision of an Amazon ECS task definition\.

AWS Systems Manager Parameter Store can help you improve the security posture of your organization\. We recommend using the Parameter Store to store secrets and credentials instead of directing passing them into your container instances or hard coding them into your code\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-8-remediation"></a>

To create parameters using SSM, see [Creating Systems Manager parameters](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-paramstore-su-create.html) in the *AWS Systems Manager User Guide*\. For more information about creating a task definition that specifies a secret, see [Specifying sensitive data using Secrets Manager](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/specifying-sensitive-data-secrets.html#secrets-create-taskdefinition) in the *Amazon Elastic Container Service Developer Guide*\.

## \[ECS\.10\] ECS Fargate services should run on the latest Fargate platform version<a name="ecs-10"></a>

**Related requirements:** NIST\.800\-53\.r5 SI\-2, NIST\.800\-53\.r5 SI\-2\(2\), NIST\.800\-53\.r5 SI\-2\(4\), NIST\.800\-53\.r5 SI\-2\(5\)

**Category:** Identify > Vulnerability, patch, and version management

**Severity:** Medium

**Resource type:** `AWS::ECS::Service`

**AWS Configrule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecs-fargate-latest-platform-version.html](https://docs.aws.amazon.com/config/latest/developerguide/ecs-fargate-latest-platform-version.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if Amazon ECS Fargate services are running the latest Fargate platform version\. This control fails if the platform version is not the latest\.

AWS Fargate platform versions refer to a specific runtime environment for Fargate task infrastructure, which is a combination of kernel and container runtime versions\. New platform versions are released as the runtime environment evolves\. For example, a new version may be released for kernel or operating system updates, new features, bug fixes, or security updates\. Security updates and patches are deployed automatically for your Fargate tasks\. If a security issue is found that affects a platform version, AWS patches the platform version\. 

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-10-remediation"></a>

To update an existing service, including its platform version, see [Updating a service](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/update-service.html) in the *Amazon Elastic Container Service Developer Guide*\.

## \[ECS\.12\] ECS clusters should use Container Insights<a name="ecs-12"></a>

**Related requirements:** NIST\.800\-53\.r5 AU\-6\(3\), NIST\.800\-53\.r5 AU\-6\(4\), NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 SI\-2

**Category:** Identify > Logging

**Severity:** Medium

**Resource type:** `AWS::ECS::Cluster`

**AWS Configrule:** [https://docs.aws.amazon.com/config/latest/developerguide/ecs-container-insights-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/ecs-container-insights-enabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks if ECS clusters use Container Insights\. This control fails if Container Insights are not set up for a cluster\.

Monitoring is an important part of maintaining the reliability, availability, and performance of Amazon ECS clusters\. Use CloudWatch Container Insights to collect, aggregate, and summarize metrics and logs from your containerized applications and microservices\. CloudWatch automatically collects metrics for many resources, such as CPU, memory, disk, and network\. Container Insights also provides diagnostic information, such as container restart failures, to help you isolate issues and resolve them quickly\. You can also set CloudWatch alarms on metrics that Container Insights collects\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
China \(Beijing\)
China \(Ningxia\)
Europe \(Milan\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="ecs-12-remediation"></a>

To use Container Insights, see [Updating a service](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/deploy-container-insights-ECS.html) in the *Amazon CloudWatch User Guide*\.