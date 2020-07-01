# AWS Security Finding Format \(ASFF\)<a name="securityhub-findings-format"></a>

AWS Security Hub consumes, aggregates, organizes, and prioritizes findings from AWS security services and from the third\-party product integrations\. Security Hub processes these findings using a standard findings format called the AWS Security Finding Format \(ASFF\), which eliminates the need for time\-consuming data conversion efforts\. Then it correlates ingested findings across products to prioritize the most important ones\.

**Topics**
+ [ASFF syntax](#securityhub-findings-format-syntax)
+ [ASFF attributes](#securityhub-findings-format-attributes)
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
                        "Address": ["string"]
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
                        ],
                    },
                    "Protocol": "string",
                    "Source": {
                        "Address": ["string"]
                    }
                }
            }
        ],
        "Note": { 
            "Text": "string",
            "UpdatedAt": "string",
            "UpdatedBy": "string"
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
                            "Items": {
                                "OriginPath": "string",
                                "Id": "string",
                                "DomainName": "string"
                            }
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
                          "Size": number
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
                                "CidrBlockState": "string"
                                "Ipv6CidrBlock": "string",
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
                    "AwsIamRole": {
                        "AssumeRolePolicyDocument": "string",
                        "CreateDate": "string",
                        "MaxSessionDuration": number,
                        "Path": "string",
                        "RoleId": "string",
                        "RoleName": "string"
                    },
                    "AwsKmsKey": {
                        "AWSAccountId": "string",
                        "CreationDate": "string",
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
                    "AwsRdsDbInstance": {
                        "AssociatedRoles": [
                            {
                                "RoleArn": "string",
                                "FeatureName": "string",
                                "Status": "string"
                            }
                        ],
                        "CACertificateIdentifier": "string",
                        "DBClusterIdentifier": "string",
                        "DBInstanceClass": "string",
                        "DBInstanceIdentifier": "string",
                        "DbInstancePort": number,
                        "DbiResourceId": "string",
                        "DBName": "string",
                        "DeletionProtection": boolean,
                        "Endpoint": {
                            "Address": "string",
                            "Port": number,
                            "HostedZoneId": "string"
                        },
                        "Engine": "string",
                        "EngineVersion": "string",
                        "IAMDatabaseAuthenticationEnabled": boolean,
                        "InstanceCreateTime": "string",
                        "KmsKeyId": "string",
                        "PubliclyAccessible": boolean,
                        "TdeCredentialArn": "string",
                        "StorageEncrypted": boolean,
                        "VpcSecurityGroups": [
                            {
                                "VpcSecurityGroupId": "string",
                                "Status": "string"
                            }
                        ]
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
|  `Confidence`  |  No  |  A finding's confidence\. Confidence is defined as the likelihood that a finding accurately identifies the behavior or issue that it was intended to identify\. A finding provider can provide an initial value for this attribute, but cannot update it after that\. This attribute can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\. Type: Integer \(range 0–100\) Confidence is scored on a 0–100 basis using a ratio scale, where 0 means zero\-percent confidence and 100 means 100\-percent confidence\. However, a data exfiltration detection based on a statistical deviation of network traffic has a much lower confidence because an actual exfiltration hasn't been verified\. Example: <pre>"Confidence": 42</pre>  | 
|  `CreatedAt`  |  Yes  |  An ISO8601\-formatted timestamp \(as defined in [RFC\-3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)\) that indicates when the potential security issue captured by a finding was created\. The `CreatedAt` timestamp reflects the time when the finding record was created\. Consequently, it can differ from the `FirstObservedAt` timestamp, which reflects the time when the event or vulnerability was first observed\. This timestamp *must* be provided on the first generation of the finding and *can't* be changed upon subsequent updates to the finding\. Type: Timestamp Example: <pre>"CreatedAt": "2017-03-22T13:22:13.933Z"</pre>  Findings are deleted 90 days after the most recent update or 90 days after the creation date if no update occurs\. To store findings for longer than 90 days, you can configure a rule in CloudWatch Events that routes findings to your Amazon S3 bucket\.  | 
|  `Criticality`  |  No  | The level of importance that is assigned to the resources that are associated with the finding\. A score of 0 means that the underlying resources have no criticality, and a score of 100 is reserved for the most critical resources\.  A finding provider can provide an initial value for this attribute, but cannot update it after that\. This attribute can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\. Type: Integer \(range 0–100\) Criticality is scored on a 0–100 basis, using a ratio scale that supports only full integers\. A score of 0 means that the underlying resources have no criticality, and a score of 100 is reserved for the most critical resources\. At a high level, when assessing criticality, you need to consider the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) For each resource, consider the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) You can use the following guidelines: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Criticality": 99</pre>  | 
|  `Description`  |  Yes  | A finding's description\. This field can be nonspecific boilerplate text or details that are specific to the instance of the finding\. Type: String \(1,024 characters max\) Example: <pre>"Description": "The version of openssl found on instance i-abcd1234 is known to contain a vulnerability."</pre>  | 
|  `FirstObservedAt`  |  No  | An ISO8601\-formatted timestamp \(as defined in [RFC\-3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)\) that indicates when the potential security issue captured by a finding was first observed\. Type: Timestamp Because this timestamp reflects the time of when the event or vulnerability was first observed, it can differ from the `CreatedAt` timestamp, which reflects the time this finding record was created\.  This timestamp should be immutable between updates of the finding record, but can be updated if a more accurate timestamp has been determined\. Example: <pre>"FirstObservedAt": "2017-03-22T13:22:13.933Z"</pre>  | 
|  `GeneratorId`  |  Yes  | The identifier for the solution\-specific component \(a discrete unit of logic\) that generated a finding\. In various solutions from security findings products, this generator can be called a rule, a check, a detector, a plugin, and so on\. Type: String \(512 characters max\) or Amazon Resource Name \(ARN\) Example: <pre>"GeneratorId": "acme-vuln-9ab348"</pre>  | 
|  `Id`  |  Yes  | The product\-specific identifier for a finding\. Type: String \(512 characters max\) or ARN The finding ID must comply with the following constraints: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) These constraints are expected to hold within a findings product, but are not required to hold across findings products\. Example: <pre>"Id": "us-west-2/111111111111/98aebb2207407c87f51e89943f12b1ef"</pre>  | 
|  `LastObservedAt`  |  No  | An ISO8601\-formatted timestamp \(as defined in [RFC\-3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)\) that indicates when the potential security issue captured by a finding was most recently observed by the security findings product\. Type: Timestamp This timestamp reflects the time of when the event or vulnerability was last or most recently observed\. Consequently, it can differ from the `UpdatedAt` timestamp, which reflects the time this finding record was last or most recently updated\.  You can provide this timestamp, but it isn't required upon the first observation\. If you provide the field in this case, the timestamp should be the same as the `FirstObservedAt` timestamp\. You should update this field to reflect the last or most recently observed timestamp each time a finding is observed\. Example: <pre>"LastObservedAt": "2017-03-23T13:22:13.933Z"</pre>  | 
|  [`Malware`](#asff-malware)  |  No  | A list of malware related to a finding\. Type: Array of up to five malware objects Example: <pre>"Malware": [<br />    {<br />        "Name": "Stringler",<br />        "Type": "COIN_MINER",<br />        "Path": "/usr/sbin/stringler",<br />        "State": "OBSERVED"<br />    }<br />]</pre>  | 
|  [`Network`](#asff-network)  |  No  | The details of network\-related information about a finding\. Type: Object Example: <pre>"Network": {<br />    "Direction": "IN",<br />    "Protocol": "TCP",<br />    "SourceIpV4": "1.2.3.4",<br />    "SourceIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",<br />    "SourcePort": "42",<br />    "SourceDomain": "here.com",<br />    "SourceMac": "00:0d:83:b1:c0:8e",<br />    "DestinationIpV4": "2.3.4.5",<br />    "DestinationIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",<br />    "DestinationPort": "80",<br />    "DestinationDomain": "there.com"<br />}</pre>  | 
|  [`NetworkPath`](#asff-networkpath)  |  No  |  A network path that is related to the finding\. Each entry in `NetworkPath` represents a component of the path\. Type: Array of objects  | 
|  [`Note`](#asff-note)  |  No  |  A user\-defined note that is added to a finding\. A finding provider can provide an initial note for a finding, but cannot add notes after that\. A note can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Notes can be added by both master accounts and member accounts\. Type: Object Example: <pre>"Note": {<br />    "Text": "Don't forget to check under the mat.",<br />    "UpdatedBy": "jsmith",<br />    "UpdatedAt": "2018-08-31T00:15:09Z"<br />}</pre>  | 
|  [`Process`](#asff-process)  |  No  | The details of process\-related information about a finding\.Type: Object Example: <pre>"Process": {<br />    "Name": "syslogd",<br />    "Path": "/usr/sbin/syslogd",<br />    "Pid": 12345,<br />    "ParentPid": 56789,<br />    "LaunchedAt": "2018-09-27T22:37:31Z",<br />    "TerminatedAt": "2018-09-27T23:37:31Z"<br />}</pre>  | 
|  `ProductArn`  |  Yes  | The ARN generated by Security Hub that uniquely identifies a third\-party findings product after the product is registered with Security Hub\. Type: ARN The format of this field is `arn:partition:securityhub:region:account-id:product/company-id/product-id`\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>// Private ARN<br />    "ProductArn": "arn:aws:securityhub:us-east-1:111111111111:product/111111111111/default"<br /><br />// Public ARN<br />    "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty"<br />    "ProductArn": "arn:aws:securityhub:us-west-2:222222222222:product/generico/secure-pro"</pre>  | 
|  `ProductFields`  |  No  | A data type where security findings products can include additional solution\-specific details that aren't part of the defined AWS Security Finding Format\. Type: Map of up to 50 key\-value pairs This field should not contain redundant data and must not contain data that conflicts with AWS Security Finding Format fields\. The "`aws/`" prefix represents a reserved namespace for AWS products and services only and must not be submitted with findings from partner products\. Although not required, products should format field names as `company-id/product-id/field-name`, where the `company-id` and `product-id` match those supplied in the `ProductArn` of the finding\. Field names can include alphanumeric characters, white space, and the following symbols: \_ \. / = \+ \\ \- @ Example: <pre>"ProductFields": {<br />    "generico/secure-pro/Count": "6",<br />    "generico/secure-pro/Action.Type", "AWS_API_CALL",<br />    "API", "DeleteTrail",<br />    "Service_Name": "cloudtrail.amazonaws.com",<br />    "aws/inspector/AssessmentTemplateName": "My daily CVE assessment",<br />    "aws/inspector/AssessmentTargetName": "My prod env",<br />    "aws/inspector/RulesPackageName": "Common Vulnerabilities and Exposures"<br />}</pre>  | 
|  `RecordState`  |  No  | The record state of a finding\.  By default, when initially generated by a service, findings are considered `ACTIVE`\. The `ARCHIVED` state indicates that a finding should be hidden from view\. Archived findings are not immediately deleted\. You can search, review, and report against them\. Finding providers can update the record state\. Security Hub also automatically archives control\-based findings if the associated resource is deleted\. Type: Enum Valid values: `ACTIVE` \| `ARCHIVED` Example: <pre>"RecordState": "ACTIVE"</pre>  | 
|  [`RelatedFindings`](#asff-relatedfindings)  |  No  | A list of related findings\.  A finding provider can provide an initial list of related findings, but cannot update the list after that\. The list of related findings can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\. Type: Array of up to 10 `RelatedFinding` objects Example: <pre>"RelatedFindings": [<br />    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", <br />      "Id": "123e4567-e89b-12d3-a456-426655440000" },<br />    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", <br />      "Id": "AcmeNerfHerder-111111111111-x189dx7824" }<br />]</pre>  | 
|  [`Remediation`](#asff-remediation)  |  No  | The remediation options for a finding\. Type: Object Example: <pre>"Remediation": {<br />    "Recommendation": {<br />        "Text": "Run sudo yum update and cross your fingers and toes.",<br />        "Url": "http://myfp.com/recommendations/dangerous_things_and_how_to_fix_them.html"<br />    }<br />}</pre>  | 
|  [`Resources`](#asff-resources)  |  Yes  | A set of resource data types that describe the resources that the finding refers to\. Type: Array of up to 32 resource objects Example: <pre>"Resources": [<br />  {<br />    "Type": "AwsEc2Instance",<br />    "Id": "i-cafebabe",<br />    "Partition": "aws",<br />    "Region": "us-west-2",<br />    "Tags": {<br />      "billingCode": "Lotus-1-2-3",<br />      "needsPatching": "true"<br />    },<br />    "Details": {<br />      "AwsEc2Instance": {<br />        "Type": "i3.xlarge",<br />        "ImageId": "ami-abcd1234",<br />        "IpV4Addresses": [ "54.194.252.215", "192.168.1.88" ],<br />        "IpV6Addresses": [ "2001:db8:1234:1a2b::123" ],<br />        "KeyName": "my_keypair",<br />        "IamInstanceProfileArn": "arn:aws:iam::111111111111:instance-profile/AdminRole",<br />        "VpcId": "vpc-11112222",<br />        "SubnetId": "subnet-56f5f633",<br />        "LaunchedAt": "2018-05-08T16:46:19.000Z"<br />      }  <br />    }<br />  }<br />]</pre>  | 
|  `SchemaVersion`  |  Yes  | The schema version that a finding is formatted for\. The value of this field must be one of the officially published versions identified by AWS\. In the current release, the AWS Security Finding Format schema version is `2018-10-08`\.  Type: String \(10 characters max, conforms to `YYYY-MM-DD`\) Example: <pre>"SchemaVersion": "2018-10-08"</pre>  | 
|  [`Severity`](#asff-severity)  |  Yes  | A finding's severity\. The finding must have either `Label` or `Normalized` populated\. `Label` is the preferred attribute\. If neither attribute is populated, then the finding is invalid\. A finding provider can provide initial severity information for a finding, but cannot update it after that\. The severity information can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\.Type: Object Example: <pre>"Severity": {<br />    "Label": "CRITICAL",<br />    "Original": 8.3<br />}</pre>  | 
|  `SourceUrl`  |  No  | A URL that links to a page about the current finding in the finding product\. Type: URL | 
|  [`ThreatIntelIndicators`](#asff-threatintelindicators)  |  No  | Threat intelligence details that are related to a finding\. Type: Array of up to five threat intelligence indicator objects Example: <pre>"ThreatIntelIndicators": [<br />  {<br />    "Type": "IPV4_ADDRESS",<br />    "Value": "8.8.8.8",<br />    "Category": "BACKDOOR",<br />    "LastObservedAt": "2018-09-27T23:37:31Z",<br />    "Source": "Threat Intel Weekly",<br />    "SourceUrl": "http://threatintelweekly.org/backdoors/8888"<br />  }<br />]</pre>  | 
|  `Title`  |  Yes  | A finding's title\. This field can contain nonspecific boilerplate text or details that are specific to this instance of the finding\.Type: String \(256 characters max\) | 
|  `Types`  |  Yes  | One or more finding types in the format of `namespace/category/classifier` that classify a finding\. Type: Array of 50 strings max [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Namespaces are required for all finding types, but categories and classifiers are optional\. If you specify a classifier, you must also specify a category\. The '`/`' character is reserved and must *not* be used in a category or classifier\. Escaping the '`/`' character is not supported\. Example: <pre>"Types": [<br />    "Software and Configuration Checks/Vulnerabilities/CVE"<br />]</pre>  | 
|  `UpdatedAt`  |  Yes  | An ISO8601\-formatted timestamp \(as defined in [RFC\-3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)\) that indicates when the findings product last updated the finding record\. This timestamp reflects the time when the finding record was last or most recently updated\. Consequently, it can differ from the `LastObservedAt` timestamp, which reflects when the event or vulnerability was last or most recently observed\. When you update the finding record, you must update this timestamp to the current timestamp\. Upon creation of a finding record, the `CreatedAt` and `UpdatedAt` timestamps must be the same timestamp\. After an update to the finding record, the value of this field must be greater than all of the previous values that it contained\. Note that `UpdatedAt` is not updated by changes from [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It is only updated by [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html)\.Type: Timestamp Findings are deleted 90 days after the most recent update or 90 days after the creation date if no update occurs\. To store findings for longer than 90 days, you can configure a rule in CloudWatch Events that routes findings to your Amazon S3 bucket\.  | 
|  `UserDefinedFields`  |  No  | A list of name\-value string pairs that are associated with the finding\. These are custom, user\-defined fields that are added to a finding\. These fields can be generated automatically via your specific configuration\. Findings products must *not* use this field for data that the product generates\. Instead, findings products can use the `ProductFields` field for data that doesn't map to any standard AWS Security Finding Format field\. These fields can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. They can only be updated by a master account\. They cannot be updated by a member account\.Type: map of up to 50 key\-value pairs Example: <pre>"UserDefinedFields": {<br />    "reviewedByCio": "true",<br />    "comeBackToLater": "Check this again on Monday"<br />}</pre>  | 
|  `VerificationState`  |  No  | The veracity of a finding\. Findings products can provide the value of `UNKNOWN` for this field\. A findings product should provide this value if there is a meaningful analog in the findings product's system\. This field is typically populated by a user determination or action after they investigate a finding\. A finding provider can provide an initial value for this attribute, but cannot update it after that\. This attribute can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\.Type: Enum Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 
|  [`Vulnerabilities`](#asff-vulnerabilities)  |  No  |  A list of vulnerabilities that apply to the finding\. Type: Array of objects  | 
|  [`Workflow`](#asff-workflow)  |  No  |  Provides information about the status of the investigation into a finding\. The workflow status is not intended for finding providers\. The workflow status can only be updated using `BatchUpdateFindings`\. Customers can also update it from the console\. See [Setting the workflow status for a finding](finding-workflow-status.md)\. The workflow status can only be updated by a master account\. It cannot be updated by a member account\. Type: Object Example: <pre>Workflow: {<br />    "Status": "NEW"<br />}</pre>  | 
|  `WorkflowState` \(deprecated\)  |  No  |  This field is being deprecated in favor of the `Status` field of the `Workflow` object\.The workflow state of a finding\. Findings products can provide the value of `NEW` for this field\. A findings product can provide a value for this field if there is a meaningful analog in the findings product's system\. Type: Enum Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"WorkflowState": "NEW"</pre>  | 

**Contents**
+ [Compliance](#asff-compliance)
  + [StatusReasons](#asff-compliance-statusreasons)
+ [Malware](#asff-malware)
+ [Network](#asff-network)
  + [OpenPortRange](#asff-network-openportrange)
+ [NetworkPath](#asff-networkpath)
  + [Egress](#asff-networkpath-egress)
    + [Destination](#asff-networkpath-egress-destination)
    + [Source](#asff-networkpath-egress-source)
  + [Ingress](#asff-networkpath-ingress)
    + [Destination](#asff-networkpath-ingress-destination)
    + [Source](#asff-networkpath-ingress-source)
+ [Note](#asff-note)
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
  + [AwsIamRole](#asff-resourcedetails-awsiamrole)
  + [AwsKmsKey](#asff-resourcedetails-awskmskey)
  + [AwsLambdaFunction](#asff-resourcedetails-awslambdafunction)
    + [Code](#asff-resourcedetails-awslambdafunction-code)
    + [DeadLetterConfig](#asff-resourcedetails-awslambdafunction-deadletterconfig)
    + [Environment](#asff-resourcedetails-awslambdafunction-environment)
    + [Layers](#asff-resourcedetails-awslambdafunction-layers)
    + [TracingConfig](#asff-resourcedetails-awslambdafunction-tracingconfig)
    + [VpcConfig](#asff-resourcedetails-awslambdafunction-vpcconfig)
  + [AwsLambdaLayerVersion](#asff-resourcedetails-awslambdalayerversion)
  + [AwsRdsDbInstance](#asff-resourcedetails-awsrdsdbinstance)
    + [AssociatedRoles](#asff-resourcedetails-awsrdsdbinstance-associatedroles)
    + [Endpoint](#asff-resourcedetails-awsrdsdbinstance-endpoint)
    + [VpcSecurityGroups](#asff-resourcedetails-awsrdsdbinstance-vpcsecuritygroups)
  + [AwsS3Bucket](#asff-resourcedetails-awss3bucket)
    + [ApplyServerSideEncryptionByDefault](#asff-resourcedetails-awss3bucket-applyserversideencryptionbydefault)
  + [AwsS3Object](#asff-resourcedetails-awss3object)
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
|  [`StatusReasons`](#asff-compliance-statusreasons)  |  No  |  For findings generated from controls, a list of reasons behind the value of `Compliance.Status`\. For the list of status codes and their meanings, see [Standards\-related information in the ASFF](securityhub-standards-results.md#securityhub-standards-results-asff)\. Type: String Example: <pre>"StatusReasons": [<br />    {<br /><br />        "Description": "CloudWatch alarms do not exist in the account",<br />        "ReasonCode": "CW_ALARMS_NOT_PRESENT"<br />    }<br />]<br /></pre>  | 

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

Example:

```
"Network": {
    "Direction": "IN",
    "Protocol": "TCP",
    "SourceIpV4": "1.2.3.4",
    "SourceIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",
    "SourcePort": "42",
    "SourceDomain": "here.com",
    "SourceMac": "00:0d:83:b1:c0:8e",
    "DestinationIpV4": "2.3.4.5",
    "DestinationIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",
    "DestinationPort": "80",
    "DestinationDomain": "there.com"
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
                ],
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
|  [`Ingress`](#asff-networkpath-ingress)  |  No  |  Information about the component that comes before the current node in the network path\. Type: Object  | 

#### Egress<a name="asff-networkpath-egress"></a>

The `Egress` object contains information about the component that comes after the current component in the network path\. It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`Destination`](#asff-networkpath-egress-destination)  |  No  |  Information about the destination of the component\. Type: Object  | 
|  `Protocol`  |  No  |  The protocol used for the component\. Type: String  | 
|  [`Source`](#asff-networkpath-egress-source)  |  No  |  Information about the origin of the component\. Type: Object  | 

##### Destination<a name="asff-networkpath-egress-destination"></a>

The `Destination` object contains information about the destination of the next component in the network path\. It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Address`  |  No  |  The IP addresses of the destination\. Type: Array of strings  | 
|  `PortRanges`  |  No  |  A list of port ranges for the destination\. Type: Array of objects  | 
|  `PortRanges.Begin`  |  No  |  For a destination port range, the beginning port number\. Type: Integer  | 
|  `PortRanges.End`  |  No  |  For a destination port range, the ending port number\. Type: Integer  | 

##### Source<a name="asff-networkpath-egress-source"></a>

The `Source` object provides information about the origin of the next component\. It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Address`  |  No  |  The IP addresses of the origin\. Type: Array of strings  | 

#### Ingress<a name="asff-networkpath-ingress"></a>

The `Ingress` object contains information about the previous component in the network path\. It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`Destination`](#asff-networkpath-ingress-destination)  |  No  |  Information about the destination for the previous component\. Type: Object  | 
|  `Protocol`  |  No  |  The protocol used by the previous component\. Type: String  | 
|  [`Source`](#asff-networkpath-ingress-source)  |  No  |  Information about the origin of the previous component\. Type: Object  | 

##### Destination<a name="asff-networkpath-ingress-destination"></a>

The `Destination` object contains the destination information for the previous component\. It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Address`  |  No  |  IP addresses of the previous component\. Type: Array of strings  | 
|  `PortRanges`  |  No  |  List of open port ranges for the previous component\. Type: Array of objects  | 
|  `PortRanges.Begin`  |  No  |  For an open port range, the beginning of the range\. Type: Integer  | 
|  `PortRanges.End`  |  No  |  For an open port range, the end of the range\. Type: Number  | 

##### Source<a name="asff-networkpath-ingress-source"></a>

The `Source` object contains information about the origin of the previous component\. It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Address`  |  No  |  IP addresses for the origin of the previous component\. Type: Array of strings  | 

### Note<a name="asff-note"></a>

The `Note` object adds a user\-defined note to the finding\.

A finding provider can provide an initial note for a finding, but cannot add notes after that\. A note can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Notes can be added by both master accounts and member accounts\.

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
|  `UpdatedAt`  |  Yes  | The timestamp of when the note was updated\.Type: Timestamp Example: <pre>"UpdatedAt": "2018-08-31T00:15:09Z"</pre>  | 
|  `UpdatedBy`  |  Yes  | The principal that created a note\.Type: String \(512 characters max\) or ARN Example: <pre>"UpdatedBy": "jsmith"</pre>  | 

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
|  `LaunchedAt`  |  No  | The timestamp for the date and time when the process was launched\. Type: Timestamp Example: <pre>"LaunchedAt": "2018-09-27T22:37:31Z"</pre>  | 
|  `Name`  |  No  | The name of the process\.Type: String \(64 characters max\) Example: <pre>"Name": "syslogd"</pre>  | 
|  `ParentPid`  |  No  | The parent process ID\.Type: Number Example: <pre>"ParentPid": 56789</pre>  | 
|  `Path`  |  No  | The path to the process executable\. Type: String \(512 characters max\) Example: <pre>"Path": "/usr/sbin/syslogd"</pre>  | 
|  `Pid`  |  No  | The process ID\. Type: Number Example: <pre>"Pid": 12345</pre>  | 
|  `TerminatedAt`  |  No  | The timestamp for the date and time when the process was terminated\. Type: Timestamp Example: <pre>"TerminatedAt": "2018-09-27T23:37:31Z"</pre>  | 

### RelatedFindings<a name="asff-relatedfindings"></a>

The `RelatedFindings` object provides a list of findings that are related to the current finding\.

A finding provider can provide an initial list of related findings, but cannot update it after that\. `RelatedFindings` can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\.

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

Example:

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
|  `CreatedTime`  |  Yes  |  The date and time when the automatic scaling group was created\. Type: String \(timestamp\) Format: yyyy\-MM\-ddTHH:mm:ssZ  | 
|  `HealthCheckGracePeriod`  |  No  |  The amount of time, in seconds, that Amazon EC2 Auto Scaling waits before it checks the health status of an EC2 instance that has come into service\. Type: Integer  | 
|  `HealthCheckType`  |  Yes  |  The service to use for the health checks\. Type: String \(32 characters max\) Valid values: `EC2` \| `ELB`  | 
|  `LaunchConfigurationName`  |  Yes  |  The name of the launch configuration\. Type: String \(32 characters max\)  | 
|  `LoadBalancerNames`  |  No  |  The list of load balancers that are associated with the group\. Type: Array of strings Each load balancer name is limited to 255 characters\.  | 

#### AwsCloudFrontDistribution<a name="asff-resourcedetails-awscloudfrontdistribution"></a>

The `AwsCloudFrontDistribution` object provides details about a distribution configuration\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DomainName`  |  No  | The domain name corresponding to the distribution\.Type: String | 
|  `Etag`  |  No  | The entity tag is a hash of the object\.Type: String | 
|  `LastModifiedTime`  |  No  | The date and time that the distribution was last modified\.Type: String | 
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
|  `Items`  |  No  |  A complex type that contains origins or origin groups for this distribution\. Type: Object  | 

Each item can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `OriginPath`  |  No  |  An optional element that causes CloudFront to request your content from a directory in your S3 bucket or your custom origin\. Type: String  | 
|  `Id`  |  No  |  A unique identifier for the origin or origin group\. Type: String  | 
|  `DomainName`  |  No  |  Amazon S3 origins: The DNS name of the S3 bucket from which you want CloudFront to get objects for this origin\. Type: String  | 

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
|  `LaunchedAt`  |  No  | The date and time when the instance was launched\. Type: Timestamp | 
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
|  `AttachTime`  |  No  |  The timestamp indicating when the attachment initiated\. Type: Timestamp  | 
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
            "DeleteOnTermination": true
            "InstanceId": "i-123abc456def789g",
            "Status": "attached",
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
|  `CreateTime`  |  Yes  |  The date and time when the volume was created\. Type: String \(timestamp\) Format: yyyy\-MM\-ddTHH:mm:ssZ  | 
|  `Encrypted`  |  Yes  |  Whether the volume is encrypted\. Type: Boolean  | 
|  `KmsKeyId`  |  Yes  |  The ARN of the AWS KMS customer master key \(CMK\) that was used to protect the volume encryption key for the volume\. Type: String  | 
|  `Size`  |  Yes  |  The size of the volume, in GiBs\. Type: Integer  | 
|  `SnapshotId`  |  Yes  |  The snapshot from which the volume was created\. Type: String  | 
|  `Status`  |  Yes  |  The volume state\. Type: String Valid values: `creating` \| `available` \| `in-use` \| `deleting` \| `deleted` \| `error`  | 

##### Attachments<a name="asff-resourcedetails-awsec2volume-attachments"></a>

The `Attachments` object contains the set of attachments for the EC2 volume\. Each attachment can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AttachTime`  |  Yes  |  The date and time when the attachment initiated\. Type: String \(timestamp\) Format: `yyyy-MM-ddTHH:mm:ssZ`  | 
|  `DeleteOnTermination`  |  Yes  |  Whether the EBS volume is deleted when the EC2 instance is terminated\. Type: Boolean  | 
|  `InstanceId`  |  Yes  |  The identifier of the EC2 instance\. Type: String  | 
|  `Status`  |  Yes  |  The attachment state of the volume\. Type: String Valid values: `attaching` \| `attached` \| `detaching` \| `detached` \| `busy`  | 

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
            "CidrBlockState": "associated"
            "Ipv6CidrBlock": "192.0.2.0/24",
       }

    ],
    "State": "available",
}
```

The `AwsEc2Vpc` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`CidrBlockAssociationSet`](#asff-resourcedetails-awsec2vpc-cidrblockassociationset)  |  No  |  Information about the IPv4 CIDR blocks that are associated with the VPC\. Type: Array of objects  | 
|  `DhcpOptionsId`  |  Yes  |  The identifier of the set of Dynamic Host Configuration Protocol \(DHCP\) options that are associated with the VPC\. If the default options are associated with the VPC, then this is `default`\. Type: String \(32 characters max\)  | 
|  [`IpV6CidrBlockAssociationSet`](#asff-resourcedetails-awsec2vpc-ipv6cidrblockassociationset)  |  No  |  Information about the IPv6 CIDR blocks that are associated with the VPC\. Type: Array of objects\.  | 
|  `State`  |  Yes  |  The current state of the VPC\. Type: String \(32 characters max\) Valid values: `pending` \| `available`  | 

##### CidrBlockAssociationSet<a name="asff-resourcedetails-awsec2vpc-cidrblockassociationset"></a>

The `CidrBlockAssociationSet` object provides a list of IPV4 CIDR block associations\.

Each CIDR block association can contain the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AssociationId`  |  Yes  |  The association ID for the IPv4 CIDR block\. Type: String \(32 characters max\)  | 
|  `CidrBlock`  |  Yes  |  The IPv4 CIDR block\. Type: CIDR IPV4  | 
|  `CidrBlockState`  |  No  |  Information about the state of the CIDR block\. Type: String \(32 characters max\)  | 

##### IpV6CidrBlockAssociationSet<a name="asff-resourcedetails-awsec2vpc-ipv6cidrblockassociationset"></a>

The `IPV6CidrBlockAssociationSet` object provides a list of IPV6 CIDR block associations\.

Each CIDR block association can contain the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Associationid`  |  Yes  |  The association ID for the IPv6 CIDR block\. Type: String \(32 characters max\)  | 
|  `CidrBlockState`  |  No  |  Information about the state of the CIDR block\. Type: String \(32 characters max\)  | 
|  `IpV6CidrBlock`  |  Yes  |  The IPv6 CIDR block\. Type: CIDR IPV6  | 

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
|  `CanonicalHostedZoneId`  |  No  | The ID of the Amazon Route 53 hosted zone that is associated with the load balancer\.Type: String | 
|  `CreatedTime`  |  No  | The date and time the load balancer was created\.Type: String | 
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

IAM access key details that are related to a finding\.

Type: Object

The `AwsIamAccessKey` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CreatedAt`  |  No  | The creation date and time of the IAM access key that is related to a finding\.Type: Timestamp | 
|  `PrincipalId`  |  No  | The ID of the principal that is associated with an access key\. Type: String | 
|  `PrincipalName`  |  No  | The name of the principal\.Type: String | 
|  `PrincipalType`  |  No  | The type of principal\.Type: String | 
|  `Status`  |  No  | The status of the IAM access key that is related to a finding\. Valid values are `ACTIVE` and `INACTIVE`\.Type: Enum | 

#### AwsIamRole<a name="asff-resourcedetails-awsiamrole"></a>

Contains information about an IAM role, including all of the role's policies\.

Type: Object

The `AwsIamRole` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AssumeRolePolicyDocument`  |  No  | The trust policy that grants permission to assume the role\.Type: String | 
|  `CreateDate`  |  No  | The date and time, in ISO 8601 date\-time format, when the role was created\.Type: String | 
|  `RoleId`  |  No  | The stable and unique string identifying the role\.Type: String | 
|  `RoleName`  |  No  | The friendly name that identifies the role\.Type: String | 
|  `MaxSessionDuration`  |  No  | The maximum session duration \(in seconds\) that you want to set for the specified role\.Type: Integer | 
|  `Path`  |  No  | The path to the role\.Type: String | 

#### AwsKmsKey<a name="asff-resourcedetails-awskmskey"></a>

Details about an AWS KMS customer master key \(CMK\)\.

Type: Object

The `AwsKmsKey` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AWSAccountId`  |  No  |  The AWS account identifier of the account that owns the CMK\. Type: String  | 
|  `CreationDate`  |  No  |  The date and time when the CMK was created\. Type: Timestamp  | 
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
|  `Handler`  |  No  | The function that Lambda calls to begin executing your function\.Type: String | 
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
|  `Arn`  |  No  | The Amazon Resource Name \(ARN\) of the function layer\.Type: String | 
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
|  `CreatedDate`  |  No  |  The date that the version was created, in ISO 8601 format\. For example, 2018\-11\-27T15:10:45\.123\+0000\. Type: String  | 
|  `Version`  |  No  |  The version number\. Type: Long  | 

#### AwsRdsDbInstance<a name="asff-resourcedetails-awsrdsdbinstance"></a>

The `AwsRdsDbInstance` object provides details about an Amazon RDS DB instance\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`AssociatedRoles`](#asff-resourcedetails-awsrdsdbinstance-associatedroles)  |  No  |  The IAM roles that are associated with the DB instance\. Type: Array of role objects  | 
|  `CACertificateIdentifier`  |  No  |  The identifier of the CA certificate for this DB instance\. Type: String  | 
|  `DBClusterIdentifier`  |  No  |  If the DB instance is a member of a DB cluster, contains the name of the DB cluster that the DB instance is a member of\. Type: String  | 
|  `DBInstanceClass`  |  No  |  Contains the name of the compute and memory capacity class of the DB instance\. Type: String  | 
|  `DBInstanceIdentifier`  |  No  |  Contains a user\-supplied database identifier\. This identifier is the unique key that identifies a DB instance\. Type: String  | 
|  `DbInstancePort`  |  No  |  Specifies the port that the DB instance listens on\. If the DB instance is part of a DB cluster, this can be a different port than the DB cluster port\. Type: Integer  | 
|  `DbiResourceId`  |  No  |  The AWS Region\-unique, immutable identifier for the DB instance\. This identifier is found in CloudTrail log entries whenever the AWS KMS key for the DB instance is accessed\. Type: String  | 
|  `DBName`  |  No  |  The meaning of this parameter differs according to the database engine you use\. **MySQL, MariaDB, SQL Server, PostgreSQL** Contains the name of the initial database of this instance that was provided at create time, if one was specified when the DB instance was created\. This same name is returned for the life of the DB instance\. Type: String **Oracle** Contains the Oracle System ID \(SID\) of the created DB instance\. Not shown when the returned parameters do not apply to an Oracle DB instance\. Type: String  | 
|  `DeletionProtection`  |  No  |  Indicates whether the DB instance has deletion protection enabled\. The database can't be deleted when deletion protection is enabled\. Type: Boolean  | 
|  [`Endpoint`](#asff-resourcedetails-awsrdsdbinstance-endpoint)  |  No  |  Specifies the connection endpoint\. Type: Object  | 
|  `Engine`  |  No  |  Provides the name of the database engine to be used for this DB instance\. Type: String  | 
|  `EngineVersion`  |  No  |  Indicates the database engine version\. Type: String  | 
|  `IAMDatabaseAuthenticationEnabled`  |  No  |  True if mapping of IAM accounts to database accounts is enabled, and otherwise false\. IAM database authentication can be enabled for the following database engines\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Type: Boolean  | 
|  `InstanceCreateTime`  |  No  |  Provides the date and time the DB instance was created\. Type: Timestamp  | 
|  `KmsKeyId`  |  No  |  If `StorageEncrypted` is true, the AWS KMS key identifier for the encrypted DB instance\. Type: String  | 
|  `PubliclyAccessible`  |  No  |  Specifies the accessibility options for the DB instance\. A value of true specifies an Internet\-facing instance with a publicly resolvable DNS name, which resolves to a public IP address\. A value of false specifies an internal instance with a DNS name that resolves to a private IP address\. Type: Boolean  | 
|  `StorageEncrypted`  |  No  |  Specifies whether the DB instance is encrypted\. Type: Boolean  | 
|  `TdeCredentialArn`  |  No  |  The ARN from the key store with which the instance is associated for TDE encryption\. Type: String  | 
|  [`VpcSecurityGroups`](#asff-resourcedetails-awsrdsdbinstance-vpcsecuritygroups)  |  No  |  List of VPC security groups that the DB instance belongs to\. Type: Array of objects  | 

##### AssociatedRoles<a name="asff-resourcedetails-awsrdsdbinstance-associatedroles"></a>

The `AssociatedRoles` array lists the IAM roles that are associated with the DB instance\.

Each role object in the `AssociatedRoles` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `FeatureName`  |  No  |  The name of the feature that is associated with the IAM role\. Type: String  | 
|  `RoleArn`  |  No  |  The ARN of the IAM role that is associated with the DB instance\. Type: String  | 
|  `Status`  |  No  |  Describes the state of association between the IAM role and the DB instance\. Type: String Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 

##### Endpoint<a name="asff-resourcedetails-awsrdsdbinstance-endpoint"></a>

The `Endpoint` object provides details about the connection endpoint for the DB instance\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Address`  |  No  |  Specifies the DNS address of the DB instance\. Type: String  | 
|  `HostedZoneId`  |  No  |  Specifies the ID that Amazon Route 53 assigns when you create a hosted zone\. Type: String  | 
|  `Port`  |  No  |  Specifies the port that the database engine is listening on\. Type: Integer  | 

##### VpcSecurityGroups<a name="asff-resourcedetails-awsrdsdbinstance-vpcsecuritygroups"></a>

The `VpcSecurityGroups` array provides the list of VPC security groups that the DB instance belongs to\.

Each object in the `VpcSecurityGroups` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `VpcSecurityGroupId`  |  No  |  The name of the VPC security group\. Type: String  | 
|  `Status`  |  No  |  The status of the VPC security group\. Type: String  | 

#### AwsS3Bucket<a name="asff-resourcedetails-awss3bucket"></a>

The details of an Amazon S3 bucket\.

Type: Object

The `AwsS3Bucket` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CreatedAt`  |  No  |  The date and time when the S3 bucket was created\. Type: String \(uses the RFC 3339 format\)  | 
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

Details about an Amazon S3 object\.

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
|  `LastModified`  |  No  |  The date and time when the object was last modified\. Type: Datetime  | 
|  `ServerSideEncryption`  |  No  |  If the object is stored using server\-side encryption, the value of the server\-side encryption algorithm used when storing this object in Amazon S3\. Type: String  | 
|  `SSEKMSKeyId`  |  No  |  The identifier of the AWS Key Management Service\) symmetric customer managed customer master key \(CMK\) that was used for the object\. Type: String  | 
|  `VersionId`  |  No  |  The version of the object\. Type: String  | 

#### AwsSnsTopic<a name="asff-resourcedetails-awssnstopic"></a>

A wrapper type for the topic's Amazon Resource Name \(ARN\)\.

Type: Object

The `AwsSnsTopic` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `KmsMasterKeyId`  |  No  | The ID of an AWS managed customer master key \(CMK\) for Amazon SNS or a custom CMK\.Type: String | 
|  `Subscription`  |  No  | Subscription is an embedded property that describes the subscription endpoints of an Amazon SNS topic\.Type: Array of objects | 
|  `TopicName`  |  No  | The name of the topic\.Type: String | 
|  `Owner`  |  No  | The subscription's owner\.Type: String | 

##### Subscription<a name="asff-resourcedetails-awssnstopic-subscription"></a>

The `Subscription` object in an `AwsSnsTopic` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Endpoint`  |  No  |  The subscription's endpoint \(format depends on the protocol\)\. Type: String  | 
|  `Protocol`  |  No  |  The subscription's protocol\. Type: String  | 

#### AwsSqsQueue<a name="asff-resourcedetails-awssqsqueue"></a>

Data about an Amazon SQS queue\.

Type: Object

The `AwsSqsQueue` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `KmsDataKeyReusePeriodSeconds`  |  No  | The length of time, in seconds, for which Amazon SQS can reuse a data key to encrypt or decrypt messages before calling AWS KMS again\.Type: Integer | 
|  `KmsMasterKeyId`  |  No  | The ID of an AWS managed customer master key \(CMK\) for Amazon SQS or a custom CMK\.Type: String | 
|  `QueueName`  |  No  | The name of the new queue\.Type: String | 
|  `DeadLetterTargetArn`  |  No  | The Amazon Resource Name \(ARN\) of the dead\-letter queue to which Amazon SQS moves messages after the value of `maxReceiveCount` is exceeded\.Type: String | 

#### AwsWafWebAcl<a name="asff-resourcedetails-awswafwebacl"></a>

The `AwsWafWebAcl` object provides details about an AWS WAF WebACL\.

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
|  `DefaultAction`  |  Yes  |  The action to perform if none of the rules contained in the WebACL match\. The action is specified by the `WafAction` object\. Type: `WafAction` object  | 
|  `Name`  |  No  |  A friendly name or description of the WebACL\. You can't change the name of a WebACL after you create it\. Type: String Length constraints: Minimum length of 1\. Maximum length of 128\.  | 
|  [`Rules`](#asff-resourcedetails-awswafwebacl-rule)  |  Yes  |  A list of rules for the WebACL\. Type: Array of objects  | 
|  `WebAclId`  |  Yes  |  A unique identifier for a WebACL\. Type: String Length constraints: Minimum length of 1\. Maximum length of 128\.  | 

##### Rule object<a name="asff-resourcedetails-awswafwebacl-rule"></a>

The `Rules` array provides the list of rules for the WebACL\.

Each rule object in the array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Action`  |  No  |  Specifies the action that CloudFront or AWS WAF takes when a web request matches the conditions in the rule\. Type: Object  | 
|  `ExcludedRules`  |  No  |  An array of rules to exclude from a rule group\. This is applicable only when the `ActivatedRule` refers to a rule group\. Type: Array of objects  | 
|  `OverrideAction`  |  No  |  Use the `OverrideAction` to test your RuleGroup\. Any rule in a rule group can potentially block a request\. If you set the `OverrideAction` to `None`, the rule group blocks a request if any individual rule in the rule group matches the request and is configured to block that request\. However, if you first want to test the rule group, set the `OverrideAction` to `Count`\. The rule group then overrides any block action specified by individual rules contained within the group\. Instead of blocking matching requests, those requests are counted\. `ActivatedRule\|OverrideAction` applies only when updating or adding a rule group to a WebACL\. In this case, you do not use `ActivatedRule\|Action`\. For all other update requests, `ActivatedRule\|Action` is used instead of `ActivatedRule\|OverrideAction`\. Type: Object  | 
|  `Priority`  |  Yes  |  Specifies the order in which to evaluate the rules in a WebACL\. Rules with a lower value for `Priority` are evaluated before rules with a higher value\. The value must be a unique integer\. If you add multiple rules to a WebACL, the values don't need to be consecutive\. Type: Integer  | 
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
|  `LaunchedAt`  |  No  | The date and time that the container was started\.Type: Timestamp | 
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

The finding provider can provide the initial severity, but cannot update it after that\. The severity can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\.

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

Example:

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
|  `LastObservedAt`  |  No  | The date and time of the last observation of a threat intelligence indicator\.Type: Timestamp | 
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
|  `VendorCreatedAt`  |  No  |  The date and time when the vulnerability advisory was created\. Type: String \(timestamp\) Format: `yyyy-MM-ddTHH:mm:ssZ`  | 
|  `VendorSeverity`  |  No  |  The severity that the vendor assigned to the vulnerability\. Type: String \(32 characters max\)  | 
|  `VendorUpdatedAt`  |  No  |  The date and time when the vulnerability advisory was last updated\. Type: String \(timestamp\) Format: `yyyy-MM-ddTHH:mm:ssZ`  | 

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

The workflow status can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Customers can also update it from the console\. See [Setting the workflow status for a finding](finding-workflow-status.md)\. The workflow status can only be updated by a master account\. It cannot be updated by a member account\.

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