# AwsElasticSearchDomain<a name="asff-resourcedetails-awselasticsearchdomain"></a>

The `AwsElasticSearchDomain` object provides details about an Amazon OpenSearch Service domain\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsElasticSearchDomain` object\. To view descriptions of `AwsElasticSearchDomain` attributes, see [AwsElasticSearchDomainDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsElasticSearchDomainDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
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
}
```

The following is a list of valid value examples for `AwsElasticSearchDomain` attributes:
+ `ElasticsearchClusterConfig DedicatedMasterType`

  The hardware configuration of the computer that hosts the dedicated master node\. For example, `m3.medium.elasticsearch`\. If this attribute is specified, then `DedicatedMasterEnabled` must be `true`\.

  Valid values: See [Supported instance types](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/supported-instance-types.html) in the *Amazon OpenSearch Service Developer Guide*\.
+ `ElasticsearchClusterConfig InstanceType`

  Valid values: See [Supported instance types](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/supported-instance-types.html) in the *Amazon OpenSearch Service Developer Guide*\.
+ `ServiceSoftwareOptions UpdateStatus`

  Valid values: `ELIGIBLE` \| `PENDING_UPDATE` \| `IN_PROGRESS` \| `COMPLETED` \| `NOT_ELIGIBLE`