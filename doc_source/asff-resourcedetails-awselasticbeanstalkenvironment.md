# AwsElasticBeanstalkEnvironment<a name="asff-resourcedetails-awselasticbeanstalkenvironment"></a>

The `AwsElasticBeanstalkEnvironment` object contains details about an AWS Elastic Beanstalk environment\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsElasticBeanstalkEnvironment` object\. To view descriptions of `AwsElasticBeanstalkEnvironment` attributes, see [AwsElasticBeanstalkEnvironmentDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsElasticBeanstalkEnvironmentDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsElasticBeanstalkEnvironment": {
    "ApplicationName": "MyApplication",
    "Cname": "myexampleapp-env.devo-2.elasticbeanstalk-internal.com",
    "DateCreated": "2021-04-30T01:38:01.090Z",
    "DateUpdated": "2021-04-30T01:38:01.090Z",
    "Description": "Example description of my awesome application",
    "EndpointUrl": "eb-dv-e-p-AWSEBLoa-abcdef01234567890-021345abcdef6789.us-east-1.elb.amazonaws.com",
    "EnvironmentArn": "arn:aws:elasticbeanstalk:us-east-1:123456789012:environment/MyApplication/myapplication-env",
    "EnvironmentId": "e-abcd1234",
    "EnvironmentLinks": [
        {
            "EnvironmentName": "myexampleapp-env",
            "LinkName": "myapplicationLink"
        }
    ],
    "EnvironmentName": "myapplication-env",
    "OptionSettings": [
        {
            "Namespace": "aws:elasticbeanstalk:command",
            "OptionName": "BatchSize",
            "Value": "100"
        },
        {
            "Namespace": "aws:elasticbeanstalk:command",
            "OptionName": "Timeout",
            "Value": "600"
        },
        {
            "Namespace": "aws:elasticbeanstalk:command",
            "OptionName": "BatchSizeType",
            "Value": "Percentage"
        },
        {
            "Namespace": "aws:elasticbeanstalk:command",
            "OptionName": "IgnoreHealthCheck",
            "Value": "false"
        },
        {
            "Namespace": "aws:elasticbeanstalk:application",
            "OptionName": "Application Healthcheck URL",
            "Value": "TCP:80"
        }
    ],
    "PlatformArn": "arn:aws:elasticbeanstalk:us-east-1::platform/Tomcat 8 with Java 8 running on 64bit Amazon Linux/2.7.7",
    "SolutionStackName": "64bit Amazon Linux 2017.09 v2.7.7 running Tomcat 8 Java 8",
    "Status": "Ready",
    "Tier": {
        "Name": "WebServer"
       "Type": "Standard"
       "Version": "1.0"
    },
    "VersionLabel": "Sample Application"
}
```

The following is a list of valid value examples for `AwsElasticBeanstalkEnvironment` attributes:
+ `Status`

  Valid values: `Aborting` \| `Launching` \| `Updating` \| `LinkingFrom` \| `LinkingTo` \| `Ready` \| `Terminating` \| `Terminated`
+ `Tier Name`

  Valid values: `WebServer` \| `Worker`
+ `Tier Type`

  Valid values: `Standard` \| `SQS/HTTP`