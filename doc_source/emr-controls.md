# Amazon EMR controls<a name="emr-controls"></a>

These controls are related to Amazon EMR resources\.

## \[EMR\.1\] Amazon Elastic MapReduce cluster master nodes should not have public IP addresses<a name="emr-1"></a>

**Related requirements:** PCI DSS v3\.2\.1/1\.2\.1,PCI DSS v3\.2\.1/1\.3\.1,PCI DSS v3\.2\.1/1\.3\.2,PCI DSS v3\.2\.1/1\.3\.4,PCI DSS v3\.2\.1/1\.3\.6, NIST\.800\-53\.r5 AC\-21, NIST\.800\-53\.r5 AC\-3, NIST\.800\-53\.r5 AC\-3\(7\), NIST\.800\-53\.r5 AC\-4, NIST\.800\-53\.r5 AC\-4\(21\), NIST\.800\-53\.r5 AC\-6, NIST\.800\-53\.r5 SC\-7, NIST\.800\-53\.r5 SC\-7\(11\), NIST\.800\-53\.r5 SC\-7\(16\), NIST\.800\-53\.r5 SC\-7\(20\), NIST\.800\-53\.r5 SC\-7\(21\), NIST\.800\-53\.r5 SC\-7\(3\), NIST\.800\-53\.r5 SC\-7\(4\), NIST\.800\-53\.r5 SC\-7\(9\)

**Category:** Protect > Secure network configuration

**Severity:** High

**Resource type:** `AWS::EMR::Cluster`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/emr-master-no-public-ip.html](https://docs.aws.amazon.com/config/latest/developerguide/emr-master-no-public-ip.html)

**Schedule type:** Periodic

**Parameters:** None

This control checks whether master nodes on Amazon EMR clusters have public IP addresses\. 

The control fails if the master node has public IP addresses that are associated with any of its instances\. Public IP addresses are designated in the `PublicIp` field of the `NetworkInterfaces` configuration for the instance\. This control only checks Amazon EMR clusters that are in a `RUNNING` or `WAITING` state\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Europe \(Milan\)
Middle East \(UAE\)

### Remediation<a name="emr-1-remediation"></a>

During launch, you can control whether your instance in a default or nondefault subnet is assigned a public IPv4 address\.

By default, default subnets have this attribute set to `true`\. Nondefault subnets have the IPv4 public addressing attribute set to `false`, unless it was created by the Amazon EC2 launch instance wizard\. In that case, the wizard sets the attribute to `true`\.

You need to launch your cluster in a VPC with a private subnet that has the IPv4 public addressing attribute set to `false`\. 

After launch, you cannot manually disassociate a public IPv4 address from your instance\.

To remediate this finding, you need to create a new cluster in VPC private subnet\. For information on how to launch a cluster in into a VPC private subnet, see [Launch clusters into a VPC](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-vpc-launching-job-flows.html) in the *Amazon EMR Management Guide*\.