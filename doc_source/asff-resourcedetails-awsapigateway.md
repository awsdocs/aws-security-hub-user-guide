# AwsApiGateway<a name="asff-resourcedetails-awsapigateway"></a>

The following are examples of the AWS Security Finding Format for `AwsApiGateway` resources\.

## AwsApiGatewayRestApi<a name="asff-resourcedetails-awsapigatewayrestapi"></a>

The `AwsApiGatewayRestApi` object contains information about a REST API in version 1 of Amazon API Gateway\.

The following is an example `AwsApiGatewayRestApi` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsApiGatewayRestApi` attributes, see [AwsApiGatewayRestApiDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsApiGatewayRestApiDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
AwsApiGatewayRestApi: {
    "Id": "exampleapi",
    "Name": "Security Hub",
    "Description": "AWS Security Hub",
    "CreatedDate": "2018-11-18T10:20:05-08:00",
    "Version": "2018-10-26",
    "BinaryMediaTypes" : ["-'*~1*'"],
    "MinimumCompressionSize": 1024,
    "ApiKeySource": "AWS_ACCOUNT_ID",
    "EndpointConfiguration": {
        "Types": [
            "REGIONAL"
        ]
    }
}
```

## AwsApiGatewayStage<a name="asff-resourcedetails-awsapigatewaystage"></a>

The `AwsApiGatewayStage` object provides information about a version 1 Amazon API Gateway stage\.

The following is an example `AwsApiGatewayStage` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsApiGatewayStage` attributes, see [AwsApiGatewayStageDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsApiGatewayStageDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsApiGatewayStage": {
    "DeploymentId": "n7hlmf",
    "ClientCertificateId": "a1b2c3", 
    "StageName": "Prod",
    "Description" : "Stage Description",
    "CacheClusterEnabled": false,
    "CacheClusterSize" : "1.6",
    "CacheClusterStatus": "NOT_AVAILABLE",
    "MethodSettings": [
        {
            "MetricsEnabled": true,
            "LoggingLevel": "INFO",
            "DataTraceEnabled": false,
            "ThrottlingBurstLimit": 100,
            "ThrottlingRateLimit": 5.0,
            "CachingEnabled": false,
            "CacheTtlInSeconds": 300,
            "CacheDataEncrypted": false,
            "RequireAuthorizationForCacheControl": true,
            "UnauthorizedCacheControlHeaderStrategy": "SUCCEED_WITH_RESPONSE_HEADER",
            "HttpMethod": "POST",
            "ResourcePath": "/echo"
        }
    ],
    "Variables": {"test": "value"},
    "DocumentationVersion": "2.0",
    "AccessLogSettings": {
        "Format": "{\"requestId\": \"$context.requestId\", \"extendedRequestId\": \"$context.extendedRequestId\", \"ownerAccountId\": \"$context.accountId\", \"requestAccountId\": \"$context.identity.accountId\", \"callerPrincipal\": \"$context.identity.caller\", \"httpMethod\": \"$context.httpMethod\", \"resourcePath\": \"$context.resourcePath\", \"status\": \"$context.status\", \"requestTime\": \"$context.requestTime\", \"responseLatencyMs\": \"$context.responseLatency\", \"errorMessage\": \"$context.error.message\", \"errorResponseType\": \"$context.error.responseType\", \"apiId\": \"$context.apiId\", \"awsEndpointRequestId\": \"$context.awsEndpointRequestId\", \"domainName\": \"$context.domainName\", \"stage\": \"$context.stage\", \"xrayTraceId\": \"$context.xrayTraceId\", \"sourceIp\": \"$context.identity.sourceIp\", \"user\": \"$context.identity.user\", \"userAgent\": \"$context.identity.userAgent\", \"userArn\": \"$context.identity.userArn\", \"integrationLatency\": \"$context.integrationLatency\", \"integrationStatus\": \"$context.integrationStatus\", \"authorizerIntegrationLatency\": \"$context.authorizer.integrationLatency\" }",
        "DestinationArn": "arn:aws:logs:us-west-2:111122223333:log-group:SecurityHubAPIAccessLog/Prod"
    },
    "CanarySettings": {
        "PercentTraffic": 0.0,
        "DeploymentId": "ul73s8",
        "StageVariableOverrides" : [
            "String" : "String"
        ],
        "UseStageCache": false
    },
    "TracingEnabled": false,
    "CreatedDate": "2018-07-11T10:55:18-07:00",
    "LastUpdatedDate": "2020-08-26T11:51:04-07:00",
    "WebAclArn" : "arn:aws:waf-regional:us-west-2:111122223333:webacl/cb606bd8-5b0b-4f0b-830a-dd304e48a822"
}
```

## AwsApiGatewayV2Api<a name="asff-resourcedetails-awsapigatewayv2api"></a>

The `AwsApiGatewayV2Api` object contains information about a version 2 API in Amazon API Gateway\.

The following is an example `AwsApiGatewayV2Api` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsApiGatewayV2Api` attributes, see [AwsApiGatewayV2ApiDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsApiGatewayV2ApiDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsApiGatewayV2Api": {
    "ApiEndpoint": "https://example.us-west-2.amazonaws.com",
    "ApiId": "a1b2c3d4",
    "ApiKeySelectionExpression": "$request.header.x-api-key",
    "CreatedDate": "2020-03-28T00:32:37Z",
   "Description": "ApiGatewayV2 Api",
   "Version": "string",
    "Name": "my-api",
    "ProtocolType": "HTTP",
    "RouteSelectionExpression": "$request.method $request.path",
   "CorsConfiguration": {
        "AllowOrigins": [ "*" ],
        "AllowCredentials": true,
        "ExposeHeaders": [ "string" ],
        "MaxAge": 3000,
        "AllowMethods": [
          "GET",
          "PUT",
          "POST",
          "DELETE",
          "HEAD"
        ],
        "AllowHeaders": [ "*" ]
    }
}
```

## AwsApiGatewayV2Stage<a name="asff-resourcedetails-awsapigatewayv2stage"></a>

`AwsApiGatewayV2Stage` contains information about a version 2 stage for Amazon API Gateway\.

The following is an example `AwsApiGatewayV2Stage` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsApiGatewayV2Stage` attributes, see [AwsApiGatewayV2StageDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsApiGatewayV2StageDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsApiGatewayV2Stage": {
    "CreatedDate": "2020-04-08T00:36:05Z",
    "Description" : "ApiGatewayV2",
    "DefaultRouteSettings": {
        "DetailedMetricsEnabled": false,
        "LoggingLevel": "INFO",
        "DataTraceEnabled": true,
        "ThrottlingBurstLimit": 100,
        "ThrottlingRateLimit": 50
    },
    "DeploymentId": "x1zwyv",
    "LastUpdatedDate": "2020-04-08T00:36:13Z",
    "RouteSettings": {
        "DetailedMetricsEnabled": false,
        "LoggingLevel": "INFO",
        "DataTraceEnabled": true,
        "ThrottlingBurstLimit": 100,
        "ThrottlingRateLimit": 50
    },
    "StageName": "prod",
    "StageVariables": [
        "function": "my-prod-function"
    ],
    "AccessLogSettings": {
        "Format": "{\"requestId\": \"$context.requestId\", \"extendedRequestId\": \"$context.extendedRequestId\", \"ownerAccountId\": \"$context.accountId\", \"requestAccountId\": \"$context.identity.accountId\", \"callerPrincipal\": \"$context.identity.caller\", \"httpMethod\": \"$context.httpMethod\", \"resourcePath\": \"$context.resourcePath\", \"status\": \"$context.status\", \"requestTime\": \"$context.requestTime\", \"responseLatencyMs\": \"$context.responseLatency\", \"errorMessage\": \"$context.error.message\", \"errorResponseType\": \"$context.error.responseType\", \"apiId\": \"$context.apiId\", \"awsEndpointRequestId\": \"$context.awsEndpointRequestId\", \"domainName\": \"$context.domainName\", \"stage\": \"$context.stage\", \"xrayTraceId\": \"$context.xrayTraceId\", \"sourceIp\": \"$context.identity.sourceIp\", \"user\": \"$context.identity.user\", \"userAgent\": \"$context.identity.userAgent\", \"userArn\": \"$context.identity.userArn\", \"integrationLatency\": \"$context.integrationLatency\", \"integrationStatus\": \"$context.integrationStatus\", \"authorizerIntegrationLatency\": \"$context.authorizer.integrationLatency\" }",
        "DestinationArn": "arn:aws:logs:us-west-2:111122223333:log-group:SecurityHubAPIAccessLog/Prod"
    },
    "AutoDeploy": false,
    "LastDeploymentStatusMessage": "Message",
    "ApiGatewayManaged": true,
}
```