# AwsCertificateManagerCertificate<a name="asff-resourcedetails-awscertificatemanagercertificate"></a>

The `AwsCertificateManagerCertificate` object provides details about an AWS Certificate Manager \(ACM\) certificate\.

The following is an example `AwsCertificateManagerCertificate` finding in the AWS Security Finding Format \(ASFF\)\. To view descriptions of `AwsCertificateManagerCertificate` attributes, see [AwsCertificateManagerCertificateDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsCertificateManagerCertificateDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsCertificateManagerCertificate": {
    "CertificateAuthorityArn": "arn:aws:acm:us-west-2:444455556666:certificate-authority/example",
    "CreatedAt": "2019-05-24T18:12:02.000Z",
    "DomainName": "example.amazondomains.com",
    "DomainValidationOptions": [
        {
            "DomainName": "example.amazondomains.com",
            "ResourceRecord": {
                "Name": "_1bacb61828d3a1020c40a560ceed08f7.example.amazondomains.com",
                "Type": "CNAME",
                "Value": "_example.acm-validations.aws."
             },
             "ValidationDomain": "example.amazondomains.com"",
             "ValidationEmails": [],
             "ValidationMethod": "DNS",
             "ValidationStatus": "SUCCESS"
        }
    ],
    "ExtendedKeyUsages": [
        {
            "Name": "TLS_WEB_SERVER_AUTHENTICATION",
            "OId": "1.3.6.1.5.5.7.3.1"
        },
        {
            "Name": "TLS_WEB_CLIENT_AUTHENTICATION",
            "OId": "1.3.6.1.5.5.7.3.2"
        }
    ],
    "FailureReason": "",
    "ImportedAt": "2018-08-17T00:13:00.000Z",
    "InUseBy": ["arn:aws:amazondomains:us-west-2:444455556666:loadbalancer/example"],
    "IssuedAt": "2020-04-26T00:41:17.000Z",
    "Issuer": "Amazon",
    "KeyAlgorithm": "RSA-1024",
    "KeyUsages": [
        {
            "Name": "DIGITAL_SIGNATURE",
        },
        {
            "Name": "KEY_ENCIPHERMENT",
        }
    ],
    "NotAfter": "2021-05-26T12:00:00.000Z",
    "NotBefore": "2020-04-26T00:00:00.000Z",
    "Options": {
        "CertificateTransparencyLoggingPreference": "ENABLED",
    }
    "RenewalEligibility": "ELIGIBLE",
    "RenewalSummary": {
        "DomainValidationOptions": [
            {
                "DomainName": "example.amazondomains.com",
                "ResourceRecord": {
                    "Name": "_1bacb61828d3a1020c40a560ceed08f7.example.amazondomains.com",
                    "Type": "CNAME",
                    "Value": "_example.acm-validations.aws.com",
                },
                "ValidationDomain": "example.amazondomains.com",
                "ValidationEmails": [],
                "ValidationMethod": "DNS",
                "ValidationStatus": "SUCCESS"
            }
        ],
        "RenewalStatus": "SUCCESS",
        "RenewalStatusReason": "",
        "UpdatedAt": "2020-04-26T00:41:35.000Z",
    },
    "Serial": "02:ac:86:b6:07:2f:0a:61:0e:3a:ac:fd:d9:ab:17:1a",
    "SignatureAlgorithm": "SHA256WITHRSA",
    "Status": "ISSUED",
    "Subject": "CN=example.amazondomains.com"",
    "SubjectAlternativeNames": ["example.amazondomains.com"],
    "Type": "AMAZON_ISSUED"
}
```

The following is a list of valid value examples for `AwsCertificateManagerCertificate` attributes:
+ `FailureReason`

  Valid values: `NO_AVAILABLE_CONTACTS` \| `ADDITIONAL_VERIFICATION_REQUIRED` \| `DOMAIN_NOT_ALLOWED` \| `INVALID_PUBLIC_DOMAIN` \| `DOMAIN_VALIDATION_DENIED` \| `CAA_ERROR` \| `PCA_LIMIT_EXCEEDED` \| `PCA_INVALID_ARN` \| `PCA_INVALID_STATE` \| `PCA_REQUEST_FAILED` \| `PCA_NAME_CONSTRAINTS_VALIDATION` \| `PCA_RESOURCE_NOT_FOUND` \| `PCA_INVALID_ARGS` \| `PCA_INVALID_DURATION` \| `PCA_ACCESS_DENIED` \| `SLR_NOT_FOUND` \| `OTHER`
+ `KeyAlgorithm`

  `RSA_2048` \| `RSA_1024` \| `RSA_4096` \| `EC_prime256v1` \| `EC_secp384r1` \| `EC_secp521r1`
+ `Status`

  `PENDING_VALIDATION` \| `ISSUED` \| `INACTIVE` \| `EXPIRED` \| `VALIDATION_TIMED_OUT` \| `REVOKED` \| `FAILED`
+ `Type`

  `IMPORTED` \| `AMAZON_ISSUED` \| `PRIVATE`
+ `RenewalStatus`

  `PENDING_AUTO_RENEWAL` \| `PENDING_VALIDATION` \| `SUCCESS` \| `FAILED`
+ `RenewalStatusReason`

  Valid values: `NO_AVAILABLE_CONTACTS` \| `ADDITIONAL_VERIFICATION_REQUIRED` \| `DOMAIN_NOT_ALLOWED` \| `INVALID_PUBLIC_DOMAIN` \| `DOMAIN_VALIDATION_DENIED` \| `CAA_ERROR` \| `PCA_LIMIT_EXCEEDED` \| `PCA_INVALID_ARN` \| `PCA_INVALID_STATE` \| `PCA_REQUEST_FAILED` \| `PCA_NAME_CONSTRAINTS_VALIDATION` \| `PCA_RESOURCE_NOT_FOUND` \| `PCA_INVALID_ARGS` \| `PCA_INVALID_DURATION` \| `PCA_ACCESS_DENIED` \| `SLR_NOT_FOUND` \| `OTHER`