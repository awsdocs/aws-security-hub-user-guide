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
            "Status": "string",
            "RelatedRequirements": ["string"]
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
            "Protocol": "string",
            "SourceDomain": "string",
            "SourceIpV4": "string",
            "SourceIpV6": "string",
            "SourceMac": "string",
            "SourcePort": number
        },
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
                            "DeleteOnTermination": true,
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
                        "NetworkInterfaceId": '"string",
                        "SourceDestCheck": false
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
                                "ToPort": number
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
                                "ToPort": number
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
    }
]
```

## ASFF attributes<a name="securityhub-findings-format-attributes"></a>

The following table lists the top\-level attributes and objects for the ASFF\. For objects, to see the details for the object attributes and subfields, choose the object name\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AwsAccountId`  |  Yes  | The AWS account ID where a finding is generated\. Type: string \(12 digits max\) Example: <pre>"AwsAccountId": "111111111111"</pre>  | 
|  [`Compliance`](#asff-compliance)  |  No  | Exclusive to findings that are generated as the result of a check run against a specific rule in a supported standard \(for example, CIS AWS Foundations\)\. Contains standards\-related finding details\. Type: object Example: <pre>"Compliance": {<br />    "Status": "PASSED",<br />    "RelatedRequirements": ["Req1", "Req2"]<br />}</pre>  | 
|  `Confidence`  |  No  |  A finding's confidence\. Confidence is defined as the likelihood that a finding accurately identifies the behavior or issue that it was intended to identify\. A finding provider can provide an initial value for this attribute, but cannot update it after that\. This attribute can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\. Type: integer \(range 0–100\) Confidence is scored on a 0–100 basis using a ratio scale, where 0 means zero\-percent confidence and 100 means 100\-percent confidence\. However, a data exfiltration detection based on a statistical deviation of network traffic has a much lower confidence because an actual exfiltration hasn't been verified\. Example: <pre>"Confidence": 42</pre>  | 
|  `CreatedAt`  |  Yes  |  An ISO8601\-formatted timestamp \(as defined in [RFC\-3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)\) that indicates when the potential security issue captured by a finding was created\. Because the `CreatedAt` timestamp reflects the time when the finding record was created, it can differ from the `FirstObservedAt` timestamp, which reflects the time when the event or vulnerability was first observed\. This timestamp *must* be provided on the first generation of the finding and *can't* be changed upon subsequent updates to the finding\. Type: timestamp Example: <pre>"CreatedAt": "2017-03-22T13:22:13.933Z"</pre>  Findings are deleted 90 days after the most recent update or 90 days after the creation date if no update occurs\. To store findings for longer than 90 days, you can configure a rule in CloudWatch Events that routes findings to your Amazon S3 bucket\.  | 
|  `Criticality`  |  No  | The level of importance that is assigned to the resources associated with the finding\. A score of 0 means that the underlying resources have no criticality, and a score of 100 is reserved for the most critical resources\.  A finding provider can provide an initial value for this attribute, but cannot update it after that\. This attribute can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\. Type: integer \(range 0–100\) Criticality is scored on a 0–100 basis, using a ratio scale that supports only full integers\. This means that you should assess not only which findings impact resources that are more critical than others but also how much more critical those resources are compared to other resources\. A score of 0 means that the underlying resources have no criticality, and a score of 100 is reserved for the most critical resources\. When assessing criticality of a finding, consider the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) You can use the following guidelines: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Criticality": 99</pre>  | 
|  `Description`  |  Yes  | A finding's description\. This field can be nonspecific boilerplate text or details that are specific to the instance of the finding\. Type: string \(1,024 characters max\) Example: <pre>"Description": "The version of openssl found on instance i-abcd1234 is known to contain a vulnerability."</pre>  | 
|  `FirstObservedAt`  |  No  | An ISO8601\-formatted timestamp \(as defined in [RFC\-3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)\) that indicates when the potential security issue captured by a finding was first observed\. Type: timestamp Because this timestamp reflects the time of when the event or vulnerability was first observed, it can differ from the `CreatedAt` timestamp, which reflects the time this finding record was created\.  This timestamp should be immutable between updates of the finding record, but can be updated if a more accurate timestamp has been determined\. Example: <pre>"FirstObservedAt": "2017-03-22T13:22:13.933Z"</pre>  | 
|  `GeneratorId`  |  Yes  | The identifier for the solution\-specific component \(a discrete unit of logic\) that generated a finding\. In various solutions from security findings products, this generator can be called a rule, a check, a detector, a plug\-in, and so on\. Type: string \(512 characters max\) or Amazon Resource Name \(ARN\) Example: <pre>"GeneratorId": "acme-vuln-9ab348"</pre>  | 
|  `Id`  |  Yes  | The product\-specific identifier for a finding\. Type: string \(512 characters max\) or ARN The finding ID must comply with the following constraints: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) These constraints are expected to hold within a findings product, but are not required to hold across findings products\. Example: <pre>"Id": "us-west-2/111111111111/98aebb2207407c87f51e89943f12b1ef"</pre>  | 
|  `LastObservedAt`  |  No  | An ISO8601\-formatted timestamp \(as defined in [RFC\-3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)\) that indicates when the potential security issue captured by a finding was most recently observed by the security findings product\. Type: timestamp Because this timestamp reflects the time of when the event or vulnerability was last or most recently observed, it can differ from the `UpdatedAt` timestamp, which reflects the time this finding record was last or most recently updated\.  You can provide this timestamp, but it isn't required upon the first observation\. If you provide the field in this case, the timestamp should be the same as the `FirstObservedAt` timestamp\. You should update this field to reflect the last or most recently observed timestamp each time a finding is observed\. Example: <pre>"LastObservedAt": "2017-03-23T13:22:13.933Z"</pre>  | 
|  [`Malware`](#asff-malware)  |  No  | A list of malware related to a finding\. Type: array of up to five malware objects Example: <pre>"Malware": [<br />    {<br />        "Name": "Stringler",<br />        "Type": "COIN_MINER",<br />        "Path": "/usr/sbin/stringler",<br />        "State": "OBSERVED"<br />    }<br />]</pre>  | 
|  [`Network`](#asff-network)  |  No  | The details of network\-related information about a finding\. Type: object Example: <pre>"Network": {<br />    "Direction": "IN",<br />    "Protocol": "TCP",<br />    "SourceIpV4": "1.2.3.4",<br />    "SourceIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",<br />    "SourcePort": "42",<br />    "SourceDomain": "here.com",<br />    "SourceMac": "00:0d:83:b1:c0:8e",<br />    "DestinationIpV4": "2.3.4.5",<br />    "DestinationIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C",<br />    "DestinationPort": "80",<br />    "DestinationDomain": "there.com"<br />}</pre>  | 
|  [`Note`](#asff-note)  |  No  |  A user\-defined note that is added to a finding\. A finding provider can provide an initial note for a finding, but cannot add notes after that\. A note can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Notes can be added by both master accounts and member accounts\. Type: object Example: <pre>"Note": {<br />    "Text": "Don't forget to check under the mat.",<br />    "UpdatedBy": "jsmith",<br />    "UpdatedAt": "2018-08-31T00:15:09Z"<br />}</pre>  | 
|  [`Process`](#asff-process)  |  No  | The details of process\-related information about a finding\.Type: object Example: <pre>"Process": {<br />    "Name": "syslogd",<br />    "Path": "/usr/sbin/syslogd",<br />    "Pid": 12345,<br />    "ParentPid": 56789,<br />    "LaunchedAt": "2018-09-27T22:37:31Z",<br />    "TerminatedAt": "2018-09-27T23:37:31Z"<br />}</pre>  | 
|  `ProductArn`  |  Yes  | The ARN generated by Security Hub that uniquely identifies a third\-party findings product after the product is registered with Security Hub\. Type: ARN The format of this field is `arn:partition:securityhub:region:account-id:product/company-id/product-id`\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>// Private ARN<br />    "ProductArn": "arn:aws:securityhub:us-east-1:111111111111:product/111111111111/default"<br /><br />// Public ARN<br />    "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty"<br />    "ProductArn": "arn:aws:securityhub:us-west-2:222222222222:product/generico/secure-pro"</pre>  | 
|  `ProductFields`  |  No  | A data type where security findings products can include additional solution\-specific details that aren't part of the defined AWS Security Finding Format\. Type: map of up to 50 key/value pairs This field should not contain redundant data and must not contain data that conflicts with AWS Security Finding Format fields\. The "aws/" prefix represents a reserved namespace for AWS products and services only and must not be submitted with findings from partner products\. Although not required, products should format field names as `company-id/product-id/field-name`, where the `company-id` and `product-id` match those supplied in the `ProductArn` of the finding\. Field names can include alphanumeric characters, white space, and the following symbols: \_ \. / = \+ \\ \- @ Example: <pre>"ProductFields": {<br />    "generico/secure-pro/Count": "6",<br />    "generico/secure-pro/Action.Type", "AWS_API_CALL",<br />    "API", "DeleteTrail",<br />    "Service_Name": "cloudtrail.amazonaws.com",<br />    "aws/inspector/AssessmentTemplateName": "My daily CVE assessment",<br />    "aws/inspector/AssessmentTargetName": "My prod env",<br />    "aws/inspector/RulesPackageName": "Common Vulnerabilities and Exposures"<br />}</pre>  | 
|  `RecordState`  |  No  | The record state of a finding\.  By default, when initially generated by a service, findings are considered `ACTIVE`\. The `ARCHIVED` state indicates that a finding should be hidden from view\. Archived findings aren't deleted and remain in the service historically\. You can search, review, and report against them at any time\.  Type: enum Valid values: `ACTIVE` \| `ARCHIVED` Example: <pre>"RecordState": "ACTIVE"</pre>  | 
|  [`RelatedFindings`](#asff-relatedfindings)  |  No  | A list of related findings\.  A finding provider can provide an initial list of related findings, but cannot update the list after that\. The list of related findings can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\. Type: array of up to 10 `RelatedFinding` objects Example: <pre>"RelatedFindings": [<br />    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", <br />      "Id": "123e4567-e89b-12d3-a456-426655440000" },<br />    { "ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty", <br />      "Id": "AcmeNerfHerder-111111111111-x189dx7824" }<br />]</pre>  | 
|  [`Remediation`](#asff-remediation)  |  No  | The remediation options for a finding\. Type: object Example: <pre>"Remediation": {<br />    "Recommendation": {<br />        "Text": "Run sudo yum update and cross your fingers and toes.",<br />        "Url": "http://myfp.com/recommendations/dangerous_things_and_how_to_fix_them.html"<br />    }<br />}</pre>  | 
|  [`Resources`](#asff-resources)  |  Yes  | A set of resource data types that describe the resources that the finding refers to\. Type: array of up to 32 resource objects Example: <pre>"Resources": [<br />  {<br />    "Type": "AwsEc2Instance",<br />    "Id": "i-cafebabe",<br />    "Partition": "aws",<br />    "Region": "us-west-2",<br />    "Tags": {<br />      "billingCode": "Lotus-1-2-3",<br />      "needsPatching": "true"<br />    },<br />    "Details": {<br />      "AwsEc2Instance": {<br />        "Type": "i3.xlarge",<br />        "ImageId": "ami-abcd1234",<br />        "IpV4Addresses": [ "54.194.252.215", "192.168.1.88" ],<br />        "IpV6Addresses": [ "2001:db8:1234:1a2b::123" ],<br />        "KeyName": "my_keypair",<br />        "IamInstanceProfileArn": "arn:aws:iam::111111111111:instance-profile/AdminRole",<br />        "VpcId": "vpc-11112222",<br />        "SubnetId": "subnet-56f5f633",<br />        "LaunchedAt": "2018-05-08T16:46:19.000Z"<br />      }  <br />    }<br />  }<br />]</pre>  | 
|  `SchemaVersion`  |  Yes  | The schema version that a finding is formatted for\. The value of this field must be one of the officially published versions identified by AWS\. In the current release, the AWS Security Finding Format schema version is `2018-10-08`\.  Type: string \(10 characters max, conforms to `YYYY-MM-DD`\) Example: <pre>"SchemaVersion": "2018-10-08"</pre>  | 
|  [`Severity`](#asff-severity)  |  Yes  | A finding's severity\. The finding must have either `Label` or `Normalized` populated\. `Label` is the preferred attribute\. If neither attribute is populated, then the finding is invalid\. A finding provider can provide initial severity information for a finding, but cannot update it after that\. The severity information can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\.Type: object Example: <pre>"Severity": {<br />    "Label": "CRITICAL",<br />    "Product": 8.3<br />}</pre>  | 
|  `SourceUrl`  |  No  | A URL that links to a page about the current finding in the finding product\. Type: URL | 
|  [`ThreatIntelIndicators`](#asff-threatintelindicators)  |  No  | Threat intelligence details that are related to a finding\. Type: array of up to five threat intelligence indicator objects Example: <pre>"ThreatIntelIndicators": [<br />  {<br />    "Type": "IPV4_ADDRESS",<br />    "Value": "8.8.8.8",<br />    "Category": "BACKDOOR",<br />    "LastObservedAt": "2018-09-27T23:37:31Z",<br />    "Source": "Threat Intel Weekly",<br />    "SourceUrl": "http://threatintelweekly.org/backdoors/8888"<br />  }<br />]</pre>  | 
|  `Title`  |  Yes  | A finding's title\. This field can contain nonspecific boilerplate text or details that are specific to this instance of the finding\.Type: string \(256 characters max\) | 
|  `Types`  |  Yes  | One or more finding types in the format of `namespace/category/classifier` that classify a finding\. Type: array of 50 strings max [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Namespaces are required for all finding types, but categories and classifiers are optional\. If you specify a classifier, you must also specify a category\. The '`/`' character is reserved and must *not* be used in a category or classifier\. Escaping the '`/`' character is not supported\. Example: <pre>"Types": [<br />    "Software and Configuration Checks/Vulnerabilities/CVE"<br />]</pre>  | 
|  `UpdatedAt`  |  Yes  | An ISO8601\-formatted timestamp \(as defined in [RFC\-3339 Date and Time on the Internet: Timestamps](https://tools.ietf.org/html/rfc3339)\) that indicates when the findings product last updated the finding record\. Because this timestamp reflects the time when the finding record was last or most recently updated, it can differ from the `LastObservedAt` timestamp, which reflects when the event or vulnerability was last or most recently observed\. When you update the finding record, you must update this timestamp to the current timestamp\. Upon creation of a finding record, the `CreatedAt` and `UpdatedAt` timestamps must be the same timestamp\. After an update to the finding record, the value of this field must be greater than all of the previous values that it contained\. Note that `UpdatedAt` is not updated by changes from [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) \. It is only updated by [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) \.Type: timestamp Findings are deleted 90 days after the most recent update or 90 days after the creation date if no update occurs\. To store findings for longer than 90 days, you can configure a rule in CloudWatch Events that routes findings to your Amazon S3 bucket\.  | 
|  `UserDefinedFields`  |  No  | A list of name/value string pairs that are associated with the finding\. These are custom, user\-defined fields that are added to a finding\. These fields can be generated automatically via your specific configuration\. Findings products must *not* use this field for data that the product generates\. Instead, findings products can use the `ProductFields` field for data that doesn't map to any standard AWS Security Finding Format field\. These fields can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) \. They can only be updated by a master account\. They cannot be updated by a member account\.Type: map of up to 50 key/value pairs Example: <pre>"UserDefinedFields": {<br />    "reviewedByCio": "true",<br />    "comeBackToLater": "Check this again on Monday"<br />}</pre>  | 
|  `VerificationState`  |  No  | The veracity of a finding\. Findings products can provide the value of `UNKNOWN` for this field\. A findings product should provide this value if there is a meaningful analog in the findings product's system\. This field is typically populated by a user determination or action after they have investigated a finding\. A finding provider can provide an initial value for this attribute, but cannot update it after that\. This attribute can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) \. It can only be updated by a master account\. It cannot be updated by a member account\.Type: enum Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 
|  [`Workflow`](#asff-workflow)  |  No  |  Provides information about the status of the investigation into a finding\. The workflow status is not intended for finding providers\. The workflow status can only be updated using `BatchUpdateFindings` \. Customers can also update it from the console\. See[Setting the workflow status for a finding](finding-workflow-status.md)\. The workflow status can only be updated by a master account\. It cannot be updated by a member account\. Type: object Example: <pre>Workflow: {<br />    "Status": "NEW"<br />}</pre>  | 
|  `WorkflowState` \(deprecated\)  |  No  |  This field is being deprecated in favor of the `Status` field of the `Workflow` object\.The workflow state of a finding\. Findings products can provide the value of `NEW` for this field\. A findings product can provide a value for this field if there is a meaningful analog in the findings product's system\. Type: enum Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"WorkflowState": "NEW"</pre>  | 

**Contents**
+ [Compliance](#asff-compliance)
+ [Malware](#asff-malware)
+ [Network](#asff-network)
+ [Note](#asff-note)
+ [Process](#asff-process)
+ [RelatedFindings](#asff-relatedfindings)
+ [Remediation](#asff-remediation)
  + [Recommendation](#asff-remediation-recommendation)
+ [Resources](#asff-resources)
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
  + [How Security Hub maps `Label` and `Normalized` values](#asff-severity-map-normalized-label)
  + [Guidance for Assigning the Normalized Severity \(AWS Services and Partners\)](#asff-severity-normalized-guidance)
+ [ThreatIntelIndicators](#asff-threatintelindicators)
+ [Workflow](#asff-workflow)

### Compliance<a name="asff-compliance"></a>

Exclusive to findings that are generated as the result of a check run against a specific rule in a supported standard \(for example, CIS AWS Foundations\)\. Contains standards\-related finding details\.

Example:

```
"Compliance": {
    "Status": "PASSED",
    "RelatedRequirements": ["Req1", "Req2"]
}
```

The `Compliance` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Status`  | No | The result of a security check\. Type: enum Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Status": "PASSED"</pre>  | 
|  `RelatedRequirements`  |  No  |  For a Security Hub control, the related requirements within an industry or regulatory framework\. The check for that control is aligned with those requirements\. You can provide up to 32 related requirements\. To identify a requirement, use its identifier\. Type: array of strings  | 

### Malware<a name="asff-malware"></a>

The `Malware` object provides a list of malware related to a finding\. It is an array that can contain up to 5 malware objects\.

Example:

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
|  `Name`  |  Yes  | The name of the malware that was observed\. Type: string \(64 characters max\) Example: <pre>"Name": "Stringler"</pre>  | 
|  `Path`  |  No  | The filesystem path of the malware that was observed\.  Type: string \(512 characters max\) Example: <pre>"Path": "/usr/sbin/stringler"</pre>  | 
|  `State`  |  No  | The state of the malware that was observed\. Type: enum  Valid values: `OBSERVED` \| `REMOVAL_FAILED` \| `REMOVED` Example: <pre>"State": "OBSERVED"</pre>  | 
|  `Type`  |  No  | The type of the malware that was observed\. Type: enum Valid values: `ADWARE` \| `BLENDED_THREAT` \| `BOTNET_AGENT` \| `COIN_MINER` \| `EXPLOIT_KIT` \| `KEYLOGGER` \| `MACRO` \| `POTENTIALLY_UNWANTED` \| `SPYWARE` \| `RANSOMWARE` \| `REMOTE_ACCESS` \| `ROOTKIT` \| `TROJAN` \| `VIRUS` \| `WORM` Example: <pre>"Type": "COIN_MINER"</pre>  | 

### Network<a name="asff-network"></a>

The details of network\-related information about a finding\.

Type: object

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
|  `DestinationDomain`  |  No  | The destination domain of network\-related information about a finding\.Type: string \(128 characters max\) Example: <pre>"DestinationDomain": "there.com"</pre>  | 
|  `DestinationIpV4`  |  No  | The destination IPv4 address of network\-related information about a finding\.Type: IPv4 Example: <pre>"DestinationIpV4": "2.3.4.5"</pre>  | 
|  `DestinationIpV6`  |  No  | The destination IPv6 address of network\-related information about a finding\. Type: IPv6 Example: <pre>"DestinationIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C"</pre>  | 
|  `DestinationPort`  |  No  | The destination port of network\-related information about a finding\.Type: number \(range of 0–65535\) Example: <pre>"DestinationPort": "80"</pre>  | 
|  `Direction`  |  No  | The direction of network traffic associated with a finding\. Type: enum Valid values: `IN` \| `OUT` Example: <pre>"Direction": "IN"</pre>  | 
|  `Protocol`  |  No  | The protocol of network\-related information about a finding\. Type: string \(16 characters max\) The name should be the [IANA registered name](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml) for the associated port except in the case where the finding product can determine a more accurate protocol\. Example: <pre>"Protocol": "TCP"</pre>  | 
|  `SourceDomain`  |  No  | The source domain of network\-related information about a finding\.  Type: string \(128 characters max\) Example: <pre>"SourceDomain": "here.com"</pre>  | 
|  `SourceIpV4`  |  No  | The source IPv4 address of network\-related information about a finding\. Type: IPv4 Example: <pre>"SourceIpV4": "1.2.3.4"</pre>  | 
|  `SourceIpV6`  |  No  | The source IPv6 address of network\-related information about a finding\.Type: IPv6 Example: <pre>"SourceIpV6": "FE80:CD00:0000:0CDE:1257:0000:211E:729C"</pre>  | 
|  `SourceMac`  |  No  | The source media access control \(MAC\) address of network\-related information about a finding\.Type: string \(must match `MM:MM:MM:SS:SS:SS`\) Example: <pre>"SourceMac": "00:0d:83:b1:c0:8e"</pre>  | 
|  `SourcePort`  |  No  | The source port of network\-related information about a finding\. Type: number \(range of 0–65535\) Example: <pre>"SourcePort": "80"</pre>  | 

### Note<a name="asff-note"></a>

The `Note` object adds a user\-defined note to the finding\.

A finding provider can provide an initial note for a finding, but cannot add notes after that\. A note can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Notes can be added by both master accounts and member accounts\.

Example:

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
|  `Text`  |  Yes  | The text of a finding note\.Type: string \(512 characters max\)  Example: <pre>"Text": "Example text."</pre>  | 
|  `UpdatedAt`  |  Yes  | The timestamp of when the note was updated\.Type: timestamp Example: <pre>"UpdatedAt": "2018-08-31T00:15:09Z"</pre>  | 
|  `UpdatedBy`  |  Yes  | The principal that created a note\.Type: string \(512 characters max\) or ARN Example: <pre>"UpdatedBy": "jsmith"</pre>  | 

### Process<a name="asff-process"></a>

The `Process` object provides process\-related details about the finding\.

Example:

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
|  `LaunchedAt`  |  No  | The timestamp for the date and time when the process was launched\. Type: timestamp Example: <pre>"LaunchedAt": "2018-09-27T22:37:31Z"</pre>  | 
|  `Name`  |  No  | The name of the process\.Type: string \(64 characters max\) Example: <pre>"Name": "syslogd"</pre>  | 
|  `ParentPid`  |  No  | The parent process ID\.Type: number Example: <pre>"ParentPid": 56789</pre>  | 
|  `Path`  |  No  | The path to the process executable\. Type: string \(512 characters max\) Example: <pre>"Path": "/usr/sbin/syslogd"</pre>  | 
|  `Pid`  |  No  | The process ID\. Type: number Example: <pre>"Pid": 12345</pre>  | 
|  `TerminatedAt`  |  No  | The timestamp for the date and time when the process was terminated\. Type: timestamp Example: <pre>"TerminatedAt": "2018-09-27T23:37:31Z"</pre>  | 

### RelatedFindings<a name="asff-relatedfindings"></a>

The `RelatedFindings` object provides a list of findings that are related to the current finding\.

A finding provider can provide an initial list of related findings, but cannot update it after that\. `RelatedFindings` can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\.

Example:

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
|  `Id`  |  Yes  | The product\-generated identifier for a related finding\. Type: string \(512 characters max\) or ARN Example: <pre>"Id": "123e4567-e89b-12d3-a456-426655440000"</pre>  | 
|  `ProductArn`  |  Yes  | The ARN of the product that generated a related finding\. Type: ARN Example: <pre>"ProductArn": "arn:aws:securityhub:us-west-2::product/aws/guardduty"</pre>  | 

### Remediation<a name="asff-remediation"></a>

The `Remediation` object provides information about recommended remediation steps to address the finding\.

Example:

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
|  [`Recommendation`](#asff-remediation-recommendation)  |  No  | A recommendation on how to remediate the issue identified within a finding\. The `Recommendation` field is meant to facilitate manual instructions or details to resolve a finding\. If the recommendation object is present, then either the `Text` or `Url` field must be present and populated\. Both fields can be present and populated\. Type: object Example: <pre>"Recommendation": {<br />    "Text": "Example text.",<br />    "Url": "http://myfp.com/recommendations/dangerous_things_and_how_to_fix_them.html"<br />}</pre>  | 

#### Recommendation<a name="asff-remediation-recommendation"></a>

The `Recommendation` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Text`  |  No  |  A free\-form string that is the recommendation of what to do about the finding when presented to a user\. This field can contain nonspecific boilerplate text or details that are specific to this instance of the finding\. Type: string \(512 characters max\) Example: <pre>"Text": "Example text."</pre>  | 
|  `Url`  |  No  |  A URL to link to general remediation information for the finding type of a finding\. This URL must not require credentials to access\. It must be accessible from the public internet and must not expect any context or session\. Type: URL Example: <pre>"Url": "http://myfp.com/recommendations/example_domain.html"</pre>  | 

### Resources<a name="asff-resources"></a>

The `Resources` object provides information about the resources involved in a finding\.

Type: array of up to 10 resource objects

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
|  `Details`  |  No  |  This field provides additional details about a single resource using the appropriate subfields\. Each resource must be provided in a separate resource object in the `Resources` field\. Security Hub provides a set of available subfields for its supported resource types\. These subfields correspond to values of the resource `Type`\. Use the provided types and subfields whenever possible\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) For example, if the resource is an S3 bucket, then set the resource `Type` to `AwsS3Bucket`, and provide the resource details in the `AwsS3Bucket` subfield\. The [`Other`](#asff-resourcedetails-other) subfield allows you to provide custom fields and values\. You use the `Other` subfield in the following cases\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Type: object Example: <pre>"Details": {<br />  "AwsEc2Instance": {<br />    "Type": "i3.xlarge",<br />    "ImageId": "ami-abcd1234",<br />    "IpV4Addresses": [ "54.194.252.215", "192.168.1.88" ],<br />    "IpV6Addresses": [ "2001:db8:1234:1a2b::123" ],<br />    "KeyName": "my_keypair",<br />    "IamInstanceProfileArn": "arn:aws:iam::111111111111:instance-profile/AdminRole",<br />    "VpcId": "vpc-11112222",<br />    "SubnetId": "subnet-56f5f633",<br />    "LaunchedAt": "2018-05-08T16:46:19.000Z"<br />  },<br />  "AwsS3Bucket": {<br />    "OwnerId": "da4d66eac431652a4d44d490a00500bded52c97d235b7b4752f9f688566fe6de",<br />    "OwnerName": "acmes3bucketowner"<br />  },<br />  "Other": [<br />    { "Key": "LightPen", "Value": "blinky" },<br />    { "Key": "SerialNo", "Value": "1234abcd" }<br />  ]<br />}</pre>  | 
|  `Id`  |  Yes  | The canonical identifier for the given resource type\. For AWS resources that are identified by ARNs, this must be the ARN\. For all other AWS resource types that lack ARNs, this must be the identifier as defined by the AWS service that created the resource\. For non\-AWS resources, this should be a unique identifier associated with the resource\.Type: string \(512 characters max\) or ARN Example: <pre>"Id": "arn:aws:s3:::example-bucket"</pre>  | 
|  `Partition`  |  No  | The canonical AWS partition name that the Region is assigned to\.  Type: enum Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Partition": "aws"</pre>  | 
|  `Region`  |  No  | The canonical AWS external Region name where this resource is located\. Type: string \(16 characters max\) Example: <pre>"Region": "us-west-2"</pre>  | 
|  `Tags`  |  No  | A list of AWS tags that are associated with a resource at the time the finding was processed\. Include the `Tags` attribute only for resources that have an associated tag\. If a resource has no associated tag, don't include a `Tags` attribute in the finding\. Type: map of up to 50 tags \(values are limited to 256 characters max\) The following basic restrictions apply to tags: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Tags": {<br />    "billingCode": "Lotus-1-2-3",<br />    "needsPatching": "true"<br />}</pre>  | 
|  `Type`  |  Yes  |  The type of the resource that you are providing details for\. Whenever possible, use one of the provided resource types, such as `AwsEc2Instance` or `AwsS3Bucket`\. If the resource type does not match any the provided resource types, then set the resource `Type` to `Other`, and use the `Other` details subfield to populate the details\. Type: string \(32 characters max\) Valid values are as follows\. If a type has a corresponding subfield, then to view the details for the subfield, choose the type name\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Example: <pre>"Type": "AwsS3Bucket"</pre>  | 
| aws | Commercial | 
| aws\-cn | China | 
| aws\-us\-gov | AWS GovCloud \(US\) | 

#### AwsCloudFrontDistribution<a name="asff-resourcedetails-awscloudfrontdistribution"></a>

The `AwsCloudFrontDistribution` object provides details about a distribution configuration\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DomainName`  |  No  | The domain name corresponding to the distribution\.Type: string | 
|  `Etag`  |  No  | The entity tag is a hash of the object\.Type: string | 
|  `LastModifiedTime`  |  No  | The date and time that the distribution was last modified\.Type: string | 
|  [`Logging`](#asff-resourcedetails-awscloudfrontdistribution-logging)  |  No  | A complex type that controls whether access logs are written for the distribution\.Type: object | 
|  [`Origins`](#asff-resourcedetails-awscloudfrontdistribution-origins)  |  No  | A complex type that contains information about origins and origin groups for this distribution\.Type: string | 
|  `Status`  |  No  | Indicates the current status of the distribution\.Type: string | 
|  `WebAclId`  |  No  | A unique identifier that specifies the AWS WAF web ACL, if any, to associate with this distribution\.Type: string | 

##### Logging<a name="asff-resourcedetails-awscloudfrontdistribution-logging"></a>

The `Logging` object provides information about the logging for the distribution\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Bucket`  |  No  | The S3 bucket to store the access logs in\.Type: string | 
|  `Enabled`  |  No  | With this field, you can enable or disable the selected distribution\.Type: Boolean | 
|  `IncludeCookies`  |  No  | Specifies whether you want CloudFront to include cookies in access logs\.Type: Boolean | 
|  `Prefix`  |  No  | An optional string that you want CloudFront to prefix to the access log filenames for this distribution\.Type: string | 

##### Origins<a name="asff-resourcedetails-awscloudfrontdistribution-origins"></a>

The `Origins` object contains information about origins and origin groups for this distribution\.

It can contain the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Items`  |  No  |  A complex type that contains origins or origin groups for this distribution\. Type: object  | 

Each item can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `OriginPath`  |  No  |  An optional element that causes CloudFront to request your content from a directory in your S3 bucket or your custom origin\. Type: string  | 
|  `Id`  |  No  |  A unique identifier for the origin or origin group\. Type: string  | 
|  `DomainName`  |  No  |  Amazon S3 origins: The DNS name of the S3 bucket from which you want CloudFront to get objects for this origin\. Type: string  | 

#### AwsCodeBuildProject<a name="asff-resourcedetails-awscodebuildproject"></a>

The `AwsCodeBuildProject` object provides information about an AWS CodeBuild project\.

Example:

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
|  `EncryptionKey`  |  No  |  The AWS KMS customer master key \(CMK\) to be used for encrypting the build output artifacts\.  You can use a cross\-account KMS key to encrypt the build output artifacts if your service role has permission to that key\.  You can specify either the ARN of the CMK or, if available, the CMK alias \(using the format *alias*/*alias\-name*\)\. Type: string Length constraints: Minimum length of 1  | 
|  [`Environment`](#asff-resourcedetails-awscodebuildproject-environment)  |  No  |  Information about the build environment for this build project\. Type: object  | 
|  `Name`  |  No  |  The name of the build project\. Type: string Length constraints: Minimum length of 2\. Maximum length of 255\. Pattern: \[A\-Za\-z0\-9\]\[A\-Za\-z0\-9\\\-\_\]\{1,254\}  | 
|  `ServiceRole`  |  No  |  The ARN of the IAM role that enables CodeBuild to interact with dependent AWS services on behalf of the AWS account\. Type: string Length constraints: Minimum length of 1  | 
|  [`Source`](#asff-resourcedetails-awscodebuildproject-source)  |  No  |  Information about the build input source code for this build project\. Type: object  | 
|  [`VpcConfig`](#asff-resourcedetails-awscodebuildproject-vpcconfig)  |  No  |  Information about the VPC configuration that CodeBuild accesses\. Type: object  | 

##### Environment<a name="asff-resourcedetails-awscodebuildproject-environment"></a>

The `Environment` object provides information about the build environment for the build project\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Certificate`  |  No  |  The certificate to use with this build project\. Type: string  | 
|  `ImagePullCredentialsType`  |  No  |  The type of credentials CodeBuild uses to pull images in your build\. There are two valid values: `CODEBUILD` specifies that CodeBuild uses its own credentials\. This requires that you modify your ECR repository policy to trust the CodeBuild service principal\. `SERVICE_ROLE` specifies that CodeBuild uses your build project's service role\. When you use a cross\-account or private registry image, you must use `SERVICE_ROLE` credentials\. When you use a CodeBuild curated image, you must use `CODEBUILD` credentials\. Type: string Valid values: `CODEBUILD` \| `SERVICE_ROLE`  | 
|  `RegistryCredential`  |  No  |  The credentials for access to a private registry\. Type: object  | 
|  `Type`  |  Yes  |  The type of build environment to use for related builds\. Type: string Valid values: `WINDOWS_CONTAINER` \| `LINUX_CONTAINER` \| `LINUX_GPU_CONTAINER` \| `ARM_CONTAINER`  | 

Each registry credential in the `RegistryCredentials` object has the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Credential`  |  Yes  |  The ARN or name of credentials created using AWS Secrets Manager\.  The credential can use the name of the credentials only if they exist in your current AWS Region\.  Type: string Length constraints: Minimum length of 1  | 
|  `CredentialProvider`  |  Yes  |  The service that created the credentials to access a private Docker registry\. The valid value,` SECRETS_MANAGER`, is for Secrets Manager\. Type: string Valid values: `SECRETS_MANAGER`  | 

##### Source<a name="asff-resourcedetails-awscodebuildproject-source"></a>

The `Source` object provides information about the build input source code for this build project\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `GitCloneDepth`  |  No  |  Information about the Git clone depth for the build project\. Type: integer Valid range: Minimum value of 0  | 
|  `Location`  |  No  |  Information about the location of the source code to be built\. Type: string Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 
|  `Type`  |  Yes  |  The type of repository that contains the source code to be built\. Type: String Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 

##### VpcConfig<a name="asff-resourcedetails-awscodebuildproject-vpcconfig"></a>

The `VpcConfig` object provides information about the VPC configuration that CodeBuild accesses\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `SecurityGroupIds`  |  No  |  A list of one or more security group IDs in your Amazon VPC\. Type: Array of strings Array members: Maximum number of 5 items Length constraints: Minimum length of 1  | 
|  `Subnets`  |  No  |  A list of one or more subnet IDs in your Amazon VPC\. Type: Array of strings Array members: Maximum number of 16 items Length constraints: Minimum length of 1  | 
|  VpcId  |  No  |  The ID of the VPC\. Type: string Length constraints: Minimum length of 1  | 

#### AwsEc2Instance<a name="asff-resourcedetails-awsec2instance"></a>

The details of an Amazon EC2 instance\.

Type: object

The `AwsEc2Instance` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `IamInstanceProfileArn`  |  No  | The IAM profile ARN of the instance\. Type: string \(conforms to the AWS ARN format\) | 
|  `ImageId`  |  No  | The Amazon Machine Image \(AMI\) ID of the instance\.Type: string \(64 characters max\) | 
|  `IpV4Addresses`  |  No  | The IPv4 addresses that are associated with the instance\.Type: array of up to 10 IPv4 addresses | 
|  `IpV6Addresses`  |  No  | The IPv6 addresses that are associated with the instance\.Type: array of up to 10 IPv6 addresses | 
|  `KeyName`  |  No  | The key name that is associated with the instance\.Type: string \(128 characters max\) | 
|  `LaunchedAt`  |  No  | The date and time when the instance was launched\. Type: timestamp | 
|  `SubnetId`  |  No  | The identifier of the subnet where the instance was launched\. Type: string \(32 characters max\) | 
|  `Type`  |  No  | The instance type of the instance\. This must be a valid [EC2 instance type](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html)\. Type: string \(16 characters max\) | 
|  `VpcId`  |  No  | The identifier of the VPC where the instance was launched\. Type: string \(32 characters max\) | 

#### AwsEc2NetworkInterface<a name="asff-resourcedetails-awsec2networkinterface"></a>

The `AwsEc2NetworkInterface` object provides information about an Amazon EC2 network interface\.

Example:

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
|  [`Attachment`](#asff-resourcedetails-awsec2networkinterface-attachment)  |  No  |  Information about the network interface attachment\. Type: object  | 
|  `NetworkInterfaceId`  |  No  |  The ID of the network interface\. Type: string  | 
|  [`SecurityGroups`](#asff-resourcedetails-awsec2networkinterface-securitygroups)  |  No  |  Security groups for the network interface\. Type: array of group objects  | 
|  `SourceDestCheck`  |  No  |  Indicates whether traffic to or from the instance is validated\. Type: Boolean  | 

##### Attachment<a name="asff-resourcedetails-awsec2networkinterface-attachment"></a>

The `Attachment` object provides information about the network interface attachment\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AttachmentId`  |  No  |  The identifier of the network interface attachment Type: string  | 
|  `AttachTime`  |  No  |  The timestamp indicating when the attachment initiated\. Type: timestamp  | 
|  `DeleteOnTermination`  |  No  |  Indicates whether the network interface is deleted when the instance is terminated\. Type: Boolean  | 
|  `DeviceIndex`  |  No  |  The device index of the network interface attachment on the instance\. Type: integer  | 
|  `InstanceId`  |  No  |  The ID of the instance\. Type: string  | 
|  `InstanceOwnerId`  |  No  |  The AWS account ID of the owner of the instance\. Type: string  | 
|  `Status`  |  No  |  The attachment state\. Type: String Valid values: `attaching` \| `attached` \| `detaching` \| `detached`  | 

##### SecurityGroups<a name="asff-resourcedetails-awsec2networkinterface-securitygroups"></a>

The `SecurityGroups` object contains the list of security groups for the network interface\.

Each security group can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `GroupId`  |  No  |  The ID of the security group\. Type: string  | 
|  GroupName  |  |  The name of the security group\. Type: string  | 

#### AwsEc2SecurityGroup<a name="asff-resourcedetails-awsec2securitygroup"></a>

The `AwsEc2SecurityGroup` object describes an Amazon EC2 security group\.

Example:

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
|  `GroupId`  |  No  |  The ID of the security group\. Type: string  | 
|  `GroupName`  |  No  |  The name of the security group\. Type: string  | 
|  [`IpPermissions`](#asff-resourcedetails-awsec2securitygroup-ippermission)  |  No  |  The inbound rules associated with the security group\. Type: array of IP permission objects  | 
|  [`IpPermissionsEgress`](#asff-resourcedetails-awsec2securitygroup-ippermission)  |  No  |  \[VPC only\] The outbound rules associated with the security group\. Type: Array of IP permission objects  | 
|  `OwnerId`  |  No  |  The AWS account ID of the owner of the security group\. Type: String  | 
|  `VpcId`  |  No  |  \[VPC only\] The ID of the VPC for the security group\. Type: String  | 

##### IP permission object<a name="asff-resourcedetails-awsec2securitygroup-ippermission"></a>

The `IpPermissions` and `IpPermissionsEgress` objects both contain an array of IP permission objects\.

Each IP permission object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `FromPort`  |  No  |  The start of the port range for the TCP and UDP protocols, or an ICMP/ICMPv6 type number\. A value of `-1` indicates all ICMP/ICMPv6 types\. If you specify all ICMP/ICMPv6 types, you must specify all codes\. Type: integer  | 
|  `IpProtocol`  |  No  |  The IP protocol name \(`tcp`, `udp`, `icmp`, `icmpv6`\) or number \(see the [protocol numbers list](http://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml)\)\. \[VPC only\] Use `-1` to specify all protocols\. When authorizing security group rules, specifying `-1` or a protocol number other than `tcp`, `udp`, `icmp`, or `icmpv6` allows traffic on all ports, regardless of any port range you specify\. For `tcp`, `udp`, and `icmp`, you must specify a port range\. For `icmpv6`, the port range is optional\. If you omit the port range, traffic for all types and codes is allowed\. Type: string  | 
|  `IpRanges`  |  No  |  The ranges of IP addresses\. Type: array of IP range objects  | 
|  `PrefixListIds`  |  No  |  \[VPC only\] The prefix list IDs for an AWS service\. With outbound rules, this is the AWS service to access through a VPC endpoint from instances associated with the security group\. Type: array of prefix list ID objects  | 
|  `ToPort`  |  No  |  The end of the port range for the TCP and UDP protocols, or an ICMP/ICMPv6 code\. A value of `-1` indicates all ICMP/ICMPv6 codes\. If you specify all ICMP/ICMPv6 types, you must specify all codes\. Type: integer  | 
|  `UserIdGroupPairs`  |  No  |  The security group and AWS account ID pairs\. Type: array of user ID group pair objects  | 

Each entry in the `IpRanges` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CidrIp`  |  No  |  A range of IP addresses\. You can either specify a CIDR range or a source security group, but not both\. To specify a single IPv4 address, use the /32 prefix length\. To specify a single IPv6 address, use the /128 prefix length\. Type: string  | 

Each entry in the `PrefixListIds` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `PrefixListId`  |  No  |  The ID of the prefix\. Type: String  | 

Each entry in the `UserIdGroupPairs` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  GroupId  |  No  |  The ID of the security group\. Type: string  | 
|  UserId  |  No  |  The ID of an AWS account\. For a referenced security group in another VPC, the account ID of the referenced security group is returned in the response\. If the referenced security group is deleted, this value is not returned\. \[Amazon EC2\-Classic\] Required when adding or removing rules that reference a security group in another AWS account\. Type: string  | 

#### AwsElasticSearchDomain<a name="asff-resourcedetails-awselasticsearchdomain"></a>

The `AwsElasticSearchDomain` object provides details about an Elasticsearch domain\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AccessPolicies`  |  No  |  IAM policy document specifying the access policies for the new Amazon ES domain\. Type: string  | 
|  [`DomainEndpointOptions`](#asff-resourcedetails-awselasticsearchdomain-domainendpointoptions)  |  No  |  Additional options for the domain endpoint\. Type: object  | 
|  [`DomainStatus`](#asff-resourcedetails-awselasticsearchdomain-domainstatus)  |  No  |  Details about the domain status\. Type: object  | 
|  `ElasticsearchVersion`  |  No  |  Elasticsearch version\. Type: string  | 
|  [`EncryptionAtRestOptions`](#asff-resourcedetails-awselasticsearchdomain-encryptionatrestoptions)  |  No  |  Details about the configuration for encryption at rest\. Type: object  | 
|  [`NodeToNodeEncryptionOptions`](#asff-resourcedetails-awselasticsearchdomain-nodetonodeencryptionoptions)  |  No  |  Details about the configuration for node\-to\-node encryption\. Type: object  | 
|  [`VPCOptions`](#asff-resourcedetails-awselasticsearchdomain-vpcoptions)  |  No  |  Information that Amazon ES derives based on `VPCOptions` for the domain\. Type: object  | 

##### DomainEndpointOptions<a name="asff-resourcedetails-awselasticsearchdomain-domainendpointoptions"></a>

The `DomainEndpointOptions` object provides information about additional options for the domain endpoint\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `EnforceHTTPS`  |  No  |  Whether to require that all traffic to the domain arrive over HTTPS\. Type: Boolean  | 
|  `TLSSecurityPolicy`  |  No  |  The TLS security policy to apply to the HTTPS endpoint of the Elasticsearch domain\. Type: string Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 

##### DomainStatus<a name="asff-resourcedetails-awselasticsearchdomain-domainstatus"></a>

The `DomainStatus` object provides details about the domain status\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `DomainId`  |  No  |  Unique identifier for an Amazon ES domain\. Type: string  | 
|  `DomainName`  |  No  |  Name of an Amazon ES domain\. Domain names are unique across all domains owned by the same account within an AWS Region\. Domain names must start with a lowercase letter and must be between 3 and 28 characters\. Valid characters are a\-z \(lowercase only\), 0\-9, and – \(hyphen\)\. Type: string  | 
|  `Endpoint`  |  No  |  Domain\-specific endpoint used to submit index, search, and data upload requests to an Amazon ES domain\. The endpoint is a service URL\. Type: string  | 
|  `Endpoints`  |  No  |  The key\-value pair that exists if the Amazon ES domain uses VPC endpoints\. Type: map of key\-value pairs Example: <pre>"vpc": "<VPC_ENDPOINT>"</pre>  | 

##### EncryptionAtRestOptions<a name="asff-resourcedetails-awselasticsearchdomain-encryptionatrestoptions"></a>

The `EncryptionAtRestOptions` object provides details about the configuration for encryption at rest\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Enabled`  |  No  |  Whether encryption at rest is enabled\. Type: Boolean  | 
|  `KmsKeyId`  |  No  |  The AWS KMS key ID\. Takes the form `1a2a3a4-1a2a-3a4a-5a6a-1a2a3a4a5a6a`\. Type: string  | 

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
|  `AvailabilityZones`  |  No  |  The list of Availability Zones associated with the VPC subnets\. Type: array of strings  | 
|  `SecurityGroupIds`  |  No  |  The list of security group IDs associated with the VPC endpoints for the domain Type: array of strings\.  | 
|  `SubnetIds`  |  No  |  A list of subnet IDs associated with the VPC endpoints for the domain\. Type: array of strings  | 
|  `VPCId`  |  No  |  ID for the VPC\. Type: string  | 

#### AwsElbv2LoadBalancer<a name="asff-resourcedetails-awselbv2loadbalancer"></a>

The `AwsElbv2LoadBalancer` object provides information about a load balancer\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`AvailabilityZones`](#asff-resourcedetails-awselbv2loadbalancer-availabilityzones)  |  No  | The Availability Zones for the load balancer\.Type: object | 
|  `CanonicalHostedZoneId`  |  No  | The ID of the Amazon Route 53 hosted zone associated with the load balancer\.Type: string | 
|  `CreatedTime`  |  No  | The date and time the load balancer was created\.Type: string | 
|  `DNSName`  |  No  | The public DNS name of the load balancer\.Type: string | 
|  `IpAddressType`  |  No  | The type of IP addresses used by the subnets for your load balancer\. The possible values are `ipv4` \(for IPv4 addresses\) and `dualstack` \(for IPv4 and IPv6 addresses\)\.Type: string | 
|  `Scheme`  |  No  | The nodes of an Internet\-facing load balancer have public IP addresses\.Type: string | 
|  `SecurityGroups`  |  No  | The IDs of the security groups for the load balancer\.Type: array of strings | 
|  [`State`](#asff-resourcedetails-awselbv2loadbalancer-state)  |  No  | The state of the load balancer\.Type: object | 
|  `Type`  |  No  | The type of load balancer\.Type: string | 
|  `VpcId`  |  No  | The ID of the VPC for the load balancer\.Type: string | 

##### AvailabilityZones<a name="asff-resourcedetails-awselbv2loadbalancer-availabilityzones"></a>

Specifies the availability zones for the load balancer\.

Each availability zone can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `SubnetId`  |  No  | The ID of the subnet\.Type: string | 
|  `ZoneName`  |  No  | The name of the Availability Zone\.Type: string | 

##### State<a name="asff-resourcedetails-awselbv2loadbalancer-state"></a>

Information about the state of the load balancer\.

The `State` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Code`  |  No  | The state code\. The initial state of the load balancer is provisioning\. After the load balancer is fully set up and ready to route traffic, its state is active\. If the load balancer could not be set up, its state is failed\.Type: string | 
|  `Reason`  |  No  | A description of the state\.Type: string | 

#### AwsIamAccessKey<a name="asff-resourcedetails-awsiamaccesskey"></a>

IAM access key details that are related to a finding\.

Type: object

The `AwsIamAccessKey` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CreatedAt`  |  No  | The creation date and time of the IAM access key that is related to a finding\.Type: timestamp | 
|  `PrincipalId`  |  No  | The ID of the principal associated with an access key\. Type: string | 
|  `PrincipalName`  |  No  | The name of the principal\.Type: string | 
|  `PrincipalType`  |  No  | The type of principal\.Type: string | 
|  `Status`  |  No  | The status of the IAM access key that is related to a finding\. Valid values are `ACTIVE` and `INACTIVE`\.Type: enum | 

#### AwsIamRole<a name="asff-resourcedetails-awsiamrole"></a>

Contains information about an IAM role, including all of the role's policies\.

Type: object

The `AwsIamRole` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AssumeRolePolicyDocument`  |  No  | The trust policy that grants permission to assume the role\.Type: string | 
|  `CreateDate`  |  No  | The date and time, in ISO 8601 date\-time format, when the role was created\.Type: string | 
|  `RoleId`  |  No  | The stable and unique string identifying the role\.Type: string | 
|  `RoleName`  |  No  | The friendly name that identifies the role\.Type: string | 
|  `MaxSessionDuration`  |  No  | The maximum session duration \(in seconds\) that you want to set for the specified role\.Type: integer | 
|  `Path`  |  No  | The path to the role\.Type: string | 

#### AwsKmsKey<a name="asff-resourcedetails-awskmskey"></a>

Details about a AWS KMS customer master key \(CMK\)\.

Type: object

The `AwsKmsKey` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `AWSAccountId`  |  No  |  The AWS account identifier of the account that owns the CMK\. Type: string  | 
|  `CreationDate`  |  No  |  The date and time when the CMK was created\. Type: timestamp  | 
|  `KeyId`  |  Yes  |  The globally unique identifier for the CMK\. Type: String The minimum length is 1\. The maximum length is 2048\.  | 
|  `KeyManager`  |  No  |  The manager of the CMK\. CMKs in an AWS account are either customer managed or AWS managed\. Type: string Valid values: `AWS` \| `CUSTOMER`\.  | 
|  `KeyState`  |  No  |  The state of the CMK\. Type: string Valid values: `Enabled` \| `Disabled` \| `PendingDeletion` \| `PendingImport` \| `Unavailable`  | 
|  `Origin`  |  No  |  The source of the CMK's key material\. When this value is `AWS_KMS`, AWS KMS created the key material\. When this value is `EXTERNAL`, either the key material was imported from your existing key management infrastructure, or the CMK lacks key material\. When this value is `AWS_CLOUDHSM`, the key material was created in the AWS CloudHSM cluster associated with a custom key store\. Type: String Valid values: `AWS_KMS` \| `EXTERNAL` \| `AWS_CLOUDHSM`  | 

#### AwsLambdaFunction<a name="asff-resourcedetails-awslambdafunction"></a>

The `AwsLambdaFunction` object provides details about a Lambda function's configuration\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`Code`](#asff-resourcedetails-awslambdafunction-code)  |  No  | An `AwsLambdaFunctionCode` object\.Type: object | 
|  `CodeSha256`  |  No  | The SHA256 hash of the function's deployment package\.Type: string | 
|  [`DeadLetterConfig`](#asff-resourcedetails-awslambdafunction-deadletterconfig)  |  No  | The function's dead letter queue\.Type: object | 
|  [`Environment`](#asff-resourcedetails-awslambdafunction-environment)  |  No  | A function's environment variable settings\.Type: object | 
|  `FunctionName`  |  No  | The name of the function\.Type: string | 
|  `Handler`  |  No  | The function that Lambda calls to begin executing your function\.Type: string | 
|  `KmsKeyArn`  |  No  | The AWS KMS key that's used to encrypt the function's environment variables\. This key is only returned if you've configured a customer managed CMK\.Type: string | 
|  `LastModified`  |  No  | The date and time that the function was last updated, in ISO\-8601 format \(YYYY\-MM\-DDThh:mm:ss\.sTZD\)\.Type: string | 
|  [`Layers`](#asff-resourcedetails-awslambdafunction-layers)  |  No  | The function's layers\.Type: object | 
|  `MasterArn`  |  No  | For Lambda@Edge functions, the ARN of the master function\.Type: string | 
|  `MemorySize`  |  No  | The memory that's allocated to the function\.Type: integer | 
|  `RevisionId`  |  No  | The latest updated revision of the function or alias\.Type: string | 
|  `Role`  |  No  | The function's execution role\.Type: string | 
|  `Runtime`  |  No  | The runtime environment for the Lambda function\.Type: string | 
|  `Timeout`  |  No  | The amount of time that Lambda allows a function to run before stopping it\.Type: integer | 
|  [`TracingConfig`](#asff-resourcedetails-awslambdafunction-tracingconfig)  |  No  | The function's AWS X\-Ray tracing configuration\.Type: object | 
|  `Version`  |  No  | The version of the Lambda function\.Type: string | 
|  [`VpcConfig`](#asff-resourcedetails-awslambdafunction-vpcconfig)  |  No  | The function's networking configuration\.Type: object | 

##### Code<a name="asff-resourcedetails-awslambdafunction-code"></a>

An `AwsLambdaFunctionCode` object\.

The `Code` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `S3Bucket`  |  No  | An S3 bucket in the same AWS Region as your function\. The bucket can be in a different AWS account\.Type: string | 
|  `S3Key`  |  No  | The Amazon S3 key of the deployment package\.Type: string | 
|  `S3ObjectVersion`  |  No  | For versioned objects, the version of the deployment package object to use\.Type: string | 
|  `ZipFile`  |  No  | The base64\-encoded contents of the deployment package\. AWS SDK and AWS CLI clients handle the encoding for you\.Type: string | 

##### DeadLetterConfig<a name="asff-resourcedetails-awslambdafunction-deadletterconfig"></a>

Contains information about the Lambda function's dead letter queue\.

The `DeadLetterConfig` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `TargetArn`  |  No  | The Amazon Resource Name \(ARN\) of the Amazon SQS queue or Amazon SNS topic containing the dead letter queue\.Type: string | 

##### Environment<a name="asff-resourcedetails-awslambdafunction-environment"></a>

Contains the Lambda function's environment variable settings\.

The `Environment` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Variables`  |  No  | Environment variable key\-value pairs\.Type: string to string map | 
|  `Error`  |  No  | Error messages for environment variables that couldn't be applied\.Type: object | 

The `Error` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `ErrorCode`  |  No  |  The error code\. Type: string  | 
|  `Message`  |  No  |  The error message\. Type: string  | 

##### Layers<a name="asff-resourcedetails-awslambdafunction-layers"></a>

The Lambda function's layers\.

Each layer object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Arn`  |  No  | The Amazon Resource Name \(ARN\) of the function layer\.Type: string | 
|  `CodeSize`  |  No  | The size of the layer archive in bytes\.Type: integer | 

##### TracingConfig<a name="asff-resourcedetails-awslambdafunction-tracingconfig"></a>

Contains the function's AWS X\-Ray tracing configuration\.

The `TracingConfig` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Mode`  |  No  | The tracing mode\.Type: string | 

##### VpcConfig<a name="asff-resourcedetails-awslambdafunction-vpcconfig"></a>

Contains the Lambda function's networking configuration\.

The `VpcConfig` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `SecurityGroupIds`  |  No  |  A list of VPC security groups IDs\. Type: array of strings  | 
|  `SubnetIds`  |  No  |  A list of VPC subnet IDs\. Type: array of strings  | 

#### AwsLambdaLayerVersion<a name="asff-resourcedetails-awslambdalayerversion"></a>

The `AwsLambdaLayerVersion` object provides details about a Lambda layer version\.

Example:

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
|  `CompatibleRuntimes`  |  No  |  The layer's compatible runtimes\. Type: array of strings Maximum number of items: 5 Valid values: `nodejs10.x` \| `nodejs12.x` \| `java8` \| `java11` \| `python2.7` \| `python3.6` \| `python3.7` \| `python3.8` \| `dotnetcore1.0` \| `dotnetcore2.1` \| `go1.x` \| `ruby2.5` \| `provided`  | 
|  `CreatedDate`  |  No  |  The date that the version was created, in ISO 8601 format\. For example, 2018\-11\-27T15:10:45\.123\+0000\. Type: string  | 
|  `Version`  |  No  |  The version number\. Type: long  | 

#### AwsRdsDbInstance<a name="asff-resourcedetails-awsrdsdbinstance"></a>

The `AwsRdsDbInstance` object provides details about an Amazon RDS DB instance\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  [`AssociatedRoles`](#asff-resourcedetails-awsrdsdbinstance-associatedroles)  |  No  |  The IAM roles associated with the DB instance\. Type: array of role objects  | 
|  `CACertificateIdentifier`  |  No  |  The identifier of the CA certificate for this DB instance\. Type: string  | 
|  `DBClusterIdentifier`  |  No  |  If the DB instance is a member of a DB cluster, contains the name of the DB cluster that the DB instance is a member of\. Type: string  | 
|  `DBInstanceClass`  |  No  |  Contains the name of the compute and memory capacity class of the DB instance\. Type: string  | 
|  `DBInstanceIdentifier`  |  No  |  Contains a user\-supplied database identifier\. This identifier is the unique key that identifies a DB instance\. Type: string  | 
|  `DbInstancePort`  |  No  |  Specifies the port that the DB instance listens on\. If the DB instance is part of a DB cluster, this can be a different port than the DB cluster port\. Type: integer  | 
|  `DbiResourceId`  |  No  |  The AWS Region\-unique, immutable identifier for the DB instance\. This identifier is found in CloudTrail log entries whenever the AWS KMS key for the DB instance is accessed\. Type: string  | 
|  `DBName`  |  No  |  The meaning of this parameter differs according to the database engine you use\. **MySQL, MariaDB, SQL Server, PostgreSQL** Contains the name of the initial database of this instance that was provided at create time, if one was specified when the DB instance was created\. This same name is returned for the life of the DB instance\. Type: string **Oracle** Contains the Oracle System ID \(SID\) of the created DB instance\. Not shown when the returned parameters do not apply to an Oracle DB instance\. Type: string  | 
|  `DeletionProtection`  |  No  |  Indicates whether the DB instance has deletion protection enabled\. The database can't be deleted when deletion protection is enabled\. Type: Boolean  | 
|  [`Endpoint`](#asff-resourcedetails-awsrdsdbinstance-endpoint)  |  No  |  Specifies the connection endpoint\. Type: object  | 
|  `Engine`  |  No  |  Provides the name of the database engine to be used for this DB instance\. Type: string  | 
|  `EngineVersion`  |  No  |  Indicates the database engine version\. Type: string  | 
|  `IAMDatabaseAuthenticationEnabled`  |  No  |  True if mapping of IAM accounts to database accounts is enabled, and otherwise false\. IAM database authentication can be enabled for the following database engines\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Type: Boolean  | 
|  `InstanceCreateTime`  |  No  |  Provides the date and time the DB instance was created\. Type: timestamp  | 
|  `KmsKeyId`  |  No  |  If `StorageEncrypted` is true, the AWS KMS key identifier for the encrypted DB instance\. Type: string  | 
|  `PubliclyAccessible`  |  No  |  Specifies the accessibility options for the DB instance\. A value of true specifies an Internet\-facing instance with a publicly resolvable DNS name, which resolves to a public IP address  A value of false specifies an internal instance with a DNS name that resolves to a private IP address\. Type: Boolean  | 
|  `StorageEncrypted`  |  No  |  Specifies whether the DB instance is encrypted\. Type: Boolean  | 
|  `TdeCredentialArn`  |  No  |  The ARN from the key store with which the instance is associated for TDE encryption\. Type: string  | 
|  [`VpcSecurityGroups`](#asff-resourcedetails-awsrdsdbinstance-vpcsecuritygroups)  |  No  |  List of VPC security groups that the DB instance belongs to\. Type: array of objects  | 

##### AssociatedRoles<a name="asff-resourcedetails-awsrdsdbinstance-associatedroles"></a>

The `AssociatedRoles` array lists the IAM roles associated with the DB instance\.

Each role object in the `AssociatedRoles` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `FeatureName`  |  No  |  The name of the feature associated with the IAM role\. Type: string  | 
|  `RoleArn`  |  No  |  The ARN of the IAM role that is associated with the DB instance\. Type: string  | 
|  `Status`  |  No  |  Describes the state of association between the IAM role and the DB instance\. Type: string Valid values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 

##### Endpoint<a name="asff-resourcedetails-awsrdsdbinstance-endpoint"></a>

The `Endpoint` object provides details about the connection endpoint for the DB instance\.

It can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Address`  |  No  |  Specifies the DNS address of the DB instance\. Type: string  | 
|  `HostedZoneId`  |  No  |  Specifies the ID that Amazon Route 53 assigns when you create a hosted zone\. Type: string  | 
|  `Port`  |  No  |  Specifies the port that the database engine is listening on\. Type: integer  | 

##### VpcSecurityGroups<a name="asff-resourcedetails-awsrdsdbinstance-vpcsecuritygroups"></a>

The `VpcSecurityGroups` array provides the list of VPC security groups that the DB instance belongs to\.

Each object in the `VpcSecurityGroups` array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `VpcSecurityGroupId`  |  No  |  The name of the VPC security group\. Type: string  | 
|  `Status`  |  No  |  The status of the VPC security group\. Type: string  | 

#### AwsS3Bucket<a name="asff-resourcedetails-awss3bucket"></a>

The details of an Amazon S3 bucket\.

Type: object

The `AwsS3Bucket` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `CreatedAt`  |  No  |  The date and time when the S3 bucket was created\. Type: string \(Uses the RFC 3339 format\)  | 
|  `OwnerId`  |  No  |  The canonical user ID of the owner of the Amazon S3 bucket\. Type: string \(64 char max\)  | 
|  `OwnerName`  |  No  | The display name of the owner of the Amazon S3 bucket\.Type: string \(128 char max\) | 
|  `ServerSideEncryptionConfiguration`  |  No  |  The encryption rules that are applied to the S3 bucket\. Type: object Consists of a `Rules` object, which contains the [`ApplyServerSideEncryptionByDefault`](#asff-resourcedetails-awss3bucket-applyserversideencryptionbydefault) object\.  Example: <pre>"ServerSideEncryptionConfiguration": {<br />  "Rules": [<br />    {<br />      "ApplyServerSideEncryptionByDefault": {<br />        "KMSMasterKeyID": "12345678-abcd-abcd-abcd-123456789012",<br />        "SSEAlgorithm": "aws.kms"<br />      }<br />    }<br />  ]<br />}</pre>  | 

##### ApplyServerSideEncryptionByDefault<a name="asff-resourcedetails-awss3bucket-applyserversideencryptionbydefault"></a>

Specifies the default server\-side encryption to apply to new objects in the bucket\.

`ApplyServerSideEncryptionByDefault` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `KMSMasterKeyID`  |  No  |  AWS KMS customer master key \(CMK\) ID to use for the default encryption\. Can be either the key ID or the CMK ARN\. Type: string  | 
|  `SSEAAlgorithm`  |  Yes  |  Server\-side encryption algorithm to use for the default encryption\. Type: string Valid values: `AES256` \| `aws:kms`  | 

#### AwsS3Object<a name="asff-resourcedetails-awss3object"></a>

Details about an AWS S3 object\.

Example:

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
|  `ContentType`  |  No  |  A standard MIME type describing the format of the object data\. Type: string  | 
|  `ETag`  |  No  |  The opaque identifier assigned by a web server to a specific version of a resource found at a URL\. Type: string  | 
|  `LastModified`  |  No  |  The date and time when the object was last modified\. Type: datetime  | 
|  `ServerSideEncryption`  |  No  |  If the object is stored using server\-side encryption, the value of the server\-side encryption algorithm used when storing this object in Amazon S3\. Type: string  | 
|  `SSEKMSKeyId`  |  No  |  The identifier of the AWS Key Management Service\) symmetric customer managed customer master key \(CMK\) that was used for the object\. Type: string  | 
|  `VersionId`  |  No  |  The version of the object\. Type: string  | 

#### AwsSnsTopic<a name="asff-resourcedetails-awssnstopic"></a>

A wrapper type for the topic's Amazon Resource Name \(ARN\)\.

Type: object

The `AwsSnsTopic` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `KmsMasterKeyId`  |  No  | The ID of an AWS\-managed customer master key \(CMK\) for Amazon SNS or a custom CMK\.Type: string | 
|  `Subscription`  |  No  | Subscription is an embedded property that describes the subscription endpoints of an Amazon SNS topic\.Type: array of objects | 
|  `TopicName`  |  No  | The name of the topic\.Type: string | 
|  `Owner`  |  No  | The subscription's owner\.Type: string | 

##### Subscription<a name="asff-resourcedetails-awssnstopic-subscription"></a>

The `Subscription` object in an `AwsSnsTopic` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Endpoint`  |  No  |  The subscription's endpoint \(format depends on the protocol\)\. Type: string  | 
|  `Protocol`  |  No  |  The subscription's protocol\. Type: string  | 

#### AwsSqsQueue<a name="asff-resourcedetails-awssqsqueue"></a>

Data about an Amazon SQS queue\.

Type: object

The `AwsSqsQueue` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `KmsDataKeyReusePeriodSeconds`  |  No  | The length of time, in seconds, for which Amazon SQS can reuse a data key to encrypt or decrypt messages before calling AWS KMS again\.Type: integer | 
|  `KmsMasterKeyId`  |  No  | The ID of an AWS\-managed customer master key \(CMK\) for Amazon SQS or a custom CMK\.Type: string | 
|  `QueueName`  |  No  | The name of the new queue\.Type: string | 
|  `DeadLetterTargetArn`  |  No  | The Amazon Resource Name \(ARN\) of the dead\-letter queue to which Amazon SQS moves messages after the value of `maxReceiveCount` is exceeded\.Type: string | 

#### AwsWafWebAcl<a name="asff-resourcedetails-awswafwebacl"></a>

The `AwsWafWebAcl` object provides details about an AWS WAF WebACL\.

Example:

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
|  `Name`  |  No  |  A friendly name or description of the WebACL\. You can't change the name of a WebACL after you create it\. Type: string Length constraints: Minimum length of 1\. Maximum length of 128\.  | 
|  [`Rules`](#asff-resourcedetails-awswafwebacl-rule)  |  Yes  |  A list of rules for the WebACL\. Type: array of objects  | 
|  `WebAclId`  |  Yes  |  A unique identifier for a WebACL\. Type: string Length constraints: Minimum length of 1\. Maximum length of 128\.  | 

##### Rule object<a name="asff-resourcedetails-awswafwebacl-rule"></a>

The `Rules` array provides the list of rules for the WebACL\.

Each rule object in the array can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Action`  |  No  |  Specifies the action that CloudFront or AWS WAF takes when a web request matches the conditions in the rule\. Type: object  | 
|  `ExcludedRules`  |  No  |  An array of rules to exclude from a rule group\. This is applicable only when the `ActivatedRule` refers to a rule grup\. Type: array of objects  | 
|  `OverrideAction`  |  No  |  Use the `OverrideAction` to test your RuleGroup\. Any rule in a rule group can potentially block a request\. If you set the `OverrideAction` to `None`, the rule group blocks a request if any individual rule in the rule group matches the request and is configured to block that request\. However, if you first want to test the rule group, set the `OverrideAction` to `Count`\. The rule group then overrides any block action specified by individual rules contained within the group\. Instead of blocking matching requests, those requests are counted\. `ActivatedRule\|OverrideAction` applies only when updating or adding a rule group to a WebACL\. In this case you do not use `ActivatedRule\|Action`\. For all other update requests, `ActivatedRule\|Action` is used instead of `ActivatedRule\|OverrideAction`\. Type: object  | 
|  `Priority`  |  Yes  |  Specifies the order in which to evaluate the rules in a WebACL\. Rules with a lower value for Priority are evaluated before rules with a higher value\. The value must be a unique integer\. If you add multiple rules to a WebACL, the values don't need to be consecutive\. Type: integer  | 
|  `RuleId`  |  Yes  |  The identifier for a rule\. Type: String Length constraints: Minimum length of 1\. Maximum length of 128\.  | 
|  `Type`  |  No  |  The rule type, either `REGULAR`,` RATE_BASED`, or `GROUP`\. The default is `REGULAR`\. Type: string Valid values: `REGULAR` \| `RATE_BASED` \| `GROUP`  | 

Each action can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Type`  |  No  |  Specifies how you want AWS WAF to respond to requests that match the settings in a rule\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) Type: string Valid values: `BLOCK` \| `ALLOW` \| `COUNT`  | 

Each excluded rule can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `RuleId`  |  Yes  |  The unique identifier for the rule to exclude from the rule group\. Type: string Length constraints: Minimum length of 1\. Maximum length of 128\.  | 

Each override action for a rule can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Type`  |  Yes  |  `COUNT` overrides the action specified by the individual rule within a rule group\. If set to `NONE`, the rule's action takes place\. Type: string Valid values: `NONE` \| `COUNT`  | 

#### Container<a name="asff-resourcedetails-container"></a>

Container details that are related to a finding\. 

Type: object

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
|  `ImageId`  |  No  | The identifier of the image that is related to a finding\.Type: string \(128 characters max\) | 
|  `ImageName`  |  No  | The name of the image that is related to a finding\.Type: string \(128 characters max\) | 
|  `LaunchedAt`  |  No  | The date and time that the container was started\.Type: timestamp | 
|  `Name`  |  No  | The name of the container that is related to a finding\.Type: string \(128 characters max\) | 

#### Other<a name="asff-resourcedetails-other"></a>

The `Other` subfield allows you to provide custom fields and values\. You use the `Other` subfield in the following cases\.
+ The resource type does not have a corresponding subfield\. To provide details for the resource, you use the `Other` subfield\.
+ The subfield for the resource type does not include all of the fields you want to populate\. In this case, use the subfield for the resource type to populate the available fields\. Use the `Other` subfield to populate the fields that are not in the type\-specific subfield\.
+ The resource type is not one of the provided types\. In this case, you set `Resource.Type` to `Other`, and use the `Other` subfield to populate the details\.

Type: map of up to 50 key\-value pairs

Each key\-value pair must meet the following requirements\.
+ The key must contain fewer than 128 characters\.
+ The value must contain fewer than 1,024 characters\.

### Severity<a name="asff-severity"></a>

Details about the severity of the finding\.

The finding provider can the initial severity, but cannot update it after that\. The severity can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. It can only be updated by a master account\. It cannot be updated by a member account\.

The finding severity does not consider the criticality of the involved assets or the underlying resource\. Criticality is defined as the level of importance of the resources associated with the finding\. For example, a resource associated with a mission critical application versus one associated with non\-production testing\. To capture information about resource criticality, use the `Criticality` field\.

The finding must have either `Label` or `Normalized` populated\. If neither attribute is populated, then the finding is invalid\. `Label` is the preferred attribute\.

The `Severity` object can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Label`  |  No  |  The severity value for the finding\. Type: enum Available values: `INFORMATIONAL` \| `LOW` \| `MEDIUM` \| `HIGH` \|`CRITICAL` At a high level, the `Label` values can be interpreted as follows\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 
|  `Normalized` \(To be deprecated\)  |  No  |  The normalized severity of a finding\. We plan to deprecate this attribute\. Instead of `Normalized`, provide `Label`\. Type: integer The value of `Normalized` must be an integer between 0 and 100\. Zero means that no severity applies, and 100 means that the finding has the maximum possible severity\. For guidance on setting the value of `Normalized`, see [Guidance for Assigning the Normalized Severity \(AWS Services and Partners\)](#asff-severity-normalized-guidance)\.  | 
|  `Product`  |  No  |  The native severity as defined by the finding product that generated the finding\. Type: number \(single\-precision 32\-bit IEEE 754 floating point number, restricted to finite values\)  | 

#### How Security Hub maps `Label` and `Normalized` values<a name="asff-severity-map-normalized-label"></a>

If you only provide `Label` or only provide `Normalized`, then Security Hub automatically populates the value of the other field\.

If you provide `Normalized` and do not provide `Label`, `Label` is set automatically as follows\.


|  Normalized  |  Label  | 
| --- | --- | 
|  0  |  `INFORMATIONAL`  | 
|  1–39  |  `LOW`  | 
|  40–69  |  `MEDIUM`  | 
|  70–89  |  `HIGH`  | 
|  90–100  |  `CRITICAL`  | 

If you only provide `Label` and do not provide `Normalized`, `Normalized` is set automatically as follows\.


|  Label  |  Normalized  | 
| --- | --- | 
|  `INFORMATIONAL`  |  0  | 
|  `LOW`  |  1  | 
|  `MEDIUM`  |  40  | 
|  `HIGH`  |  70  | 
|  `CRITICAL`  |  90  | 

#### Guidance for Assigning the Normalized Severity \(AWS Services and Partners\)<a name="asff-severity-normalized-guidance"></a>

For findings generated by AWS services and third\-party partner products, the severity is based on the following\.
+ Most severe – Findings that are associated with actual data loss or denial of service
+ Second\-most severe – Findings that are associated with an active compromise but that do not indicate that data loss or other negative effects have occurred
+ Third\-most severe – Findings associated with issues that indicate potential for a future compromise

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

Type: array of up to five threat intelligence indicator objects

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
|  `Category`  |  No  | The category of a threat intel indicator\.Type: enum Valid values: `BACKDOOR` \| `CARD_STEALER` \| `COMMAND_AND_CONTROL` \| `DROP_SITE` \| `EXPLOIT_SITE` \| `KEYLOGGER` | 
|  `LastObservedAt`  |  No  | The date and time of the last observation of a threat intelligence indicator\.Type: timestamp | 
|  `Source`  |  No  | The source of the threat intelligence\.Type: string \(64 characters max\) | 
|  `SourceUrl`  |  No  | The URL for more details from the source of the threat intelligence\.Type: URL | 
|  `Type`  |  No  | The type of a threat intelligence indicator\.Type: enum Valid values: `DOMAIN` \| `EMAIL_ADDRESS` \| `HASH_MD5` \| `HASH_SHA1` \| `HASH_SHA256` \|` HASH_SHA512` \| `IPV4_ADDRESS` \| `IPV6_ADDRESS` \| `MUTEX` \| `PROCESS` \| `URL` | 
|  `Value`  |  No  | The value of a threat intelligence indicator\.Type: string \(512 characters max\) | 

### Workflow<a name="asff-workflow"></a>

The `Workflow` object provides information about the status of the investigation into a finding\.

It is not intended for finding providers\. It is only to be used by customers and by remediation, orchestration, and ticketing tools used by customers\.

The workflow status can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\. Customers can also update it from the console\. See [Setting the workflow status for a finding](finding-workflow-status.md)\. The workflow status can only be updated by a master account\. It cannot be updated by a member account\.

`Workflow` can have the following attributes\.


|  Attribute  |  Required  |  Description  | 
| --- | --- | --- | 
|  `Status`  |  No  |  The status of the investigation into the finding\. Type: enum Valid values: `NEW` \| `NOTIFIED` \| `RESOLVED` \| `SUPPRESSED` [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)  | 

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

TTPs stands for Tactics, Techniques, and Procedures\. The TTP categories in the following list align to the [MITRE ATT&CK MatrixTM](https://attack.mitre.org/matrices/enterprise/)\. Unusual Behaviors reflect general unusual behavior, such as general statistical anomalies, and are not aligned with a specific TTP\. However, you could classify a finding with both Unusual Behaviors and TTPs finding types\.
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