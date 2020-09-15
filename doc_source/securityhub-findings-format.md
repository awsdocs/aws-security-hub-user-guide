# AWS Security Finding Format \(ASFF\)<a name="securityhub-findings-format"></a>

AWS Security Hub consumes, aggregates, organizes, and prioritizes findings from AWS security services and from the third\-party product integrations\. Security Hub processes these findings using a standard findings format called the AWS Security Finding Format \(ASFF\), which eliminates the need for time\-consuming data conversion efforts\. Then it correlates ingested findings across products to prioritize the most important ones\.

**Contents**
+ [ASFF syntax](#securityhub-findings-format-syntax)
+ [ASFF attributes](#securityhub-findings-format-attributes)
  + [Compliance](#asff-compliance)
    + [StatusReasons](#asff-compliance-statusreasons)
  + [Malware](#asff-malware)
  + [Network](#asff-network)
    + [OpenPortRange](#asff-network-openportrange)
  + [NetworkPath](#asff-networkpath)
    + [Egress](#asff-networkpath-egress)
    + [Ingress](#asff-networkpath-ingress)
    + [Destination](#asff-networkpath-egress-ingress-destination)
    + [Source](#asff-networkpath-egress-ingress-source)
  + [Note](#asff-note)
  + [PatchSummary](#asff-patchsummary)
  + [Process](#asff-process)
  + [RelatedFindings](#asff-relatedfindings)
  + [Remediation](#asff-remediation)
    + [Recommendation](#asff-remediation-recommendation)
  + [Resources](#asff-resources)
    + [AwsAutoScalingAutoScalingGroup](#asff-resourcedetails-awsautoscalingautoscalinggroup)
    + [AwsCloudFrontDistribution](#asff-resourcedetails-awscloudfrontdistribution)
      + [Logging](#asff-resourcedetails-awscloudfrontdistribution-logging)
      + [Origins](#asff-resourcedetails-awscloudfrontdistribution-origins)
    + [AwsCodeBuildProject](#asff-resourcedetails-awscodebuildproject)
      + [Environment](#asff-resourcedetails-awscodebuildproject-environment)
      + [Source](#asff-resourcedetails-awscodebuildproject-source)
      + [VpcConfig](#asff-resourcedetails-awscodebuildproject-vpcconfig)
    + [AwsDynamoDbTable](#asff-resourcedetails-awsdynamodbtable)
      + [AttributeDefinitions](#asff-resourcedetails-awsdynamodbtable-attributedefinitions)
      + [BillingModeSummary](#asff-resourcedetails-awsdynamodbtable-billingmodesummary)
      + [GlobalSecondaryIndexes](#asff-resourcedetails-awsdynamodbtable-globalsecondaryindexes)
      + [KeySchema](#asff-resourcedetails-awsdynamodbtable-keyschema)
      + [LocalSecondaryIndexes](#asff-resourcedetails-awsdynamodbtable-localsecondaryindexes)
      + [Projection \(for global and local secondary indexes\)](#asff-resourcedetails-awsdynamodbtable-projection)
      + [ProvisionedThroughput](#asff-resourcedetails-awsdynamodbtable-provisionedthroughput)
      + [Replicas](#asff-resourcedetails-awsdynamodbtable-replicas)
      + [RestoreSummary](#asff-resourcedetails-awsdynamodbtable-restoresummary)
      + [SseDescription](#asff-resourcedetails-awsdynamodbtable-ssedescription)
      + [StreamSpecification](#asff-resourcedetails-awsdynamodbtable-streamspecification)
    + [AwsEc2Eip](#asff-resourcedetails-awsec2eip)
    + [AwsEc2Instance](#asff-resourcedetails-awsec2instance)
    + [AwsEc2NetworkInterface](#asff-resourcedetails-awsec2networkinterface)
      + [Attachment](#asff-resourcedetails-awsec2networkinterface-attachment)
      + [SecurityGroups](#asff-resourcedetails-awsec2networkinterface-securitygroups)
    + [AwsEc2SecurityGroup](#asff-resourcedetails-awsec2securitygroup)
      + [IP permission object](#asff-resourcedetails-awsec2securitygroup-ippermission)
    + [AwsEc2Volume](#asff-resourcedetails-awsec2volume)
      + [Attachments](#asff-resourcedetails-awsec2volume-attachments)
    + [AwsEc2Vpc](#asff-resourcedetails-awsec2vpc)
      + [CidrBlockAssociationSet](#asff-resourcedetails-awsec2vpc-cidrblockassociationset)
      + [IpV6CidrBlockAssociationSet](#asff-resourcedetails-awsec2vpc-ipv6cidrblockassociationset)
    + [AwsElasticSearchDomain](#asff-resourcedetails-awselasticsearchdomain)
      + [DomainEndpointOptions](#asff-resourcedetails-awselasticsearchdomain-domainendpointoptions)
      + [DomainStatus](#asff-resourcedetails-awselasticsearchdomain-domainstatus)
      + [EncryptionAtRestOptions](#asff-resourcedetails-awselasticsearchdomain-encryptionatrestoptions)
      + [NodeToNodeEncryptionOptions](#asff-resourcedetails-awselasticsearchdomain-nodetonodeencryptionoptions)
      + [VpcOptions](#asff-resourcedetails-awselasticsearchdomain-vpcoptions)
    + [AwsElbv2LoadBalancer](#asff-resourcedetails-awselbv2loadbalancer)
      + [AvailabilityZones](#asff-resourcedetails-awselbv2loadbalancer-availabilityzones)
      + [State](#asff-resourcedetails-awselbv2loadbalancer-state)
    + [AwsIamAccessKey](#asff-resourcedetails-awsiamaccesskey)
    + [AwsIamPolicy](#asff-resourcedetails-awsiampolicy)
      + [PolicyVersionList](#asff-resourcedetails-awsiampolicy-policyversionlist)
    + [AwsIamRole](#asff-resourcedetails-awsiamrole)
    + [AwsIamUser](#asff-resourcedetails-awsiamuser)
      + [AttachedManagedPolicies](#asff-resourcedetails-awsiamuser-attachedmanagedpolicies)
      + [PermissionsBoundary](#asff-resourcedetails-awsiamuser-permissionsboundary)
      + [UserPolicyList](#asff-resourcedetails-awsiamuser-userpolicylist)
    + [AwsKmsKey](#asff-resourcedetails-awskmskey)
    + [AwsLambdaFunction](#asff-resourcedetails-awslambdafunction)
      + [Code](#asff-resourcedetails-awslambdafunction-code)
      + [DeadLetterConfig](#asff-resourcedetails-awslambdafunction-deadletterconfig)
      + [Environment](#asff-resourcedetails-awslambdafunction-environment)
      + [Layers](#asff-resourcedetails-awslambdafunction-layers)
      + [TracingConfig](#asff-resourcedetails-awslambdafunction-tracingconfig)
      + [VpcConfig](#asff-resourcedetails-awslambdafunction-vpcconfig)
    + [AwsLambdaLayerVersion](#asff-resourcedetails-awslambdalayerversion)
    + [AwsRdsDbCluster](#asff-resourcedetails-awsrdsdbcluster)
      + [AssociatedRoles](#asff-resourcedetails-awsrdsdbcluster-associatedroles)
      + [DbClusterMembers](#asff-resourcedetails-awsrdsdbcluster-dbclustermembers)
      + [DbClusterOptionGroupMemberships](#asff-resourcedetails-awsrdsdbcluster-dbclusteroptiongroupmemberships)
      + [DomainMemberships](#asff-resourcedetails-awsrdsdbcluster-domainmemberships)
      + [VpcSecurityGroups](#asff-resourcedetails-awsrdsdbcluster-vpcsecuritygroups)
    + [AwsRdsDbClusterSnapshot](#asff-resourcedetails-awsrdsdbclustersnapshot)
    + [AwsRdsDbInstance](#asff-resourcedetails-awsrdsdbinstance)
      + [AssociatedRoles](#asff-resourcedetails-awsrdsdbinstance-associatedroles)
      + [DbParameterGroups](#asff-resourcedetails-awsrdsdbinstance-dbparametergroups)
      + [DbSubnetGroup](#asff-resourcedetails-awsrdsdbinstance-dbsubnetgroup)
      + [DomainMemberships](#asff-resourcedetails-awsrdsdbinstance-domainmemberships)
      + [Endpoint](#asff-resourcedetails-awsrdsdbinstance-endpoint)
      + [ListenerEndpoint](#asff-resourcedetails-awsrdsdbinstance-listenerendpoint)
      + [OptionGroupMemberships](#asff-resourcedetails-awsrdsdbinstance-optiongroupmemberships)
      + [PendingModifiedValues](#asff-resourcedetails-awsrdsdbinstance-pendingmodifiedvalues)
      + [ProcessorFeatures](#asff-resourcedetails-awsrdsdbinstance-processorfeatures)
      + [StatusInfos](#asff-resourcedetails-awsrdsdbinstance-statusinfos)
      + [VpcSecurityGroups](#asff-resourcedetails-awsrdsdbinstance-vpcsecuritygroups)
    + [AwsRdsDbSnapshot](#asff-resourcedetails-awsrdsdbsnapshot)
    + [AwsS3Bucket](#asff-resourcedetails-awss3bucket)
      + [ApplyServerSideEncryptionByDefault](#asff-resourcedetails-awss3bucket-applyserversideencryptionbydefault)
    + [AwsS3Object](#asff-resourcedetails-awss3object)
    + [AwsSecretsManagerSecret](#asff-resourcedetails-awssecretsmanagersecret)
    + [AwsSnsTopic](#asff-resourcedetails-awssnstopic)
      + [Subscription](#asff-resourcedetails-awssnstopic-subscription)
    + [AwsSqsQueue](#asff-resourcedetails-awssqsqueue)
    + [AwsWafWebAcl](#asff-resourcedetails-awswafwebacl)
      + [Rule object](#asff-resourcedetails-awswafwebacl-rule)
    + [Container](#asff-resourcedetails-container)
    + [Other](#asff-resourcedetails-other)
  + [Severity](#asff-severity)
    + [How Security Hub maps Label and Normalized values](#asff-severity-map-normalized-label)
    + [Guidance for assigning the normalized severity \(AWS services and partners\)](#asff-severity-normalized-guidance)
  + [ThreatIntelIndicators](#asff-threatintelindicators)
  + [Vulnerabilities](#asff-vulnerabilities)
    + [Cvss](#asff-vulnerabilities-cvss)
    + [Vendor](#asff-vulnerabilities-vendor)
    + [VulnerablePackages](#asff-vulnerabilities-vulnerablepackages)
  + [Workflow](#asff-workflow)
+ [Types taxonomy for ASFF](#securityhub-findings-format-type-taxonomy)

## ASFF syntax<a name="securityhub-findings-format-syntax"></a>

The following is the syntax of the complete finding JSON in the ASFF\.

```
"Findings": [ 
    {
        "AwsAccountId": "string",
        "Compliance": { 
            "RelatedRequirements": ["string"],
            "Status": "string",
            "StatusReasons": [
                {
                    "Description": "string",
                    "ReasonCode": "string"
                }
            ]
        },
        "Confidence": number,
        "CreatedAt": "string",
        "Criticality": number,
        "Description": "string",
        "FirstObservedAt": "string",
        "GeneratorId": "string",
        "Id": "string",
        "LastObservedAt": "string",
        "Malware": [ 
            { 
                "Name": "string",
                "Path": "string",
                "State": "string",
                "Type": "string"
            }
        ],
        "Network": { 
            "DestinationDomain": "string",
            "DestinationIpV4": "string",
            "DestinationIpV6": "string",
            "DestinationPort": number,
            "Direction": "string",
            "OpenPortRange": {
                  "Begin": integer,
                  "End": integer
            },
            "Protocol": "string",
            "SourceDomain": "string",
            "SourceIpV4": "string",
            "SourceIpV6": "string",
            "SourceMac": "string",
            "SourcePort": number
        },
        "NetworkPath" : [
            {
                "ComponentId": "string",
                "ComponentType": "string",
                "Egress": {
                    "Destination": {
                        "Address": ["string"],
                        "PortRanges": [
                            {
                                "Begin": integer,
                                "End": integer
                            }
                        ]
                    },
                    "Protocol": "string",
                    "Source": {
                        "Address": ["string"],
                        "PortRanges": [
                            {
                                "Begin": integer,
                                "End": integer
                            }
                        ]
                    }
                },
                "Ingress": {
                    "Destination": {
                        "Address": ["string"],
                        "PortRanges": [
                            {
                                "Begin": integer,
                                "End": integer
                            }
                        ]
                    },
                    "Protocol": "string",
                    "Source": {
                        "Address": ["string"],
                        "PortRanges": [
                            {
                                "Begin": integer,
                                "End": integer
                            }
                        ]
                    }
                }
            }
        ],
        "Note": { 
            "Text": "string",
            "UpdatedAt": "string",
            "UpdatedBy": "string"
        },
        "PatchSummary" : {
            "FailedCount" : number,
            "Id" : "string",
            "InstalledCount" : number,
            "InstalledOtherCount" : number,
            "InstalledPendingReboot" : number,
            "InstalledRejectedCount" : number,
            "MissingCount" : number,
            "Operation" : "string",
            "OperationEndTime" : "string",
            "OperationStartTime" : "string",
            "RebootOption" : "string"
        },
        "Process": { 
            "LaunchedAt": "string",
            "Name": "string",
            "ParentPid": number,
            "Path": "string",
            "Pid": number,
            "TerminatedAt": "string"
        },
        "ProductArn": "string",
        "ProductFields": { 
            "string" : "string" 
        },
        "RecordState": "string",
        "RelatedFindings": [ 
            { 
                "Id": "string",
                "ProductArn": "string"
            }
        ],
        "Remediation": { 
            "Recommendation": { 
                "Text": "string",
                "Url": "string"
            }
        },
        "Resources": [ 
            { 
                "Details": { 
                    "AwsAutoScalingAutoScalingGroup": {
                        "CreatedTime": "string",
                        "HealthCheckGracePeriod": integer,
                        "HealthCheckType": "string",
                        "LaunchConfigurationName": "string",
                        "LoadBalancerNames": ["string"]
                    },
                    "AwsCloudFrontDistribution": {
                        "DomainName": "string",
                        "Etag": "string",
                        "LastModifiedTime": "string",
                        "Logging": {
                            "Bucket": "string",
                            "Enabled": boolean,
                            "IncludeCookies": boolean,
                            "Prefix": "string"
                        },
                        "Origins": {
                            "Items": [
                                {
                                    "DomainName": "string",
                                    "Id": "string",
                                    "OriginPath": "string"
                                }
                            ]
                        },
                        "Status": "string",
                        "WebAclId": "string"
                    },
                    "AwsCodeBuildProject": {
                        "EncryptionKey": "string",
                        "Environment": {
                            "Type": "string",
                            "Certificate": "string",
                            "ImagePullCredentialsType": "string",
                            "RegistryCredential": {
                                "Credential": "string",
                                "CredentialProvider": "string"
                            }
                        },
                        "Name": "string",
                        "ServiceRole": "string",
                        "Source": {
                            "Type": "string",
                            "Location": "string",
                            "GitCloneDepth": integer
                        },
                        "VpcConfig": {
                            "VpcId": "string",
                            "Subnets": ["string"],
                            "SecurityGroupIds": ["string"]
                        }
                    },
                    "AwsDynamoDbTable": {
                        "AttributeDefinitions": [
                            {
                                "AttributeName": "string",
                                "AttributeType": "string"
                            }
                        ],
                        "BillingModeSummary" {
                            "BillingMode": "string",
                            "LastUpdateToPayPerRequestDateTime": "string"
                        },
                        "CreationDateTime": "string",
                        "GlobalSecondaryIndexes": [
                            {
                                "Backfilling": boolean,
                                "IndexArn": "string",
                                "IndexName": "string",
                                "IndexSizeBytes": number,
                                "IndexStatus": "string",
                                "ItemCount": number,
                                "KeySchema": [
                                    {
                                        "AttributeName": "string",
                                        "KeyType": "string"
                                    }
                                ],
                                "Projection": {
                                    "NonKeyAttributes": [ "string" ],
                                    "ProjectionType": "string"
                                },
                                "ProvisionedThroughput": {
                                    "LastDecreaseDateTime": "string",
                                    "LastIncreaseDateTime": "string",
                                    "NumberOfDecreasesToday": number,
                                    "ReadCapacityUnits": number,
                                    "WriteCapacityUnits": number
                                },
                            }
                        ],
                        "GlobalTableVersion": "string",
                        "ItemCount": number,
                        "KeySchema": [
                            {
                                "AttributeName": "string",
                                "KeyType": "string"
                            }
                        ],
                        "LatestStreamArn": "string",
                        "LatestStreamLabel": "string",
                        "LocalSecondaryIndexes": [
                            {
                                "IndexArn": "string",
                                "IndexName": "string",
                                "KeySchema": [
                                    {
                                    "AttributeName": "string",
                                    "KeyType": "string"
                                    }
                                ],
                                "Projection": {
                                    "NonKeyAttributes": [ "string" ],
                                    "ProjectionType": "string"
                                }
                            }
                        ],
                        "ProvisionedThroughput": {
                            "LastDecreaseDateTime": "string",
                            "LastIncreaseDateTime": "string",
                            "NumberOfDecreasesToday": number,
                            "ReadCapacityUnits": number,
                            "WriteCapacityUnits": number
                        },
                        "Replicas": [
                            {
                                "GlobalSecondaryIndexes":[
                                    {
                                        "IndexName": "string",
                                        "ProvisionedThroughputOverride": {
                                            "ReadCapacityUnits": number
                                    }
                                ],
                                "KmsMasterKeyId" : "string"
                                "ProvisionedThroughputOverride": {
                                    "ReadCapacityUnits": number
                                },
                                "RegionName": "string"
                                "ReplicaStatus": "string"
                                "ReplicaStatusDescription": "string"
                            }
                        ],
                        "RestoreSummary": {
                                "RestoreDateTime": "string",
                                "RestoreInProgress": boolean,
                                "SourceBackupArn": "string",
                                "SourceTableArn": "string"
                        },
                        "SseDescription": {
                            "InaccessibleEncryptionDateTime": "string",
                            "KmsMasterKeyArn": "string",
                            "SseType": "string",
                            "Status": "string"
                        },
                        "StreamSpecification": {
                            "StreamEnabled": boolean,
                            "StreamViewType": "string"
                        },
                        "TableId": "string",
                        "TableName": "string",
                        "TableSizeBytes": number,
                        "TableStatus": "string"
                    },
                    "AwsEc2Eip": {
                        "AllocationId": "string",
                        "AssociationId": "string",
                        "Domain": "string",
                        "InstanceId": "string",
                        "NetworkBorderGroup": "string",
                        "NetworkInterfaceId": "string",
                        "NetworkInterfaceOwnerId": "string",
                        "PrivateIpAddress": "string",
                        "PublicIp": "string",
                        "PublicIpv4Pool": "string"
                    },
                    "AwsEc2Instance": { 
                        "IamInstanceProfileArn": "string",
                        "ImageId": "string",
                        "IpV4Addresses": [ "string" ],
                        "IpV6Addresses": [ "string" ],
                        "KeyName": "string",
                        "LaunchedAt": "string",
                        "SubnetId": "string",
                        "Type": "string",
                        "VpcId": "string"
                    },
                    "AwsEc2NetworkInterface": {
                        "Attachment": {
                            "AttachmentId": "string",
                            "AttachTime": "string",
                            "DeleteOnTermination": boolean,
                            "DeviceIndex": number,
                            "InstanceId": "string"
                            "InstanceOwnerId": "string",
                            "Status": "string"
                        },
                        "SecurityGroups": [
                            {
                                "GroupId": "string",
                                "GroupName": "string"
                            }
                        ],
                        "NetworkInterfaceId": "string",
                        "SourceDestCheck": boolean
                    },
                    "AwsEc2SecurityGroup": {
                        "GroupId": "string",
                        "GroupName": "string",
                        "IpPermissions": [
                            {
                                "FromPort": number,
                                "IpProtocol": "string",
                                "IpRanges": [
                                    {
                                        "CidrIp": "string"
                                    }
                                ],
                                "PrefixListIds": [
                                    {"PrefixListId": "string"}
                                ],
                                "ToPort": number,
                                "UserIdGroupPairs": [
                                    {
                                        "UserId": "string",
                                        "GroupId": "string"
                                    }
                                ]
                            }
                        ],
                        "IpPermissionsEgress": [
                            {
                                "FromPort": number,
                                "IpProtocol": "string",
                                "IpRanges": [
                                    {
                                        "CidrIp": "string"
                                    }
                                ],
                                "PrefixListIds": [
                                    {"PrefixListId": "string"}
                                ],
                                "ToPort": number,
                                "UserIdGroupPairs": [
                                    {
                                        "UserId": "string",
                                        "GroupId": "string"
                                    }
                                ]
                            }
                        ],
                        "OwnerId": "string",
                        "VpcId": "string"
                    },
                    "AwsEc2Volume": {
                         "Attachments": [
                            {
                                "AttachTime": "string",
                                "DeleteOnTermination": Boolean,
                                "InstanceId": "string",
                                "Status": "string"
                           }
                          ],
                          "CreateTime": "string",
                          "Encrypted": Boolean,
                          "KmsKeyId": "string",
                          "Size": number,
                          "SnapshotId": "string",
                          "Status": "string"
                    },
                    "AwsEc2Vpc": {
                        "CidrBlockAssociationSet": [
                            {
                                "AssociationId": "string",
                                "CidrBlock": "string",
                                "CidrBlockState": "string"
                            }
                        ],
                        "DhcpOptionsId": "string",
                        "Ipv6CidrBlockAssociationSet": [
                            {
                                "AssociationId": "string",
                                "CidrBlockState": "string",
                                "Ipv6CidrBlock": "string"
                           }
                        ],
                        "State": "string"
                    },
                    "AwsElasticSearchDomain": {
                        "AccessPolicies": "string",
                        "DomainStatus": {
                            "DomainId": "string",
                            "DomainName": "string",
                            "Endpoint": "string",
                            "Endpoints": {
                                "string": "string"
                            }
                        },
                         "DomainEndpointOptions": {
                            "EnforceHTTPS": boolean,
                            "TLSSecurityPolicy": "string"
                        },
                        "ElasticsearchVersion": "string",
                        "EncryptionAtRestOptions": {
                            "Enabled": boolean,
                            "KmsKeyId": "string"
                        },
                        "NodeToNodeEncryptionOptions": {
                            "Enabled": boolean
                        },
                        "VPCOptions": {
                            "AvailabilityZones": [
                                "string"
                            ],
                            "SecurityGroupIds": [
                                "string"
                            ],
                            "SubnetIds": [
                                "string"
                            ],
                            "VPCId": "string"
                        }
                    },
                    "AwsElbv2LoadBalancer": {
                        "AvailabilityZones": {
                            "SubnetId": "string",
                            "ZoneName": "string"
                        },
                        "CanonicalHostedZoneId": "string",
                        "CreatedTime": "string",
                        "DNSName": "string",
                        "IpAddressType": "string",
                        "Scheme": "string",
                        "SecurityGroups": [ "string" ],
                        "State": {
                            "Code": "string",
                            "Reason": "string"
                        },
                        "Type": "string",
                        "VpcId": "string"
                    },
                    "AwsIamAccessKey": { 
                        "CreatedAt": "string",
                        "PrincipalId": "string",
                        "PrincipalName": "string",
                        "PrincipalType": "string",
                        "Status": "string"
                    },
                    "AwsIamPolicy": {
                        "AttachmentCount": number,
                        "CreateDate": "string",
                        "DefaultVersionId": "string",
                        "Description": "string",
                        "IsAttachable": boolean,
                        "Path": "string",
                        "PermissionsBoundaryUsageCount": number,
                        "PolicyId": "string",
                        "PolicyName": "string",
                        "PolicyVersionList": [
                            {
                                "CreateDate": "string",
                                "IsDefaultVersion": boolean,
                                "VersionId": "string"
                            }
                        ,
                        "UpdateDate": "string"
                    },
                    "AwsIamRole": {
                        "AssumeRolePolicyDocument": "string",
                        "CreateDate": "string",
                        "MaxSessionDuration": number,
                        "Path": "string",
                        "RoleId": "string",
                        "RoleName": "string"
                    },
                    "AwsIamUser": {
                        "AttachedManagedPolicies": [
                            {
                                "PolicyArn": "string",
                                "PolicyName": "string"
                            }
                        ],
                        "CreateDate": "string",
                        "GroupList": [ "string" ],
                        "Path": "string",
                        "PermissionsBoundary" : {
                            "PermissionsBoundaryArn" : "string",
                            "PermissionsBoundaryType" : "string"
                        }.
                        "UserId": "string",
                        "UserName": "string",
                        "UserPolicyList": [
                            {
                                "PolicyName": "string"
                            }
                        ]
                    },
                    "AwsKmsKey": {
                        "AWSAccountId": "string",
                        "CreationDate": "string",
                        "Description": string,
                        "KeyId": "string",
                        "KeyManager": "string",
                        "KeyState": "string",
                        "Origin": "string"
                    },
                    "AwsLambdaFunction": {
                        "Code" {
                            "S3Bucket": "string",
                            "S3Key": "string",
                                    "S3ObjectVersion": "string",
                                    "ZipFile": "string"
                         },
                         "CodeSha256": "string",
                         "DeadLetterConfig": {
                              "TargetArn": "string",
                          },
                         "Environment": {
                            "Variables": {
                                "string": "string"
                            },
                            "Error": {
                                "ErrorCode": "string",
                                "Message": "string"
                            }
                         },
                        "FunctionName": "string",
                        "Handler": "string",
                        "KmsKeyArn": "string",
                        "LastModified": "string",
                        "Layers": {
                            "Arn": "string",
                            "CodeSize": number
                        },
                        "RevisionId": "string",
                        "Role": "string",
                        "Runtime": "string",
                        "Timeout": "integer",
                        "TracingConfig": {
                            "TracingConfig.Mode": "string"
                        },
                        "Version": "string",
                        "VpcConfig": {
                            "SecurityGroupIds": [ "string" ],
                            "SubnetIds": [ "string" ]
                        },
                        "MasterArn": "string",
                        "MemorySize": number
                    },
                    "AwsLambdaLayerVersion": {
                        "CompatibleRuntimes": [
                          "string"
                        ],
                        "CreatedDate": "string",
                        "Version": number
                    },
                    "AwsRdsDbCluster": {
                        "ActivityStreamStatus": "string",
                        "AllocatedStorage": number,
                        "AssociatedRoles": [
                            {
                                "RoleArn": "string",
                                "Status": "string"
                            }
                        ],
                        "AvailabilityZones": [ "string" ],
                        "BackupRetentionPeriod": integer,
                        "ClusterCreateTime": "string",
                        "CopyTagsToSnapshot": boolean,
                        "CrossAccountClone": boolean,
                        "CustomEndpoints": [ "string" ],
                        "DatabaseName": "string",
                        "DbClusterIdentifier": "string",
                        "DbClusterMembers": [
                            {
                                "DbClusterParameterGroupStatus": "string",
                                "DbInstanceIdentifier": "string",
                                "IsClusterWriter": boolean,
                                "PromotionTier": integer
                            }
                        ],
                        "DbClusterOptionGroupMemberships": [
                            {
                                "DbClusterOptionGroupName": "string",
                                "Status": "string"
                            }
                         ],
                        "DbClusterParameterGroup": "string",
                        "DbClusterResourceId": "string",
                        "DbSubnetGroup": "string",
                        "DeletionProtection": boolean,
                        "DomainMemberships": [
                            {
                                "Domain": "string",
                                "Fqdn": "string",
                                "IamRoleName": "string",
                                "Status": "string"
                            }
                        ],
                        "EnabledCloudwatchLogsExports": [ "string" ],
                        "Endpoint": "string",
                        "Engine": "string",
                        "EngineMode": "string",
                        "EngineVersion": "string",
                        "HostedZoneId": "string",
                        "HttpEndpointEnabled": boolean,
                        "IamDatabaseAuthenticationEnabled": boolean
                        "KmsKeyId": "string",
                        "MasterUsername": "string",
                        "MultiAz": boolean,
                        "Port": integer,
                        "PreferredBackupWindow": "string",
                        "PreferredMaintenanceWindow": "string",
                        "ReaderEndpoint": "string",
                        "ReadReplicaIdentifiers": [ "string" ],
                        "Status": "string",
                        "StorageEncrypted": boolean,
                        "VpcSecurityGroups": [
                            {
                                "Status": "string",
                                "VpcSecurityGroupId": "string"
                            }
                        ]
                    },
                    "AwsRdsDbClusterSnapshot": {
                        "AllocatedStorage": integer,
                        "AvailabilityZones": [ "string" ],
                        "ClusterCreateTime": "string",
                        "DbClusterIdentifier": "string",
                        "DbClusterSnapshotIdentifier": "string",
                        "Engine": "string",
                        "EngineVersion": "string",
                        "IamDatabaseAuthenticationEnabled": boolean,
                        "KmsKeyId": "string",
                        "LicenseModel": "string",
                        "MasterUsername": "string",
                        "PercentProgress": integer,
                        "Port": integer,
                        "SnapshotCreateTime": "string",
                        "SnapshotType": "string",
                        "Status": "string",
                        "StorageEncrypted": boolean,
                        "VpcId": "string"
                    },
                    "AwsRdsDbInstance": {
                        "AllocatedStorage": number,
                        "AssociatedRoles": [
                            {
                                "RoleArn": "string",
                                "FeatureName": "string",
                                "Status": "string"
                            }
                        ],
                        "AutoMinorVersionUpgrade": boolean,
                        "AvailabilityZone": "string",
                        "BackupRetentionPeriod": number,
                        "CACertificateIdentifier": "string",
                        "CharacterSetName": "string",
                        "CopyTagsToSnapshot": boolean,
                        "DBClusterIdentifier": "string",
                        "DBInstanceClass": "string",
                        "DBInstanceIdentifier": "string",
                        "DbInstancePort": number,
                        "DbInstanceStatus": "string",
                        "DbiResourceId": "string",
                        "DBName": "string",
                        "DbParameterGroups": [
                            {
                                "DbParameterGroupName": "string",
                                "ParameterApplyStatus": "string"
                            }
                        ],
                        "DbSecurityGroups": [ "string" ],
                        "DbSubnetGroup": {
                            "DbSubnetGroupArn": "string",
                            "DbSubnetGroupDescription": "string",
                            "DbSubnetGroupName": "string",
                            "SubnetGroupStatus": "string",
                            "Subnets": [
                                {
                                    "SubnetAvailabilityZone": {
                                        "Name": "string"
                                    },
                                    "SubnetIdentifier": "string",
                                    "SubnetStatus": "string"
                                }
                            ],
                            "VpcId": "string",
                        },
                        "DeletionProtection": boolean,
                        "Endpoint": {
                            "Address": "string",
                            "Port": number,
                            "HostedZoneId": "string"
                        },
                        "DomainMemberships": [
                            {
                                "Domain": "string",
                                "Fqdn": "string",
                                "IamRoleName": "string",
                                "Status": "string"
                            }
                        ],
                        "EnabledCloudwatchLogsExports": [ "string" ],
                        "Engine": "string",
                        "EngineVersion": "string",
                        "EnhancedMonitoringResourceArn": "string",
                        "IAMDatabaseAuthenticationEnabled": boolean,
                        "InstanceCreateTime": "string",
                        "Iops": number,
                        "KmsKeyId": "string",
                        "LatestRestorableTime": "string",
                        "LicenseModel": "string",
                        "ListenerEndpoint": {
                            "Address": "string",
                            "HostedZoneId": "string",
                            "Port": number
                        },
                        "MasterUsername": "admin",
                        "MaxAllocatedStorage": number.
                        "MonitoringInterval": number,
                        "MonitoringRoleArn": "string",
                        "MultiAz": boolean,
                        "OptionGroupMemberships": [
                            {
                                "OptionGroupName": "string",
                                "Status": "string"
                            }
                        ],
                        "PendingModifiedValues": {
                            "AllocatedStorage": number,
                            "BackupRetentionPeriod": number,
                            "CaCertificateIdentifier": "string",
                            "DbInstanceClass": "string",
                            "DbInstanceIdentifier": "string",
                            "DbSubnetGroupName": "string",
                            "EngineVersion": "string",
                            "Iops": number,
                            "LicenseModel": "string",
                            "MasterUserPassword": "string",
                            "MultiAZ": boolean,
                            "PendingCloudWatchLogsExports": {
                               "LogTypesToDisable": [ "string" ],
                               "LogTypesToEnable": [ "string" ]
                            },
                            "Port": number,
                            "ProcessorFeatures": [
                                {
                                    "Name": "string",
                                    "Value": "string"
                                }
                            ],
                            "StorageType": "string"
                        },
                        "PerformanceInsightsEnabled": boolean,
                        "PerformanceInsightsKmsKeyId": "string",
                        "PerformanceInsightsRetentionPeriod": number,
                        "PreferredBackupWindow": "string",
                        "PreferredMaintenanceWindow": "string",
                        "ProcessorFeatures": [
                            {
                                "Name": "string",
                                "Value": "string"
                            }
                        ],
                        "PromotionTier": number,
                        "PubliclyAccessible": boolean,
                        "ReadReplicaDBClusterIdentifiers": [ "string" ],
                        "ReadReplicaDBInstanceIdentifiers": [ "string" ],
                        "ReadReplicaSourceDBInstanceIdentifier": "string",
                        "SecondaryAvailabilityZone": "string",
                        "StatusInfos": [
                            {
                                "Message": "string"
                                "Normal": boolean,
                                "Status": "string",
                                "StatusType": "string"
                            }
                        ],
                        "StorageEncrypted": boolean,
                        "TdeCredentialArn": "string",
                        "Timezone": "string",
                        "VpcSecurityGroups": [
                            {
                                "VpcSecurityGroupId": "string",
                                "Status": "string"
                            }
                        ]
                    },
                    "AwsRdsDbSnapshot": {
                        "AllocatedStorage": integer,
                        "AvailabilityZone": "string",
                        "DbInstanceIdentifier": "string",
                        "DbiResourceId": "string",
                        "DbSnapshotIdentifier": "string",
                         Encrypted": boolean,
                        "Engine": "string",
                        "EngineVersion": "string",
                        "IamDatabaseAuthenticationEnabled": boolean,
                        "InstanceCreateTime": "string",
                        "Iops": number,
                        "KmsKeyId": "string",
                        "LicenseModel": "string",
                        "MasterUsername": "string",
                        "OptionGroupName": "string",
                        "PercentProgress": integer,
                        "Port": integer,
                        "ProcessorFeatures": [],
                        "SnapshotCreateTime": "string",
                        "SnapshotType": "string",
                        "SourceDbSnapshotIdentifier": "string",
                        "SourceRegion": "string",
                        "Status": "string",
                        "StorageType": "string",
                         TdeCredentialArn": "string",
                        "Timezone": "string",
                        "VpcId": "string"
                    },
                    "AwsS3Bucket": { 
                        "CreatedAt": "string",
                        "OwnerId": "string",
                        "OwnerName": "string"
                        "ServerSideEncryptionConfiguration": {
                            "Rules": [
                                {
                                    "ApplyServerSideEncryptionByDefault": {
                                        "KMSMasterKeyID": "string",
                                        "SSEAlgorithm": "string"
                                     }
                                }
                            ]
                        }
                    },
                    "AwsS3Object": {
                        "ContentType": "string",
                        "ETag": "string",
                        "LastModified": "string",
                        "ServerSideEncryption": "string",
                        "SSEKMSKeyId": "string",
                        "VersionId": "string"
                    },
                    "AwsSecretsManagerSecret": {
                        "Deleted": Boolean,
                        "Description": "string",
                        "KmsKeyId": "string",
                        "Name": "string",
                        "RotationEnabled": boolean,
                        "RotationLambdaArn": "string",
                        "RotationOccurredWithinFrequency": boolean,
                        "RotationRules": {
                            "AutomaticallyAfterDays": integer
                        }
                    },
                    "AwsSnsTopic": {
                        "KmsMasterKeyId": "string",
                        "Owner": "string",
                        "Subscription": {
                            "Endpoint": "string",
                            "Protocol": "string"
                        },
                        "TopicName": "string"
                    },
                    "AwsSqsQueue": {
                        "DeadLetterTargetArn": "string",
                        "KmsDataKeyReusePeriodSeconds": number,
                        "KmsMasterKeyId": "string",
                        "QueueName": "string"
                    },
                    "AwsWafWebAcl": {
                        "DefaultAction": "string",
                        "Name": "string",
                        "Rules": [
                            {
                                "Action": {
                                    "Type": "string"
                                },
                                "ExcludedRules": [
                                    {
                                        "RuleId": "string"
                                    }
                                ],
                                "OverrideAction": {
                                    "Type": "string"
                                },
                                "Priority": number,
                                "RuleId": "string",
                                "Type": "string"
                            }
                        ],
                        "WebAclId": "string"
                    },
                    "Container": { 
                        "ImageId": "string",
                        "ImageName": "string",
                        "LaunchedAt": "string",
                        "Name": "string"
                    },
                    "Other": { 
                        "string" : "string" 
                    }
                },
                "Id": "string",
                "Partition": "string",
                "Region": "string",
                "Tags": { 
                    "string" : "string" 
                },
                "Type": "string"
            }
        ],
        "SchemaVersion": "string",
        "Severity": { 
                "Label": "string",
                "Normalized": number,
                "Original": "string",
                "Product": number
        },
        "SourceUrl": "string",
        "ThreatIntelIndicators": [ 
            { 
                "Category": "string",
                "LastObservedAt": "string",
                "Source": "string",
                "SourceUrl": "string",
                "Type": "string",
                "Value": "string"
            }
        ],
        "Title": "string",
        "Types": [ "string" ],
        "UpdatedAt": "string",
        "UserDefinedFields": { 
            "string" : "string" 
		},
        "VerificationState": "string",
        "Workflow": {
            "Status": "string"
        },
        "WorkflowState": "string"
    },
    "Vulnerabilities" : [
        {
            "Cvss": [
                {
                    "BaseScore": number,
                    "BaseVector": "string",
                    "Version": "string"
                },
            ],
            "Id": "string",
            "ReferenceUrls":["string"],
            "RelatedVulnerabilities": ["string"],
            "Vendor": {
                "Name": "string",
                "Url":"string",
                "VendorCreatedAt":"string",
                "VendorSeverity":"string",
                "VendorUpdatedAt":"string"
            },
            "VulnerablePackages": [
                {
                    "Architecture": "string",
                    "Epoch": "string",
                    "Name": "string",
                    "Release": "string",
                    "Version": "string"
                }
            ]
        }
    ]
]
```

## ASFF attributes<a name="securityhub-findings-format-attributes"></a>

The following table lists the top\-level attributes and objects for the ASFF\. For objects, to see the details for the object attributes and subfields, choose the object name\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AwsAccountId`  |  Yes  | The AWS account ID that the finding applies to\. Type: String \(12 digits max\) Example: <pre>"AwsAccountId": "111111111111"</pre>  | 
|  [`Compliance`](#asff-compliance)  |  No  | Finding details related to a control\. Only returned for findings generated from a control\. Type: Object Example: <pre>"Compliance": {<br />    "RelatedRequirements": ["Req1", "Req2"],<br />    "Status": "PASSED",<br />    "StatusReasons": [<br />        {<br />            "ReasonCode": "CLOUDWATCH_ALARMS_NOT_PRESENT";<br />            "Description": "CloudWatch alarms do not exist in the account"<br />        }<br />    ]<br />}</pre>  | 
|  `Confidence`  |  No  |  A finding's confidence\. Confidence is defined as the likelihood that a finding accurately identifies the behavior or issue that it was intended to identify\. A finding provider can provide an initial value for this attribute, but cannot update it after that\. This attribute can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Type: Integer \(range 0–100\) Confidence is scored on a 0–100 basis using a ratio scale, where 0 means zero\-percent confidence and 100 means 100\-percent confidence\. However, a data exfiltration detection based on a statistical deviation of network traffic has a much lower confidence because an actual exfiltration hasn't been verified\. Example: <pre>"Confidence": 42</pre>  | 
|  `CreatedAt`  |  Yes  |  Indicates when the potential security issue captured by a finding was created\. The `CreatedAt` timestamp reflects the time when the finding record was created\. Consequently, it can differ from the `FirstObservedAt` timestamp, which reflects the time when the event or vulnerability was first observed\. This timestamp *must* be provided on the first generation of the finding and *can't* be changed upon subsequent updates to the finding\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"CreatedAt": "2017-03-22T13:22:13.933Z"</pre>  Findings are deleted 90 days after the most recent update or 90 days after the creation date if no update occurs\. To store findings for longer than 90 days, you can configure a rule in CloudWatch Events that routes findings to your Amazon S3 bucket\.  | 
|  `Criticality`  |  No  | The level of importance that is assigned to the resources that are associated with the finding\. A score of 0 means that the underlying resources have no criticality, and a score of 100 is reserved for the most critical resources\.  A finding provider can provide an initial value for this attribute, but cannot update it after that\. This attribute can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Type: Integer \(range 0–100\) Criticality is scored on a 0–100 basis, using a ratio scale that supports only full integers\. A score of 0 means that the underlying resources have no criticality, and a score of 100 is reserved for the most critical resources\. At a high level, when assessing criticality, you need to consider the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) For each resource, consider the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) You can use the following guidelines: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Criticality": 99</pre>  | 
|  `Description`  |  Yes  | A finding's description\. This field can be nonspecific boilerplate text or details that are specific to the instance of the finding\. Type: String \(1,024 characters max\) Example: <pre>"Description": "The version of openssl found on instance i-abcd1234 is known to contain a vulnerability."</pre>  | 
|  `FirstObservedAt`  |  No  |  Indicates when the potential security issue captured by a finding was first observed\. This timestamp reflects the time of when the event or vulnerability was first observed\. Consequently, it can differ from the `CreatedAt` timestamp, which reflects the time this finding record was created\.  This timestamp should be immutable between updates of the finding record, but can be updated if a more accurate timestamp is determined\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"FirstObservedAt": "2017-03-22T13:22:13.933Z"</pre>  | 
|  `GeneratorId`  |  Yes  | The identifier for the solution\-specific component \(a discrete unit of logic\) that generated a finding\. In various solutions from security findings products, this generator can be called a rule, a check, a detector, a plugin, and so on\. Type: String \(512 characters max\) or Amazon Resource Name \(ARN\) Example: <pre>"GeneratorId": "acme-vuln-9ab348"</pre>  | 
|  `Id`  |  Yes  | The product\-specific identifier for a finding\. Type: String \(512 characters max\) or ARN The finding ID must comply with the following constraints: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) These constraints are expected to hold within a findings product, but are not required to hold across findings products\. Example: <pre>"Id": "us-west-2/111111111111/98aebb2207407c87f51e89943f12b1ef"</pre>  | 
|  `LastObservedAt`  |  No  |  Indicates when the potential security issue captured by a finding was most recently observed by the security findings product\. This timestamp reflects the time of when the event or vulnerability was last or most recently observed\. Consequently, it can differ from the `UpdatedAt` timestamp, which reflects when this finding record was last or most recently updated\.  You can provide this timestamp, but it isn't required upon the first observation\. If you provide the field in this case, the timestamp should be the same as the `FirstObservedAt` timestamp\. You should update this field to reflect the last or most recently observed timestamp each time a finding is observed\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"LastObservedAt": "2017-03-23T13:22:13.933Z"</pre>  | 
|  [`Malware`](#asff-malware)  |  No  | A list of malware related to a finding\. Type: Array of up to five malware objects Example: <pre>"Malware": [<br />    {<br />        "Name": "Stringler",<br />        "Type": "COIN_MINER",<br />        "Path": "/usr/sbin/stringler",<br />        "State": "OBSERVED"<br />    }<br />]</pre>  | 
|  [`Network`](#asff-network)  |  No  | The details of network\-related information about a finding\. Type: Object Example: <pre>"Network": {<br />    "Direction": "IN",<br />    "OpenPortRange": {<br />        "Begin": 443,<br />        "End": 443<br />    },<br />    "Protocol": "TCP",<br />    "SourceIpV4": "1.2.3.4",<br />    "SourceIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",<br />    "SourcePort": "42",<br />    "SourceDomain": "example1.com",<br />    "SourceMac": "00:0d:83:b1:c0:8e",<br />    "DestinationIpV4": "2.3.4.5",<br />    "DestinationIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",<br />    "DestinationPort": "80",<br />    "DestinationDomain": "example2.com"<br />}</pre>  | 
|  [`NetworkPath`](#asff-networkpath)  |  No  |  A network path that is related to the finding\. Each entry in `NetworkPath` represents a component of the path\. Type: Array of objects  | 
|  [`Note`](#asff-note)  |  No  |  A user\-defined note that is added to a finding\. A finding provider can provide an initial note for a finding, but cannot add notes after that\. A note can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Type: Object Example: <pre>"Note": {<br />    "Text": "Don't forget to check under the mat.",<br />    "UpdatedBy": "jsmith",<br />    "UpdatedAt": "2018-08-31T00:15:09Z"<br />}</pre>  | 
|  [`PatchSummary`](#asff-patchsummary)  |  No  |  Provides a summary of patch compliance\. Type: Object  | 
|  [`Process`](#asff-process)  |  No  | The details of process\-related information about a finding\.Type: Object Example: <pre>"Process": {<br />    "Name": "syslogd",<br />    "Path": "/usr/sbin/syslogd",<br />    "Pid": 12345,<br />    "ParentPid": 56789,<br />    "LaunchedAt": "2018-09-27T22:37:31Z",<br />    "TerminatedAt": "2018-09-27T23:37:31Z"<br />}</pre>  | 
|  `ProductArn`  |  Yes  | The ARN generated by Security Hub that uniquely identifies a third\-party findings product after the product is registered with Security Hub\. Type: ARN The format of this field is `arn:partition:securityhub:region:account-id:product/company-id/product-id`\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>// Private ARN<br />    "ProductArn": "arn:aws:securityhub:us-east-1:111111111111:product/111111111111/default"<br /><br />// Public ARN<br />    "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty"<br />    "ProductArn": "arn:aws:securityhub:us-west-2:222222222222:product/generico/secure-pro"</pre>  | 
|  `ProductFields`  |  No  | A data type where security findings products can include additional solution\-specific details that aren't part of the defined AWS Security Finding Format\. Type: Map of up to 50 key\-value pairs This field should not contain redundant data and must not contain data that conflicts with AWS Security Finding Format fields\. The "`aws/`" prefix represents a reserved namespace for AWS products and services only and must not be submitted with findings from partner products\. Although not required, products should format field names as `company-id/product-id/field-name`, where the `company-id` and `product-id` match those supplied in the `ProductArn` of the finding\. Field names can include alphanumeric characters, white space, and the following symbols: \_ \. / = \+ \\ \- @ Example: <pre>"ProductFields": {<br />    "generico/secure-pro/Count": "6",<br />    "generico/secure-pro/Action.Type", "AWS_API_CALL",<br />    "API", "DeleteTrail",<br />    "Service_Name": "cloudtrail.amazonaws.com",<br />    "aws/inspector/AssessmentTemplateName": "My daily CVE assessment",<br />    "aws/inspector/AssessmentTargetName": "My prod env",<br />    "aws/inspector/RulesPackageName": "Common Vulnerabilities and Exposures"<br />}</pre>  | 
|  `RecordState`  |  No  | The record state of a finding\.  By default, when initially generated by a service, findings are considered `ACTIVE`\. The `ARCHIVED` state indicates that a finding should be hidden from view\. Archived findings are not immediately deleted\. You can search, review, and report against them\. Finding providers can update the record state\. Security Hub also automatically archives control\-based findings if the associated resource is deleted, the resource does not exist, or the control is disabled\. Type: Enum Valid values: `ACTIVE` \| `ARCHIVED` Example: <pre>"RecordState": "ACTIVE"</pre>  | 
|  [`RelatedFindings`](#asff-relatedfindings)  |  No  | A list of related findings\.  A finding provider can provide an initial list of related findings, but cannot update the list after that\. The list of related findings can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Type: Array of up to 10 `RelatedFinding` objects Example: <pre>"RelatedFindings": [<br />    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", <br />      "Id": "123e4567-e89b-12d3-a456-426655440000" },<br />    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", <br />      "Id": "AcmeNerfHerder-111111111111-x189dx7824" }<br />]</pre>  | 
|  [`Remediation`](#asff-remediation)  |  No  | The remediation options for a finding\. Type: Object Example: <pre>"Remediation": {<br />    "Recommendation": {<br />        "Text": "Run sudo yum update and cross your fingers and toes.",<br />        "Url": "http://myfp.com/recommendations/dangerous_things_and_how_to_fix_them.html"<br />    }<br />}</pre>  | 
|  [`Resources`](#asff-resources)  |  Yes  | A set of resource data types that describe the resources that the finding refers to\. Type: Array of up to 32 resource objects Example: <pre>"Resources": [<br />  {<br />    "Type": "AwsEc2Instance",<br />    "Id": "i-cafebabe",<br />    "Partition": "aws",<br />    "Region": "us-west-2",<br />    "Tags": {<br />      "billingCode": "Lotus-1-2-3",<br />      "needsPatching": "true"<br />    },<br />    "Details": {<br />      "AwsEc2Instance": {<br />        "Type": "i3.xlarge",<br />        "ImageId": "ami-abcd1234",<br />        "IpV4Addresses": [ "54.194.252.215", "192.168.1.88" ],<br />        "IpV6Addresses": [ "2001:db8:1234:1a2b::123" ],<br />        "KeyName": "my_keypair",<br />        "IamInstanceProfileArn": "arn:aws:iam::111111111111:instance-profile/AdminRole",<br />        "VpcId": "vpc-11112222",<br />        "SubnetId": "subnet-56f5f633",<br />        "LaunchedAt": "2018-05-08T16:46:19.000Z"<br />      }  <br />    }<br />  }<br />]</pre>  | 
|  `SchemaVersion`  |  Yes  | The schema version that a finding is formatted for\. The value of this field must be one of the officially published versions identified by AWS\. In the current release, the AWS Security Finding Format schema version is `2018-10-08`\.  Type: String \(10 characters max, conforms to `YYYY-MM-DD`\) Example: <pre>"SchemaVersion": "2018-10-08"</pre>  | 
|  [`Severity`](#asff-severity)  |  Yes  | A finding's severity\. The finding must have either `Label` or `Normalized` populated\. `Label` is the preferred attribute\. If neither attribute is populated, then the finding is invalid\. A finding provider can provide initial severity information for a finding, but cannot update it after that\. The severity information can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.Type: Object Example: <pre>"Severity": {<br />    "Label": "CRITICAL",<br />    "Original": 8.3<br />}</pre>  | 
|  `SourceUrl`  |  No  | A URL that links to a page about the current finding in the finding product\. Type: URL | 
|  [`ThreatIntelIndicators`](#asff-threatintelindicators)  |  No  | Threat intelligence details that are related to a finding\. Type: Array of up to five threat intelligence indicator objects Example: <pre>"ThreatIntelIndicators": [<br />  {<br />    "Type": "IPV4_ADDRESS",<br />    "Value": "8.8.8.8",<br />    "Category": "BACKDOOR",<br />    "LastObservedAt": "2018-09-27T23:37:31Z",<br />    "Source": "Threat Intel Weekly",<br />    "SourceUrl": "http://threatintelweekly.org/backdoors/8888"<br />  }<br />]</pre>  | 
|  `Title`  |  Yes  | A finding's title\. This field can contain nonspecific boilerplate text or details that are specific to this instance of the finding\.Type: String \(256 characters max\) | 
|  `Types`  |  Yes  | One or more finding types in the format of `namespace/category/classifier` that classify a finding\. Type: Array of 50 strings max [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Namespaces are required for all finding types, but categories and classifiers are optional\. If you specify a classifier, you must also specify a category\. The '`/`' character is reserved and must *not* be used in a category or classifier\. Escaping the '`/`' character is not supported\. Example: <pre>"Types": [<br />    "Software and Configuration Checks/Vulnerabilities/CVE"<br />]</pre>  | 
|  `UpdatedAt`  |  Yes  |  Indicates when the finding provider last updated the finding record\. This timestamp reflects the time when the finding record was last or most recently updated\. Consequently, it can differ from the `LastObservedAt` timestamp, which reflects when the event or vulnerability was last or most recently observed\. When you update the finding record, you must update this timestamp to the current timestamp\. Upon creation of a finding record, the `CreatedAt` and `UpdatedAt` timestamps must be the same timestamp\. After an update to the finding record, the value of this field must be greater than all of the previous values that it contained\. Note that `UpdatedAt` is not updated by changes from [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It is only updated by [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html)\. Findings are deleted 90 days after the most recent update or 90 days after the creation date if no update occurs\. To store findings for longer than 90 days, you can configure a rule in CloudWatch Events that routes findings to your Amazon S3 bucket\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 
|  `UserDefinedFields`  |  No  | A list of name\-value string pairs that are associated with the finding\. These are custom, user\-defined fields that are added to a finding\. These fields can be generated automatically via your specific configuration\. Findings products must *not* use this field for data that the product generates\. Instead, findings products can use the `ProductFields` field for data that doesn't map to any standard AWS Security Finding Format field\. These fields can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.Type: map of up to 50 key\-value pairs Format: The key name can only contain letters, numbers, and the following special characters: \-\_=\+@\./: Example: <pre>"UserDefinedFields": {<br />    "reviewedByCio": "true",<br />    "comeBackToLater": "Check this again on Monday"<br />}</pre>  | 
|  `VerificationState`  |  No  | The veracity of a finding\. Findings products can provide the value of `UNKNOWN` for this field\. A findings product should provide this value if there is a meaningful analog in the findings product's system\. This field is typically populated by a user determination or action after they investigate a finding\. A finding provider can provide an initial value for this attribute, but cannot update it after that\. This attribute can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\.Type: Enum Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 
|  [`Vulnerabilities`](#asff-vulnerabilities)  |  No  |  A list of vulnerabilities that apply to the finding\. Type: Array of objects  | 
|  [`Workflow`](#asff-workflow)  |  No  |  Provides information about the status of the investigation into a finding\. The workflow status is not intended for finding providers\. The workflow status can only be updated using `BatchUpdateFindings`\. Customers can also update it from the console\. See [Setting the workflow status for findings](finding-workflow-status.md)\. Type: Object Example: <pre>Workflow: {<br />    "Status": "NEW"<br />}</pre>  | 
|  `WorkflowState` \(deprecated\)  |  No  |  This field is being deprecated in favor of the `Status` field of the `Workflow` object\.The workflow state of a finding\. Findings products can provide the value of `NEW` for this field\. A findings product can provide a value for this field if there is a meaningful analog in the findings product's system\. Type: Enum Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"WorkflowState": "NEW"</pre>  | 

### Compliance<a name="asff-compliance"></a>

Contains finding details related to a control\. Only returned for findings that are generated as the result of a check that is run on a control\.

**Example**

```
"Compliance": {
    "RelatedRequirements": ["Req1", "Req2"],
    "Status": "FAILED",
    "StatusReasons": [
        {
            "ReasonCode": "CLOUDWATCH_ALARMS_NOT_PRESENT",
            "Description": "CloudWatch alarms do not exist in the account"
        }
    ]
}
```

The `Compliance` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `RelatedRequirements`  |  No  |  For a Security Hub control, the industry or regulatory framework requirements that are related to the control\. The check for that control is aligned with those requirements\. You can provide up to 32 related requirements\. To identify a requirement, use its identifier\. Type: Array of strings  | 
|  `Status`  | No | The result of a security check\. Type: Enum Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Status": "PASSED"</pre>  | 
|  [`StatusReasons`](#asff-compliance-statusreasons)  |  No  |  For findings generated from controls, a list of reasons behind the value of `Compliance.Status`\. For the list of status codes and their meanings, see [Control\-related information in the ASFF](securityhub-standards-results.md#securityhub-standards-results-asff)\. Type: String Example: <pre>"StatusReasons": [<br />    {<br /><br />        "Description": "CloudWatch alarms do not exist in the account",<br />        "ReasonCode": "CW_ALARMS_NOT_PRESENT"<br />    }<br />]<br /></pre>  | 

#### StatusReasons<a name="asff-compliance-statusreasons"></a>

For findings generated from controls, a list of reasons for the value of `Compliance.Status`\.

```
"StatusReasons": [
    {
        "Description": "CloudWatch alarms do not exist in the account",
        "ReasonCode": "CW_ALARMS_NOT_PRESENT"
    }
]
```

Each reason in the `StatusReasons` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Description`  |  No  |  The corresponding description for the reason\. Type: String  | 
|  `ReasonCode`  |  Yes  |  A code that represents a reason for the current control status\. Type: String For the list of available status codes and their meanings, see [Results of security checks](securityhub-standards-results.md)\.  | 

### Malware<a name="asff-malware"></a>

The `Malware` object provides a list of malware related to a finding\. It is an array that can contain up to five malware objects\.

**Example**

```
"Malware": [
    {
        "Name": "Stringler",
        "Type": "COIN_MINER",
        "Path": "/usr/sbin/stringler",
        "State": "OBSERVED"
    }
]
```

Each malware object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Name`  |  Yes  | The name of the malware that was observed\. Type: String \(64 characters max\) Example: <pre>"Name": "Stringler"</pre>  | 
|  `Path`  |  No  | The filesystem path of the malware that was observed\.  Type: String \(512 characters max\) Example: <pre>"Path": "/usr/sbin/stringler"</pre>  | 
|  `State`  |  No  | The state of the malware that was observed\. Type: Enum Valid values: `OBSERVED` \| `REMOVAL_FAILED` \| `REMOVED` Example: <pre>"State": "OBSERVED"</pre>  | 
|  `Type`  |  No  | The type of the malware that was observed\. Type: Enum Valid values: `ADWARE` \| `BLENDED_THREAT` \| `BOTNET_AGENT` \| `COIN_MINER` \| `EXPLOIT_KIT` \| `KEYLOGGER` \| `MACRO` \| `POTENTIALLY_UNWANTED` \| `SPYWARE` \| `RANSOMWARE` \| `REMOTE_ACCESS` \| `ROOTKIT` \| `TROJAN` \| `VIRUS` \| `WORM` Example: <pre>"Type": "COIN_MINER"</pre>  | 

### Network<a name="asff-network"></a>

The details of network\-related information about a finding\.

Type: Object

**Example**

```
"Network": {
    "Direction": "IN",
    "OpenPortRange": {
        "Begin": 443,
        "End": 443
    },
    "Protocol": "TCP",
    "SourceIpV4": "1.2.3.4",
    "SourceIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",
    "SourcePort": "42",
    "SourceDomain": "example1.com",
    "SourceMac": "00:0d:83:b1:c0:8e",
    "DestinationIpV4": "2.3.4.5",
    "DestinationIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",
    "DestinationPort": "80",
    "DestinationDomain": "example2.com"
}
```

The `Network` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DestinationDomain`  |  No  | The destination domain of network\-related information about a finding\.Type: String \(128 characters max\) Example: <pre>"DestinationDomain": "there.com"</pre>  | 
|  `DestinationIpV4`  |  No  | The destination IPv4 address of network\-related information about a finding\.Type: IPv4 Example: <pre>"DestinationIpV4": "2.3.4.5"</pre>  | 
|  `DestinationIpV6`  |  No  | The destination IPv6 address of network\-related information about a finding\. Type: IPv6 Example: <pre>"DestinationIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C"</pre>  | 
|  `DestinationPort`  |  No  | The destination port of network\-related information about a finding\.Type: Number \(range of 0–65535\) Example: <pre>"DestinationPort": "80"</pre>  | 
|  `Direction`  |  No  | The direction of network traffic that is associated with a finding\. Type: Enum Valid values: `IN` \| `OUT` Example: <pre>"Direction": "IN"</pre>  | 
|  [`OpenPortRange`](#asff-network-openportrange)  |   |  The range of open ports that is present in the network\. Type: Object  | 
|  `Protocol`  |  No  | The protocol of network\-related information about a finding\. Type: String \(16 characters max\) The name should be the [IANA registered name](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml) for the associated port except in the case where the finding product can determine a more accurate protocol\. Example: <pre>"Protocol": "TCP"</pre>  | 
|  `SourceDomain`  |  No  | The source domain of network\-related information about a finding\.  Type: String \(128 characters max\) Example: <pre>"SourceDomain": "here.com"</pre>  | 
|  `SourceIpV4`  |  No  | The source IPv4 address of network\-related information about a finding\. Type: IPv4 Example: <pre>"SourceIpV4": "1.2.3.4"</pre>  | 
|  `SourceIpV6`  |  No  | The source IPv6 address of network\-related information about a finding\.Type: IPv6 Example: <pre>"SourceIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C"</pre>  | 
|  `SourceMac`  |  No  | The source media access control \(MAC\) address of network\-related information about a finding\.Type: String \(must match `MM:MM:MM:SS:SS:SS`\) Example: <pre>"SourceMac": "00:0d:83:b1:c0:8e"</pre>  | 
|  `SourcePort`  |  No  | The source port of network\-related information about a finding\. Type: Number \(range of 0–65535\) Example: <pre>"SourcePort": "80"</pre>  | 

#### OpenPortRange<a name="asff-network-openportrange"></a>

Provides the beginning and end ports of the open port range\.

`OpenPortRange` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Begin`  |  No  |  The first port in the port range\. Type: Integer  | 
|  End  |  No  |  The last port in the port range\. Type: Integer  | 

### NetworkPath<a name="asff-networkpath"></a>

The `NetworkPath` object provides information about a network path that is relevant to a finding\. Each entry under `NetworkPath` represents a component of that path\.

**Example**

```
"NetworkPath" : [
    {
        "ComponentId": "abc-01a234bc56d8901ee",
        "ComponentType": "AWS::EC2::InternetGateway",
        "Egress": {
            "Destination": {
                "Address": [ "192.0.2.0/24" ],
                "PortRanges": [
                    {
                        "Begin": 443,
                        "End": 443
                    }
                ]
            },
            "Protocol": "TCP",
            "Source": {
                Address": ["203.0.113.0/24"]
            }
        },
        "Ingress": {
            "Destination": {
                "Address": [ "198.51.100.0/24" ],
                "PortRanges": [
                    {
                        "Begin": 443,
                        "End": 443
                    }
                 ]
            },
            "Protocol": "TCP",
            "Source": {
                "Address": [ "203.0.113.0/24" ]
            }
        }
     }
]
```

Each component of the network path can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `ComponentId`  |  Yes  |  The identifier of a component in the network path\. Type: String  | 
|  `ComponentType`  |  Yes  |  The type of component\. Type: String  | 
|  [`Egress`](#asff-networkpath-egress)  |  No  |  Information about the component that comes after the current component in the network path\. Type: Object  | 
|  [`Ingress`](#asff-networkpath-ingress)  |  No  |  Information about the component that comes before the current component in the network path\. Type: Object  | 

#### Egress<a name="asff-networkpath-egress"></a>

The `Egress` object contains information about the component that comes after the current component in the network path\. It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`Destination`](#asff-networkpath-egress-ingress-destination)  |  No  |  Information about the destination of the component\. Type: Object  | 
|  `Protocol`  |  No  |  The protocol used for the component\. Type: String  | 
|  [`Source`](#asff-networkpath-egress-ingress-source)  |  No  |  Information about the origin of the component\. Type: Object  | 

#### Ingress<a name="asff-networkpath-ingress"></a>

The `Ingress` object contains information about the previous component in the network path\. It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`Destination`](#asff-networkpath-egress-ingress-destination)  |  No  |  Information about the destination for the previous component\. Type: Object  | 
|  `Protocol`  |  No  |  The protocol used by the previous component\. Type: String  | 
|  [`Source`](#asff-networkpath-egress-ingress-source)  |  No  |  Information about the origin of the previous component\. Type: Object  | 

#### Destination<a name="asff-networkpath-egress-ingress-destination"></a>

The `Destination` object in `Egress` or `Ingress` contains the destination information for the previous or next component\. It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Address`  |  No  |  IP addresses of the previous or next component\. Type: Array of strings  | 
|  `PortRanges`  |  No  |  List of open port ranges for the destination of the previous or next component\. Type: Array of objects  | 
|  `PortRanges.Begin`  |  No  |  For an open port range, the beginning of the range\. Type: Integer  | 
|  `PortRanges.End`  |  No  |  For an open port range, the end of the range\. Type: Number  | 

#### Source<a name="asff-networkpath-egress-ingress-source"></a>

The `Source` object under `Egress` or `Ingress` contains information about the origin of the previous or next component\. It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Address`  |  No  |  IP addresses for the origin of the previous or next component\. Type: Array of strings  | 
|  `PortRanges`  |  No  |  List of open port ranges for the origin of the previous or next component\. Type: Array of objects  | 
|  `PortRanges.Begin`  |  No  |  For an open port range, the beginning of the range\. Type: Integer  | 
|  `PortRanges.End`  |  No  |  For an open port range, the end of the range\. Type: Number  | 

### Note<a name="asff-note"></a>

The `Note` object adds a user\-defined note to the finding\.

A finding provider can provide an initial note for a finding, but cannot add notes after that\. A note can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

**Example**

```
"Note": {
    "Text": "Don't forget to check under the mat.",
    "UpdatedBy": "jsmith",
    "UpdatedAt": "2018-08-31T00:15:09Z"
}
```

The `Note` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Text`  |  Yes  | The text of a finding note\.Type: String \(512 characters max\)  Example: <pre>"Text": "Example text."</pre>  | 
|  `UpdatedAt`  |  Yes  | Indicates when the note was updated\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"UpdatedAt": "2018-08-31T00:15:09Z"</pre>  | 
|  `UpdatedBy`  |  Yes  | The principal that created a note\.Type: String \(512 characters max\) or ARN Example: <pre>"UpdatedBy": "jsmith"</pre>  | 

### PatchSummary<a name="asff-patchsummary"></a>

The `PatchSummary` object provides an overview of the patch compliance status for an instance against a selected compliance standard\.

**Example**

```
"PatchSummary" : {
    "Id" : "pb-123456789098"
    "InstalledCount" : "100",
    "MissingCount" : "100",
    "FailedCount" : "0",
    "InstalledOtherCount" : "1023",
    "InstalledRejectedCount" : "0",
    "InstalledPendingReboot" : "0",
    "OperationStartTime" : "2018-09-27T23:37:31Z",
    "OperationEndTime" : "2018-09-27T23:39:31Z",
    "RebootOption" : "RebootIfNeeded",
    "Operation" : "Install"
}
```

The `PatchSummary` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `FailedCount`  |  No  |  The number of patches from the compliance standard with installation failures\. Type: Number Minimum value: 0 Maximum value: 100,000  | 
|  `Id`  |  Yes  |  The identifier of the compliance standard that was used to determine the patch compliance status\. Type: String Minimum length: 20 Maximum length: 128  | 
|  `InstalledCount`  |  No  |  The number of patches from the compliance standard that were installed successfully\. Type: Number Minimum value: 0 Maximum value: 100,000  | 
|  `InstalledOtherCount`  |  No  |  The number of installed patches that are not part of the compliance standard\. Type: Number Minimum value: 0 Maximum value: 100,000  | 
|  `InstalledPendingReboot`  |  No  |  The number of patches that were applied but that require the instance to be rebooted in order to be marked as installed\. Type: Number Minimum value: 0 Maximum value: 100,000  | 
|  `InstalledRejectedCount`  |  No  |  The number of patches that are installed but are also on a list of patches that the customer rejected\. Type: Number Minimum value: 0 Maximum value: 100,000  | 
|  `MissingCount`  |  No  |  The number of patches that are part of the compliance standard but are not installed\. The count includes patches with installation failures\. Type: Number Minimum value: 0 Maximum value: 100,000  | 
|  `Operation`  |  No  |  The type of patch operation that was performed\. For Patch Manager, the values are `SCAN` and `INSTALL`\. Type: String Maximum length: 256  | 
|  OperationEndTime  |  No  |  Indicates when the operation was completed\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"OperationEndTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `OperationStartTime`  |  No  |  Indicates when the operation started\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"OperationStartTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `RebootOption`  |  No  |  The reboot option specified for the instance\. Type: String Maximum length: 256 Valid values: `NoReboot` \| `RebootIfNeeded`\.   | 

### Process<a name="asff-process"></a>

The `Process` object provides process\-related details about the finding\.

**Example**

```
"Process": {
    "Name": "syslogd",
    "Path": "/usr/sbin/syslogd",
    "Pid": 12345,
    "ParentPid": 56789,
    "LaunchedAt": "2018-09-27T22:37:31Z",
    "TerminatedAt": "2018-09-27T23:37:31Z"
}
```

The `Process` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `LaunchedAt`  |  No  | Indicates when the process was launched\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"LaunchedAt": "2018-09-27T22:37:31Z"</pre>  | 
|  `Name`  |  No  | The name of the process\.Type: String \(64 characters max\) Example: <pre>"Name": "syslogd"</pre>  | 
|  `ParentPid`  |  No  | The parent process ID\.Type: Number Example: <pre>"ParentPid": 56789</pre>  | 
|  `Path`  |  No  | The path to the process executable\. Type: String \(512 characters max\) Example: <pre>"Path": "/usr/sbin/syslogd"</pre>  | 
|  `Pid`  |  No  | The process ID\. Type: Number Example: <pre>"Pid": 12345</pre>  | 
|  `TerminatedAt`  |  No  | Indicates when the process was terminated\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"TerminatedAt": "2018-09-27T23:37:31Z"</pre>  | 

### RelatedFindings<a name="asff-relatedfindings"></a>

The `RelatedFindings` object provides a list of findings that are related to the current finding\.

A finding provider can provide an initial list of related findings, but cannot update it after that\. `RelatedFindings` can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

**Example**

```
"RelatedFindings": [
    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", 
      "Id": "123e4567-e89b-12d3-a456-426655440000" },
    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", 
      "Id": "AcmeNerfHerder-111111111111-x189dx7824" }
]
```

Each related finding object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Id`  |  Yes  | The product\-generated identifier for a related finding\. Type: String \(512 characters max\) or ARN Example: <pre>"Id": "123e4567-e89b-12d3-a456-426655440000"</pre>  | 
|  `ProductArn`  |  Yes  | The ARN of the product that generated a related finding\. Type: ARN Example: <pre>"ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty"</pre>  | 

### Remediation<a name="asff-remediation"></a>

The `Remediation` object provides information about recommended remediation steps to address the finding\.

**Example**

```
"Remediation": {
    "Recommendation": {
        "Text": "Run sudo yum update and cross your fingers and toes.",
        "Url": "http://myfp.com/recommendations/dangerous_things_and_how_to_fix_them.html"
    }
}
```

The `Remediation` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`Recommendation`](#asff-remediation-recommendation)  |  No  | A recommendation on how to remediate the issue identified within a finding\. The `Recommendation` field is meant to facilitate manual instructions or details to resolve a finding\. If the recommendation object is present, then either the `Text` or `Url` field must be present and populated\. Both fields can be present and populated\. Type: Object Example: <pre>"Recommendation": {<br />    "Text": "Example text.",<br />    "Url": "http://myfp.com/recommendations/dangerous_things_and_how_to_fix_them.html"<br />}</pre>  | 

#### Recommendation<a name="asff-remediation-recommendation"></a>

The `Recommendation` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Text`  |  No  |  A free\-form string that is the recommendation of what to do about the finding when presented to a user\. This field can contain nonspecific boilerplate text or details that are specific to this instance of the finding\. Type: String \(512 characters max\) Example: <pre>"Text": "Example text."</pre>  | 
|  `Url`  |  No  |  A URL to link to general remediation information for the finding type of a finding\. This URL must not require credentials to access\. It must be accessible from the public internet and must not expect any context or session\. Type: URL Example: <pre>"Url": "http://myfp.com/recommendations/example_domain.html"</pre>  | 

### Resources<a name="asff-resources"></a>

The `Resources` object provides information about the resources involved in a finding\.

Type: Array of up to 32 resource objects

**Example**

```
"Resources": [
  {
    "Type": "AwsEc2Instance",
    "Id": "i-cafebabe",
    "Partition": "aws",
    "Region": "us-west-2",
    "Tags": {
      "billingCode": "Lotus-1-2-3",
      "needsPatching": "true"
    },
    "Details": {
      "AwsEc2Instance": {
        "Type": "i3.xlarge",
        "ImageId": "ami-abcd1234",
        "IpV4Addresses": [ "54.194.252.215", "192.168.1.88" ],
        "IpV6Addresses": [ "2001:db8:1234:1a2b::123" ],
        "KeyName": "my_keypair",
        "IamInstanceProfileArn": "arn:aws:iam::111111111111:instance-profile/AdminRole",
        "VpcId": "vpc-11112222",
        "SubnetId": "subnet-56f5f633",
        "LaunchedAt": "2018-05-08T16:46:19.000Z"
      }  
    }
  }
]
```

Each resource object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
| Partition | Description | 
| --- | --- | 
|  `Details`  |  No  |  This field provides additional details about a single resource using the appropriate subfields\. Each resource must be provided in a separate resource object in the `Resources` field\. Security Hub provides a set of available subfields for its supported resource types\. These subfields correspond to values of the resource `Type`\. Use the provided types and subfields whenever possible\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) For example, if the resource is an S3 bucket, then set the resource `Type` to `AwsS3Bucket`, and provide the resource details in the `AwsS3Bucket` subfield\. The [`Other`](#asff-resourcedetails-other) subfield allows you to provide custom fields and values\. You use the `Other` subfield in the following cases\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Type: Object Example: <pre>"Details": {<br />  "AwsEc2Instance": {<br />    "Type": "i3.xlarge",<br />    "ImageId": "ami-abcd1234",<br />    "IpV4Addresses": [ "54.194.252.215", "192.168.1.88" ],<br />    "IpV6Addresses": [ "2001:db8:1234:1a2b::123" ],<br />    "KeyName": "my_keypair",<br />    "IamInstanceProfileArn": "arn:aws:iam::111111111111:instance-profile/AdminRole",<br />    "VpcId": "vpc-11112222",<br />    "SubnetId": "subnet-56f5f633",<br />    "LaunchedAt": "2018-05-08T16:46:19.000Z"<br />  },<br />  "AwsS3Bucket": {<br />    "OwnerId": "da4d66eac431652a4d44d490a00500bded52c97d235b7b4752f9f688566fe6de",<br />    "OwnerName": "acmes3bucketowner"<br />  },<br />  "Other": [<br />    { "Key": "LightPen", "Value": "blinky" },<br />    { "Key": "SerialNo", "Value": "1234abcd" }<br />  ]<br />}</pre>  | 
|  `Id`  |  Yes  | The canonical identifier for the given resource type\. For AWS resources that are identified by ARNs, this must be the ARN\. For all other AWS resource types that lack ARNs, this must be the identifier as defined by the AWS service that created the resource\. For non AWS resources, this should be a unique identifier that is associated with the resource\.Type: String \(512 characters max\) or ARN Example: <pre>"Id": "arn:aws:s3:::example-bucket"</pre>  | 
|  `Partition`  |  No  | The canonical AWS partition name that the Region is assigned to\.  Type: Enum Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Partition": "aws"</pre>  | 
|  `Region`  |  No  | The canonical AWS external Region name where this resource is located\. Type: String \(16 characters max\) Example: <pre>"Region": "us-west-2"</pre>  | 
|  `Tags`  |  No  | A list of AWS tags that are associated with a resource at the time the finding was processed\. Include the `Tags` attribute only for resources that have an associated tag\. If a resource has no associated tag, don't include a `Tags` attribute in the finding\. Type: Map of up to 50 tags \(values are limited to 256 characters max\) The following basic restrictions apply to tags: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Tags": {<br />    "billingCode": "Lotus-1-2-3",<br />    "needsPatching": "true"<br />}</pre>  | 
|  `Type`  |  Yes  |  The type of the resource that you are providing details for\. Whenever possible, use one of the provided resource types, such as `AwsEc2Instance` or `AwsS3Bucket`\. If the resource type does not match any of the provided resource types, then set the resource `Type` to `Other`, and use the `Other` details subfield to populate the details\. Type: String \(256 characters max\) Supported values are as follows\. If a type has a corresponding subfield, then to view the details for the subfield, choose the type name\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Type": "AwsS3Bucket"</pre>  | 
| aws | Commercial | 
| aws\-cn | China | 
| aws\-us\-gov | AWS GovCloud \(US\) | 

#### AwsAutoScalingAutoScalingGroup<a name="asff-resourcedetails-awsautoscalingautoscalinggroup"></a>

The `AwsAutoScalingAutoScalingGroup` object provides details about an automatic scaling group\.

**Example**

```
"AwsAutoScalingAutoScalingGroup": {
        "CreatedTime": "2017-10-17T14:47:11Z",
        "HealthCheckGracePeriod": 300,
        "HealthCheckType": "EC2",
        "LaunchConfigurationName": "mylaunchconf",
        "LoadBalancerNames": []
}
```

The `AwsAutoScalingAutoScalingGroup` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CreatedTime`  |  No  |  Indicates when the automatic scaling group was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 
|  `HealthCheckGracePeriod`  |  No  |  The amount of time, in seconds, that Amazon EC2 Auto Scaling waits before it checks the health status of an EC2 instance that has come into service\. Type: Integer  | 
|  `HealthCheckType`  |  No  |  The service to use for the health checks\. Type: String \(32 characters max\) Valid values: `EC2` \| `ELB`  | 
|  `LaunchConfigurationName`  |  No  |  The name of the launch configuration\. Type: String \(32 characters max\)  | 
|  `LoadBalancerNames`  |  No  |  The list of load balancers that are associated with the group\. Type: Array of strings Each load balancer name is limited to 255 characters\.  | 

#### AwsCloudFrontDistribution<a name="asff-resourcedetails-awscloudfrontdistribution"></a>

The `AwsCloudFrontDistribution` object provides details about a distribution configuration\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DomainName`  |  No  | The domain name corresponding to the distribution\.Type: String | 
|  `Etag`  |  No  | The entity tag is a hash of the object\.Type: String | 
|  `LastModifiedTime`  |  No  | Indicates when the distribution was last modified\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. | 
|  [`Logging`](#asff-resourcedetails-awscloudfrontdistribution-logging)  |  No  | A complex type that controls whether access logs are written for the distribution\.Type: Object | 
|  [`Origins`](#asff-resourcedetails-awscloudfrontdistribution-origins)  |  No  | A complex type that contains information about origins and origin groups for this distribution\.Type: String | 
|  `Status`  |  No  | Indicates the current status of the distribution\.Type: String | 
|  `WebAclId`  |  No  | A unique identifier that specifies the AWS WAF web ACL, if any, to associate with this distribution\.Type: String | 

##### Logging<a name="asff-resourcedetails-awscloudfrontdistribution-logging"></a>

The `Logging` object provides information about the logging for the distribution\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Bucket`  |  No  | The S3 bucket to store the access logs in\.Type: String | 
|  `Enabled`  |  No  | With this field, you can enable or disable the selected distribution\.Type: Boolean | 
|  `IncludeCookies`  |  No  | Specifies whether you want CloudFront to include cookies in access logs\.Type: Boolean | 
|  `Prefix`  |  No  | An optional string that you want CloudFront to prefix to the access log file names for this distribution\.Type: String | 

##### Origins<a name="asff-resourcedetails-awscloudfrontdistribution-origins"></a>

The `Origins` object contains information about origins and origin groups for this distribution\.

It can contain the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Items`  |  No  |  A complex type that contains origins or origin groups for this distribution\. Type: Array of objects  | 

Each item can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DomainName`  |  No  |  Amazon S3 origins: The DNS name of the S3 bucket from which you want CloudFront to get objects for this origin\. Type: String  | 
|  `Id`  |  No  |  A unique identifier for the origin or origin group\. Type: String  | 
|  `OriginPath`  |  No  |  An optional element that causes CloudFront to request your content from a directory in your S3 bucket or your custom origin\. Type: String  | 

#### AwsCodeBuildProject<a name="asff-resourcedetails-awscodebuildproject"></a>

The `AwsCodeBuildProject` object provides information about an AWS CodeBuild project\.

**Example**

```
"AwsCodeBuildProject": {
    "EncryptionKey": "my-symm-key",
    "Environment": {
        "Type": "LINUX_CONTAINER",
        "Certificate": "myX509",
        "ImagePullCredentialsType": "CODEBUILD",
        "RegistryCredential": {
            "Credential": "my_dockerhub_secret",
            "CredentialProvider": "SECRETS_MANAGER"
        }
    },
    "Name": "my-cd-project",
    "Source": {
        "Type": "CODECOMMIT",
        "Location": "https://git-codecommit.us-east-2.amazonaws.com/v1/repos/MyDemoRepo",
        "GitCloneDepth": 1
    },
    "ServiceRole": "arn:aws:iam:myrole",
    "VpcConfig": {
        "VpcId": "vpc-1234456",
        "Subnets": ["sub-12344566"],
        "SecurityGroupIds": ["sg-123456789012"]
    }
}
```

The `AwsCodeBuildProject` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `EncryptionKey`  |  No  |  The AWS KMS customer master key \(CMK\) to be used for encrypting the build output artifacts\.  You can use a cross\-account KMS key to encrypt the build output artifacts if your service role has permission to that key\.  You can specify either the ARN of the CMK or, if available, the CMK alias \(using the format *alias*/*alias\-name*\)\. Type: String Length constraints: Minimum length of 1  | 
|  [`Environment`](#asff-resourcedetails-awscodebuildproject-environment)  |  No  |  Information about the build environment for this build project\. Type: Object  | 
|  `Name`  |  No  |  The name of the build project\. Type: String Length constraints: Minimum length of 2\. Maximum length of 255\. Pattern: \[A\-Za\-z0\-9\]\[A\-Za\-z0\-9\\\-\_\]\{1,254\}  | 
|  `ServiceRole`  |  No  |  The ARN of the IAM role that enables CodeBuild to interact with dependent AWS services on behalf of the AWS account\. Type: String Length constraints: Minimum length of 1  | 
|  [`Source`](#asff-resourcedetails-awscodebuildproject-source)  |  No  |  Information about the build input source code for this build project\. Type: Object  | 
|  [`VpcConfig`](#asff-resourcedetails-awscodebuildproject-vpcconfig)  |  No  |  Information about the VPC configuration that CodeBuild accesses\. Type: Object  | 

##### Environment<a name="asff-resourcedetails-awscodebuildproject-environment"></a>

The `Environment` object provides information about the build environment for the build project\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Certificate`  |  No  |  The certificate to use with this build project\. Type: String  | 
|  `ImagePullCredentialsType`  |  No  |  The type of credentials CodeBuild uses to pull images in your build\. There are two valid values: `CODEBUILD` specifies that CodeBuild uses its own credentials\. This requires that you modify your ECR repository policy to trust the CodeBuild service principal\. `SERVICE_ROLE` specifies that CodeBuild uses your build project's service role\. When you use a cross\-account or private registry image, you must use `SERVICE_ROLE` credentials\. When you use a CodeBuild curated image, you must use `CODEBUILD` credentials\. Type: String Valid values: `CODEBUILD` \| `SERVICE_ROLE`  | 
|  `RegistryCredential`  |  No  |  The credentials for access to a private registry\. Type: Object  | 
|  `Type`  |  Yes  |  The type of build environment to use for related builds\. Type: String Valid values: `WINDOWS_CONTAINER` \| `LINUX_CONTAINER` \| `LINUX_GPU_CONTAINER` \| `ARM_CONTAINER`  | 

Each registry credential in the `RegistryCredentials` object has the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Credential`  |  Yes  |  The ARN or name of credentials created using AWS Secrets Manager\.  The credential can use the name of the credentials only if they exist in your current AWS Region\.  Type: String Length constraints: Minimum length of 1  | 
|  `CredentialProvider`  |  Yes  |  The service that created the credentials to access a private Docker registry\. The valid value,` SECRETS_MANAGER`, is for Secrets Manager\. Type: String Valid values: `SECRETS_MANAGER`  | 

##### Source<a name="asff-resourcedetails-awscodebuildproject-source"></a>

The `Source` object provides information about the build input source code for this build project\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `GitCloneDepth`  |  No  |  Information about the Git clone depth for the build project\. Type: Integer Valid range: Minimum value of 0  | 
|  `Location`  |  No  |  Information about the location of the source code to be built\. Type: String Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 
|  `Type`  |  Yes  |  The type of repository that contains the source code to be built\. Type: String Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 

##### VpcConfig<a name="asff-resourcedetails-awscodebuildproject-vpcconfig"></a>

The `VpcConfig` object provides information about the VPC configuration that CodeBuild accesses\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `SecurityGroupIds`  |  No  |  A list of one or more security group IDs in your Amazon VPC\. Type: Array of strings Array members: Maximum number of 5 items Length constraints: Minimum length of 1  | 
|  `Subnets`  |  No  |  A list of one or more subnet IDs in your Amazon VPC\. Type: Array of strings Array members: Maximum number of 16 items Length constraints: Minimum length of 1  | 
|  VpcId  |  No  |  The ID of the VPC\. Type: String Length constraints: Minimum length of 1  | 

#### AwsDynamoDbTable<a name="asff-resourcedetails-awsdynamodbtable"></a>

The `AwsDynamoDbTable` object provides details about a DynamoDB table\.

**Example**

```
"AwsDynamoDbTable": {
    "AttributeDefinitions": [   
        {        
            "AttributeName": "attribute1",
            "AttributeType": "value 1"
        },
        {
            "AttributeName": "attribute2",
            "AttributeType": "value 2"
        },
        {
            "AttributeName": "attribute3",
            "AttributeType": "value 3"
        }
    ],
    "BillingModeSummary": {
        "BillingMode": "PAY_PER_REQUEST",
        "LastUpdateToPayPerRequestDateTime": "2019-12-03T15:23:10.323Z"
    },
    "CreationDateTime": "2019-12-03T15:23:10.248Z",
    "GlobalSecondaryIndexes": [
        {
            "Backfilling": false,
            "IndexArn": "arn:aws:dynamodb:us-west-2:111122223333:table/exampleTable/index/exampleIndex",                
            "IndexName": "standardsControlArnIndex",
            "IndexSizeBytes": 1862513,
            "IndexStatus": "ACTIVE",
            "ItemCount": 20,
            "KeySchema": [
                {
                    "AttributeName": "City",
                    "KeyType": "HASH"
                },     
                {
                    "AttributeName": "Date",
                    "KeyType": "RANGE"
                }
            ],      
            "Projection": {
                "NonKeyAttributes": ["predictorName"],
                "ProjectionType": "ALL"
            },     
            "ProvisionedThroughput": {
                "LastIncreaseDateTime": "2019-03-14T13:21:00.399Z",
                "LastDecreaseDateTime": "2019-03-14T12:47:35.193Z",
                "NumberOfDecreasesToday": 0,
                "ReadCapacityUnits": 100,
                "WriteCapacityUnits": 50
            },
        }
   ],
   "GlobalTableVersion": "V1",
   "ItemCount": 2705,
   "KeySchema": [
        {
            "AttributeName": "zipcode",
            "KeyType": "HASH"
        }
    ],
    "LatestStreamArn": "arn:aws:dynamodb:us-west-2:111122223333:table/exampleTable/stream/2019-12-03T23:23:10.248",
    "LatestStreamLabel": "2019-12-03T23:23:10.248",
    "LocalSecondaryIndexes": [
        {
            "IndexArn": "arn:aws:dynamodb:us-east-1:111122223333:table/exampleGroup/index/exampleId",
            "IndexName": "CITY_DATE_INDEX_NAME",
            "KeySchema": [
                {
                    "AttributeName": "zipcode",
                    "KeyType": "HASH"
                }
            ],
            "Projection": {
                "NonKeyAttributes": ["predictorName"],
                "ProjectionType": "ALL"
            },  
        }
    ],
    "ProvisionedThroughput": {
        "LastIncreaseDateTime": "2019-03-14T13:21:00.399Z",
        "LastDecreaseDateTime": "2019-03-14T12:47:35.193Z",
        "NumberOfDecreasesToday": 0,
        "ReadCapacityUnits": 100,
        "WriteCapacityUnits": 50
    },
    "Replicas": [
        {
            "GlobalSecondaryIndexes":[
                {
                    "IndexName": "CITY_DATE_INDEX_NAME", 
                    "ProvisionedThroughputOverride": {
                        "ReadCapacityUnits": 10
                    }
                }
            ],
            "KmsMasterKeyId" : "KmsMasterKeyId"
            "ProvisionedThroughputOverride": {
                "ReadCapacityUnits": 10
            },
            "RegionName": "regionName",
            "ReplicaStatus": "CREATING",
            "ReplicaStatusDescription": "replicaStatusDescription"
        }
    ],
    "RestoreSummary" : {
        "SourceBackupArn": "arn:aws:dynamodb:us-west-2:111122223333:table/exampleTable/backup/backup1",
        "SourceTableArn": "arn:aws:dynamodb:us-west-2:111122223333:table/exampleTable",
        "RestoreDateTime": "2020-06-22T17:40:12.322Z",
        "RestoreInProgress": true
    },
    "SseDescription": {
        "InaccessibleEncryptionDateTime": "2018-01-26T23:50:05.000Z",
        "Status": "ENABLED",
        "SseType": "KMS",
        "KmsMasterKeyArn": "arn:aws:kms:us-east-1:111122223333:key/key1"
    },
    "StreamSpecification" : {
        "StreamEnabled": true,
        "StreamViewType": "NEW_IMAGE"
    },
    "TableId": "example-table-id-1",
    "TableName": "example-table",
    "TableSizeBytes": 1862513,
    "TableStatus": "ACTIVE"
}
```

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`AttributeDefinitions`](#asff-resourcedetails-awsdynamodbtable-attributedefinitions)  |  No  |  A list of attribute definitions for the table\. Type: Array of objects\.  | 
|  [`BillingModeSummary`](#asff-resourcedetails-awsdynamodbtable-billingmodesummary)  |  No  |  Information about the billing for read/write capacity on the table\. Type: Object  | 
|  `CreationDateTime`  |  No  |  Indicates when the table was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"CreationDateTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  [`GlobalSecondaryIndexes`](#asff-resourcedetails-awsdynamodbtable-globalsecondaryindexes)  |  No  |  List of global secondary indexes for the table\. Type: Array of objects  | 
|  `GlobalTableVersion`  |  No  |  The version of global tables being used\. Type: String  | 
|  `ItemCount`  |  No  |  The number of items in the table\. Type: Number  | 
|  [`KeySchema`](#asff-resourcedetails-awsdynamodbtable-keyschema)  |  No  |  The primary key structure for the table\. Type: Array of objects  | 
|  `LatestStreamArn`  |  No  |  The ARN of the latest stream for the table\. Type: String  | 
|  `LatestStreamLabel`  |  No  |  The label of the latest stream\. The label is not a unique identifier\. Type: String  | 
|  [`LocalSecondaryIndexes`](#asff-resourcedetails-awsdynamodbtable-localsecondaryindexes)  |  No  |  The list of local secondary indexes for the table\. Type: Array of objects  | 
|  [`ProvisionedThroughput`](#asff-resourcedetails-awsdynamodbtable-provisionedthroughput)  |  No  |  Information about the provisioned throughput for the table\. Type: Object  | 
|  [`Replicas`](#asff-resourcedetails-awsdynamodbtable-replicas)  |  No  |  The list of replicas of this table\. Type: Array of objects  | 
|  [`RestoreSummary`](#asff-resourcedetails-awsdynamodbtable-restoresummary)  |  No  |  Information about the restore for the table\. Type: Object  | 
|  [`SseDescription`](#asff-resourcedetails-awsdynamodbtable-ssedescription)  |  No  |  Information about the server\-side encryption for the table\. Type: Object  | 
|  [`StreamSpecification`](#asff-resourcedetails-awsdynamodbtable-streamspecification)  |  No  |  The current DynamoDB Streams configuration for the table\. Type: Object  | 
|  `TableId`  |  No  |  The identifier of the table\. Type: String  | 
|  `TableName`  |  No  |  The name of the table\. Type: String Minimum length: 3 Maximum length: 255  | 
|  `TableSizeBytes`  |  No  |  The total size of the table in bytes\. Type: Integer  | 
|  `TableStatus`  |  No  |  The current status of the table\. Type: String Valid values: `CREATING` \| `UPDATING` \| `DELETING` \| `ACTIVE` \| `INACCESSIBLE_ENCRYPTION_CREDENTIALS` \| `ARCHIVING` \| `ARCHIVED`  | 

##### AttributeDefinitions<a name="asff-resourcedetails-awsdynamodbtable-attributedefinitions"></a>

The `AttributeDefinitions` object contains a list of attribute definitions for the table\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AttributeName`  |  No  |  The name of the attribute\. Type: String  | 
|  `AttributeType`  |  No  |  The type of the attribute\. Type: String  | 

##### BillingModeSummary<a name="asff-resourcedetails-awsdynamodbtable-billingmodesummary"></a>

The `BillingModeSummary` object provides information about the billing for read/write capacity on the table\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `BillingMode`  |  No  |  The method used to charge for read and write throughput and to manage capacity\. Type: String Valid values: `PROVISIONED` \| `PAY_PER_REQUEST`  | 
|  `LastUpdateToPayPerRequestDateTime`  |  No  |  If the billing mode is `PAY_PER_REQUEST`, indicates when the billing mode was set to that value\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"LastUpdateToPayPerRequestDateTime": "2020-06-22T17:40:12.322Z"</pre>  | 

##### GlobalSecondaryIndexes<a name="asff-resourcedetails-awsdynamodbtable-globalsecondaryindexes"></a>

The `GlobalSecondaryIndexes` object contains a list of global secondary indexes for the table\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Backfilling`  |  No  |  Whether the index is currently backfilling\. Type: Boolean  | 
|  `IndexArn`  |  No  |  The ARN of the index\. Type: String  | 
|  `IndexName`  |  No  |  The name of the index\. Type: String  | 
|  `IndexSizeBytes`  |  No  |  The total size in bytes of the index\. Type: Number  | 
|  `IndexStatus`  |  No  |  The current status of the index\. Type: String Valid values: `CREATING` \| `UPDATING` \| `DELETING` \| `ACTIVE`   | 
|  `ItemCount`  |  No  |  The number of items in the index\. Type: Number  | 
|  [`KeySchema`](#asff-resourcedetails-awsdynamodbtable-keyschema)  |  No  |  The key schema for the index\. Type: Array of objects  | 
|  [`Projection`](#asff-resourcedetails-awsdynamodbtable-projection)  |  No  |  Attributes that are copied from the table into an index\. Type: Object  | 
|  [`ProvisionedThroughput`](#asff-resourcedetails-awsdynamodbtable-provisionedthroughput)  |  No  |  Information about the provisioned throughput settings for the indexes\. Type: Object  | 

##### KeySchema<a name="asff-resourcedetails-awsdynamodbtable-keyschema"></a>

The `KeySchema` object contains the key schema for the table, a global secondary index, or a local secondary index\.

Each component of the key schema can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AttributeName`  |  No  |  The name of the attribute\. Type: String\.  | 
|  `KeyType`  |  No  |  The type of key used for the attribute\. Type: String Valid values: `HASH` \| `RANGE`  | 

##### LocalSecondaryIndexes<a name="asff-resourcedetails-awsdynamodbtable-localsecondaryindexes"></a>

`LocalSecondaryIndexes` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `IndexArn`  |  No  |  The ARN of the index\. Type: String  | 
|  `IndexName`  |  No  |  The name of the index\. Type: String Minimum length: 3 Maximum length: 255  | 
|  [`KeySchema`](#asff-resourcedetails-awsdynamodbtable-keyschema)  |  No  |  The complete key schema for the index\. Type: Array of objects  | 
|  [`Projection`](#asff-resourcedetails-awsdynamodbtable-projection)  |  No  |  Attributes that are copied from the table into the index\. These are in addition to the primary key attributes and index key attributes, which are automatically projected\. Type: Object  | 

##### Projection \(for global and local secondary indexes\)<a name="asff-resourcedetails-awsdynamodbtable-projection"></a>

For global and local secondary indexes, the `Projection` object identifies the attributes that are copied from the table into the index\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `NonKeyAttributes`  |  No  |  The nonkey attributes that are projected into the index\. For each attribute, provide the attribute name\. Type: Array of strings Maximum number of items: 20 Minimum length per attribute: 1 Maximum length per attribute: 225  | 
|  `ProjectionType`  |  No  |  The types of attributes that are projected into the index\. Type: String Valid values: `ALL` \| `KEYS_ONLY` \| `INCLUDE`  | 

##### ProvisionedThroughput<a name="asff-resourcedetails-awsdynamodbtable-provisionedthroughput"></a>

The `ProvisionedThroughput` object contains information about the provisioned throughput for the table or for a global secondary index\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `LastDecreaseDateTime`  |  No  |  Indicates when the provisioned throughput was last decreased\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"LastDecreaseDateTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `LastIncreaseDateTime`  |  No  |  Indicates when the provisioned throughput was last increased\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"LastIncreaseDateTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `NumberOfDecreasesToday`  |  No  |  The number of times during the current UTC calendar day that the provisioned throughput was decreased\. Type: Number  | 
|  `ReadCapacityUnits`  |  No  |  The maximum number of strongly consistent reads consumed per second before DynamoDB returns a `ThrottlingException`\.  Type: Number  | 
|  `WriteCapacityUnits`  |  No  |  The maximum number of writes consumed per second before DynamoDB returns a `ThrottlingException`\. Type: Number  | 

##### Replicas<a name="asff-resourcedetails-awsdynamodbtable-replicas"></a>

The `Replicas` object contains the list of replicas of this table\.

Each replica can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `GlobalSecondaryIndexes`  | No |  List of global secondary indexes for the replica\. Type: Array of objects  | 
| GlobalSecondaryIndexes\.IndexName  |  No  |  The name of the index\. Type: String  | 
|  `GlobalSecondaryIndexes.ProvisionedThroughputOverride`  |  No  |  Replica\-specific configuration for the provisioned throughput for the index\. Type: Object  | 
|  `KmsMasterKeyID`  |  No  |  The identifier of the AWS KMS customer master key \(CMK\) that will be used for AWS KMS encryption for the replica\. Type: String  | 
|  `ProvisionedThroughputOverride`  |  No  |  Replica\-specific configuration for the provisioned throughput\. Type: Object  | 
|  `RegionName`  |  No  |  The name of the Region where the replica is located\. Type: String  | 
|  `ReplicaStatus`  |  No  |  The current status of the replica\. Type: String Valid values: `CREATING` \| `CREATION_FAILED` \| `UPDATING` \| `DELETING` \| `ACTIVE`  | 
|  `ReplicaStatusDescription`  |  No  |  Detailed information about the replica status\. Type: String  | 

The `ProvisionedThroughputOverride` object provides replica\-specific configuration for the provisioned throughput for the table or the global secondary indexes\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `ReadCapacityUnits`  |  No  |  The read capacity units for the replica\. Type: Number Minimum value: 1  | 

##### RestoreSummary<a name="asff-resourcedetails-awsdynamodbtable-restoresummary"></a>

The `RestoreSummary` object provides information about the restore for the table\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `RestoreDateTime`  |  No  |  Indicates the point in time that the table was restored to\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"RestoreDateTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `RestoreInProgress`  |  No  |  Whether a restore is currently in progress\. Type: Boolean  | 
|  `SourceBackupArn`  |  No  |  The ARN of the source backup from which the table was restored\. Type: String  | 
|  `SourceTableArn`  |  No  |  The ARN of the source table for the backup\. Type: String  | 

##### SseDescription<a name="asff-resourcedetails-awsdynamodbtable-ssedescription"></a>

The `SseDescription` object provides information about the server\-side encryption for the table\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `InaccessibleEncryptionDateTime`  |  No  |  If the key is inaccessible, the date and time when DynamoDB detected that the key was inaccessible\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"InaccessibleEncryptionDateTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `KmsMasterKeyArn`  |  No  |  The ARN of the AWS KMS customer master key \(CMK\) that is used for the AWS KMS encryption\. Type: String  | 
|  `SseType`  |  No  |  The type of server\-side encryption\. Type: String Valid values: `KMS`  | 
|  `Status`  |  No  |  The status of the server\-side encryption\. Type: String Valid values: `ENABLED` \| `UPDATING`  | 

##### StreamSpecification<a name="asff-resourcedetails-awsdynamodbtable-streamspecification"></a>

The `StreamSpecification` object contains the current DynamoDB Streams configuration for the table\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `StreamEnabled`  |  No  |  Indicates whether DynamoDB Streams is enabled on the table\. Type: Boolean  | 
|  `StreamViewType`  |  No  |  Determines the information that is written to the table\. Type: String Valid values: `NEW_IMAGE` \| `OLD_IMAGE` \| `NEW_AND_OLD_IMAGES` \| `KEYS_ONLY`  | 

#### AwsEc2Eip<a name="asff-resourcedetails-awsec2eip"></a>

The `AwsEc2Eip` object provides information about an Elastic IP address\.

**Example**

```
"AwsEc2Eip": {
    "InstanceId": "instance1",
    "PublicIp": "192.0.2.04",
    "AllocationId": "eipalloc-example-id-1",
    "AssociationId": "eipassoc-example-id-1",
    "Domain": "vpc",
    "PublicIpv4Pool": "anycompany",
    "NetworkBorderGroup": "eu-central-1",
    "NetworkInterfaceId": "eni-example-id-1",
    "NetworkInterfaceOwnerId": "777788889999",
    "PrivateIpAddress": "192.0.2.03"
}
```

The `AwsEc2Eip` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AllocationId`  |  No  |  The identifier that AWS assigns to represent the allocation of the Elastic IP address for use with Amazon VPC\. Type: String  | 
|  `AssociationId`  |  No  |  The identifier that represents the association of the Elastic IP address with an EC2 instance\. Type: String  | 
|  `Domain`  |  No  |  The domain in which to allocate the address\. If the address is for use with EC2 instances in a VPC, then `Domain` is `vpc`\. Otherwise, `Domain` is `standard`\.  Type: String Valid values: `standard` \| `vpc`  | 
|  `InstanceId`  |  No  |  The identifier of the EC2 instance\. Type: String  | 
|  `NetworkBorderGroup`  |  No  |  The name of the location from which the Elastic IP address is advertised\. Type: String  | 
|  `NetworkInterfaceId`  |  No  |  The identifier of the network interface\. Type: String  | 
|  `NetworkInterfaceOwnerId`  |  No  |  The AWS account ID of the owner of the network interface\. Type: String Format: Must be a 12\-digit number\.  | 
|  `PrivateIpAddress`  |  No  |  The private IP address that is associated with the Elastic IP address\. Type: IPv4  | 
|  `PublicIp`  |  No  |  A public IP address that is associated with the EC2 instance\. Type: IPv4  | 
|  `PublicIpv4Pool`  |  No  |  The identifier of an IP address pool\. This parameter allows Amazon EC2 to select an IP address from the address pool\. Type: String  | 

#### AwsEc2Instance<a name="asff-resourcedetails-awsec2instance"></a>

The details of an Amazon EC2 instance\.

Type: Object

The `AwsEc2Instance` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `IamInstanceProfileArn`  |  No  | The IAM profile ARN of the instance\. Type: String \(conforms to the AWS ARN format\) | 
|  `ImageId`  |  No  | The Amazon Machine Image \(AMI\) ID of the instance\.Type: String \(64 characters max\) | 
|  `IpV4Addresses`  |  No  | The IPv4 addresses that are associated with the instance\.Type: Array of up to 10 IPv4 addresses | 
|  `IpV6Addresses`  |  No  | The IPv6 addresses that are associated with the instance\.Type: Array of up to 10 IPv6 addresses | 
|  `KeyName`  |  No  | The key name that is associated with the instance\.Type: String \(128 characters max\) | 
|  `LaunchedAt`  |  No  | Indicates when the instance was launched\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. | 
|  `SubnetId`  |  No  | The identifier of the subnet where the instance was launched\. Type: String \(32 characters max\) | 
|  `Type`  |  No  | The instance type of the instance\. This must be a valid [EC2 instance type](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html)\. Type: String \(16 characters max\) | 
|  `VpcId`  |  No  | The identifier of the VPC where the instance was launched\. Type: String \(32 characters max\) | 

#### AwsEc2NetworkInterface<a name="asff-resourcedetails-awsec2networkinterface"></a>

The `AwsEc2NetworkInterface` object provides information about an Amazon EC2 network interface\.

**Example**

```
"AwsEc2NetworkInterface": {
    "Attachment": {
        "AttachTime": "2019-01-01T03:03:21Z",
        "AttachmentId": "eni-attach-43348162",
        "DeleteOnTermination": true,
        "DeviceIndex": 123,
        "InstanceId": "i-1234567890abcdef0",
        "InstanceOwnerId": "123456789012",
        "Status": 'ATTACHED'
    },
    "SecurityGroups": [
        {
            "GroupName": "my-security-group",
            "GroupId": "sg-903004f8"
        },
    ],
    "NetworkInterfaceId": 'eni-686ea200',
    "SourceDestCheck": false
}
```

The `AwsEc2NetworkInterface` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`Attachment`](#asff-resourcedetails-awsec2networkinterface-attachment)  |  No  |  Information about the network interface attachment\. Type: Object  | 
|  `NetworkInterfaceId`  |  No  |  The ID of the network interface\. Type: String  | 
|  [`SecurityGroups`](#asff-resourcedetails-awsec2networkinterface-securitygroups)  |  No  |  Security groups for the network interface\. Type: Array of group objects  | 
|  `SourceDestCheck`  |  No  |  Indicates whether traffic to or from the instance is validated\. Type: Boolean  | 

##### Attachment<a name="asff-resourcedetails-awsec2networkinterface-attachment"></a>

The `Attachment` object provides information about the network interface attachment\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AttachmentId`  |  No  |  The identifier of the network interface attachment Type: String  | 
|  `AttachTime`  |  No  |  Indicates when the attachment initiated\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 
|  `DeleteOnTermination`  |  No  |  Indicates whether the network interface is deleted when the instance is terminated\. Type: Boolean  | 
|  `DeviceIndex`  |  No  |  The device index of the network interface attachment on the instance\. Type: Integer  | 
|  `InstanceId`  |  No  |  The ID of the instance\. Type: String  | 
|  `InstanceOwnerId`  |  No  |  The AWS account ID of the owner of the instance\. Type: String  | 
|  `Status`  |  No  |  The attachment state\. Type: String Valid values: `attaching` \| `attached` \| `detaching` \| `detached`  | 

##### SecurityGroups<a name="asff-resourcedetails-awsec2networkinterface-securitygroups"></a>

The `SecurityGroups` object contains the list of security groups for the network interface\.

Each security group can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `GroupId`  |  No  |  The ID of the security group\. Type: String  | 
|  GroupName  |  |  The name of the security group\. Type: String  | 

#### AwsEc2SecurityGroup<a name="asff-resourcedetails-awsec2securitygroup"></a>

The `AwsEc2SecurityGroup` object describes an Amazon EC2 security group\.

**Example**

```
"AwsEc2SecurityGroup": {
    "GroupName": "MySecurityGroup",
    "GroupId": "sg-903004f8",
    "OwnerId": "123456789012",
    "VpcId": "vpc-1a2b3c4d",
    "IpPermissions": [
        {
            "IpProtocol": "-1",
            "IpRanges": [],
            "UserIdGroupPairs": [
                {
                    "UserId": "123456789012",
                    "GroupId": "sg-903004f8"
                }
            ],
            "PrefixListIds": [
                {"PrefixListId": "pl-63a5400a"}
            ]
        },
        {
            "PrefixListIds": [],
            "FromPort": 22,
            "IpRanges": [
                {
                    "CidrIp": "203.0.113.0/24"
                }
            ],
            "ToPort": 22,
            "IpProtocol": "tcp",
            "UserIdGroupPairs": []
        }
    ]
}
```

The `AwsEc2SecurityGroup` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `GroupId`  |  No  |  The ID of the security group\. Type: String  | 
|  `GroupName`  |  No  |  The name of the security group\. Type: String  | 
|  [`IpPermissions`](#asff-resourcedetails-awsec2securitygroup-ippermission)  |  No  |  The inbound rules that are associated with the security group\. Type: Array of IP permission objects  | 
|  [`IpPermissionsEgress`](#asff-resourcedetails-awsec2securitygroup-ippermission)  |  No  |  \[VPC only\] The outbound rules that are associated with the security group\. Type: Array of IP permission objects  | 
|  `OwnerId`  |  No  |  The AWS account ID of the owner of the security group\. Type: String  | 
|  `VpcId`  |  No  |  \[VPC only\] The ID of the VPC for the security group\. Type: String  | 

##### IP permission object<a name="asff-resourcedetails-awsec2securitygroup-ippermission"></a>

The `IpPermissions` and `IpPermissionsEgress` objects both contain an array of IP permission objects\.

Each IP permission object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `FromPort`  |  No  |  The start of the port range for the TCP and UDP protocols, or an ICMP/ICMPv6 type number\. A value of `-1` indicates all ICMP/ICMPv6 types\. If you specify all ICMP/ICMPv6 types, you must specify all codes\. Type: Integer  | 
|  `IpProtocol`  |  No  |  The IP protocol name \(`tcp`, `udp`, `icmp`, `icmpv6`\) or number \(see the [protocol numbers list](http://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml)\)\. \[VPC only\] Use `-1` to specify all protocols\. When authorizing security group rules, specifying `-1` or a protocol number other than `tcp`, `udp`, `icmp`, or `icmpv6` allows traffic on all ports, regardless of any port range you specify\. For `tcp`, `udp`, and `icmp`, you must specify a port range\. For `icmpv6`, the port range is optional\. If you omit the port range, traffic for all types and codes is allowed\. Type: String  | 
|  `IpRanges`  |  No  |  The ranges of IP addresses\. Type: Array of IP range objects  | 
|  `PrefixListIds`  |  No  |  \[VPC only\] The prefix list IDs for an AWS service\. With outbound rules, this is the AWS service to access through a VPC endpoint from instances that are associated with the security group\. Type: Array of prefix list ID objects  | 
|  `ToPort`  |  No  |  The end of the port range for the TCP and UDP protocols, or an ICMP/ICMPv6 code\. A value of `-1` indicates all ICMP/ICMPv6 codes\. If you specify all ICMP/ICMPv6 types, you must specify all codes\. Type: Integer  | 
|  `UserIdGroupPairs`  |  No  |  The security group and AWS account ID pairs\. Type: Array of user ID group pair objects  | 

Each entry in the `IpRanges` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CidrIp`  |  No  |  A range of IP addresses\. You can either specify a CIDR range or a source security group, but not both\. To specify a single IPv4 address, use the /32 prefix length\. To specify a single IPv6 address, use the /128 prefix length\. Type: String  | 

Each entry in the `PrefixListIds` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `PrefixListId`  |  No  |  The ID of the prefix\. Type: String  | 

Each entry in the `UserIdGroupPairs` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  GroupId  |  No  |  The ID of the security group\. Type: String  | 
|  UserId  |  No  |  The ID of an AWS account\. For a referenced security group in another VPC, the account ID of the referenced security group is returned in the response\. If the referenced security group is deleted, this value is not returned\. \[Amazon EC2\-Classic\] Required when adding or removing rules that reference a security group in another AWS account\. Type: String  | 

#### AwsEc2Volume<a name="asff-resourcedetails-awsec2volume"></a>

The `AwsEc2Volume` object provides details about an EC2 volume\.

**Example**

```
"AwsEc2Volume": {
     "Attachments": [
        {
            "AttachTime": "2017-10-17T14:47:11Z",
            "DeleteOnTermination": true,
            "InstanceId": "i-123abc456def789g",
            "Status": "attached"
       }
      ],
      "CreateTime": "2020-02-24T15:54:30Z",
      "Encrypted": true,
      "KmsKeyId": "arn:aws:kms:us-east-1:111122223333:key/wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY",
      "Size": 80,
      "SnapshotId": "",
      "Status": "available"
}
```

The `AwsEc2Volume` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`Attachments`](#asff-resourcedetails-awsec2volume-attachments)  |  No  |  The volume attachments\. Type: Array of objects  | 
|  `CreateTime`  |  No  |  Indicates when the volume was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 
|  `Encrypted`  |  No  |  Whether the volume is encrypted\. Type: Boolean  | 
|  `KmsKeyId`  |  No  |  The ARN of the AWS KMS customer master key \(CMK\) that was used to protect the volume encryption key for the volume\. Type: String  | 
|  `Size`  |  No  |  The size of the volume, in GiBs\. Type: Integer  | 
|  `SnapshotId`  |  No  |  The snapshot from which the volume was created\. Type: String  | 
|  `Status`  |  No  |  The volume state\. Type: String Valid values: `creating` \| `available` \| `in-use` \| `deleting` \| `deleted` \| `error`  | 

##### Attachments<a name="asff-resourcedetails-awsec2volume-attachments"></a>

The `Attachments` object contains the set of attachments for the EC2 volume\. Each attachment can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AttachTime`  |  No  |  The date and time when the attachment initiated\. Type: String \(timestamp\) Format: `yyyy-MM-ddTHH:mm:ssZ`  | 
|  `DeleteOnTermination`  |  No  |  Whether the EBS volume is deleted when the EC2 instance is terminated\. Type: Boolean  | 
|  `InstanceId`  |  No  |  The identifier of the EC2 instance\. Type: String  | 
|  `Status`  |  No  |  The attachment state of the volume\. Type: String Valid values: `attaching` \| `attached` \| `detaching` \| `detached` \| `busy`  | 

#### AwsEc2Vpc<a name="asff-resourcedetails-awsec2vpc"></a>

The `AwsEc2Vpc` object provides details about an EC2 virtual private cloud \(VPC\)\.

**Example**

```
"AwsEc2Vpc": {
    "CidrBlockAssociationSet": [
        {
            "AssociationId": "vpc-cidr-assoc-0dc4c852f52abda97",
            "CidrBlock": "192.0.2.0/24",
            "CidrBlockState": "associated"
        }
    ],
    "DhcpOptionsId": "dopt-4e42ce28",
    "Ipv6CidrBlockAssociationSet": [
        {
            "AssociationId": "vpc-cidr-assoc-0dc4c852f52abda97",
            "CidrBlockState": "associated",
            "Ipv6CidrBlock": "192.0.2.0/24"
       }

    ],
    "State": "available"
}
```

The `AwsEc2Vpc` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`CidrBlockAssociationSet`](#asff-resourcedetails-awsec2vpc-cidrblockassociationset)  |  No  |  Information about the IPv4 CIDR blocks that are associated with the VPC\. Type: Array of objects  | 
|  `DhcpOptionsId`  |  No  |  The identifier of the set of Dynamic Host Configuration Protocol \(DHCP\) options that are associated with the VPC\. If the default options are associated with the VPC, then this is `default`\. Type: String \(32 characters max\)  | 
|  [`IpV6CidrBlockAssociationSet`](#asff-resourcedetails-awsec2vpc-ipv6cidrblockassociationset)  |  No  |  Information about the IPv6 CIDR blocks that are associated with the VPC\. Type: Array of objects\.  | 
|  `State`  |  No  |  The current state of the VPC\. Type: String \(32 characters max\) Valid values: `pending` \| `available`  | 

##### CidrBlockAssociationSet<a name="asff-resourcedetails-awsec2vpc-cidrblockassociationset"></a>

The `CidrBlockAssociationSet` object provides a list of IPV4 CIDR block associations\.

Each CIDR block association can contain the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AssociationId`  |  No  |  The association ID for the IPv4 CIDR block\. Type: String \(32 characters max\)  | 
|  `CidrBlock`  |  No  |  The IPv4 CIDR block\. Type: CIDR IPV4  | 
|  `CidrBlockState`  |  No  |  Information about the state of the CIDR block\. Type: String \(32 characters max\)  | 

##### IpV6CidrBlockAssociationSet<a name="asff-resourcedetails-awsec2vpc-ipv6cidrblockassociationset"></a>

The `IPV6CidrBlockAssociationSet` object provides a list of IPV6 CIDR block associations\.

Each CIDR block association can contain the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Associationid`  |  No  |  The association ID for the IPv6 CIDR block\. Type: String \(32 characters max\)  | 
|  `CidrBlockState`  |  No  |  Information about the state of the CIDR block\. Type: String \(32 characters max\)  | 
|  `IpV6CidrBlock`  |  No  |  The IPv6 CIDR block\. Type: CIDR IPV6  | 

#### AwsElasticSearchDomain<a name="asff-resourcedetails-awselasticsearchdomain"></a>

The `AwsElasticSearchDomain` object provides details about an Elasticsearch domain\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AccessPolicies`  |  No  |  IAM policy document specifying the access policies for the new Amazon ES domain\. Type: String  | 
|  [`DomainEndpointOptions`](#asff-resourcedetails-awselasticsearchdomain-domainendpointoptions)  |  No  |  Additional options for the domain endpoint\. Type: Object  | 
|  [`DomainStatus`](#asff-resourcedetails-awselasticsearchdomain-domainstatus)  |  No  |  Details about the domain status\. Type: Object  | 
|  `ElasticsearchVersion`  |  No  |  Elasticsearch version\. Type: String  | 
|  [`EncryptionAtRestOptions`](#asff-resourcedetails-awselasticsearchdomain-encryptionatrestoptions)  |  No  |  Details about the configuration for encryption at rest\. Type: Object  | 
|  [`NodeToNodeEncryptionOptions`](#asff-resourcedetails-awselasticsearchdomain-nodetonodeencryptionoptions)  |  No  |  Details about the configuration for node\-to\-node encryption\. Type: Object  | 
|  [`VPCOptions`](#asff-resourcedetails-awselasticsearchdomain-vpcoptions)  |  No  |  Information that Amazon ES derives based on `VPCOptions` for the domain\. Type: Object  | 

##### DomainEndpointOptions<a name="asff-resourcedetails-awselasticsearchdomain-domainendpointoptions"></a>

The `DomainEndpointOptions` object provides information about additional options for the domain endpoint\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `EnforceHTTPS`  |  No  |  Whether to require that all traffic to the domain arrive over HTTPS\. Type: Boolean  | 
|  `TLSSecurityPolicy`  |  No  |  The TLS security policy to apply to the HTTPS endpoint of the Elasticsearch domain\. Type: String Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 

##### DomainStatus<a name="asff-resourcedetails-awselasticsearchdomain-domainstatus"></a>

The `DomainStatus` object provides details about the domain status\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DomainId`  |  No  |  Unique identifier for an Amazon ES domain\. Type: String  | 
|  `DomainName`  |  No  |  Name of an Amazon ES domain\. Domain names are unique across all domains owned by the same account within an AWS Region\. Domain names must start with a lowercase letter and must be between 3 and 28 characters\. Valid characters are a\-z \(lowercase only\), 0\-9, and – \(hyphen\)\. Type: String  | 
|  `Endpoint`  |  No  |  Domain\-specific endpoint used to submit index, search, and data upload requests to an Amazon ES domain\. The endpoint is a service URL\. Type: String  | 
|  `Endpoints`  |  No  |  The key\-value pair that exists if the Amazon ES domain uses VPC endpoints\. Type: Map of key\-value pairs Example: <pre>"vpc": "<VPC_ENDPOINT>"</pre>  | 

##### EncryptionAtRestOptions<a name="asff-resourcedetails-awselasticsearchdomain-encryptionatrestoptions"></a>

The `EncryptionAtRestOptions` object provides details about the configuration for encryption at rest\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Enabled`  |  No  |  Whether encryption at rest is enabled\. Type: Boolean  | 
|  `KmsKeyId`  |  No  |  The AWS KMS key ID\. Takes the form `1a2a3a4-1a2a-3a4a-5a6a-1a2a3a4a5a6a`\. Type: String  | 

##### NodeToNodeEncryptionOptions<a name="asff-resourcedetails-awselasticsearchdomain-nodetonodeencryptionoptions"></a>

The `NodeToNodeEncryptionOptions` object provides details about the configuration for node\-to\-node encryption\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  Enabled  |  No  |  Whether node\-to\-node encryption is enabled\. Type: Boolean  | 

##### VpcOptions<a name="asff-resourcedetails-awselasticsearchdomain-vpcoptions"></a>

The `VpcOptions` object contains information that Amazon ES derives based on the `VPCOptions` for the domain\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AvailabilityZones`  |  No  |  The list of Availability Zones that are associated with the VPC subnets\. Type: Array of strings  | 
|  `SecurityGroupIds`  |  No  |  The list of security group IDs that are associated with the VPC endpoints for the domain Type: Array of strings\.  | 
|  `SubnetIds`  |  No  |  A list of subnet IDs that are associated with the VPC endpoints for the domain\. Type: Array of strings  | 
|  `VPCId`  |  No  |  ID for the VPC\. Type: String  | 

#### AwsElbv2LoadBalancer<a name="asff-resourcedetails-awselbv2loadbalancer"></a>

The `AwsElbv2LoadBalancer` object provides information about a load balancer\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`AvailabilityZones`](#asff-resourcedetails-awselbv2loadbalancer-availabilityzones)  |  No  | The Availability Zones for the load balancer\.Type: Object | 
|  `CanonicalHostedZoneId`  |  No  | The ID of the Amazon Route 53 hosted zone that is associated with the load balancer\.Type: String | 
|  `CreatedTime`  |  No  | Indicates when the load balancer was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. | 
|  `DNSName`  |  No  | The public DNS name of the load balancer\.Type: String | 
|  `IpAddressType`  |  No  | The type of IP addresses used by the subnets for your load balancer\. The possible values are `ipv4` \(for IPv4 addresses\) and `dualstack` \(for IPv4 and IPv6 addresses\)\.Type: String | 
|  `Scheme`  |  No  | The nodes of an Internet\-facing load balancer have public IP addresses\.Type: String | 
|  `SecurityGroups`  |  No  | The IDs of the security groups for the load balancer\.Type: Array of strings | 
|  [`State`](#asff-resourcedetails-awselbv2loadbalancer-state)  |  No  | The state of the load balancer\.Type: Object | 
|  `Type`  |  No  | The type of load balancer\.Type: String | 
|  `VpcId`  |  No  | The ID of the VPC for the load balancer\.Type: String | 

##### AvailabilityZones<a name="asff-resourcedetails-awselbv2loadbalancer-availabilityzones"></a>

Specifies the Availability Zones for the load balancer\.

Each Availability Zone can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `SubnetId`  |  No  | The ID of the subnet\.Type: String | 
|  `ZoneName`  |  No  | The name of the Availability Zone\.Type: String | 

##### State<a name="asff-resourcedetails-awselbv2loadbalancer-state"></a>

Information about the state of the load balancer\.

The `State` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Code`  |  No  | The state code\. The initial state of the load balancer is provisioning\. After the load balancer is fully set up and ready to route traffic, its state is active\. If the load balancer could not be set up, its state is failed\.Type: String | 
|  `Reason`  |  No  | A description of the state\.Type: String | 

#### AwsIamAccessKey<a name="asff-resourcedetails-awsiamaccesskey"></a>

The `AwsIamAccessKey` object contains details about an IAM access key that is related to a finding\.

The `AwsIamAccessKey` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CreatedAt`  |  No  | Indicates when the related IAM access key was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. | 
|  `PrincipalId`  |  No  | The ID of the principal that is associated with an access key\. Type: String | 
|  `PrincipalName`  |  No  | The name of the principal\.Type: String | 
|  `PrincipalType`  |  No  | The type of principal\.Type: String | 
|  `Status`  |  No  | The status of the IAM access key that is related to a finding\. Valid values are `ACTIVE` and `INACTIVE`\.Type: Enum | 

#### AwsIamPolicy<a name="asff-resourcedetails-awsiampolicy"></a>

The `AwsIamPolicy` object represents an IAM permissions policy\.

**Example**

```
"AwsIamPolicy": {
    "AttachmentCount": 1,
    "CreateDate": "2017-09-14T08:17:29.000Z",
    "DefaultVersionId": "v1",
    "Description": "Example IAM policy",
    "IsAttachable": true,
    "Path": "/",
    "PermissionsBoundaryUsageCount": 5,
    "PolicyId": "ANPAJ2UCCR6DPCEXAMPLE",
    "PolicyName": "EXAMPLE-MANAGED-POLICY",
    "PolicyVersionList": [
        {
            "VersionId": "v1",
            "IsDefaultVersion": true,
            "CreateDate": "2017-09-14T08:17:29.000Z"
        }
    ],
    "UpdateDate": "2017-09-14T08:17:29.000Z"
}
```

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AttachmentCount`  |  No  |  The number of users, groups, and roles that the policy is attached to\. Type: Number  | 
|  CreateDate  |  No  |  When the policy was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"CreateDate": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `DefaultVersionId`  |  No  |  The identifier of the default version of the policy\. Type: String  | 
|  `Description`  |  No  |  A description of the policy\. Type: String Maximum length: 1000 characters  | 
|  `IsAttachable`  |  No  |  Whether the policy can be attached to a user, group, or role\. Type: Boolean  | 
|  `Path`  |  No  |  The path to the policy\. Type: String Minimum length: 1 Maximum length: 512 For more information about paths, see [IAM Identifiers]() in the *IAM User Guide*\.  | 
|  `PermissionsBoundaryUsageCount`  |  No  |  The number of users and roles that use the policy to set the permissions boundary\. Type: Number  | 
|  `PolicyId`  |  No  |  The unique identifier of the policy\. Type: String Minimum length: 16 Maximum length: 128  | 
|  `PolicyName`  |  No  |  The name of the policy\. Type: String Minimum length: 1 Maximum length: 128  | 
|  [`PolicyVersionList`](#asff-resourcedetails-awsiampolicy-policyversionlist)  |  No  |  List of versions of the policy\. Type: Array of objects  | 
|  `UpdateDate`  |  No  |  When the policy was most recently updated\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"UpdateDate": "2020-06-22T17:40:12.322Z"</pre>  | 

##### PolicyVersionList<a name="asff-resourcedetails-awsiampolicy-policyversionlist"></a>

The `PolicyVersionList` object contains a list of versions of the IAM policy\.

Each version can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CreateDate`  |  No  |  Indicates when the version was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"CreateDate": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `IsDefaultVersion`  |  No  |  Whether the version is the default version\. Type: Boolean  | 
|  `VersionId`  |  No  |  The identifier of the policy version\. Type: String  | 

#### AwsIamRole<a name="asff-resourcedetails-awsiamrole"></a>

The `AwsIamRole` object contains information about an IAM role, including all of the role's policies\.

The `AwsIamRole` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AssumeRolePolicyDocument`  |  No  | The trust policy that grants permission to assume the role\.Type: String | 
|  `CreateDate`  |  No  | Indicates when the role was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. | 
|  `RoleId`  |  No  | The stable and unique string identifying the role\.Type: String | 
|  `RoleName`  |  No  | The friendly name that identifies the role\.Type: String | 
|  `MaxSessionDuration`  |  No  | The maximum session duration \(in seconds\) that you want to set for the specified role\.Type: Integer | 
|  `Path`  |  No  | The path to the role\.Type: String | 

#### AwsIamUser<a name="asff-resourcedetails-awsiamuser"></a>

The `AwsIamUser` object provides information about an IAM user\.

**Example**

```
"AwsIamUser": {
    "AttachedManagedPolicies": [
        {
            "PolicyName": "ExamplePolicy",
            "PolicyArn": "arn:aws:iam::aws:policy/ExampleAccess"
        }
    ],
    "CreateDate": "2018-01-26T23:50:05.000Z",
    "GroupList": [],
    "Path": "/",
    "PermissionsBoundary" : {
        "PermissionsBoundaryArn" : "arn:aws:iam::aws:policy/AdministratorAccess",
        "PermissionsBoundaryType" : "PermissionsBoundaryPolicy"
    },
    "UserId": "AIDACKCEVSQ6C2EXAMPLE",
    "UserName": "ExampleUser",
    "UserPolicyList": [
        {
            "PolicyName": "InstancePolicy"
        }
    ]
}
```

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`AttachedManagedPolicies`](#asff-resourcedetails-awsiamuser-attachedmanagedpolicies)  |  No  |  A list of the managed policies that are attached to the user\. Type: Array of objects  | 
|  `CreateDate`  |  No  |  Indicates when the user was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"CreateDate": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `GroupList`  |  No  |  A list of IAM groups that the user belongs to\. Type: Array of strings Minimum length: 1 Maximum length: 128  | 
|  `Path`  |  No  |  The path to the user\. Type: String Minimum length: 1 Maximum length: 512  | 
|  [`PermissionsBoundary`](#asff-resourcedetails-awsiamuser-permissionsboundary)  |  No  |  The permissions boundary for the user\. Type: Object  | 
|  `UserId`  |  No  |  The unique identifier for the user\. Type: String Minimum length: 16 Maximum length: 128  | 
|  `UserName`  |  No  |  The name of the user\. Type: String Minimum length: 1 Maximum length: 64  | 
|  [`UserPolicyList`](#asff-resourcedetails-awsiamuser-userpolicylist)  |  No  |  The list of inline policies that are embedded in the user\. Type: Array of objects  | 

##### AttachedManagedPolicies<a name="asff-resourcedetails-awsiamuser-attachedmanagedpolicies"></a>

The `AttachedManagedPolicies` object contains the list of managed policies that are attached to the IAM user\.

Each policy can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `PolicyArn`  |  No  |  The ARN of the policy\. Type: String  | 
|  `PolicyName`  |  No  |  The name of the policy\. Type: String  | 

##### PermissionsBoundary<a name="asff-resourcedetails-awsiamuser-permissionsboundary"></a>

The `PermissionsBoundary` object contains information about the policy used to set the permissions boundary for the user\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `PermissionsBoundaryArn`  |  No  |  The ARN of the policy used to set the permissions boundary for the user\. Type: String Minimum length: 20 Maximum length: 2,048  | 
|  `PermissionsBoundaryType`  |  No  |  The usage type for the permissions boundary\. Type: String The value must be `PermissionsBoundaryPolicy`\.  | 

##### UserPolicyList<a name="asff-resourcedetails-awsiamuser-userpolicylist"></a>

The `UserPolicyList` object contains the list of inline policies that are embedded in the user\.

Each policy can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `PolicyName`  |  No  |  The name of the policy\. Type: String Minimum length: 1 Maximum length: 128  | 

#### AwsKmsKey<a name="asff-resourcedetails-awskmskey"></a>

The `AwsKmsKey` object provides details about an AWS KMS customer master key \(CMK\)\.

The `AwsKmsKey` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AWSAccountId`  |  No  |  The AWS account identifier of the account that owns the CMK\. Type: String  | 
|  `CreationDate`  |  No  |  Indicates when the CMK was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 
|  `Description`  |  No  |  A description of the key\. Type: String  | 
|  `KeyId`  |  Yes  |  The globally unique identifier for the CMK\. Type: String The minimum length is 1\. The maximum length is 2048\.  | 
|  `KeyManager`  |  No  |  The manager of the CMK\. CMKs in an AWS account are either customer managed or AWS managed\. Type: String Valid values: `AWS` \| `CUSTOMER`\.  | 
|  `KeyState`  |  No  |  The state of the CMK\. Type: String Valid values: `Enabled` \| `Disabled` \| `PendingDeletion` \| `PendingImport` \| `Unavailable`  | 
|  `Origin`  |  No  |  The source of the CMK's key material\. When this value is `AWS_KMS`, AWS KMS created the key material\. When this value is `EXTERNAL`, either the key material was imported from your existing key management infrastructure, or the CMK lacks key material\. When this value is `AWS_CLOUDHSM`, the key material was created in the AWS CloudHSM cluster that is associated with a custom key store\. Type: String Valid values: `AWS_KMS` \| `EXTERNAL` \| `AWS_CLOUDHSM`  | 

#### AwsLambdaFunction<a name="asff-resourcedetails-awslambdafunction"></a>

The `AwsLambdaFunction` object provides details about a Lambda function's configuration\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`Code`](#asff-resourcedetails-awslambdafunction-code)  |  No  | An `AwsLambdaFunctionCode` object\.Type: Object | 
|  `CodeSha256`  |  No  | The SHA256 hash of the function's deployment package\.Type: String | 
|  [`DeadLetterConfig`](#asff-resourcedetails-awslambdafunction-deadletterconfig)  |  No  | The function's dead letter queue\.Type: Object | 
|  [`Environment`](#asff-resourcedetails-awslambdafunction-environment)  |  No  | A function's environment variable settings\.Type: Object | 
|  `FunctionName`  |  No  | The name of the function\.Type: String | 
|  `Handler`  |  No  | The function that Lambda calls to begin running your function\.Type: String | 
|  `KmsKeyArn`  |  No  | The AWS KMS key that's used to encrypt the function's environment variables\. This key is only returned if you've configured a customer managed CMK\.Type: String | 
|  `LastModified`  |  No  | The date and time that the function was last updated, in ISO\-8601 format \(YYYY\-MM\-DDThh:mm:ss\.sTZD\)\.Type: String | 
|  [`Layers`](#asff-resourcedetails-awslambdafunction-layers)  |  No  | The function's layers\.Type: Object | 
|  `MasterArn`  |  No  | For Lambda@Edge functions, the ARN of the master function\.Type: String | 
|  `MemorySize`  |  No  | The memory that is allocated to the function\.Type: Integer | 
|  `RevisionId`  |  No  | The latest updated revision of the function or alias\.Type: String | 
|  `Role`  |  No  | The function's execution role\.Type: String | 
|  `Runtime`  |  No  | The runtime environment for the Lambda function\.Type: String | 
|  `Timeout`  |  No  | The amount of time that Lambda allows a function to run before stopping it\.Type: Integer | 
|  [`TracingConfig`](#asff-resourcedetails-awslambdafunction-tracingconfig)  |  No  | The function's AWS X\-Ray tracing configuration\.Type: Object | 
|  `Version`  |  No  | The version of the Lambda function\.Type: String | 
|  [`VpcConfig`](#asff-resourcedetails-awslambdafunction-vpcconfig)  |  No  | The function's networking configuration\.Type: Object | 

##### Code<a name="asff-resourcedetails-awslambdafunction-code"></a>

An `AwsLambdaFunctionCode` object\.

The `Code` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `S3Bucket`  |  No  | An S3 bucket in the same AWS Region as your function\. The bucket can be in a different AWS account\.Type: String | 
|  `S3Key`  |  No  | The Amazon S3 key of the deployment package\.Type: String | 
|  `S3ObjectVersion`  |  No  | For versioned objects, the version of the deployment package object to use\.Type: String | 
|  `ZipFile`  |  No  | The base64\-encoded contents of the deployment package\. AWS SDK and AWS CLI clients handle the encoding for you\.Type: String | 

##### DeadLetterConfig<a name="asff-resourcedetails-awslambdafunction-deadletterconfig"></a>

Contains information about the Lambda function's dead letter queue\.

The `DeadLetterConfig` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `TargetArn`  |  No  | The Amazon Resource Name \(ARN\) of the Amazon SQS queue or Amazon SNS topic containing the dead letter queue\.Type: String | 

##### Environment<a name="asff-resourcedetails-awslambdafunction-environment"></a>

Contains the Lambda function's environment variable settings\.

The `Environment` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Variables`  |  No  | Environment variable key\-value pairs\.Type: String to string map | 
|  `Error`  |  No  | Error messages for environment variables that couldn't be applied\.Type: Object | 

The `Error` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `ErrorCode`  |  No  |  The error code\. Type: String  | 
|  `Message`  |  No  |  The error message\. Type: String  | 

##### Layers<a name="asff-resourcedetails-awslambdafunction-layers"></a>

The Lambda function's layers\.

Each layer object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Arn`  |  No  | The ARN of the function layer\.Type: String | 
|  `CodeSize`  |  No  | The size of the layer archive in bytes\.Type: Integer | 

##### TracingConfig<a name="asff-resourcedetails-awslambdafunction-tracingconfig"></a>

Contains the function's AWS X\-Ray tracing configuration\.

The `TracingConfig` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Mode`  |  No  | The tracing mode\.Type: String | 

##### VpcConfig<a name="asff-resourcedetails-awslambdafunction-vpcconfig"></a>

Contains the Lambda function's networking configuration\.

The `VpcConfig` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `SecurityGroupIds`  |  No  |  A list of VPC security groups IDs\. Type: Array of strings  | 
|  `SubnetIds`  |  No  |  A list of VPC subnet IDs\. Type: Array of strings  | 

#### AwsLambdaLayerVersion<a name="asff-resourcedetails-awslambdalayerversion"></a>

The `AwsLambdaLayerVersion` object provides details about a Lambda layer version\.

**Example**

```
"AwsLambdaLayerVersion": {
    "Version": 2,
    "CompatibleRuntimes": [
        "java8"
    ],
    "CreatedDate": "2019-10-09T22:02:00.274+0000"
}
```

The `AwsLambdaLayerVersion` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CompatibleRuntimes`  |  No  |  The layer's compatible runtimes\. Type: Array of strings Maximum number of items: 5 Valid values: `nodejs10.x` \| `nodejs12.x` \| `java8` \| `java11` \| `python2.7` \| `python3.6` \| `python3.7` \| `python3.8` \| `dotnetcore1.0` \| `dotnetcore2.1` \| `go1.x` \| `ruby2.5` \| `provided`  | 
|  `CreatedDate`  |  No  |  Indicates when the layer version was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 
|  `Version`  |  No  |  The version number\. Type: Long  | 

#### AwsRdsDbCluster<a name="asff-resourcedetails-awsrdsdbcluster"></a>

The `AwsRdsDbCluster` object provides details about an Amazon RDS database cluster\.

`Example`

```
"AwsRdsDbCluster": {
    "AllocatedStorage": 1,
    "AvailabilityZones": [
        "us-east-1c",
        "us-east-1e",
        "us-east-1a"
    ],
    "BackupRetentionPeriod": 1,
    "DatabaseName": "",
    "Status": "modifying",
    "Endpoint": "database-3.cluster-example.us-east-1.rds.amazonaws.com",
    "ReaderEndpoint": "database-3.cluster-ro-example.us-east-1.rds.amazonaws.com",
    "CustomEndpoints": [],
    "MultiAz": false,
    "Engine": "aurora-mysql",
    "EngineVersion": "5.7.mysql_aurora.2.03.4",
    "Port": 3306,
    "MasterUsername": "admin",
    "PreferredBackupWindow": "04:52-05:22",
    "PreferredMaintenanceWindow": "sun:09:32-sun:10:02",
    "ReadReplicaIdentifiers": [],
    "VpcSecurityGroups": [
        {
            "VpcSecurityGroupId": "sg-example-1",
            "Status": "active"
        }
    ],
    "HostedZoneId": "ZONE1",
    "StorageEncrypted": true,
    "KmsKeyId": "arn:aws:kms:us-east-1:777788889999:key/key1",
    "DbClusterResourceId": "cluster-example",
    "AssociatedRoles": [
        {
        "RoleArn": "arn:aws:iam::777788889999:role/aws-service-role/rds.amazonaws.com/AWSServiceRoleForRDS",
        "Status": "PENDING"
        }
    ],
    "ClusterCreateTime": "2020-06-22T17:40:12.322Z",
    "EnabledCloudwatchLogsExports": [
        "audit",
        "error",
        "general",
        "slowquery"
    ],
    "EngineMode": "provisioned",
    "DeletionProtection": false,
    "HttpEndpointEnabled": false,
    "ActivityStreamStatus": "stopped",
    "CopyTagsToSnapshot": true,
    "CrossAccountClone": false,
    "DomainMemberships": [],
    "DbClusterParameterGroup": "cluster-parameter-group",
    "DbSubnetGroup": "subnet-group",
    "DbClusterOptionGroupMemberships": [],
    "DbClusterIdentifier": "database-3",
    "DbClusterMembers": [
        {
        "IsClusterWriter": true,
        "PromotionTier": 1,
        "DbInstanceIdentifier": "database-3-instance-1",
        "DbClusterParameterGroupStatus": "in-sync"
        }
    ],
    "IamDatabaseAuthenticationEnabled": false
}
```

The `AwsRdsDbCluster` object can contain the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `ActivityStreamStatus`  |  No  |  The status of the database activity stream\. Type: String Valid values: `stopped`\| `starting` \| `started` \| `stopping`  | 
|  `AllocatedStorage`  |  No  |  For all database engines except Amazon Aurora, specifies the allocated storage size in gibibytes \(GiB\)\. For Aurora, `AllocatedStorage` is always 1\. The Aurora database cluster storage size is not fixed\. Instead, it automatically adjusts as needed\. Type: Number  | 
|  [`AssociatedRoles`](#asff-resourcedetails-awsrdsdbcluster-associatedroles)  |  No  |  A list of the IAM roles that are associated with the DB cluster\. Type: Array of objects  | 
|  `AvailabilityZones`  |  No  |  A list of Availability Zones \(AZs\) where instances in the DB cluster can be created\. Type: Array of strings Example: <pre>"AvailabilityZones": [<br />    "us-east-1c",<br />    "us-east-1e",<br />    "us-east-1a"<br />]</pre>  | 
|  `BackupRetentionPeriod`  |  No  |  The number of days for which automated backups are retained\. Type: Number Minimum value: 1 Maximum value: 35  | 
|  `ClusterCreateTime`  |  No  |  Indicates when the DB cluster was created, in Universal Coordinated Time \(UTC\)\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"ClusterCreateTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `CopyTagsToSnapshot`  |  No  |  Whether tags are copied from the DB cluster to snapshots of the DB cluster\. Type: Boolean  | 
|  `CrossAccountClone`  |  No  |  Whether the DB cluster is a clone of a DB cluster owned by a different AWS account\. Type: Boolean  | 
|  `CustomEndpoints`  |  No  |  A list of custom endpoints for the DB cluster\. Type: Array of strings  | 
|  `DatabaseName`  |  No  |  The name of the database\. Type: String  | 
|  `DbClusterIdentifier`  |  No  |  The DB cluster identifier that the user assigned to the cluster\. This identifier is the unique key that identifies a DB cluster\. Type: String  | 
|  [`DbClusterMembers`](#asff-resourcedetails-awsrdsdbcluster-dbclustermembers)  |  No  |  The list of instances that make up the DB cluster\. Type: Array of objects  | 
|  [`DbClusterOptionGroupMemberships`](#asff-resourcedetails-awsrdsdbcluster-dbclusteroptiongroupmemberships)  |  No  |  The list of option group memberships for this DB cluster\. Type: Array of objects  | 
|  `DbClusterParameterGroup`  |  No  |  The name of the DB cluster parameter group for the DB cluster\. Type: String  | 
|  `DbClusterResourceId`  |  No  |  The identifier of the DB cluster\. The identifier must be unique within each AWS Region and is immutable\. Type: String  | 
|  `DbSubnetGroup`  |  No  |  The subnet group that is associated with the DB cluster, including the name, description, and subnets in the subnet group\. Type: String  | 
|  `DeletionProtection`  |  No  |  Whether the DB cluster has deletion protection enabled\. Type: Boolean  | 
|  [`DomainMemberships`](#asff-resourcedetails-awsrdsdbcluster-domainmemberships)  |  No  |  The Active Directory domain membership records that are associated with the DB cluster\. Type: Array of objects  | 
|  `EnabledCloudwatchLogsExports`  |  No  |  A list of log types that this DB cluster is configured to export to CloudWatch Logs\. Type: Array of strings Example: <pre>"EnabledCloudwatchLogsExports": [<br />    "audit",<br />    "error",<br />    "general",<br />    "slowquery"<br />]</pre>  | 
|  `Endpoint`  |  No  |  The connection endpoint for the primary instance of the DB cluster\. Type: String  | 
|  `Engine`  |  No  |  The name of the database engine to use for this DB cluster\. Type: String Valid values: `aurora` \| `aurora-mysql` \| a`urora-postgresql`  | 
|  `EngineMode`  |  No  |  The database engine mode of the DB cluster\. Type: String Valid values: `provisioned` \| `serverless` \| `parallelquery` \| `global` \| `multimaster`  | 
|  `EngineVersion`  |  No  |  The version number of the database engine to use\. Type: String Example: <pre>"EngineVersion": "5.7.mysql_aurora.2.03.4",</pre>  | 
|  `HostedZoneId`  |  No  |  Specifies the identifier that Amazon Route 53 assigns when you create a hosted zone\. Type: String  | 
|  `HttpEndpointEnabled`  |  No  |  Whether the HTTP endpoint for an Aurora Serverless DB cluster is enabled\. Type: Boolean  | 
|  `IamDatabaseAuthenticationEnabled`  |  No  |  Whether the mapping of IAM accounts to database accounts is enabled\. Type: Boolean  | 
|  `KmsKeyId`  |  No  |  The ARN of the AWS KMS master key that is used to encrypt the database instances in the DB cluster\. Type: String  | 
|  `MasterUsername`  |  No  |  The name of the master user for the DB cluster\. Type: String  | 
|  `MultiAz`  |  No  |  Whether the DB cluster has instances in multiple Availability Zones\. Type: Boolean  | 
|  `Port`  |  No  |  The port number on which the DB instances in the DB cluster accept connections\. Type: Number  | 
|  `PreferredBackupWindow`  |  No  |  The range of time each day when automated backups are created, if automated backups are enabled\. Type: string Format: `HH:MM-HH:MM`  Example: <pre>"PreferredBackupWindow": "04:52-05:22"</pre>  | 
|  `PreferredMaintenanceWindow`  |  No  |  The weekly time range during which system maintenance can occur, in Universal Coordinated Time \(UTC\)\. Type: String Format: `<day>:HH:MM-<day>:HH:MM` For the day values, use `mon`\|`tue`\|`wed`\|`thu`\|`fri`\|`sat`\|`sun` Example: <pre>"PreferredMaintenanceWindow": "sun:09:32-sun:10:02"</pre>  | 
|  `ReaderEndpoint`  |  No  |  The reader endpoint for the DB cluster\. Type: String  | 
|  `ReadReplicaIdentifiers`  |  No  |  The identifiers of the read replicas that are associated with this DB cluster\. Type: Array of strings  | 
|  `Status`  |  No  |  The current status of this DB cluster\. Type: String  | 
|  `StorageEncrypted`  |  No  |  Whether the DB cluster is encrypted\. Type: Boolean  | 
|  [`VpcSecurityGroups`](#asff-resourcedetails-awsrdsdbcluster-vpcsecuritygroups)  |  No  |  A list of VPC security groups that the DB cluster belongs to\. Type: Array of objects  | 

##### AssociatedRoles<a name="asff-resourcedetails-awsrdsdbcluster-associatedroles"></a>

The `AssociatedRoles` object specifies the list of IAM roles that are associated with the Amazon RDS DB cluster\.

Each role can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `RoleArn`  |  No  |  The ARN of an IAM role that is associated with the Amazon RDS DB cluster\. Type: String  | 
|  `Status`  |  No  |  The status of the association between the IAM role and the DB cluster\. Type: String Valid values: `ACTIVE` \| `PENDING` \| `INVALID`  | 

##### DbClusterMembers<a name="asff-resourcedetails-awsrdsdbcluster-dbclustermembers"></a>

The `DbClusterMembers` object contains the list of instances in the cluster\.

For each instance, the object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DbClusterParameterGroupStatus`  |  No  |  The status of the DB cluster parameter group for this member of the DB cluster\. Type: String  | 
|  `DbInstanceIdentifier`  |  No  |  The instance identifier for this member of the DB cluster\. Type: String  | 
|  `IsClusterWriter`  |  No  |  Whether the cluster member is the primary instance for the DB cluster\. Type: Boolean  | 
|  `PromotionTier`  |  No  |  Specifies the order in which an Aurora replica is promoted to the primary instance when the existing primary instance fails\. Type: Number  | 

##### DbClusterOptionGroupMemberships<a name="asff-resourcedetails-awsrdsdbcluster-dbclusteroptiongroupmemberships"></a>

The `DbClusterOptionGroupMemberships` object contains a list of option group members for this DB cluster\.

Each option group membership can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DbClusterOptionGroupName`  |  No  |  The name of the DB cluster option group\. Type: String  | 
|  `Status`  |  No  |  The status of the DB cluster option group\. Type: String  | 

##### DomainMemberships<a name="asff-resourcedetails-awsrdsdbcluster-domainmemberships"></a>

The `DomainMemberships` object contains the list of Active Directory domain memberships for the DB cluster\.

Each membership can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Domain`  |  No  |  The identifier of the Active Directory domain\. Type: String  | 
|  `Fqdn`  |  No  |  The fully qualified domain name of the Active Directory domain\. Type: String  | 
|  `IamRoleName`  |  No  |  The name of the IAM role to use when making API calls to the Directory Service\. Type: String  | 
|  `Status`  |  No  |  The status of the Active Directory domain membership for the DB cluster\. Type: String  | 

##### VpcSecurityGroups<a name="asff-resourcedetails-awsrdsdbcluster-vpcsecuritygroups"></a>

The `VpcSecurityGroups` object contains the list of VPC security groups that the DB cluster belongs to\.

Each security group can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Status`  |  No  |  The status of the VPC security group\. Type: string  | 
|  `VpcSecurityGroupId`  |  No  |  The name of the VPC security group\. Type: string  | 

#### AwsRdsDbClusterSnapshot<a name="asff-resourcedetails-awsrdsdbclustersnapshot"></a>

The `AwsRdsDbClusterSnapshot` object contains information about an Amazon RDS DB cluster snapshot\.

**Example**

```
"AwsRdsDbClusterSnaphot": {
    "AvailabilityZones": [
        "us-east-1a",
        "us-east-1d",
        "us-east-1e"
    ],
    "SnapshotCreateTime": "2020-06-22T17:40:12.322Z",
    "Engine": "aurora",
    "AllocatedStorage": 0,
    "Status": "available",
    "Port": 0,
    "VpcId": "vpc-faf7e380",
    "ClusterCreateTime": "2020-06-12T13:23:15.577Z",
    "MasterUsername": "admin",
    "EngineVersion": "5.6.10a",
    "LicenseModel": "aurora",
    "SnapshotType": "automated",
    "PercentProgress": 100,
    "StorageEncrypted": true,
    "KmsKeyId": "arn:aws:kms:us-east-1:777788889999:key/key1",
    "DbClusterIdentifier": "database-2",
    "DbClusterSnapshotIdentifier": "rds:database-2-2020-06-23-03-52",
    "IamDatabaseAuthenticationEnabled": false
}
```

`AwsRdsDbClusterSnapshot` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AllocatedStorage`  |  No  |  Specifies the allocated storage size in gibibytes \(GiB\)\. Type: Number  | 
|  `AvailabilityZones`  |  No  |  A list of Availability Zones where instances in the DB cluster can be created\. Type: Array of strings  | 
|  `ClusterCreateTime`  |  No  |  Indicates when the DB cluster was created, in Universal Coordinated Time \(UTC\)\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"ClusterCreateTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `DbClusterIdentifier`  |  No  |  The DB cluster identifier\. Type: String Format: Must be lowercase  | 
|  `DbClusterSnapshotIdentifier`  |  No  |  The identifier of the DB cluster snapshot\. Type: String  | 
|  `Engine`  |  No  |  The name of the database engine to be used for this DB cluster\. Type: String  | 
|  `EngineVersion`  |  No  |  The version of the database engine to use\. Type: String  | 
|  `IamDatabaseAuthenticationEnabled`  |  No  |  Whether mapping of IAM accounts to database accounts is enabled\. Type: Boolean  | 
|  `KmsKeyId`  |  No  |  The ARN of the AWS KMS master key that is used to encrypt the database instances in the DB cluster\. Type: String  | 
|  `LicenseModel`  |  No  |  The license model information for this DB cluster snapshot\. Type: String  | 
|  `MasterUsername`  |  No  |  The name of the master user for the DB cluster\. Type: String  | 
|  `PercentProgress`  |  No  |  Specifies the percentage of the estimated data that has been transferred\. Type: Number Example: <pre>"PercentProgress": 100</pre>  | 
|  `Port`  |  No  |  The port number on which the DB instances in the DB cluster accept connections\. Type: Number  | 
|  `SnapshotCreateTime`  |  No  |  Indicates when the snapshot was taken\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"SnapshotCreateTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `SnapshotType`  |  No  |  The type of DB cluster snapshot\. Type: String  | 
|  `Status`  |  No  |  The status of this DB cluster snapshot\. Type: String  | 
|  `StorageEncrypted`  |  No  |  Whether the DB cluster is encrypted\. Type: Boolean  | 
|  `VpcId`  |  No  |  The VPC ID that is associated with the DB cluster snapshot\. Type: String  | 

#### AwsRdsDbInstance<a name="asff-resourcedetails-awsrdsdbinstance"></a>

The `AwsRdsDbInstance` object provides details about an Amazon RDS DB instance\.

**Example**

```
"AwsRdsDbInstance": {
    "AllocatedStorage": 20,
    "AssociatedRoles": [],
    "AutoMinorVersionUpgrade": true,
    "AvailabilityZone": "us-east-1d",
    "BackupRetentionPeriod": 7,
    "CaCertificateIdentifier": "certificate1",
    "CharacterSetName": "",
    "CopyTagsToSnapshot": true,
    "DbClusterIdentifier": "",
    "DbInstanceArn": "arn:aws:rds:us-east-1:111122223333:db:database-1",
    "DbInstanceClass": "db.t2.micro",
    "DbInstanceIdentifier": "database-1",
    "DbInstancePort": 0,
    "DbInstanceStatus": "available",
    "DbiResourceId": "db-EXAMPLE123",
    "DbName": "",
    "DbParameterGroups": [
        {
            "DbParameterGroupName": "default.mysql5.7",
            "ParameterApplyStatus": "in-sync"
        }
    ],
    "DbSecurityGroups": [],                                                                                                                                                                                                 
    "DbSubnetGroup": {
        "DbSubnetGroupName": "my-group-123abc",
        "DbSubnetGroupDescription": "My subnet group",
        "VpcId": "vpc-example1",
        "SubnetGroupStatus": "Complete",
        "Subnets": [
            {
                "SubnetIdentifier": "subnet-123abc",
                "SubnetAvailabilityZone": {
                    "Name": "us-east-1d"
                },
                "SubnetStatus": "Active"
            },
            {
                "SubnetIdentifier": "subnet-456def",
                "SubnetAvailabilityZone": {
                    "Name": "us-east-1c"
                },
                "SubnetStatus": "Active"
            }
      ],
        "DbSubnetGroupArn": ""
    },
    "DeletionProtection": false,
    "DomainMemberships": [],
    "EnabledCloudWatchLogsExports": [],
    "Endpoint": {
        "address": "database-1.example.us-east-1.rds.amazonaws.com",
        "port": 3306,
        "hostedZoneId": "ZONEID1"
    },
    "Engine": "mysql",
    "EngineVersion": "5.7.22",
    "EnhancedMonitoringResourceArn": "arn:aws:logs:us-east-1:111122223333:log-group:Example:log-stream:db-EXAMPLE1",
    "IamDatabaseAuthenticationEnabled": false,
    "InstanceCreateTime": "2020-06-22T17:40:12.322Z",
    "Iops": "",
    "KmsKeyId": "",
    "LatestRestorableTime": "2020-06-24T05:50:00.000Z",
    "LicenseModel": "general-public-license",
    "ListenerEndpoint": "",
    "MasterUsername": "admin",
    "MaxAllocatedStorage": 1000,
    "MonitoringInterval": 60,
    "MonitoringRoleArn": "arn:aws:iam::111122223333:role/rds-monitoring-role",
    "MultiAz": false,
    "OptionGroupMemberships": [
        {
            "OptionGroupName": "default:mysql-5-7",
            "Status": "in-sync"
        }
    ],
    "PreferredBackupWindow": "03:57-04:27",
    "PreferredMaintenanceWindow": "thu:10:13-thu:10:43",
    "PendingModifiedValues": {
        "DbInstanceClass": "",
        "AllocatedStorage": "",
        "MasterUserPassword": "",
        "Port": "",
        "BackupRetentionPeriod": "",
        "MultiAZ": "",
        "EngineVersion": "",
        "LicenseModel": "",
        "Iops": "",
        "DbInstanceIdentifier": "",
        "StorageType": "",
        "CaCertificateIdentifier": "",
        "DbSubnetGroupName": "",
        "PendingCloudWatchLogsExports": "",
        "ProcessorFeatures": []
    },
    "PerformanceInsightsEnabled": false,
    "PerformanceInsightsKmsKeyId": "",
    "PerformanceInsightsRetentionPeriod": "",
    "ProcessorFeatures": [],
    "PromotionTier": "",
    "PubliclyAccessible": false,
    "ReadReplicaDBClusterIdentifiers": [],
    "ReadReplicaDBInstanceIdentifiers": [],
    "ReadReplicaSourceDBInstanceIdentifier": "",
    "SecondaryAvailabilityZone": "",
    "StatusInfos": [],
    "StorageEncrypted": false,
    "StorageType": "gp2",
    "TdeCredentialArn": "",
    "Timezone": "",
    "VpcSecurityGroups": [
        {
            "VpcSecurityGroupId": "sg-example1",
            "Status": "active"
        }
    ]
}
```

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AllocatedStorage`  |  No  |  The amount of storage \(in gigabytes\) to initially allocate for the DB instance\. Type: Number  | 
|  [`AssociatedRoles`](#asff-resourcedetails-awsrdsdbinstance-associatedroles)  |  No  |  The IAM roles that are associated with the DB instance\. Type: Array of role objects  | 
|  `AutoMinorVersionUpgrade`  |  No  |  Indicates whether minor version patches are applied automatically\. Type: Boolean  | 
|  `AvailabilityZone`  |  No  |  The Availability Zone where the DB instance will be created\. Type: String  | 
|  `BackupRetentionPeriod`  |  No  |  The number of days for which to retain automated backups\. Type: Number Minimum value: 0 Maximum value: 35  | 
|  `CACertificateIdentifier`  |  No  |  The identifier of the CA certificate for this DB instance\. Type: String  | 
|  `CharacterSetName`  |  No  |  The name of the character set that this DB instance is associated with\. Type: String  | 
|  `CopyTagsToSnapshot`  |  No  |  Whether to copy resource tags to snapshots of the DB instance\. Type: Boolean  | 
|  `DBClusterIdentifier`  |  No  |  If the DB instance is a member of a DB cluster, contains the name of the DB cluster that the DB instance is a member of\. Type: String  | 
|  `DBInstanceClass`  |  No  |  Contains the name of the compute and memory capacity class of the DB instance\. Type: String  | 
|  `DBInstanceIdentifier`  |  No  |  Contains a user\-supplied database identifier\. This identifier is the unique key that identifies a DB instance\. Type: String  | 
|  `DbInstancePort`  |  No  |  Specifies the port that the DB instance listens on\. If the DB instance is part of a DB cluster, this can be a different port than the DB cluster port\. Type: Integer  | 
|  `DbInstanceStatus`  |  No  |  The current status of the DB instance\. Type: String  | 
|  `DbiResourceId`  |  No  |  The AWS Region\-unique, immutable identifier for the DB instance\. This identifier is found in CloudTrail log entries whenever the AWS KMS key for the DB instance is accessed\. Type: String  | 
|  `DBName`  |  No  |  The meaning of this parameter differs according to the database that engine you use\. **MySQL, MariaDB, SQL Server, PostgreSQL** Contains the name of the initial database of this instance that was provided at create time, if one was specified when the DB instance was created\. This same name is returned for the life of the DB instance\. Type: String **Oracle** Contains the Oracle System ID \(SID\) of the created DB instance\. Not shown when the returned parameters do not apply to an Oracle DB instance\. Type: String  | 
|  [`DbParameterGroups`](#asff-resourcedetails-awsrdsdbinstance-dbparametergroups)  |  No  |  A list of the DB parameter groups to assign to the DB instance\. Type: Array of objects  | 
|  `DbSecurityGroups`  |  No  |  A list of the DB security groups to assign to the DB instance\. Type: Array of strings  | 
|  [`DbSubnetGroup`](#asff-resourcedetails-awsrdsdbinstance-dbsubnetgroup)  |  No  |  Information about the subnet group that is associated with the DB instance\. Type: Object  | 
|  `DeletionProtection`  |  No  |  Indicates whether the DB instance has deletion protection enabled\. The database can't be deleted when deletion protection is enabled\. Type: Boolean  | 
|  [`DomainMemberships`](#asff-resourcedetails-awsrdsdbinstance-domainmemberships)  |  No  |  The Active Directory domain membership records associated with the DB instance\. Type: Array of objects  | 
|  `EnabledCloudwatchLogsExports`  |  No  |  A list of log types that this DB instance is configured to export to CloudWatch Logs\. Type: Array of strings  | 
|  [`Endpoint`](#asff-resourcedetails-awsrdsdbinstance-endpoint)  |  No  |  Specifies the connection endpoint\. Type: Object  | 
|  `Engine`  |  No  |  Provides the name of the database engine to be used for this DB instance\. Type: String  | 
|  `EngineVersion`  |  No  |  Indicates the database engine version\. Type: String  | 
|  `EnhancedMonitoringResourceArn`  |  No  |  The ARN of the CloudWatch Logs log stream that receives the enhanced monitoring metrics data for the DB instance\. Type: String  | 
|  `IamDatabaseAuthenticationEnabled`  |  No  |  True if mapping of IAM accounts to database accounts is enabled, and otherwise false\. IAM database authentication can be enabled for the following database engines: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Type: Boolean  | 
|  `InstanceCreateTime`  |  No  |  Indicates when the DB instance was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 
|  `Iops`  |  No  |  Specifies the provisioned IOPS \(I/O operations per second\) for this DB instance\. Type: Number  | 
|  `KmsKeyId`  |  No  |  If `StorageEncrypted` is true, the AWS KMS key identifier for the encrypted DB instance\. Type: String  | 
|  `LatestRestorableTime`  |  No  |  Specifies the latest time to which a database can be restored with point\-in\-time restore\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"LatestRestorableTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `LicenseModel`  |  No  |  License model information for this DB instance\. Type: String  | 
|  [`ListenerEndpoint`](#asff-resourcedetails-awsrdsdbinstance-listenerendpoint)  |  No  |  Information about the listener connection endpoint for SQL Server Always On\. Type: Object  | 
|  `MasterUsername`  |  No  |  The master user name of the DB instance\. Type: String  | 
|  `MaxAllocatedStorage`  |  No  |  The upper limit to which Amazon RDS can automatically scale the storage of the DB instance\. Type: Number  | 
|  `MonitoringInterval`  |  No  |  The interval, in seconds, between points when enhanced monitoring metrics are collected for the DB instance\. Type: Number  | 
|  `MonitoringRoleArn`  |  No  |  The ARN for the IAM role that permits Amazon RDS to send enhanced monitoring metrics to CloudWatch Logs\. Type: String  | 
|  `MultiAz`  |  No  |  Whether the DB instance is a multiple Availability Zone deployment\. Type: Boolean  | 
|  [`OptionGroupMemberships`](#asff-resourcedetails-awsrdsdbinstance-optiongroupmemberships)  |  No  |  The list of option group memberships for this DB instance\. Type: Array of objects  | 
|  [`PendingModifiedValues`](#asff-resourcedetails-awsrdsdbinstance-pendingmodifiedvalues)  |  No  |  Changes to the DB instance that are currently pending\. Type: Object  | 
|  `PerformanceInsightsEnabled`  |  No  |  Indicates whether Performance Insights is enabled for the DB instance\. Type: Boolean  | 
|  `PerformanceInsightsKmsKeyId`  |  No  |  The identifier of the AWS KMS key used to encrypt the Performance Insights data\. Type: String  | 
|  `PerformanceInsightsRetentionPeriod`  |  No  |  The number of days to retain Performance Insights data\. Type: Number  | 
|  `PreferredBackupWindow`  |  No  |  The range of time each day when automated backups are created, if automated backups are enabled\. Type: string Format: `HH:MM-HH:MM`  Example: <pre>"PreferredBackupWindow": "04:52-05:22"</pre>  | 
|  `PreferredMaintenanceWindow`  |  No  |  The weekly time range during which system maintenance can occur, in Universal Coordinated Time \(UTC\)\. Type: String Format: `<day>:HH:MM-<day>:HH:MM` For the day values, use `mon`\|`tue`\|`wed`\|`thu`\|`fri`\|`sat`\|`sun` Example: <pre>"PreferredMaintenanceWindow": "sun:09:32-sun:10:02"</pre>  | 
|  [`ProcessorFeatures`](#asff-resourcedetails-awsrdsdbinstance-processorfeatures)  |  No  |  The number of CPU cores and the number of threads per core for the DB instance class of the DB instance\. Type: Array of objects  | 
|  `PromotionTier`  |  No  |  The order in which to promote an Aurora replica to the primary instance after a failure of the existing primary instance\. Type: Number  | 
|  `PubliclyAccessible`  |  No  |  Specifies the accessibility options for the DB instance\. A value of true specifies an internet\-facing instance with a publicly resolvable DNS name, which resolves to a public IP address\. A value of false specifies an internal instance with a DNS name that resolves to a private IP address\. Type: Boolean  | 
|  `ReadReplicaDBClusterIdentifiers`  |  No  |  List of identifiers of Aurora DB clusters to which the RDS DB instance is replicated as a read replica\. Type: Array of strings  | 
|  `ReadReplicaDBInstanceIdentifiers`  |  No  |  List of identifiers of the read replicas associated with this DB instance\. Type: Array of strings  | 
|  `ReadReplicaSourceDBInstanceIdentifier`  |  No  |  If this DB instance is a read replica, contains the identifier of the source DB instance\. Type: String  | 
|  `SecondaryAvailabilityZone`  |  No  |  For a DB instance with multi\-Availability Zone support, the name of the secondary Availability Zone\. Type: String   | 
|  `StatusInfos` No  |  |  The status of a read replica\. If the instance isn't a read replica, this is empty\. Type: Array of objects  | 
|  `StorageEncrypted`  |  No  |  Specifies whether the DB instance is encrypted\. Type: Boolean  | 
|  `StorageType`  |  No  |  The storage type for the DB instance\. Type: String  | 
|  `TdeCredentialArn`  |  No  |  The ARN from the key store with which the instance is associated for TDE encryption\. Type: String  | 
|  `Timezone`  |  No  |  The time zone of the DB instance\. Type: String  | 
|  [`VpcSecurityGroups`](#asff-resourcedetails-awsrdsdbinstance-vpcsecuritygroups)  |  No  |  List of VPC security groups that the DB instance belongs to\. Type: Array of objects  | 

##### AssociatedRoles<a name="asff-resourcedetails-awsrdsdbinstance-associatedroles"></a>

The `AssociatedRoles` array lists the IAM roles that are associated with the DB instance\.

Each role object in the `AssociatedRoles` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `FeatureName`  |  No  |  The name of the feature that is associated with the IAM role\. Type: String  | 
|  `RoleArn`  |  No  |  The ARN of the IAM role that is associated with the DB instance\. Type: String  | 
|  `Status`  |  No  |  Describes the state of association between the IAM role and the DB instance\. Type: String Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 

##### DbParameterGroups<a name="asff-resourcedetails-awsrdsdbinstance-dbparametergroups"></a>

The `DbParameterGroups` object contains the list of parameter groups to assign to the database instance\.

Each parameter group can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DbParameterGroupName`  |  No  |  The name of the parameter group\. Type: String  | 
|  `ParameterApplyStatus`  |  No  |  The status of parameter updates\. Type: String   | 

##### DbSubnetGroup<a name="asff-resourcedetails-awsrdsdbinstance-dbsubnetgroup"></a>

The `DbSubnetGroup` object contains information about the subnet group for the database instance\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DbSubnetGroupArn`  |  No  |  The ARN of the subnet group\. Type: String  | 
|  `DbSubnetGroupDescription`  |  No  |  The description of the subnet group\. Type: String  | 
|  `DbSubnetGroupName`  |  No  |  The name of the subnet group\. Type: String  | 
|  `SubnetGroupStatus`  |  No  |  The status of the subnet group\. Type: String  | 
|  `Subnets`  |  No  |  A list of subnets in the subnet group\. Type: Array of objects\.  | 
|  `VpcId`  |  No  |  The VPC ID of the subnet group\. Type: String  | 

The `Subnets` object contains the list of subnets in the subnet group\.

Each subnet can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `SubnetAvailabilityZone`  |  No  |  Information about the Availability Zone for a subnet in the subnet group\. Type: Object  | 
|  `SubnetAvailabilityZone.Name`  |  No  |  The name of the Availability Zone for a subnet in the subnet group\. Type: String  | 
|  `SubnetIdentifier`  |  No  |  The identifier of a subnet in the subnet group\. Type: String\.  | 
|  `SubnetStatus`  |  No  |  The status of a subnet in the subnet group\. Type: String  | 

##### DomainMemberships<a name="asff-resourcedetails-awsrdsdbinstance-domainmemberships"></a>

The `DomainMemberships` object contains the Active Directory domain membership records associated with the DB instance\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Domain`  |  No  |  The identifier of the Active Directory domain\. Type: String  | 
|  `Fqdn`  |  No  |  The fully qualified domain name of the Active Directory domain\. Type: String  | 
|  `IamRoleName`  |  No  |  The name of the IAM role to use when making API calls to the Directory Service\. Type: String  | 
|  `Status`  |  No  |  The status of the Active Directory Domain membership for the DB instance\. Type: String  | 

##### Endpoint<a name="asff-resourcedetails-awsrdsdbinstance-endpoint"></a>

The `Endpoint` object provides details about the connection endpoint for the DB instance\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Address`  |  No  |  Specifies the DNS address of the DB instance\. Type: String  | 
|  `HostedZoneId`  |  No  |  Specifies the ID that Amazon Route 53 assigns when you create a hosted zone\. Type: String  | 
|  `Port`  |  No  |  Specifies the port that the database engine is listening on\. Type: Integer  | 

##### ListenerEndpoint<a name="asff-resourcedetails-awsrdsdbinstance-listenerendpoint"></a>

The `ListenerEndpoint` object contains information about the listener connection endpoint for SQL Server Always On\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Address`  |  No  |  Specifies the DNS address of the DB instance\. Type: String  | 
|  `HostedZoneId`  |  No  |  The ID that Amazon Route 53 assigns when you create a hosted zone\. Type: String  | 
|  `Port`  |  No  |  The port that the database engine is listening on\. Type: Number  | 

##### OptionGroupMemberships<a name="asff-resourcedetails-awsrdsdbinstance-optiongroupmemberships"></a>

The `OptionGroupMemberships` object contains the list of option group memberships for the DB instance\.

Each option group membership can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `OptionGroupName`  |  No  |  The name of the option group\. Type: String  | 
|  `Status`  |  No  |  The status of the DB instance membership in the option group\. Type: String  | 

##### PendingModifiedValues<a name="asff-resourcedetails-awsrdsdbinstance-pendingmodifiedvalues"></a>

The `PendingModifiedValues` object lists changes to the DB instance that are currently pending\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AllocatedStorage`  |  No  |  The new value of the allocated storage for the DB instance\. Type: Number  | 
|  `BackupRetentionPeriod`  |  No  |  The new backup retention period for the DB instance\. Type: Number  | 
|  `CaCertificateIdentifier`  |  No  |  The new CA certificate identifier for the DB instance\. Type: String  | 
|  `DbInstanceClass`  |  No  |  The new DB instance class for the DB instance\. Type: String  | 
|  `DbInstanceIdentifier`  |  No  |  The new DB instance identifier for the DB instance\. Type: String  | 
|  `DbSubnetGroupName`  |  No  |  The name of the new subnet group for the DB instance\. Type: String  | 
|  `EngineVersion`  |  No  |  The new engine version for the DB instance\. Type: String  | 
|  `Iops`  |  No  |  The new provisioned IOPS value for the DB instance\. Type: Number  | 
|  `LicenseModel`  |  No  |  The new license model value for the DB instance\. Type: String  | 
|  `MasterUserPassword`  |  No  |  The new master user password for the DB instance\. Type: String  | 
|  `MultiAZ`  |  No  |  Indicates that a single Availability Zone DB instance is changing to a multiple Availability Zone deployment\. Type: Boolean  | 
|  `PendingCloudWatchLogsExports`  |  No  |  A list of log types that are being enabled or disabled\. Type: Object  | 
|  `Port`  |  No  |  The new port for the DB instance\. Type: Number  | 
|  [`ProcessorFeatures`](#asff-resourcedetails-awsrdsdbinstance-processorfeatures)  |  No  |  Processor features that are being updated\. Type: Array of objects  | 
|  `StorageType`  |  No  |  The new storage type for the DB instance\. Type: String  | 

The `PendingCloudWatchLogsExport` object identifies the log types to enable and disable\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `LogTypesToDisable`  |  No  |  A list of log types that are being disabled\. Type: Array of strings  | 
|  `LogTypesToEnable`  |  No  |  A list of log types that are being enabled\. Type: Array of strings  | 

##### ProcessorFeatures<a name="asff-resourcedetails-awsrdsdbinstance-processorfeatures"></a>

The `ProcessorFeatures` object contains a list of processor features\. In the context of `PendingModifiedValues`, it identifies the features to be updated\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Name`  |  No  |  The name of the processor feature\. Type: String  | 
|  `Value`  |  No  |  The value of the processor feature\. Type: String  | 

##### StatusInfos<a name="asff-resourcedetails-awsrdsdbinstance-statusinfos"></a>

The `StatusInfos` object contains information about the status of a read replica\. If the instance isn't a read replica, the object is empty\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Message`  |  No  |  If the read replica is currently in an error state, provides the error details\. Type: String  | 
|  `Normal`  |  No  |  Whether the read replica instance is operating normally\. Type: Boolean  | 
|  `Status`  |  No  |  The status of the read replica instance\. Type: String  | 
|  `StatusType`  |  No  |  The type of status\. For a read replica, the status type is read replication\. Type: String  | 

##### VpcSecurityGroups<a name="asff-resourcedetails-awsrdsdbinstance-vpcsecuritygroups"></a>

The `VpcSecurityGroups` array provides the list of VPC security groups that the DB instance belongs to\.

Each object in the `VpcSecurityGroups` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `VpcSecurityGroupId`  |  No  |  The name of the VPC security group\. Type: String  | 
|  `Status`  |  No  |  The status of the VPC security group\. Type: String  | 

#### AwsRdsDbSnapshot<a name="asff-resourcedetails-awsrdsdbsnapshot"></a>

The `AwsRdsDbSnapshot` object contains details about an Amazon RDS DB cluster snapshot\.

**Example**

```
"AwsRdsDbSnapshot": {
    "DbSnapshotIdentifier": "rds:database-1-2020-06-22-17-41",
    "DbInstanceIdentifier": "database-1",
    "SnapshotCreateTime": "2020-06-22T17:41:29.967Z",
    "Engine": "mysql",
    "AllocatedStorage": 20,
    "Status": "available",
    "Port": 3306,
    "AvailabilityZone": "us-east-1d",
    "VpcId": "vpc-example1",
    "InstanceCreateTime": "2020-06-22T17:40:12.322Z",
    "MasterUsername": "admin",
    "EngineVersion": "5.7.22",
    "LicenseModel": "general-public-license",
    "SnapshotType": "automated",
    "Iops": null,
    "OptionGroupName": "default:mysql-5-7",
    "PercentProgress": 100,
    "SourceRegion": null,
    "SourceDbSnapshotIdentifier": "",
    "StorageType": "gp2",
    "TdeCredentialArn": "",
    "Encrypted": false,
    "KmsKeyId": "",
    "Timezone": "",
    "IamDatabaseAuthenticationEnabled": false,
    "ProcessorFeatures": [],
    "DbiResourceId": "db-resourceexample1"
}
```

`AwsRdsDbSnapshot` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AllocatedStorage`  |  No  |  The amount of storage \(in gigabytes\) to be initially allocated for the database instance\. Type: Number  | 
|  `AvailabilityZone`  |  No  |  Specifies the name of the Availability Zone in which the DB instance was located at the time of the DB snapshot\. Type: String  | 
|  `DbInstanceIdentifier`  |  No  |  A name for the DB instance\. Type: String  | 
|  `DbiResourceId`  |  No  |  The identifier for the source DB instance\. Type: String  | 
|  `DbSnapshotIdentifier`  |  No  |  The name or ARN of the DB snapshot that is used to restore the DB instance\. Type: String  | 
|  `Encrypted`  |  No  |  Whether the DB snapshot is encrypted\. Type: Boolean  | 
|  `Engine`  |  No  |  The name of the database engine that you want to use for this DB instance\. Type: String Valid values: `aurora` \| `aurora-mysql` \| `aurora-postgresql` \| `mariadb` \| `mysql` \| `oracle-ee` \| `oracle-se2` \| `oracle-se1` \| `oracle-se` \| c`` \| `sqlserver-ee` \| `sqlserver-se` \| `sqlserver-ex` \| `sqlserver-web`  | 
|  `EngineVersion`  |  No  |  The version of the database engine\. Type: String  | 
|  `IamDatabaseAuthenticationEnabled`  |  No  |  Whether mapping of IAM accounts to database accounts is enabled\. Type: Boolean  | 
|  `InstanceCreateTime`  |  No  |  Specifies the time in Coordinated Universal Time \(UTC\) when the DB instance, from which the snapshot was taken, was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"InstanceCreateTime": "2020-06-22T17:40:12.322Z"</pre>  | 
|  `Iops`  |  No  |  The provisioned IOPS \(I/O operations per second\) value of the DB instance at the time of the snapshot\. Type: Number  | 
|  `KmsKeyId`  |  No  |  If `Encrypted` is `true`, the AWS KMS key identifier for the encrypted DB snapshot\. Type: String  | 
|  `LicenseModel`  |  No  |  License model information for the restored DB instance\. Type: String Example: <pre>"LicenseModel": "general-public-license"</pre>  | 
|  `MasterUsername`  |  No  |  The master user name for the DB snapshot\. Type: String Example:  | 
|  `OptionGroupName`  |  No  |  The option group name for the DB snapshot\. Type: String  | 
|  `PercentProgress`  |  No  |  The percentage of the estimated data that has been transferred\. Type: Number Example: <pre>"PercentProgress": 100</pre>  | 
|  `Port`  |  No  |  The port that the database engine was listening on at the time of the snapshot\. Type: Number  | 
|  ProcessorFeatures  |  No  |  The number of CPU cores and the number of threads per core for the DB instance class of the DB instance\. Type: Array of objects Example: <pre>"ProcessorFeatures": [<br />    {<br />        "Name": "coreCount",<br />        "Value": "3"<br />    }<br />]<br /></pre>  | 
|  `ProcessorFeatures.Name`  |  No  |  The name of the processor feature\. Type: String Valid values: `coreCount` \| `threadsPerCore`  | 
|  `ProcessorFeatures.Value`  |  No  |  The value of the specified processor feature\. Type: String  | 
|  `SnapshotCreateTime`  |  No  |  When the snapshot was taken in Coordinated Universal Time \(UTC\)\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. Example: <pre>"SnapshotCreateTime": "2020-06-22T17:41:29.967Z"</pre>  | 
|  `SnapshotType`  |  No  |  The type of the DB snapshot\. Type: String  | 
|  `SourceDbSnapshotIdentifier`  |  No  |  The DB snapshot ARN that the DB snapshot was copied from\. Type: String  | 
|  `SourceRegion`  |  No  |  The AWS Region that the DB snapshot was created in or copied from\. Type: String  | 
|  `Status`  |  No  |  The status of this DB snapshot\. Type: String  | 
|  `StorageType`  |  No  |  The storage type associated with DB snapshot\. Type: String Valid values: `standard` \| `gp2` \| `io1`  | 
|  `TdeCredentialArn`  |  No  |  The ARN from the key store with which to associate the instance for TDE encryption\. Type: String  | 
|  `Timezone`  |  No  |  The time zone of the DB snapshot\. Type: String  | 
|  VpcId  |  No  |  The VPC ID associated with the DB snapshot\. Type: String  | 

#### AwsS3Bucket<a name="asff-resourcedetails-awss3bucket"></a>

The `AwsS3Bucket` object provides details about an Amazon S3 bucket\.

`AwsS3Bucket` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CreatedAt`  |  No  |  Indicates when the S3 bucket was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 
|  `OwnerId`  |  No  |  The canonical user ID of the owner of the Amazon S3 bucket\. Type: String \(64 characters max\)  | 
|  `OwnerName`  |  No  | The display name of the owner of the Amazon S3 bucket\.Type: String \(128 characters max\) | 
|  `ServerSideEncryptionConfiguration`  |  No  |  The encryption rules that are applied to the S3 bucket\. Type: Object Consists of a `Rules` object, which contains the [`ApplyServerSideEncryptionByDefault`](#asff-resourcedetails-awss3bucket-applyserversideencryptionbydefault) object\.  Example: <pre>"ServerSideEncryptionConfiguration": {<br />  "Rules": [<br />    {<br />      "ApplyServerSideEncryptionByDefault": {<br />        "KMSMasterKeyID": "12345678-abcd-abcd-abcd-123456789012",<br />        "SSEAlgorithm": "aws.kms"<br />      }<br />    }<br />  ]<br />}</pre>  | 

##### ApplyServerSideEncryptionByDefault<a name="asff-resourcedetails-awss3bucket-applyserversideencryptionbydefault"></a>

Specifies the default server\-side encryption to apply to new objects in the bucket\.

`ApplyServerSideEncryptionByDefault` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `KMSMasterKeyID`  |  No  |  AWS KMS customer master key \(CMK\) ID to use for the default encryption\. Can be either the key ID or the CMK ARN\. Type: String  | 
|  `SSEAAlgorithm`  |  Yes  |  Server\-side encryption algorithm to use for the default encryption\. Type: String Valid values: `AES256` \| `aws:kms`  | 

#### AwsS3Object<a name="asff-resourcedetails-awss3object"></a>

The `AwsS3Object` object provides information about an Amazon S3 object\.

**Example**

```
"AwsS3Object": {
    "ContentType": "text/html",
    "ETag": "\"30a6ec7e1a9ad79c203d05a589c8b400\"",
    "LastModified": "2012-04-23T18:25:43.511Z",
    "ServerSideEncryption": "aws:kms",
    "SSEKMSKeyId": "arn:aws:kms:us-west-2:123456789012:key/4dff8393-e225-4793-a9a0-608ec069e5a7",
    "VersionId": "ws31OurgOOjH_HHllIxPE35P.MELYaYh"
}
```

`AWSS3Object` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `ContentType`  |  No  |  A standard MIME type describing the format of the object data\. Type: String  | 
|  `ETag`  |  No  |  The opaque identifier assigned by a web server to a specific version of a resource found at a URL\. Type: String  | 
|  `LastModified`  |  No  |  Indicates when the object was last modified\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 
|  `ServerSideEncryption`  |  No  |  If the object is stored using server\-side encryption, the value of the server\-side encryption algorithm used when storing this object in Amazon S3\. Type: String  | 
|  `SSEKMSKeyId`  |  No  |  The identifier of the AWS Key Management Service\) symmetric customer managed customer master key \(CMK\) that was used for the object\. Type: String  | 
|  `VersionId`  |  No  |  The version of the object\. Type: String  | 

#### AwsSecretsManagerSecret<a name="asff-resourcedetails-awssecretsmanagersecret"></a>

The `AwsSecretsManagerSecret` object provides details about a Secrets Manager secret\.

**Example**

```
"AwsSecretsManagerSecret": {
    "RotationRules": {
        "AutomaticallyAfterDays": 30
    },
    "RotationOccurredWithinFrequency": true,
    "KmsKeyId": "kmsKeyId",
    "RotationEnabled": true,
    "RotationLambdaArn": "arn:aws:lambda:us-west-2:777788889999:function:MyTestRotationLambda",
    "Deleted": false,
    "Name": "MyTestDatabaseSecret",
    "Description": "My test database secret"
}
```

`AwsSecretsManagerSecret` can have the following attributes\.


|  Attribute Required Description  |  |  | 
| --- | --- | --- | 
|  `Deleted`  |  No  |  Whether the secret is deleted\. Type: Boolean  | 
|  `Description`  |  No  |  The user\-provided description of the secret\. Type: String Maximum length: 2,048  | 
|  `KmsKeyId`  |  No  |  The ARN, Key ID, or alias of the AWS KMS customer master key \(CMK\) used to encrypt the `SecretString` or `SecretBinary` values for versions of this secret\. Type: String  | 
|  `Name`  |  No  |  The name of the secret\. Type: String Minimum length: 1 Maximum length: 256  | 
|  `RotationEnabled`  |  No  |  Whether rotation is enabled\. Type: Boolean  | 
|  `RotationLambdaArn`  |  No  |  The ARN of the Lambda function that rotates the secret\. Type: String  | 
|  `RotationOccurredWithinFrequency`  |  No  |  Whether the rotation occurred within the specified rotation frequency\. Type: Boolean  | 
|  `RotationRules`  |  No  |  Defines the rotation schedule for the secret\. Type: Object  | 
|  `RotationRules.AutomaticallyAfterDays`  |  No  |  The number of days after the previous rotation to rotate the secret\. Type: Integer Minimum value: 1 Maximum value: 1000  | 

#### AwsSnsTopic<a name="asff-resourcedetails-awssnstopic"></a>

The `AwsSnsTopic` object contains details about an Amazon SNS topic\.

`AwsSnsTopic` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `KmsMasterKeyId`  |  No  | The ID of an AWS managed customer master key \(CMK\) for Amazon SNS or a custom CMK\.Type: String | 
|  `Subscription`  |  No  | List of subscription endpoints of an Amazon SNS topic\.Type: Array of objects | 
|  `TopicName`  |  No  | The name of the topic\.Type: String | 
|  `Owner`  |  No  | The subscription's owner\.Type: String | 

##### Subscription<a name="asff-resourcedetails-awssnstopic-subscription"></a>

The `Subscription` object in an `AwsSnsTopic` object describes the subscription endpoints of an Amazon SNS topic\.

For each subscription endpoint, `Subscription` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Endpoint`  |  No  |  The subscription's endpoint \(format depends on the protocol\)\. Type: String  | 
|  `Protocol`  |  No  |  The subscription's protocol\. Type: String  | 

#### AwsSqsQueue<a name="asff-resourcedetails-awssqsqueue"></a>

The `AwsSqsQueue` object contains information about an Amazon SQS queue\.

`AwsSqsQueue` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `KmsDataKeyReusePeriodSeconds`  |  No  | The length of time, in seconds, for which Amazon SQS can reuse a data key to encrypt or decrypt messages before calling AWS KMS again\.Type: Integer | 
|  `KmsMasterKeyId`  |  No  | The ID of an AWS managed customer master key \(CMK\) for Amazon SQS or a custom CMK\.Type: String | 
|  `QueueName`  |  No  | The name of the new queue\.Type: String | 
|  `DeadLetterTargetArn`  |  No  | The Amazon Resource Name \(ARN\) of the dead\-letter queue to which Amazon SQS moves messages after the value of `maxReceiveCount` is exceeded\.Type: String | 

#### AwsWafWebAcl<a name="asff-resourcedetails-awswafwebacl"></a>

The `AwsWafWebAcl` object provides details about an AWS WAF web ACL\.

**Example**

```
"AwsWafWebAcl": {
    "DefaultAction": "ALLOW",
    "Name": "MyWafAcl",
    "Rules": [
        {
            "Action": {
                "Type": "ALLOW"
            },
            "ExcludedRules": [
                {
                    "RuleId": "5432a230-0113-5b83-bbb2-89375c5bfa98"
                }
            ],
            "OverrideAction": {
                "Type": "NONE"
            },
            "Priority": 1,
            "RuleId": "5432a230-0113-5b83-bbb2-89375c5bfa98",
            "Type": "REGULAR"
        }
    ],
    "WebAclId": "waf-1234567890"
}
```

An `AwsWafWebAcl` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DefaultAction`  |  Yes  |  The action to perform if none of the rules contained in the web ACL match\. The action is specified by the `WafAction` object\. Type: `WafAction` object  | 
|  `Name`  |  No  |  A friendly name or description of the web ACL\. You can't change the name of a web ACL after you create it\. Type: String Length constraints: Minimum length of 1\. Maximum length of 128\.  | 
|  [`Rules`](#asff-resourcedetails-awswafwebacl-rule)  |  Yes  |  A list of rules for the web ACL\. Type: Array of objects  | 
|  `WebAclId`  |  Yes  |  A unique identifier for a web ACL\. Type: String Length constraints: Minimum length of 1\. Maximum length of 128\.  | 

##### Rule object<a name="asff-resourcedetails-awswafwebacl-rule"></a>

The `Rules` array provides the list of rules for the web ACL\.

Each rule object in the array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Action`  |  No  |  Specifies the action that CloudFront or AWS WAF takes when a web request matches the conditions in the rule\. Type: Object  | 
|  `ExcludedRules`  |  No  |  An array of rules to exclude from a rule group\. This is applicable only when the `ActivatedRule` refers to a rule group\. Type: Array of objects  | 
|  `OverrideAction`  |  No  |  Use the `OverrideAction` to test your RuleGroup\. Any rule in a rule group can potentially block a request\. If you set the `OverrideAction` to `None`, the rule group blocks a request if any individual rule in the rule group matches the request and is configured to block that request\. However, if you first want to test the rule group, set the `OverrideAction` to `Count`\. The rule group then overrides any block action specified by individual rules contained within the group\. Instead of blocking matching requests, those requests are counted\. `ActivatedRule\|OverrideAction` applies only when updating or adding a rule group to a web ACL\. In this case, you do not use `ActivatedRule\|Action`\. For all other update requests, `ActivatedRule\|Action` is used instead of `ActivatedRule\|OverrideAction`\. Type: Object  | 
|  `Priority`  |  Yes  |  Specifies the order in which to evaluate the rules in a web ACL\. Rules with a lower value for `Priority` are evaluated before rules with a higher value\. The value must be a unique integer\. If you add multiple rules to a web ACL, the values don't need to be consecutive\. Type: Integer  | 
|  `RuleId`  |  Yes  |  The identifier for a rule\. Type: String Length constraints: Minimum length of 1\. Maximum length of 128\.  | 
|  `Type`  |  No  |  The rule type, either `REGULAR`,` RATE_BASED`, or `GROUP`\. The default is `REGULAR`\. Type: String Valid values: `REGULAR` \| `RATE_BASED` \| `GROUP`  | 

Each action can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Type`  |  No  |  Specifies how you want AWS WAF to respond to requests that match the settings in a rule\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Type: String Valid values: `BLOCK` \| `ALLOW` \| `COUNT`  | 

Each excluded rule can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `RuleId`  |  Yes  |  The unique identifier for the rule to exclude from the rule group\. Type: String Length constraints: Minimum length of 1\. Maximum length of 128\.  | 

Each override action for a rule can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Type`  |  Yes  |  `COUNT` overrides the action specified by the individual rule within a rule group\. If set to `NONE`, the rule's action takes place\. Type: String Valid values: `NONE` \| `COUNT`  | 

#### Container<a name="asff-resourcedetails-container"></a>

Container details that are related to a finding\. 

Type: Object

Example:

```
"Container": {
    "Name": "Secret Service Container",
    "ImageId": "image12",
    "ImageName": "SecSvc v1.2 Image",
    "LaunchedAt": "2018-09-29T01:25:54Z"
}
```

The `Container` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `ImageId`  |  No  | The identifier of the image that is related to a finding\.Type: String \(128 characters max\) | 
|  `ImageName`  |  No  | The name of the image that is related to a finding\.Type: String \(128 characters max\) | 
|  `LaunchedAt`  |  No  | Indicates when the container was started\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. | 
|  `Name`  |  No  | The name of the container that is related to a finding\.Type: String \(128 characters max\) | 

#### Other<a name="asff-resourcedetails-other"></a>

The `Other` subfield allows you to provide custom fields and values\. You use the `Other` subfield in the following cases\.
+ The resource type does not have a corresponding subfield\. To provide details for the resource, you use the `Other` subfield\.
+ The subfield for the resource type does not include all of the fields you want to populate\. In this case, use the subfield for the resource type to populate the available fields\. Use the `Other` subfield to populate the fields that are not in the type\-specific subfield\.
+ The resource type is not one of the provided types\. In this case, you set `Resource.Type` to `Other`, and use the `Other` subfield to populate the details\.

Type: Map of up to 50 key\-value pairs

Each key\-value pair must meet the following requirements\.
+ The key must contain fewer than 128 characters\.
+ The value must contain fewer than 1,024 characters\.

### Severity<a name="asff-severity"></a>

Details about the severity of the finding\.

The finding provider can provide the initial severity, but cannot update it after that\. The severity can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

The finding severity does not consider the criticality of the involved assets or the underlying resource\. Criticality is defined as the level of importance of the resources that are associated with the finding\. For example, a resource that is associated with a mission critical application versus one that is associated with nonproduction testing\. To capture information about resource criticality, use the `Criticality` field\.

The finding must have either `Label` or `Normalized` populated\. If neither attribute is populated, then the finding is invalid\. `Label` is the preferred attribute\.

The `Severity` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Label`  |  No  |  The severity value for the finding\. Type: Enum Available values: `INFORMATIONAL` \| `LOW` \| `MEDIUM` \| `HIGH` \|`CRITICAL` At a high level, the `Label` values can be interpreted as follows\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 
|  `Normalized` \(To be deprecated\)  |  No  |  The normalized severity of a finding\. We plan to deprecate this attribute\. Instead of `Normalized`, provide `Label`\. Type: Integer The value of `Normalized` must be an integer between 0 and 100\. Zero means that no severity applies, and 100 means that the finding has the maximum possible severity\. For guidance on setting the value of `Normalized`, see [Guidance for assigning the normalized severity \(AWS services and partners\)](#asff-severity-normalized-guidance)\.  | 
|  `Original`  |  No  |  The native severity from the finding product that generated the finding\. Type: String \(maximum 64 characters\)  | 
|  `Product` \(Deprecated\)  |  No  |  The native severity as defined by the finding product that generated the finding\. This is deprecated in favor of `Original`\. Type: Number \(single\-precision 32\-bit IEEE 754 floating point number, restricted to finite values\)  | 

#### How Security Hub maps Label and Normalized values<a name="asff-severity-map-normalized-label"></a>

If a [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) request for a new finding only provides `Label` or only provides `Normalized`, then Security Hub automatically populates the value of the other field\.

Security Hub does not make any automatic updates based on changes from [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

If [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) provides `Normalized` and does not provide `Label`, `Label` is set automatically as follows\.


|  Normalized  |  Label  | 
| --- | --- | 
|  0  |  `INFORMATIONAL`  | 
|  1–39  |  `LOW`  | 
|  40–69  |  `MEDIUM`  | 
|  70–89  |  `HIGH`  | 
|  90–100  |  `CRITICAL`  | 

If [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) only provides `Label` and does not provide `Normalized`, `Normalized` is set automatically as follows\.


|  Label  |  Normalized  | 
| --- | --- | 
|  `INFORMATIONAL`  |  0  | 
|  `LOW`  |  1  | 
|  `MEDIUM`  |  40  | 
|  `HIGH`  |  70  | 
|  `CRITICAL`  |  90  | 

#### Guidance for assigning the normalized severity \(AWS services and partners\)<a name="asff-severity-normalized-guidance"></a>

For findings generated by AWS services and third\-party partner products, the severity is based on the following\.
+ **Most severe** – Findings that are associated with actual data loss or denial of service
+ **Second\-most severe** – Findings that are associated with an active compromise but that do not indicate that data loss or other negative effects have occurred
+ **Third\-most severe** – Findings that are associated with issues that indicate potential for a future compromise

We recommend that you use the following guidance when translating findings' native severity scores to a normalized severity for the ASFF\.
+ Informational findings\. For example, a finding for a passed check or a sensitive data identification\.

  Suggested score: 0
+ Findings that are associated with issues that could result in future compromises\. For example, vulnerabilities, configuration weaknesses, exposed passwords\.

  This generally aligns to the `Software and Configuration Checks` namespace under a finding's type\.

  Suggested score: 1–39 \(Low\)
+ Findings that are associated with issues that indicate an active compromise, but no indication that an adversary completed their objectives\. For example, malware activity, hacking activity, or unusual behavior detection\.

  This generally aligns to the `Threat Detections and Unusual Behavior` namespaces under a finding's type\.

  Suggested score: 40–69 \(Medium\)
+ Findings that indicate that an adversary completed their objectives, such as active data loss or compromise or a denial of service\.

  This generally aligns to the `Effects` namespace under a finding's type\.

  Suggested score: 70–100 \(High or Critical\)

### ThreatIntelIndicators<a name="asff-threatintelindicators"></a>

Threat intelligence details that are related to a finding\.

Type: Array of up to five threat intelligence indicator objects

**Example**

```
"ThreatIntelIndicators": [
  {
    "Type": "IPV4_ADDRESS",
    "Value": "8.8.8.8",
    "Category": "BACKDOOR",
    "LastObservedAt": "2018-09-27T23:37:31Z",
    "Source": "Threat Intel Weekly",
    "SourceUrl": "http://threatintelweekly.org/backdoors/8888"
  }
]
```

Each threat intelligence indicator object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Category`  |  No  | The category of a threat intel indicator\.Type: Enum Valid values: `BACKDOOR` \| `CARD_STEALER` \| `COMMAND_AND_CONTROL` \| `DROP_SITE` \| `EXPLOIT_SITE` \| `KEYLOGGER` | 
|  `LastObservedAt`  |  No  | Indicates when the threat intelligence indicator was last observed\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\. | 
|  `Source`  |  No  | The source of the threat intelligence\.Type: String \(64 characters max\) | 
|  `SourceUrl`  |  No  | The URL for more details from the source of the threat intelligence\.Type: URL | 
|  `Type`  |  No  | The type of a threat intelligence indicator\.Type: Enum Valid values: `DOMAIN` \| `EMAIL_ADDRESS` \| `HASH_MD5` \| `HASH_SHA1` \| `HASH_SHA256` \|` HASH_SHA512` \| `IPV4_ADDRESS` \| `IPV6_ADDRESS` \| `MUTEX` \| `PROCESS` \| `URL` | 
|  `Value`  |  No  | The value of a threat intelligence indicator\.Type: String \(512 characters max\) | 

### Vulnerabilities<a name="asff-vulnerabilities"></a>

The `Vulnerabilities` object provides a list of vulnerabilities that are associated with the findings\.

**Example**

```
"Vulnerabilities" : [
    {
        "Cvss": [
            {
                "BaseScore": 4.7,
                "BaseVector": "AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N",
                "Version": "V3"
            },
            {
                "BaseScore": 4.7,
                "BaseVector": "AV:L/AC:M/Au:N/C:C/I:N/A:N",
                "Version": "V2"
            }
        ],
        "Id": "CVE-2020-12345",
        "ReferenceUrls":[
           "http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-12418",
            "http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-17563"
        ],
        "RelatedVulnerabilities": ["CVE-2020-12345"],
        "Vendor": {
            "Name": "Alas",
            "Url":"https://alas.aws.amazon.com/ALAS-2020-1337.html",
            "VendorCreatedAt":"2020-01-16T00:01:43Z",
            "VendorSeverity":"Medium",
            "VendorUpdatedAt":"2020-01-16T00:01:43Z"
        },
        "VulnerablePackages": [
            {
                "Architecture": "x86_64",
                "Epoch": "1",
                "Name": "openssl",
                "Release": "16.amzn2.0.3",
                "Version": "1.0.2k"
            }
        ]
    }
]
```

Each vulnerability can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`Cvss`](#asff-vulnerabilities-cvss)  |  No  |  Common Vulnerability Scoring System \(CVSS\) scores from the advisory that are related to the vulnerability\. Type: Array of objects  | 
|  `Id`  |  Yes  |  The identifier of the vulnerability\. Type: String \(32 characters max\)  | 
|  `ReferenceUrls`  |  No  |  A list of URLs that provide additional information about the vulnerability\. Type: Array of strings  | 
|  `RelatedVulnerabilities`  |  No  |  List of vulnerabilities that are related to this vulnerability\. For each vulnerability, provide the vulnerability ID\. Type: Array of strings  | 
|  [`Vendor`](#asff-vulnerabilities-vendor)  |  No  |  Information about the vendor that generates the vulnerability report\. Type: Object  | 
|  [`VulnerablePackages`](#asff-vulnerabilities-vulnerablepackages)  |  No  |  List of packages that have the vulnerability\. Type: Array of objects  | 

#### Cvss<a name="asff-vulnerabilities-cvss"></a>

The `Cvss` object provides a list of CVSS scores for the vulnerability\.

Each `CVSS` score can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `BaseScore`  |  No  |  The base CVSS score\. Type: Number  | 
|  `BaseVector`  |  No  |  The base scoring vector for the CVSS score\. Type: String  | 
|  `Version`  |  No  |  The version of CVSS for the CVSS score\. Type: String  | 

#### Vendor<a name="asff-vulnerabilities-vendor"></a>

The `Vendor` object provides information about the vendor that generated the vulnerability advisory for the vulnerability\.

The `Vendor` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Name`  |  Yes  |  The name of the vendor\. Type: String \(32 characters max\)  | 
|  `Url`  |  No  |  The URL of the vulnerability advisory\. Type: String  | 
|  `VendorCreatedAt`  |  No  |  Indicates when the vulnerability advisory was created\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 
|  `VendorSeverity`  |  No  |  The severity that the vendor assigned to the vulnerability\. Type: String \(32 characters max\)  | 
|  `VendorUpdatedAt`  |  No  |  Indicates when the vulnerability advisory was last updated\. Type: String Format: Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  | 

#### VulnerablePackages<a name="asff-vulnerabilities-vulnerablepackages"></a>

The `VulnerablePackages` object provides the list of packages that have the vulnerability\.

Each package can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Architecture`  |  No  |  The architecture used for the vulnerable package\. Type: String  | 
|  `Epoch`  |  No  |  The epoch for the vulnerable package\. Type: String  | 
|  `Name`  |  No  |  The name of the vulnerable package\. Type: String  | 
|  `Release`  |  No  |  The release for the vulnerable package\. Type: String  | 
|  `Version`  |  No  |  The version of the vulnerable package\. Type: String  | 

### Workflow<a name="asff-workflow"></a>

The `Workflow` object provides information about the status of the investigation into a finding\.

It is not intended for finding providers\. It is only to be used by customers and by remediation, orchestration, and ticketing tools used by customers\.

The workflow status can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Customers can also update it from the console\. See [Setting the workflow status for findings](finding-workflow-status.md)\. 

`Workflow` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Status`  |  No  |  The status of the investigation into the finding\. Type: Enum Valid values: `NEW` \| `NOTIFIED` \| `RESOLVED` \| `SUPPRESSED` [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 

## Types taxonomy for ASFF<a name="securityhub-findings-format-type-taxonomy"></a>

The following information describes the first three levels of the `Types` path\. In the list, the top\-level bullets are namespaces, the second\-level bullets are categories, and the third\-level bullets are classifiers\. Only the Software and Configuration Checks namespace has defined classifiers\.
+ Namespaces
  + Categories
    + Classifiers

Finding providers must use the defined namespaces\. The defined categories and classifiers are recommended for use, but are not required\.

A finding provider might define a partial path for namespace/category/classifier\. For example, the following finding types are all valid\.
+ TTPs
+ TTPs/Defense Evasion
+ TTPs/Defense Evasion/CloudTrailStopped

TTPs stands for tactics, techniques, and procedures\. The TTP categories in the following list align to the [MITRE ATT&CK MatrixTM](https://attack.mitre.org/matrices/enterprise/)\. Unusual Behaviors reflect general unusual behavior, such as general statistical anomalies, and are not aligned with a specific TTP\. However, you could classify a finding with both Unusual Behaviors and TTPs finding types\.
+ Software and Configuration Checks
  + Vulnerabilities
    + CVE
  + AWS Security Best Practices
    + Network Reachability
    + Runtime Behavior Analysis
  + Industry and Regulatory Standards
    + CIS Host Hardening Benchmarks
    + CIS AWS Foundations Benchmark
    + PCI\-DSS Controls
    + Cloud Security Alliance Controls
    + ISO 90001 Controls
    + ISO 27001 Controls
    + ISO 27017 Controls
    + ISO 27018 Controls
    + SOC 1
    + SOC 2
    + HIPAA Controls \(USA\)
    + NIST 800\-53 Controls \(USA\)
    + NIST CSF Controls \(USA\)
    + IRAP Controls \(Australia\)
    + K\-ISMS Controls \(Korea\)
    + MTCS Controls \(Singapore\)
    + FISC Controls \(Japan\)
    + My Number Act Controls \(Japan\)
    + ENS Controls \(Spain\)
    + Cyber Essentials Plus Controls \(UK\)
    + G\-Cloud Controls \(UK\)
    + C5 Controls \(Germany\)
    + IT\-Grundschutz Controls \(Germany\)
    + GDPR Controls \(Europe\)
    + TISAX Controls \(Europe\)
+ TTPs
  + Initial Access
  + Execution
  + Persistence
  + Privilege Escalation
  + Defense Evasion
  + Credential Access
  + Discovery
  + Lateral Movement
  + Collection
  + Command and Control
+ Effects
  + Data Exposure
  + Data Exfiltration 
  + Data Destruction 
  + Denial of Service 
  + Resource Consumption
+ Unusual Behaviors
  + Application
  + Network Flow
  + IP address
  + User
  + VM
  + Container
  + Serverless
  + Process
  + Database
  + Data 
+ Sensitive Data Identifications
  + PII
  + Passwords
  + Legal
  + Financial
  + Security
  + Business