# AwsCloudFrontDistribution<a name="asff-resourcedetails-awscloudfrontdistribution"></a>

The `AwsCloudFrontDistribution` object provides details about a distribution configuration\.

The following is an example `AwsCloudFrontDistribution` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsCloudFrontDistribution` attributes, see [AwsCloudFrontDistributionDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsCloudFrontDistributionDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
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
     "ViewerCertificate": {
            "AcmCertificateArn": "string",
            "Certificate": "string",
            "CertificateSource": "string",
            "CloudFrontDefaultCertificate": boolean,
            "IamCertificateId": "string",
            "MinimumProtocolVersion": "string",
            "SslSupportMethod": "string"
      },
      "WebAclId": "string"
}
```