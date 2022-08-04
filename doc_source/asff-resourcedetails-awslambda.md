# AwsLambda<a name="asff-resourcedetails-awslambda"></a>

The following are examples of the AWS Security Finding Format for `AwsLambda` resources\.

## AwsLambdaFunction<a name="asff-resourcedetails-awslambdafunction"></a>

The `AwsLambdaFunction` object provides details about a Lambda function's configuration\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsLambdaFunction` object\. To view descriptions of `AwsLambdaFunction` attributes, see [AwsLambdaFunctionDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsLambdaFunctionDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
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
                            "Mode": "string"
                        },
                        "Version": "string",
                        "VpcConfig": {
                            "SecurityGroupIds": [ "string" ],
                            "SubnetIds": [ "string" ]
                        },
                        "MasterArn": "string",
                        "MemorySize": number
                    }
```

## AwsLambdaLayerVersion<a name="asff-resourcedetails-awslambdalayerversion"></a>

The `AwsLambdaLayerVersion` object provides details about a Lambda layer version\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsLambdaLayerVersion` object\. To view descriptions of `AwsLambdaLayerVersion` attributes, see [AwsLambdaLayerVersionDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsLambdaLayerVersionDetails.html) in the *AWS Security Hub API Reference*\.

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