# AwsApiGatewayV2Stage<a name="asff-resourcedetails-awsapigatewayv2stage"></a>

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