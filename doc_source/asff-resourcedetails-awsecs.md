# AwsEcs<a name="asff-resourcedetails-awsecs"></a>

The following are examples of the AWS Security Finding Format for `AwsEcs` resources\.

## AwsEcsCluster<a name="asff-resourcedetails-awsecscluster"></a>

The `AwsEcsCluster` object provides details about an Amazon Elastic Container Service cluster\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcsCluster` object\. To view descriptions of `AwsEcsCluster` attributes, see [AwsEcsClusterDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcsClusterDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
    "AwsEcsCluster": {
        "CapacityProviders": [],
        "ClusterSettings": [
            {
                "Name": "containerInsights",
                "Value": "enabled"
            }
        ],
        "Configuration": {
            "ExecuteCommandConfiguration": {
                "KmsKeyId": "kmsKeyId",
                "LogConfiguration": {
                    "CloudWatchEncryptionEnabled": true,
                    "CloudWatchLogGroupName": "cloudWatchLogGroupName",
                    "S3BucketName": "s3BucketName",
                    "S3EncryptionEnabled": true,
                    "S3KeyPrefix": "s3KeyPrefix"
                },
                "Logging": "DEFAULT"
            }
        }
        "DefaultCapacityProviderStrategy": [
            {
                "Base": 0,
                "CapacityProvider": "capacityProvider",
                "Weight": 1
            }
        ]
    }
```

## AwsEcsContainer<a name="asff-resourcedetails-awsecscontainer"></a>

The `AwsEcsContainer` object contains details about an Amazon ECS container\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcsContainer` object\. To view descriptions of `AwsEcsContainer` attributes, see [AwsEcsContainerDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcsContainerDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEcsContainer": {
    "Image": "1111111/knotejs@sha256:356131c9fef111111111111115f4ed8de5f9dce4dc3bd34bg21846588a3",
    "MountPoints": [{
        "ContainerPath": "/mnt/etc",
        "SourceVolume": "vol-03909e9"
    }],
    "Name": "knote",
    "Privileged": true 
}
```

## AwsEcsService<a name="asff-resourcedetails-awsecsservice"></a>

The `AwsEcsService` object provides details about a service within an Amazon ECS cluster\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcsService` object\. To view descriptions of `AwsEcsService` attributes, see [AwsEcsServiceDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcsServiceDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEcsService": {
    "CapacityProviderStrategy": [
        {
            "Base": 12,
            "CapacityProvider": "",
            "Weight": ""
        }
    ],
    "Cluster": "arn:aws:ecs:us-east-1:111122223333:cluster/example-ecs-cluster",
    "DeploymentConfiguration": {
        "DeploymentCircuitBreaker": {
            "Enable": false,
            "Rollback": false
        },
        "MaximumPercent": 200,
        "MinimumHealthyPercent": 100
    },
    "DeploymentController": "",
    "DesiredCount": 1,
    "EnableEcsManagedTags": false,
    "EnableExecuteCommand": false,
    "HealthCheckGracePeriodSeconds": 1,
    "LaunchType": "FARGATE",
    "LoadBalancers": [
        {
            "ContainerName": "",
            "ContainerPort": 23,
            "LoadBalancerName": "",
            "TargetGroupArn": ""
        }
    ],
    "Name": "sample-app-service",
    "NetworkConfiguration": {
        "AwsVpcConfiguration": {
            "Subnets": [
                "Subnet-example1",
                "Subnet-example2"
            ],
        "SecurityGroups": [
                "Sg-0ce48e9a6e5b457f5"
        ],
        "AssignPublicIp": "ENABLED"
        }
    },
    "PlacementConstraints": [
        {
            "Expression": "",
            "Type": ""
        }
    ],
    "PlacementStrategies": [
        {
            "Field": "",
            "Type": ""
        }
    ],
    "PlatformVersion": "LATEST",
    "PropagateTags": "",
    "Role": "arn:aws:iam::111122223333:role/aws-servicerole/ecs.amazonaws.com/ServiceRoleForECS",
    "SchedulingStrategy": "REPLICA",
    "ServiceName": "sample-app-service",
    "ServiceArn": "arn:aws:ecs:us-east-1:111122223333:service/example-ecs-cluster/sample-app-service",
    "ServiceRegistries": [
        {
            "ContainerName": "",
            "ContainerPort": 1212,
            "Port": 1221,
            "RegistryArn": ""
        }
    ],
    "TaskDefinition": "arn:aws:ecs:us-east-1:111122223333:task-definition/example-taskdef:1"
}
```

## AwsEcsTask<a name="asff-resourcedetails-awsecstask"></a>

The `AwsEcsTask` object provides details about an Amazon ECS task\. 

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcsTask` object\. To view descriptions of `AwsEcsTask` attributes, see [AwsEcsTask](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcsTaskDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsEcsTask": {
	"ClusterArn": "arn:aws:ecs:us-west-2:123456789012:task/MyCluster/1234567890123456789",
	"CreatedAt": "1557134011644",
	"Group": "service:fargate-service",
	"StartedAt": "1557134011644",
	"StartedBy": "ecs-svc/1234567890123456789",
	"TaskDefinitionArn": "arn:aws:ecs:us-west-2:123456789012:task-definition/sample-fargate:2",
	"Version": 3,
	"Volumes": [{
		"Name": "string",
		"Host": {
			"SourcePath": "string"
		}
	}],
	"Containers": {
		"Image": "1111111/knotejs@sha256:356131c9fef111111111111115f4ed8de5f9dce4dc3bd34bg21846588a3",
		"MountPoints": [{
			"ContainerPath": "/mnt/etc",
			"SourceVolume": "vol-03909e9"
		}],
		"Name": "knote",
		"Privileged": true
	}
}
```

## AwsEcsTaskDefinition<a name="asff-resourcedetails-awsecstaskdefinition"></a>

The `AwsEcsTaskDefinition` object contains details about a task definition\. A task definition describes the container and volume definitions of an Amazon Elastic Container Service task\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcsTaskDefinition` object\. To view descriptions of `AwsEcsTaskDefinition` attributes, see [AwsEcsTaskDefinitionDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcsTaskDefinitionDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
    "AwsEcsTaskDefinition": {
        "ContainerDefinitions": [
            {
                "Command": ['ruby', 'hi.rb'],
                "Cpu":128,
                "Essential": true,
                "HealthCheck": {
                    "Command": ["CMD-SHELL", "curl -f http://localhost/ || exit 1"],
                    "Interval": 10,
                    "Retries": 3,
                    "StartPeriod": 5,
                    "Timeout": 20
                },
                "Image": "tongueroo/sinatra:latest",
                "Interactive": true,
                "Links": [],
                "LogConfiguration": {
                    "LogDriver": "awslogs",
                    "Options": {
                        "awslogs-group": "/ecs/sinatra-hi",
                        "awslogs-region": "ap-southeast-1",
                        "awslogs-stream-prefix": "ecs"
                    },
                    "SecretOptions": []
                    
                },
                "MemoryReservation": 128,
                "Name": "web",
                "PortMappings": [
                    {
                        "ContainerPort": 4567,
                        "HostPort":4567,
                        "Protocol": "tcp"
                    }
                ],
                "Privileged": true,
                "StartTimeout": 10,
                "StopTimeout": 100,
            }
        ],
        "Family": "sinatra-hi",
        "NetworkMode": "host",
        "RequiresCompatibilities": ["EC2"],
        "TaskRoleArn": "arn:aws:iam::111122223333:role/ecsTaskExecutionRole",
    }
```