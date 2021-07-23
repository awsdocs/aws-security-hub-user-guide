# ASFF syntax<a name="securityhub-findings-format-syntax"></a>

The following is the complete JSON syntax for the AWS Security Finding Format \(ASFF\)\.

```
"Findings": [ 
    {
        "Action": {
            "ActionType": "string",
            "AwsApiCallAction": {
                "AffectedResources": {
                    "string": "string" 
                },
                "Api": "string",
                "CallerType": "string",
                "DomainDetails": {
                    "Domain": "string"
                },
                "FirstSeen": "string",
                "LastSeen": "string",
                "RemoteIpDetails": {
                    "City": {
                        "CityName": "string"
                    },
                    "Country": {
                        "CountryCode": "string",
                        "CountryName": "string"
                    },
                    "IpAddressV4": "string",
                    "Geolocation": {
                        "Lat": number,
                        "Lon": number
                    },
                    "Organization": {
                        "Asn": number,
                        "AsnOrg": "string",
                        "Isp": "string",
                        "Org": "string"
                    }
                },
                "ServiceName": "string"   
            },
            "DnsRequestAction": {
                "Blocked": boolean,
                "Domain": "string",
                "Protocol": "string"
            },
            "NetworkConnectionAction": {
                "Blocked": boolean,
                "ConnectionDirection": "string",
                "LocalPortDetails": {
                    "Port": number,
                    "PortName": "string"
                },
                "Protocol": "string",
                "RemoteIpDetails": {
                    "City": {
                        "CityName": "string"
                    },
                    "Country": {
                        "CountryCode": "string",
                        "CountryName": "string"
                    },
                    "IpAddressV4": "string",
                    "Geolocation": {
                        "Lat": number,
                        "Lon": number
                    },
                    "Organization": {
                        "Asn": number,
                        "AsnOrg": "string",
                        "Isp": "string",
                        "Org": "string"
                    }
                },
                "RemotePortDetails": {
                    "Port": number,
                    "PortName": "string"
                }
            },
            "PortProbeAction": {
                "Blocked": boolean,
                "PortProbeDetails": [
                    {
                        "LocalIpDetails": {
                            "IpAddressV4": "string"
                        },
                        "LocalPortDetails": {
                            "Port": number,
                            "PortName": "string"
                        },
                        "RemoteIpDetails": {
                            "City": {
                                "CityName": "string"
                            },
                            "Country": {
                                "CountryCode": "string",
                                "CountryName": "string"
                            },
                            "GeoLocation": {
                                "Lat": number,
                                "Lon": number
                            },
                            "IpAddressV4": "string",
                            "Organization": {
                                 "Asn": number,
                                 "AsnOrg": "string",
                                 "Isp": "string",
                                 "Org": "string"
                            }
                        }
                    }
                ]
            }
        },
        "AwsAccountId": "string",
        "CompanyName": "string",
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
        "FindingProviderFields": {
            "Confidence": number,
            "Criticality": number,
            "RelatedFindings":[
                {
                    "ProductArn": "string", 
                    "Id": "string" 
                }
            ],
            "Severity": {
                "Label": "string", 
                "Original": "string"
            },
            "Types": [ "string" ]
        },
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
        "NetworkPath": [
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
        "PatchSummary": {
            "FailedCount": number,
            "Id": "string",
            "InstalledCount": number,
            "InstalledOtherCount": number,
            "InstalledPendingReboot": number,
            "InstalledRejectedCount": number,
            "MissingCount": number,
            "Operation": "string",
            "OperationEndTime": "string",
            "OperationStartTime": "string",
            "RebootOption": "string"
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
            "string": "string" 
        },
        "ProductName": "string",
        "RecordState": "string",
        "Region": "string",
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
                "DataClassification": {
                    "DetailedResultsLocation": "string",
                    "Result": {
                        "AdditionalOccurrences": boolean,
                        "CustomDataIdentifiers": {
                            "Detections": [
                                {
                                    "Arn": "string",
                                    "Count": integer,
                                    "Name": "string",
                                    "Occurrences": {
                                        "Cells": [
                                            {
                                                "CellReference": "string",
                                                "Column": integer,
                                                "ColumnName": "string",
                                                "Row": integer
                                            }
                                        ],
                                        "LineRanges": [
                                            {
                                                "End": integer,
                                                "Start": integer,
                                                "StartColumn": integer
                                             }
                                         ],
                                        "OffsetRanges": [
                                            {
                                                "End": integer,
                                                "Start": integer,
                                                "StartColumn": integer
                                            }
                                        ],
                                        "Pages": [
                                            {
                                                "LineRange": {
                                                    "End": integer,
                                                    "Start": integer,
                                                    "StartColumn": integer
                                                },
                                                "OffsetRange": {
                                                    "End": integer,
                                                    "Start": integer,
                                                    "StartColumn": integer
                                                },
                                                "PageNumber": integer
                                            }
                                        ],
                                        "Records": [
                                            {
                                               "JsonPath": "string",
                                               "RecordIndex": integer
                                            }
                                        ]
                                    }
                                }
                            ],
                            "TotalCount": integer
                        },
                        "MimeType": "string",
                        "SensitiveData": [
                            {
                                "Category": "string",
                                "Detections": [
                                    {
                                        "Count": integer,
                                        "Occurrences": {
                                            "Cells": [
                                                {
                                                    "CellReference": "string",
                                                    "Column": integer,
                                                    "ColumnName": "string",
                                                    "Row": integer
                                                }
                                            ],
                                            "LineRanges": [
                                                {
                                                    "End": integer,
                                                    "Start": integer,
                                                    "StartColumn": integer
                                                }
                                            ],
                                            "OffsetRanges": [
                                                {
                                                    "End": integer,
                                                    "Start": integer,
                                                    "StartColumn": integer
                                                }
                                            ],
                                            "Pages": [
                                                {
                                                    "LineRange": {
                                                        "End": integer,
                                                        "Start": integer,
                                                        "StartColumn": integer
                                                    },
                                                    "OffsetRange": {
                                                        "End": integer,
                                                        "Start": integer,
                                                        "StartColumn": integer
                                                    },
                                                    "PageNumber": integer
                                                }
                                            ],
                                            "Records": [
                                                {
                                                    "JsonPath": "string",
                                                    "RecordIndex": integer
                                                }
                                            ]
                                        },
                                        "Type": "string"
                                    }
                                ],
                                "TotalCount": integer
                            }
                        ],
                        "SizeClassified": integer,
                        "Status": {
                            "Code": "string",
                            "Reason": "string"
                        }
                    }
                },
                "Details": { 
                    "AwsApiGatewayRestApi": {
                        "ApiKeySource": "string",
                        "BinaryMediaTypes": [" string" ],
                        "CreatedDate": "string",
                        "Description": "string",
                        "EndpointConfiguration": {
                            "Types": [ "string" ]
                        },
                        "Id": "string",
                        "MinimumCompressionSize": number,
                        "Name": "string",
                        "Version": "string"
                    },
                    "AwsApiGatewayStage": {
                        "AccessLogSettings": {
                            "DestinationArn": "string",
                            "Format": "string"
                        },
                        "CacheClusterEnabled": boolean,
                        "CacheClusterSize": "string",
                        "CacheClusterStatus": "string",
                        "CanarySettings": {
                            "DeploymentId": "string",
                            "PercentTraffic": number,
                            "StageVariableOverrides": [
                                {
                                    "string": "string"
                                }
                            ],
                            "UseStageCache": boolean
                        },
                        "ClientCertificateId": "string", 
                        "CreatedDate": "string",
                        "DeploymentId": "string",
                        "Description": "string",
                        "DocumentationVersion": "string",
                        "LastUpdatedDate": "string",
                        "MethodSettings": [
                            {
                                "CacheDataEncrypted": boolean,
                                "CachingEnabled": boolean,
                                "CacheTtlInSeconds": number,
                                "DataTraceEnabled": boolean,
                                "HttpMethod": "string",
                                "LoggingLevel": "string",
                                "MetricsEnabled": boolean,
                                "RequireAuthorizationForCacheControl": boolean,
                                "ResourcePath": "string",
                                "ThrottlingBurstLimit": number,
                                "ThrottlingRateLimit": number,
                                "UnauthorizedCacheControlHeaderStrategy": "string"
                            }
                        ],
                        "StageName": "string",
                        "TracingEnabled": boolean,
                        "Variables": {
                            "string": "string"
                        },
                        "WebAclArn": "string"
                    },
                    "AwsApiGatewayV2Api": {
                        "ApiEndpoint": "string",
                        "ApiId": "string",
                        "ApiKeySelectionExpression": "string",
                        "CorsConfiguration": {
                            "AllowCredentials": boolean,
                            "AllowHeaders": [ "string" ],
                            "AllowMethods": [ "string" ],
                            "AllowOrigins": [ "string" ],
                            "ExposeHeaders": [ "string" ],
                            "MaxAge": number
                        },
                        "CreatedDate": "string",
                        "Description": "string",
                        "Name": "string",
                        "ProtocolType": "string",
                        "RouteSelectionExpression": "string",
                        "Version": "string"
                    },
                    "AwsApiGatewayV2Stage": {
                        "AccessLogSettings": {
                            "DestinationArn": "string",
                            "Format": "string"
                        },
                        "ApiGatewayManaged": boolean,
                        "AutoDeploy": boolean,
                        "ClientCertificateId": "string",
                        "CreatedDate": "string",
                        "DefaultRouteSettings": {
                            "DataTraceEnabled": boolean,
                            "DetailedMetricsEnabled": boolean,
                            "LoggingLevel": "string",
                            "ThrottlingBurstLimit": number,
                            "ThrottlingRateLimit": number
                        },
                        "DeploymentId": "string",
                        "Description": "string",
                        "LastDeploymentStatusMessage": "string",
                        "LastUpdatedDate": "string",
                        "RouteSettings": {
                            "DetailedMetricsEnabled": boolean,
                            "LoggingLevel": "string",
                            "DataTraceEnabled": boolean,
                            "ThrottlingBurstLimit": number,
                            "ThrottlingRateLimit": number
                        },
                        "StageName": "string",
                        "StageVariables": [
                            {
                                "string": "string"
                            }
                        ]
                    },
                    "AwsAutoScalingAutoScalingGroup": {
                        "CreatedTime": "string",
                        "HealthCheckGracePeriod": integer,
                        "HealthCheckType": "string",
                        "LaunchConfigurationName": "string",
                        "LoadBalancerNames": ["string"]
                    },
                    "AwsCertificateManagerCertificate": {
                        "CertificateAuthorityArn": "string",
                        "CreatedAt": "string",
                        "DomainName": "string",
                        "DomainValidationOptions": [
                            {
                                "DomainName": "string",
                                "ResourceRecord": {
                                    "Name": "string",
                                    "Type": "string",
                                    "Value": "string"
                                },
                                "ValidationDomain": "string",
                                "ValidationEmails": [ "string" ],
                                "ValidationMethod": "string",
                                "ValidationStatus": "string"
                            }
                        ],
                        "ExtendedKeyUsages": [
                            {
                                "Name": "string",
                                "OId": "string"
                            }
                        ],
                        "FailureReason": "string",
                        "ImportedAt": "string",
                        "InUseBy": [ "string" ],
                        "IssuedAt": "string",
                        "Issuer": "string",
                        "KeyAlgorithm": "string",
                        "KeyUsages": [
                            {
                                "Name": "string"
                            }
                        ],
                        "NotAfter": "string",
                        "NotBefore": "string",
                        "Options": {
                            "CertificateTransparencyLoggingPreference": "string"
                        },
                        "RenewalEligibility": "string",
                        "RenewalSummary": {
                            "DomainValidationOptions": [
                                {
                                    "DomainName": "string",
                                    "ResourceRecord": {
                                        "Name": "string",
                                        "Type": "string",
                                        "Value": "string"
                                    },
                                    "ValidationDomain": "string",
                                    "ValidationEmails": [ "string" ],
                                    "ValidationMethod": "string",
                                    "ValidationStatus": "string"
                                }
                            ],
                            "RenewalStatus": "string",
                            "RenewalStatusReason": "string",
                            "UpdatedAt": "string"
                        },
                        "Serial": "string",
                        "SignatureAlgorithm": "string",
                        "Status": "string",
                        "Subject": "string",
                        "SubjectAlternativeNames": [ "string" ],
                        "Type": "string"
                    },
                    "AwsCloudFrontDistribution": {
                        "CacheBehaviors": {
                            "Items": [
                                {
                                    "ViewerProtocolPolicy": "string"
                                }
                            ]
                        },
                        "DefaultCacheBehavior": {
                            "ViewerProtocolPolicy": "string"
                        },
                        "DefaultRootObject": "string",
                        "DomainName": "string",
                        "Etag": "string",
                        "LastModifiedTime": "string",
                        "Logging": {
                            "Bucket": "string",
                            "Enabled": boolean,
                            "IncludeCookies": boolean,
                            "Prefix": "string"
                        },
                        "OriginGroups": {
                            "Items": [
                                {
                                    "FailoverCriteria": {
                                        "StatusCodes": {
                                            "Items": [ number ],
                                            "Quantity": number
                                         }
                                    }
                                }
                            ]
                        },
                        "Origins": {
                            "Items": [
                                {
                                    "DomainName": "string",
                                    "Id": "string",
                                    "OriginPath": "string",
                                    "S3OriginConfig": {
                                        "OriginAccessIdentity": "string"
                                    }
                                }
                            ]
                        },
                        "Status": "string",
                        "WebAclId": "string"
                    },
                    "AwsCloudTrailTrail": {
                        "CloudWatchLogsLogGroupArn": "string",
                        "CloudWatchLogsRoleArn": "string",
                        "HasCustomEventSelectors": boolean,
                        "HomeRegion": "string",
                        "IncludeGlobalServiceEvents": boolean,
                        "IsMultiRegionTrail": boolean,
                        "IsOrganizationTrail": boolean,
                        "KmsKeyId": "string",
                        "LogFileValidationEnabled": boolean,
                        "Name": "string",
                        "S3BucketName": "string",
                        "S3KeyPrefix": "string",
                        "SnsTopicArn": "string",
                        "SnsTopicName": "string",
                        "TrailArn": "string"
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
                        "BillingModeSummary": {
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
                                }
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
                                    }
                                ],
                                "KmsMasterKeyId": "string",
                                "ProvisionedThroughputOverride": {
                                    "ReadCapacityUnits": number
                                },
                                "RegionName": "string",
                                "ReplicaStatus": "string",
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
                        "NetworkInterfaces": [
                            {
                                "NetworkInterfaceId": "string"
                            }
                        ],
                        "SubnetId": "string",
                        "Type": "string",
                        "VpcId": "string"
                    },
                    "AwsEc2NetworkAcl": {
                        "Associations": [
                            {
                                "NetworkAclAssociationId": "string",
                                "NetworkAclId": "string",
                                "SubnetId": "string"
                           }
                        ],
                        "Entries": [
                            {
                                "CidrBlock": "string",
                                "Egress": boolean,
                                "IcmpTypeCode": {
                                    "Code": number,
                                    "Type": number
                                },
                                "Ipv6CidrBlock": "string",
                                "PortRange": {
                                    "From": number,
                                    "To": number
                                },
                                "Protocol": "string",
                                "RuleAction": "string",
                                "RuleNumber": number
                           }
                        ],
                        "IsDefault": boolean,
                        "NetworkAclId": "string",
                        "OwnerId": "string",
                        "VpcId": "string"
                    },
                    "AwsEc2NetworkInterface": {
                        "Attachment": {
                            "AttachmentId": "string",
                            "AttachTime": "string",
                            "DeleteOnTermination": boolean,
                            "DeviceIndex": number,
                            "InstanceId": "string",
                            "InstanceOwnerId": "string",
                            "Status": "string"
                        },
                        "Ipv6Addresses": [
                            {
                                "Ipv6Address": "string"
                            }
                        ],
                        "NetworkInterfaceId": "string",
                        "PrivateIpAddresses": [
                            {
                                "PrivateDnsName": "string",
                                "PrivateIpAddress": "string"
                            }
                        ],
                        "PublicDnsName": "string",
                        "PublicIp": "string",
                        "SecurityGroups": [
                            {
                                "GroupId": "string",
                                "GroupName": "string"
                            }
                        ],
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
                                "Ipv6Ranges": [
                                    {
                                        "CidrIpv6": "string"
                                    }
                                ],                                
                                "PrefixListIds": [
                                    {"PrefixListId": "string"}
                                ],
                                "ToPort": number,
                                "UserIdGroupPairs": [
                                    {
                                        "GroupId": "string",
                                        "GroupName": "string",
                                        "PeeringStatus": "string",
                                        "UserId": "string",
                                        "VpcId": "string",
                                        "VpcPeeringConnectionId": "string"
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
                                "Ipv6Ranges": [
                                    {
                                        "CidrIpv6": "string"
                                    }
                                ],                                
                                "PrefixListIds": [
                                    {"PrefixListId": "string"}
                                ],
                                "ToPort": number,
                                "UserIdGroupPairs": [
                                    {
                                        "GroupId": "string",
                                        "GroupName": "string",
                                        "PeeringStatus": "string",
                                        "UserId": "string",
                                        "VpcId": "string",
                                        "VpcPeeringConnectionId": "string"
                                    }
                                ]
                            }
                        ],
                        "OwnerId": "string",
                        "VpcId": "string"
                    },
                    "AwsEc2Subnet": {
                        "AssignIpv6AddressOnCreation": boolean,
                        "AvailabilityZone": "string",
                        "AvailabilityZoneId": "string",
                        "AvailableIpAddressCount": number,
                        "CidrBlock": "string",
                        "DefaultForAz": boolean,
                        "Ipv6CidrBlockAssociationSet": [
                            {
                                "AssociationId": "string",
                                "Ipv6CidrBlock": "string",
                                "CidrBlockState": "string"
                            }
                        ],
                        "MapPublicIpOnLaunch": boolean,
                        "OwnerId": "string",
                        "State": "string",
                        "SubnetArn": "string",
                        "SubnetId": "string",
                        "VpcId": "string"
                    },
                    "AwsEc2Volume": {
                         "Attachments": [
                            {
                                "AttachTime": "string",
                                "DeleteOnTermination": boolean,
                                "InstanceId": "string",
                                "Status": "string"
                           }
                          ],
                          "CreateTime": "string",
                          "Encrypted": boolean,
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
                    "AwsEcsCluster": {
                        "CapacityProviders": ["string"],
                        "ClusterSettings": [
                            {
                                "Name": "string",
                                "Value": "string"
                            }
                        ],
                        "Configuration": {
                            "ExecuteCommandConfiguration": {
                                "KmsKeyId": "string",
                                "LogConfiguration": {
                                    "CloudWatchEncryptionEnabled": boolean,
                                    "CloudWatchLogGroupName": "string",
                                    "S3BucketName": "string",
                                    "S3EncryptionEnabled": boolean,
                                    "S3KeyPrefix": "string"
                                },
                                "Logging": "string"
                            }
                        },
                        "DefaultCapacityProviderStrategy": [
                            {
                                "Base": number,
                                "CapacityProvider": "string",
                                "Weight": number
                            }
                        ]
                    },
                    "AwsEcsService": {
                        "CapacityProviderStrategy": [
                            {
                                "Base": number,
                                "CapacityProvider": "string",
                                "Weight": number
                            }
                        ],
                        "Cluster": "string",
                        "DeploymentConfiguration": {
                            "DeploymentCircuitBreaker": {
                                "Enable": boolean,
                                "Rollback": boolean
                            },
                            "MaximumPercent": number,
                            "MinimumHealthyPercent": number
                        },
                        "DeploymentController": {
                            "Type": "string"
                        },
                        "DesiredCount": number,
                        "EnableEcsManagedTags": boolean,
                        "EnableExecuteCommand": boolean,
                        "HealthCheckGracePeriodSeconds": number,
                        "LaunchType": "string",
                        "LoadBalancers": [
                            {
                                "ContainerName": "string",
                                "ContainerPort": number,
                                "LoadBalancerName": "string",
                                "TargetGroupArn": "string"
                            }
                        ],
                        "Name": "string",
                        "NetworkConfiguration": {
                            "AwsVpcConfiguration": {
                                "AssignPublicIp": "string",
                                "SecurityGroups": ["string"],
                                "Subnets": ["string"]
                            }
                        },
                        "PlacementConstraints": [
                            {
                                "Expression": "string",
                                "Type": "string"
                            }
                        ],
                        "PlacementStrategies": [
                            {
                                "Field": "string",
                                "Type": "string"
                            }
                        ],
                        "PlatformVersion": "string",
                        "PropagateTags": "string",
                        "Role": "string",
                        "SchedulingStrategy": "string",
                        "ServiceArn": "string",
                        "ServiceName": "string",
                        "ServiceRegistries": [
                            {
                                "ContainerName": "string",
                                "ContainerPort": number,
                                "Port": number,
                                "RegistryArn": "string"
                            }
                        ],
                        "TaskDefinition": "string"
                    },                    
                    "AwsEcsTaskDefinition": {
                        "ContainerDefinitions": [
                            {
                                "Command": ["string"],
                                "Cpu": number,
                                "DependsOn": [
                                    {
                                        "Condition": "string",
                                        "ContainerName": "string"
                                    }
                                ],
                                "DisableNetworking": boolean,
                                "DnsSearchDomains": ["string"],
                                "DnsServers": ["string"],
                                "DockerLabels": {"string": "string"},
                                "DockerSecurityOptions": ["string"],
                                "EntryPoint": ["string"],
                                "Environment": [
                                    {
                                        "Name": "string",
                                        "Value": "string"
                                    }
                                ],
                                "EnvironmentFiles": [
                                    {
                                        "Type": "string",
                                        "Value": "string"
                                    }
                                ],
                                "Essential": boolean,
                                "ExtraHosts": [
                                    {
                                        "Hostname": "string",
                                        "IpAddress": "string"
                                    }
                                ],
                                "FirelensConfiguration": {
                                    "Options": {"string": "string"},
                                    "Type": "string"
                                },
                                "HealthCheck": {
                                    "Command": ["string"],
                                    "Interval": number,
                                    "Retries": number,
                                    "StartPeriod": number,
                                    "Timeout": number
                                },
                                "Hostname": "string",
                                "Image": "string",
                                "Interactive": boolean,
                                "Links": ["string"],
                                "LinuxParameters": {
                                    "Capabilities": {
                                        "Add": ["string"],
                                        "Drop": ["string"]
                                    },
                                    "Devices": [
                                        {
                                            "ContainerPath": "string",
                                            "HostPath": "string",
                                            "Permissions": ["string"]
                                        }
                                    ],
                                    "InitProcessEnabled": boolean,
                                    "MaxSwap": number,
                                    "SharedMemorySize": number,
                                    "Swappiness": number,
                                    "Tmpfs": [
                                        {
                                            "ContainerPath": "string",
                                            "MountOptions": ["string"],
                                            "Size": number
                                        }
                                    ]
                                },
                                "LogConfiguration": {
                                    "LogDriver": "string",
                                    "Options": {"string": "string"},
                                    "SecretOptions": [
                                        {
                                            "Name": "string",
                                            "ValueFrom": "string"
                                        }
                                    ]
                                },
                                "Memory": number,
                                "MemoryReservation": number,
                                "MountPoints": [
                                    {
                                        "ContainerPath": "string",
                                        "ReadOnly": boolean,
                                        "SourceVolume": "string"
                                    }
                                ],
                                "Name": "string",
                                "PortMappings": [
                                    {
                                        "ContainerPort": number,
                                        "HostPort": number,
                                        "Protocol": "string"
                                    }
                                ],
                                "Privileged": boolean,
                                "PseudoTerminal": boolean,
                                "ReadonlyRootFilesystem": boolean,
                                "RepositoryCredentials": {
                                    "CredentialsParameter": "string"
                                },
                                "ResourceRequirements": [
                                    {
                                        "Type": "string",
                                        "Value": "string"
                                    }
                                ],
                                "Secrets": [
                                    {
                                        "Name": "string",
                                        "ValueFrom": "string"
                                    }
                                ],
                                "StartTimeout": number,
                                "StopTimeout": number,
                                "SystemControls": [
                                    {
                                        "Namespace": "string",
                                        "Value": "string"
                                    }
                                ],
                                "Ulimits": [
                                    {
                                        "HardLimit": number,
                                        "Name": "string",
                                        "SoftLimit": number
                                    }
                                ],
                                "User": "string",
                                "VolumesFrom": [
                                    {
                                        "ReadOnly": boolean,
                                        "SourceContainer": "string"
                                    }
                                ],
                                "WorkingDirectory": "string"
                            }
                        ],
                        "Cpu": "string",
                        "ExecutionRoleArn": "string",
                        "Family": "string",
                        "InferenceAccelerators": [
                            {
                                "DeviceName": "string",
                                "DeviceType": "string"
                            }
                        ],
                        "IpcMode": "string",
                        "Memory": "string",
                        "NetworkMode": "string",
                        "PidMode": "string",
                        "PlacementConstraints": [
                            {
                                "Expression": "string",
                                "Type": "string"
                            }
                        ],
                        "ProxyConfiguration": {
                            "ContainerName": "string",
                            "ProxyConfigurationProperties": [
                                {
                                    "Name": "string",
                                    "Value": "string"
                                }
                            ],
                            "Type": "string"
                        },
                        "RequiresCompatibilities": ["string"],
                        "TaskRoleArn": "string",
                        "Status": "string",
                        "Volumes": [
                            {
                                "DockerVolumeConfiguration": {
                                    "Autoprovision": boolean,
                                    "Driver": "string",
                                    "DriverOpts": {"string": "string"},
                                    "Labels": {"string": "string"},
                                    "Scope": "string"
                                },
                                "EfsVolumeConfiguration": {
                                    "AuthorizationConfig": {
                                        "AccessPointId": "string",
                                        "Iam": "string"
                                    },
                                    "FilesystemId": "string",
                                    "RootDirectory": "string",
                                    "TransitEncryption": "string",
                                    "TransitEncryptionPort": number
                                },
                                "Host": {
                                    "SourcePath": "string"
                                },
                                "Name": "string"
                            }
                        ]
                    },
                    "AwsElasticBeanstalkEnvironment": {
                        "ApplicationName": "string",
                        "Cname": "string",
                        "DateCreated": "string",
                        "DateUpdated": "string",
                        "Description": "string",
                        "EndpointUrl": "string",
                        "EnvironmentArn": "string",
                        "EnvironmentId": "string",
                        "EnvironmentLinks": [
                            {
                                "EnvironmentName": "string",
                                "LinkName": "string"
                            }
                        ],
                        "EnvironmentName": "string",
                        "OptionSettings": [
                            {
                                "Namespace": "string",
                                "OptionName": "string",
                                "ResourceName": "string",        
                                "Value": "string"
                            }
                        ],
                        "PlatformArn": "string",
                        "SolutionStackName": "string",
                        "Status": "string",
                        "Tier": {
                            "Name": "string",
                            "Type": "string",
                            "Version": "string"
                        },
                        "VersionLabel": "string"
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
                        "ElasticsearchClusterConfig": {
                            "DedicatedMasterCount": number,
                            "DedicatedMasterEnabled": boolean,
                            "DedicatedMasterType": "string",
                            "InstanceCount": number,
                            "InstanceType": "string",
                            "ZoneAwarenessConfig": {
                                "AvailabilityZoneCount": number
                            },
                            "ZoneAwarenessEnabled": boolean
                        },
                        "ElasticsearchVersion": "string",
                        "EncryptionAtRestOptions": {
                            "Enabled": boolean,
                            "KmsKeyId": "string"
                        },
                        "LogPublishingOptions": {
                            "AuditLogs": {
                                "CloudWatchLogsLogGroupArn": "string",
                                "Enabled": boolean
                            },
                            "IndexSlowLogs": {
                                "CloudWatchLogsLogGroupArn": "string",
                                "Enabled": boolean
                            },
                            "SearchSlowLogs": {
                                "CloudWatchLogsLogGroupArn": "string",
                                "Enabled": boolean
                            }
                        },
                        "NodeToNodeEncryptionOptions": {
                            "Enabled": boolean
                        },
                        "ServiceSoftwareOptions": {
                            "AutomatedUpdateDate": "string",
                            "Cancellable": boolean,
                            "CurrentVersion": "string",
                            "Description": "string",
                            "NewVersion": "string",
                            "UpdateAvailable": boolean,
                            "UpdateStatus": "string"
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
                    "AwsElbLoadBalancer": {
                        "AvailabilityZones": [ "string" ],
                        "BackendServerDescriptions": [
                            {
                                "InstancePort": number,
                                "PolicyNames": [ "string" ]
                            }
                        ],
                        "CanonicalHostedZoneName": "string",
                        "CanonicalHostedZoneNameID": "string",
                        "CreatedTime": "string",
                        "DnsName": "string",
                        "HealthCheck": {
                            "HealthyThreshold": number,
                            "Interval": number,
                            "Target": "string",
                            "Timeout": number,
                            "UnhealthyThreshold": number
                        },
                        "Instances": [
                            {
                                "InstanceId": "string"
                            }
                        ],
                        "ListenerDescriptions": [
                            {
                                "Listener": {
                                    "InstancePort": number,
                                    "InstanceProtocol": "string",
                                    "LoadBalancerPort": number,
                                    "Protocol": "string",
                                    "SslCertificateId": "string"
                                },
                                "PolicyNames": [ "string" ]
                            }
                        ],
                        "LoadBalancerAttributes": {
                            "AccessLog": {
                                "EmitInterval": number,
                                "Enabled": boolean,
                                "S3BucketName": "string",
                                "S3BucketPrefix": "string"
                            },
                            "ConnectionDraining": {
                                "Enabled": boolean,
                                "Timeout": number
                            },
                            "ConnectionSettings": {
                                "IdleTimeout": number
                            },
                            "CrossZoneLoadBalancing": {
                                "Enabled": boolean
                            }
                        },
                        "LoadBalancerName": "string",
                        "Policies": {
                            "AppCookieStickinessPolicies": [
                                {
                                    "CookieName": "string",
                                    "PolicyName": "string"
                                }
                            ],
                            "LbCookieStickinessPolicies": [
                                {
                                    "CookieExpirationPeriod": number,
                                    "PolicyName": "string"
                                }
                            ],
                            "OtherPolicies": [ "string" ]
                        },
                        "Scheme": "string",
                        "SecurityGroups": [ "string" ],
                        "SourceSecurityGroup": {
                            "GroupName": "string",
                            "OwnerAlias": "string"
                        },
                        "Subnets": [ "string" ],
                        "VpcId": "string"
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
                        "AccessKeyId": "string",
                        "AccountId": "string",
                        "CreatedAt": "string",
                        "PrincipalId": "string",
                        "PrincipalName": "string",
                        "PrincipalType": "string",
                        "SessionContext": {
                            "Attributes": {
                                "CreationDate": "string",
                                "MfaAuthenticated": boolean
                            },
                            "SessionIssuer": {
                                "AccountId": "string",
                                "Arn": "string",
                                "PrincipalId": "string",
                                "Type": "string",
                                "UserName": "string"
                            }
                        },
                        "Status": "string"
                    },
                    "AwsIamGroup": {
                        "AttachedManagedPolicies": [
                            {
                                "PolicyArn": "string",
                                "PolicyName": "string"
                            }
                        ],
                        "CreateDate": "string",
                        "GroupId": "string",
                        "GroupName": "string",
                        "GroupPolicyList": [
                            {
                                "PolicyName": "string"
                            }
                        ],
                        "Path": "string"
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
                        ],
                        "UpdateDate": "string"
                    },
                    "AwsIamRole": {
                        "AssumeRolePolicyDocument": "string",
                        "AttachedManagedPolicies": [
                            {
                                "PolicyArn": "string",
                                "PolicyName": "string"
                            }
                        ],
                        "CreateDate": "string",
                        "InstanceProfileList": [
                            {
                                "Arn": "string",
                                "CreateDate": "string",
                                "InstanceProfileId": "string",
                                "InstanceProfileName": "string",
                                "Path": "string",
                                "Roles": [
                                    {
                                        "Arn": "string",
                                        "AssumeRolePolicyDocument": "string",
                                        "CreateDate": "string",
                                        "Path": "string",
                                        "RoleId": "string",
                                        "RoleName": "string"
                                    }
                                ]
                            }
                        ],
                        "MaxSessionDuration": number,
                        "Path": "string",
                        "PermissionsBoundary": {
                            "PermissionsBoundaryArn": "string",
                            "PermissionsBoundaryType": "string"
                        },
                        "RoleId": "string",
                        "RoleName": "string",
                        "RolePolicyList": [
                            {
                                "PolicyName": "string"
                            }
                        ]
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
                        "PermissionsBoundary": {
                            "PermissionsBoundaryArn": "string",
                            "PermissionsBoundaryType": "string"
                        },
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
                        "Description": "string",
                        "KeyId": "string",
                        "KeyManager": "string",
                        "KeyState": "string",
                        "Origin": "string"
                    },
                    "AwsLambdaFunction": {
                        "Code": {
                            "S3Bucket": "string",
                            "S3Key": "string",
                            "S3ObjectVersion": "string",
                            "ZipFile": "string"
                         },
                         "CodeSha256": "string",
                         "DeadLetterConfig": {
                              "TargetArn": "string"
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
                        "IamDatabaseAuthenticationEnabled": boolean,
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
                            "VpcId": "string"
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
                        "MaxAllocatedStorage": number,
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
                                "Message": "string",
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
                        "Encrypted": boolean,
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
                        "TdeCredentialArn": "string",
                        "Timezone": "string",
                        "VpcId": "string"
                    },
                    "AwsRdsEventSubscription": {
                        "CustomerAwsId": "string",
                        "CustSubscriptionId": "string",
                        "Enabled": boolean,
                        "EventCategoriesList": ["string"],
                        "EventSubscriptionArn": "string",
                        "SnsTopicArn": "string",
                        "SourceIdsList": ["string"],
                        "SourceType": "string",
                        "Status": "string",
                        "SubscriptionCreationTime": "string"
                    },
                    "AwsRedshiftCluster": {
                        "AllowVersionUpgrade": boolean,
                        "AutomatedSnapshotRetentionPeriod": number,
                        "AvailabilityZone": "string",
                        "ClusterAvailabilityStatus": "string",
                        "ClusterCreateTime": "string",
                        "ClusterIdentifier": "string",
                        "ClusterNodes": [
                            {
                                "NodeRole": "string",
                                "PrivateIPAddress": "string",
                                "PublicIPAddress": "string"
                            }
                        ],
                        "ClusterParameterGroups": [
                            { 
                                "ClusterParameterStatusList": [
                                    {
                                        "ParameterApplyErrorDescription": "string",
                                        "ParameterApplyStatus": "string",
                                        "ParameterName": "string"
                                    }
                                ],
                                "ParameterApplyStatus": "string",
                                "ParameterGroupName": "string"
                            }
                        ], 
                        "ClusterPublicKey": "string",
                        "ClusterRevisionNumber": "string",
                        "ClusterSecurityGroups": [
                            {
                                "ClusterSecurityGroupName": "string",
                                "Status": "string"
                            }
                        ],
                        "ClusterSnapshotCopyStatus": {
                            "DestinationRegion": "string",
                            "ManualSnapshotRetentionPeriod": number,
                            "RetentionPeriod": number,
                            "SnapshotCopyGrantName": "string"
                        },
                        "ClusterStatus": "string",
                        "ClusterSubnetGroupName": "string",
                        "ClusterVersion": "string",
                        "DBName": "string",
                        "DeferredMaintenanceWindows": [
                            {
                                "DeferMaintenanceEndTime": "string",
                                "DeferMaintenanceIdentifier": "string",
                                "DeferMaintenanceStartTime": "string"
                            }
                        ],
                        "ElasticIpStatus": {
                            "ElasticIp": "string",
                            "Status": "string"
                        },
                        "ElasticResizeNumberOfNodeOptions": "string",
                        "Encrypted": boolean,
                        "Endpoint": {
                            "Address": "string",
                            "Port": number
                        },
                        "EnhancedVpcRouting": boolean,
                        "ExpectedNextSnapshotScheduleTime": "string",
                        "ExpectedNextSnapshotScheduleTimeStatus": "string",
                        "HsmStatus": {
                            "HsmClientCertificateIdentifier": "string",
                            "HsmConfigurationIdentifier": "string",
                            "Status": "string"
                        },
                        "IamRoles": [
                            {
                                "ApplyStatus": "string",
                                "IamRoleArn": "string"   
                            }
                        ],
                        "KmsKeyId": "string",
                        "MaintenanceTrackName": "string",
                        "ManualSnapshotRetentionPeriod": "number",
                        "MasterUsername": "string",
                        "NextMaintenanceWindowStartTime": "string",
                        "NodeType": "string",
                        "NumberOfNodes": number,
                        "PendingActions": [ "string" ],
                        "PendingModifiedValues": {
                            "AutomatedSnapshotRetentionPeriod": number,
                            "ClusterIdentifier": "string",
                            "ClusterType": "string",
                            "ClusterVersion": "string",
                            "EncryptionType": "string",
                            "EnhancedVpcRouting": boolean,
                            "MaintenanceTrackName": "string",
                            "MasterUserPassword": "string",
                            "NodeType": "string",
                            "NumberOfNodes": number,
                            "PubliclyAccessible": "string"
                        },
                        "PreferredMaintenanceWindow": "string",
                        "PubliclyAccessible": boolean,
                        "ResizeInfo": {
                            "AllowCancelResize": boolean,
                            "ResizeType": "string"
                        },
                        "RestoreStatus": {
                            "CurrentRestoreRateInMegaBytesPerSecond": number,
                            "ElapsedTimeInSeconds": number,
                            "EstimatedTimeToCompletionInSeconds": number,
                            "ProgressInMegaBytes": number,
                            "SnapshotSizeInMegaBytes": number,
                            "Status": "string"
                        },
                        "SnapshotScheduleIdentifier": "string",
                        "SnapshotScheduleState": "string",
                        "VpcId": "string",
                        "VpcSecurityGroups": [
                            {
                                "Status": "string",
                                "VpcSecurityGroupId": "string"
                            }
                        ]
                    },
                    "AwsS3AccountPublicAccessBlock": {
                        "BlockPublicAcls": boolean,
                        "BlockPublicPolicy": boolean,
                        "IgnorePublicAcls": boolean,
                        "RestrictPublicBuckets": boolean
                    },
                    "AwsS3Bucket": {
                        "BucketLifecycleConfiguration": {
                            "Rules": [
                                {
                                    "AbortIncompleteMultipartUpload": {
                                        "DaysAfterInitiation": number
                                    },
                                    "ExpirationDate": "string",
                                    "ExpirationInDays": number,
                                    "ExpiredObjectDeleteMarker": boolean,
                                    "Filter": {
                                        "Predicate": {
                                            "Operands": [
                                                {
                                                    "Prefix": "string",
                                                    "Type": "string"
                                                },
                                                {
                                                    "Tag": {
                                                        "Key": "string",
                                                        "Value": "string"
                                                    },
                                                    "Type": "string"
                                                }
                                            ],
                                            "Type": "string"
                                        }
                                    },
                                    "Id": "string",
                                    "NoncurrentVersionExpirationInDays": number,
                                    "NoncurrentVersionTransitions": [
                                       {
                                           "Days": number,
                                           "StorageClass": "string"
                                       }
                                    ],
                                    "Prefix": "string",
                                    "Status": "string",
                                    "Transitions": [
                                        {
                                            "Date": "string",
                                            "Days": number,
                                            "StorageClass": "string"
                                        }
                                    ]
                                }
                            ]
                        },
                        "CreatedAt": "string",
                        "OwnerId": "string",
                        "OwnerName": "string",
                        "PublicAccessBlockConfiguration": {
                            "BlockPublicAcls": boolean,
                            "BlockPublicPolicy": boolean,
                            "IgnorePublicAcls": boolean,
                            "RestrictPublicBuckets": boolean
                        },
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
                        "Deleted": boolean,
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
                    "AwsSsmPatchCompliance": {
                        "Patch": {
                            "ComplianceSummary": {
                                "ComplianceType": "string",
                                "CompliantCriticalCount": integer,
                                "CompliantHighCount": integer,
                                "CompliantInformationalCount": integer,
                                "CompliantLowCount": integer,
                                "CompliantMediumCount": integer,
                                "CompliantUnspecifiedCount": integer,
                                "ExecutionType": "string",
                                "NonCompliantCriticalCount": integer,
                                "NonCompliantHighCount": integer,
                                "NonCompliantInformationalCount": integer,
                                "NonCompliantLowCount": integer,
                                "NonCompliantMediumCount": integer,
                                "NonCompliantUnspecifiedCount": integer,
                                "OverallSeverity": "string",
                                "PatchBaselineId": "string",
                                "PatchGroup": "string",
                                "Status": "string"
                            }
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
                        "string": "string" 
                    }
                },
                "Id": "string",
                "Partition": "string",
                "Region": "string",
                "ResourceRole": "string",
                "Tags": { 
                    "string": "string" 
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
            "string": "string" 
        },
        "VerificationState": "string",
        "Workflow": {
            "Status": "string"
        },
        "WorkflowState": "string",
        "Vulnerabilities": [
            {
                "Cvss": [
                    {
                        "BaseScore": number,
                        "BaseVector": "string",
                        "Version": "string"
                    }
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
    }
]
```