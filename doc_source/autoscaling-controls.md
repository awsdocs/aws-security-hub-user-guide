# Amazon EC2 Auto Scaling controls<a name="autoscaling-controls"></a>

These controls are related to Auto Scaling resources\.

## \[AutoScaling\.1\] Auto Scaling groups associated with a Classic Load Balancer should use load balancer health checks<a name="autoscaling-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/2\.2, NIST\.800\-53\.r5 CA\-7, NIST\.800\-53\.r5 CP\-2\(2\), NIST\.800\-53\.r5 SI\-2

**Category:** Identify > Inventory

**Severity:** Low

**Resource type:** `AWS::AutoScaling::AutoScalingGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-group-elb-healthcheck-required.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-group-elb-healthcheck-required.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether your Auto Scaling groups that are associated with a Classic Load Balancer are using Elastic Load Balancing health checks\.

This ensures that the group can determine an instance's health based on additional tests provided by the load balancer\. Using Elastic Load Balancing health checks can help support the availability of applications that use EC2 Auto Scaling groups\. 

**Note**  
This control is not supported in Middle East \(UAE\)\.

### Remediation<a name="autoscaling-1-remediation"></a>

To remediate this issue, update your Auto Scaling groups to use Elastic Load Balancing health checks\.

**To enable Elastic Load Balancing health checks**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Auto Scaling**, choose **Auto Scaling Groups**\.

1. Select the check box for your group\.

1. Choose **Edit**\.

1. Under **Health checks**, for **Health check type**, choose **ELB**\.

1. For **Health check grace period**, enter **300**\.

1. At the bottom of the page, choose **Update**\.

For more information on using a load balancer with an Auto Scaling group, see the [https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html](https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html)\.

## \[AutoScaling\.2\] Amazon Amazon EC2 Auto Scaling group should cover multiple Availability Zones<a name="autoscaling-2"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-2\(2\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > High Availability

**Severity:** Medium

**Resource type:** `AWS::AutoScaling::AutoScalingGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-multiple-az.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-multiple-az.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Auto Scaling group spans multiple Availability Zones\. The control fails if an Auto Scaling group does not span multiple Availability Zones\.

Amazon EC2 Auto Scaling groups can be configured to use multiple Availability Zones\. An Auto Scaling group with a single Availability Zone is preferred in some use cases, such as batch\-jobs or when inter\-AZ transfer costs need to be kept to a minimum\. However, an Auto Scaling group that does not span multiple Availability Zones will not launch instances in another Availability Zone to compensate if the configured single Availability Zone becomes unavailable\.

### Remediation<a name="autoscaling-2-remediation"></a>

For information on how to add Availability Zones to an existing auto scaling group, see [Availability zones](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-add-availability-zone.html) in the *Amazon EC2 Auto Scaling User Guide*\.

## \[AutoScaling\.3\] Auto Scaling group launch AWS Configurations should AWS Configure Amazon EC2 instances to require Instance Metadata Service Version 2 \(IMDSv2\)<a name="autoscaling-3"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(15\), NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::AutoScaling::LaunchConfiguration`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launchconfig-requires-imdsv2.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launchconfig-requires-imdsv2.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether IMDSv2 is enabled on all instances launched by Amazon EC2 Auto Scaling groups\. The control fails if the Instance Metadata Service \(IMDS\) version is not included in the launch configuration or if both IMDSv1 and IMDSv2 are enabled\.

IMDS provides data about your instance that you can use to configure or manage the running instance\.

Version 2 of the IMDS adds new protections that weren't available in IMDSv1 to further safeguard your EC2 instances\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="autoscaling-3-remediation"></a>

An Auto Scaling group is associated with one launch configuration at a time\. You cannot modify a launch configuration after you create it\. To change the launch configuration for an Auto Scaling group, use an existing launch configuration as the basis for a new launch configuration with IMDSv2 enabled\. For more information, see [Configure instance metadata options for new instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-options.html#configuring-IMDS-new-instances) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[AutoScaling\.4\] Auto Scaling group launch AWS Configuration should not have a metadata response hop limit greater than 1<a name="autoscaling-4"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\)

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::AutoScaling::LaunchConfiguration`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-config-hop-limit.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-config-hop-limit.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks the number of network hops that a metadata token can travel\. The control fails if the metadata response hop limit is greater than `1`\.

The Instance Metadata Service \(IMDS\) provides metadata information about an Amazon EC2 instance and is useful for application configuration\. Restricting the HTTP `PUT` response for the metadata service to only the EC2 instance protects the IMDS from unauthorized use\.

The Time To Live \(TTL\) field in the IP packet is reduced by one on every hop\. This reduction can be used to ensure that the packet does not travel outside EC2\. IMDSv2 protects EC2 instances that may have been misconfigured as open routers, layer 3 firewalls, VPNs, tunnels, or NAT devices, which prevents unauthorized users from retrieving metadata\. With IMDSv2, the `PUT` response that contains the secret token cannot travel outside the instance because the default metadata response hop limit is set to `1`\. However, if this value is greater than `1`, the token can leave the EC2 instance\. 

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="autoscaling-4-remediation"></a>

For detailed instructions on how to modify the metadata response hop limit for an existing launch configuration, see [Modify instance metadata options for existing instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-options.html#configuring-IMDS-existing-instances) in the *Amazon EC2 User Guide for Linux Instances*\.

## \[Autoscaling\.5\] Amazon Amazon EC2 instances launched using Auto Scaling group launch AWS Configurations should not have Public IP addresses<a name="autoscaling-5"></a>

**Related requirements:** NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::AutoScaling::LaunchConfiguration`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-config-public-ip-disabled.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-config-public-ip-disabled.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Auto Scaling group's associated launch configuration assigns a [public IP address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html#public-ip-addresses) to the group's instances\. The control fails if the associated launch configuration assigns a public IP address\.

Amazon EC2 instances in an Auto Scaling group launch configuration should not have an associated public IP address, except for in limited edge cases\. Amazon EC2 instances should only be accessible from behind a load balancer instead of being directly exposed to the internet\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
Asia Pacific \(Osaka\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="autoscaling-5-remediation"></a>

An Auto Scaling group is associated with one launch configuration at a time\. You cannot modify a launch configuration after you have create it\. To change the launch configuration for an Auto Scaling group, use an existing launch configuration as the basis for a new launch configuration\. Then, update the Auto Scaling group to use the new launch configuration as described in steps below\.

After you change the launch configuration for an Auto Scaling group, any new instances are launched with the new configuration options\. Existing instances are not affected\. To update existing instances, either terminate them so that they are replaced by your Auto Scaling group, or allow automatic scaling to gradually replace older instances with newer instances based on your [termination policies](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-instance-termination.html)\.

**To enable Elastic Load Balancing health checks**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Auto Scaling**, choose **Launch Configurations**\.

1. Select the launch configuration and choose **Actions**, then **Copy launch configuration**\. This sets up a new launch configuration with the same options as the original, but with "Copy" added to the name\. 

1. On the **Create Launch Configuration** page, expand **Advanced details** under **Additional configuration \- optional**\.

1. Under **IP address type**, choose **Do not assign a public IP address to any instances**\.

1. When you have finished, Choose **Create launch configuration**\.

1. On the navigation pane, under **Auto Scaling**, choose **Auto Scaling Groups**\.

1. Select the check box next to the Auto Scaling group\.

1. A split pane opens up in the bottom part of the page, showing information about the group that's selected\.

1. On the **Details** tab, choose **Launch configuration**, **Edit**\.

1. For **Launch configuration**, select the new launch configuration\.

1. When you have finished changing your launch configuration, choose **Update**\.

## \[AutoScaling\.6\] Auto Scaling groups should use multiple instance types in multiple Availability Zones<a name="autoscaling-6"></a>

**Related requirements:** NIST\.800\-53\.r5 CP\-10, NIST\.800\-53\.r5 CP\-2\(2\), NIST\.800\-53\.r5 CP\-6\(2\), NIST\.800\-53\.r5 SC\-36, NIST\.800\-53\.r5 SC\-5\(2\), NIST\.800\-53\.r5 SI\-13\(5\)

**Category:** Recover > Resilience > High Availability

**Severity:** Medium

**Resource type:** `AWS::AutoScaling::AutoScalingGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-multiple-instance-types.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-multiple-instance-types.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon EC2 Auto Scaling group uses multiple instance types\. The control fails if the Auto Scaling group has only one instance type defined\.

You can enhance availability by deploying your application across multiple instance types running in multiple Availability Zones\. Security Hub recommends using multiple instance types so that the Auto Scaling group can launch another instance type if there is insufficient instance capacity in your chosen Availability Zones\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="autoscaling-6-remediation"></a>

For instructions on creating an Auto Scaling group with multiple instance types, see [Auto Scaling groups with multiple instance types and purchase options](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-mixed-instances-groups.html) in the *Amazon EC2 Auto Scaling User Guide*\.

## \[AutoScaling\.9\] Amazon EC2 Auto Scaling groups should use Amazon EC2 launch templates<a name="autoscaling-9"></a>

**Related requirements:** NIST\.800\-53\.r5 CA\-9\(1\), NIST\.800\-53\.r5 CM\-2, NIST\.800\-53\.r5 CM\-2\(2\)

**Category:** Identify > Resource Configuration

**Severity:** Medium

**Resource type:** `AWS::AutoScaling::AutoScalingGroup`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-template.html](https://docs.aws.amazon.com/config/latest/developerguide/autoscaling-launch-template.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether an Amazon EC2 Auto Scaling group is created from an EC2 launch template\. This control fails if an Amazon EC2 Auto Scaling group is not created with a launch template or if a launch template is not specified in a mixed instances policy\.

An EC2 Auto Scaling group can be created from either an EC2 launch template or a launch configuration\. However, using a launch template to create an Auto Scaling group ensures that you have access to the latest features and improvements\.

**Note**  
This control is not supported in the following Regions:  
Asia Pacific \(Jakarta\)
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="autoscaling-9-remediation"></a>

To create an Auto Scaling group with an EC2 launch template, see [Create an Auto Scaling group using a launch template](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-asg-launch-template.html) in the *Amazon EC2 Auto Scaling User Guide*\. For information about how to replace a launch configuration with a launch template, see [Replace a launch configuration with a launch template](https://docs.aws.amazon.com/autoscaling/ec2/userguide/replace-launch-config.html) in the *Amazon EC2 User Guide for Windows Instances*\.