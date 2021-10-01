# AWS Config resources required for PCI DSS controls<a name="securityhub-standards-pci-config-resources"></a>

The PCI DSS controls perform checks against the following resources\. For AWS Security Hub to accurately report findings for all of the controls, you must enable recording for these resources in AWS Config\.
+ AWS account
+ `AWS::AutoScaling::AutoScalingGroup`
+ `AWS::CloudTrail::Trail`
+ `AWS::CodeBuild::Project`
+ `AWS::DMS::ReplicationInstance`
+ `AWS::EC2::EIP`
+ `AWS::EC2::Instance`
+ `AWS::EC2::SecurityGroup`
+ `AWS::EC2::Volume`
+ `AWS::EC2::VPC`
+ `AWS::ElasticLoadBalancingV2::LoadBalancer`
+ `AWS::Elasticsearch::Domain`
+ `AWS::IAM::Policy`
+ `AWS::IAM::User`
+ `AWS::KMS::Key`
+ `AWS::Lambda::Function`
+ `AWS::RDS::DBInstance`
+ `AWS::RDS::DBSnapshot`
+ `AWS::Redshift::Cluster`
+ `AWS::S3::Bucket`
+ `AWS::SageMaker::NotebookInstance`
+ `AWS::SSM::AssociationCompliance`
+ `AWS::SSM::PatchCompliance`