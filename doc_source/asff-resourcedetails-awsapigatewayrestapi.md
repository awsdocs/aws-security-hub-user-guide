# AwsApiGatewayRestApi<a name="asff-resourcedetails-awsapigatewayrestapi"></a>

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