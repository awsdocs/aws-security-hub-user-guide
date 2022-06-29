# AWS Config resources required for AWS Foundational Security Best Practices controls<a name="standards-fsbp-config-resources"></a>

The AWS Foundational Security Best Practices controls perform checks against the following resources\. For AWS Security Hub to accurately report findings for all of the controls, you must enable recording for these resources in AWS Config\.

**Note**  
In Regions where a control is not available, the corresponding resource is not available in AWS Config\.
+ AWS account
+ `AWS::ACM::Certificate`
+ `AWS::ApiGateway::Stage`
+ `AWS::ApiGatewayV2::Stage`
+ `AWS::AutoScaling::AutoScalingGroup`
+ `AWS::AutoScaling::LaunchConfiguration`
+ `AWS::CloudFormation::Stack`
+ `AWS::CloudFront::Distribution`
+ `AWS::CloudTrail::Trail`
+ `AWS::CodeBuild::Project`
+ `AWS::DAX::Cluster`
+ `AWS::DMS::ReplicationInstance`
+ `AWS::DynamoDB::Table`
+ `AWS::EC2::Instance`
+ `AWS::EC2::NetworkAcl`
+ `AWS::EC2::SecurityGroup`
+ `AWS::EC2::Subnet`
+ `AWS::EC2::TransitGateway`
+ `AWS::EC2::Volume`
+ `AWS::EC2::VPC`
+ `AWS::EC2::VPNConnection`
+ `AWS::ECR::Repository`
+ `AWS::ECS::Cluster`
+ `AWS::ECS::Service`
+ `AWS::ECS::TaskDefinition`
+ `AWS::EFS::AccessPoint`
+ `AWS::EFS::FileSystem`
+ `AWS::EKS::Cluster`
+ `AWS::ElasticBeanstalk::Environment`
+ `AWS::ElasticLoadBalancing::LoadBalancer`
+ `AWS::ElasticLoadBalancingV2::LoadBalancer`
+ `AWS::Elasticsearch::Domain`
+ `AWS::EMR::Cluster`
+ `AWS::IAM::Group`
+ `AWS::IAM::Policy`
+ `AWS::IAM::Role`
+ `AWS::IAM::User`
+ `AWS::Kinesis::Stream`
+ `AWS::KMS::Key`
+ `AWS::Lambda::Function`
+ `AWS::NetworkFirewall::FirewallPolicy`
+ `AWS::OpenSearch::Domain`
+ `AWS::RDS::DBCluster`
+ `AWS::RDS::DBClusterSnapshot`
+ `AWS::RDS::DBInstance`
+ `AWS::RDS::DBSnapshot`
+ `AWS::RDS::EventSubscription`
+ `AWS::Redshift::Cluster`
+ `AWS::S3::Bucket`
+ `AWS::SageMaker::NotebookInstance`
+ `AWS::SecretsManager::Secret`
+ `AWS::SNS::Topic`
+ `AWS::SQS::Queue`
+ `AWS::SSM::AssociationCompliance`
+ `AWS::SSM::Document`
+ `AWS::SSM::PatchCompliance`
+ `AWS::WAFRegional::Rule`
+ `AWS::WAFRegional::RuleGroup`
+ `AWS::WAFRegional::WebACL`
+ `AWS::WAF::Rule`
+ `AWS::WAF::RuleGroup`
+ `AWS::WAF::WebACL`