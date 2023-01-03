# AwsLambda<a name="asff-resourcedetails-awslambda"></a>

The following are examples of the AWS Security Finding Format for `AwsLambda` resources\.

## AwsLambdaFunction<a name="asff-resourcedetails-awslambdafunction"></a>

The `AwsLambdaFunction` object provides details about a Lambda function's configuration\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsLambdaFunction` object\. To view descriptions of `AwsLambdaFunction` attributes, see [AwsLambdaFunctionDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsLambdaFunctionDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsLambdaFunction": {
    "Architectures": [
        "x86_64"
    ],
    "Code": {
        "S3Bucket": "DOC-EXAMPLE-BUCKET",
        "S3Key": "samplekey",
        "S3ObjectVersion": "2",
        "ZipFile": "myzip.zip"
    },
    "CodeSha256": "1111111111111abcdef",
    "DeadLetterConfig": {
        "TargetArn": "arn:aws:lambda:us-east-2:123456789012:queue:myqueue:2"
    },
    "Environment": {
        "Variables": {
            "Stage": "foobar"
         },
        "Error": {
            "ErrorCode": "Sample-error-code",
            "Message": "Caller principal is a manager."
         }
     },
    "FunctionName": "CheckOut",
    "Handler": "main.py:lambda_handler",
    "KmsKeyArn": "arn:aws:kms:us-west-2:123456789012:key/mykey",
    "LastModified": "2001-09-11T09:00:00Z",
    "Layers": {
        "Arn": "arn:aws:lambda:us-east-2:123456789012:layer:my-layer:3",
        "CodeSize": 169
    },
    "PackageType": "Zip",
    "RevisionId": "23",
    "Role": "arn:aws:iam::123456789012:role/Accounting-Role",
    "Runtime": "go1.7",
    "Timeout": 15,
    "TracingConfig": {
        "Mode": "Active"
    },
    "Version": "$LATEST$",
    "VpcConfig": {
        "SecurityGroupIds": ["sg-085912345678492fb", "sg-08591234567bdgdc"],
         "SubnetIds": ["subnet-071f712345678e7c8", "subnet-07fd123456788a036"]
    },
    "MasterArn": "arn:aws:lambda:us-east-2:123456789012:\$LATEST",
    "MemorySize": 2048
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