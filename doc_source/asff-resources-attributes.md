# Resource attributes<a name="asff-resources-attributes"></a>

Here are descriptions and examples for the `Resources` object in the AWS Security Finding Format \(ASFF\)\. To view attributes for the `Resources` object, see [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Resource.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_Resource.html) in the *AWS Security Hub API Reference*\.

## DataClassification<a name="asff-resources-dataclassification"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DataClassificationDetails.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DataClassificationDetails.html) field provides information about sensitive data that was detected on the resource\.

**Example**

```
"DataClassification": {
    "DetailedResultsLocation": "Path_to_Folder_Or_File",
    "Result": {
        "MimeType": "text/plain",
        "SizeClassified": 2966026,
        "AdditionalOccurrences": false,
        "Status": {
            "Code": "COMPLETE",
            "Reason": "Unsupportedfield"
        },
       "SensitiveData": [
            {
                "Category": "PERSONAL_INFORMATION",
                "Detections": [
                    {
                        "Count": 34,
                        "Type": "GE_PERSONAL_ID",
                        "Occurrences": {
                            "LineRanges": [
                                {
                                    "Start": 1,
                                    "End": 10,
                                    "StartColumn": 20
                                }
                            ],
                            "Pages": [],
                            "Records": [],
                            "Cells": []
                        }
                    },
                    {
                        "Count": 59,
                        "Type": "EMAIL_ADDRESS",
                        "Occurrences": {
                            "Pages": [
                                {
                                    "PageNumber": 1,
                                    "OffsetRange": {
                                        "Start": 1,
                                        "End": 100,
                                        "StartColumn": 10
                                     },
                                    "LineRange": {
                                        "Start": 1,
                                        "End": 100,
                                        "StartColumn": 10
                                    }
                                }
                            ]
                        }
                    },
                    {
                        "Count": 2229,
                        "Type": "URL",
                        "Occurrences": {
                           "LineRanges": [
                               {
                                   "Start": 1,
                                   "End": 13
                               }
                           ]
                       }
                   },
                   {
                       "Count": 13826,
                       "Type": "NameDetection",
                       "Occurrences": {
                            "Records": [
                                {
                                    "RecordIndex": 1,
                                    "JsonPath": "$.ssn.value"
                                }
                            ]
                        }
                   },
                   {
                       "Count": 32,
                       "Type": "AddressDetection"
                   }
               ],
               "TotalCount": 32
           }
        ],
        "CustomDataIdentifiers": {
            "Detections": [
                 {
                     "Arn": "1712be25e7c7f53c731fe464f1c869b8", 
                     "Name": "1712be25e7c7f53c731fe464f1c869b8", 
                     "Count": 2,
                 }
            ],
            "TotalCount": 2
        }
    }
}
```

## Details<a name="asff-resources-details"></a>

The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ResourceDetails.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ResourceDetails.html) field provides additional information about a single resource using the appropriate objects\. Each resource must be provided in a separate resource object in the `Resources` object\.

Note that if the finding size exceeds the maximum of 240 KB, then the `Details` object is removed from the finding\. For control findings that use AWS Config rules, you can view the resource details on the AWS Config console\.

Security Hub provides a set of available resource details for its supported resource types\. These details correspond to values of the `Type` object\. Use the provided types whenever possible\.

For example, if the resource is an S3 bucket, then set the resource `Type` to `AwsS3Bucket` and provide the resource details in the [`AwsS3Bucket`](asff-resourcedetails-awss3.md#asff-resourcedetails-awss3bucket) object\.

The [`Other`](asff-resourcedetails-other.md) object allows you to provide custom fields and values\. You use the `Other` object in the following cases:
+ The resource type \(the value of the resource `Type`\) does not have a corresponding details object\. To provide details for the resource, you use the [`Other`](asff-resourcedetails-other.md) object\.
+ The object for the resource type does not include all of the fields that you want to populate\. In this case, use the details object for the resource type to populate the available fields\. Use the `Other` object to populate the fields that are not in the type\-specific object\.
+ The resource type is not one of the provided types\. In this case, set `Resource.Type` to `Other`, and use the `Other` object to populate the details\.

**Example**

```
"Details": {
  "AwsEc2Instance": {
    "IamInstanceProfileArn": "arn:aws:iam::123456789012:role/IamInstanceProfileArn",
    "ImageId": "ami-79fd7eee",
    "IpV4Addresses": ["1.1.1.1"],
    "IpV6Addresses": ["2001:db8:1234:1a2b::123"],
    "KeyName": "testkey",
    "LaunchedAt": "2018-09-29T01:25:54Z",
    "MetadataOptions": {
      "HttpEndpoint": "enabled",
      "HttpProtocolIpv6": "enabled",
      "HttpPutResponseHopLimit": 1,
      "HttpTokens": "optional",
      "InstanceMetadataTags": "disabled"
    },
    "NetworkInterfaces": [
    {
      "NetworkInterfaceId": "eni-e5aa89a3"
    }
    ],
    "SubnetId": "PublicSubnet",
    "Type": "i3.xlarge",
    "VirtualizationType": "hvm",
    "VpcId": "TestVPCIpv6"
  },
  "AwsS3Bucket": {
    "OwnerId": "da4d66eac431652a4d44d490a00500bded52c97d235b7b4752f9f688566fe6de",
    "OwnerName": "acmes3bucketowner"
  },
  "Other": { "LightPen": "blinky", "SerialNo": "1234abcd"}  
}
```

## Id<a name="asff-resources-id"></a>

The identifier for the given resource type\.

For AWS resources that are identified by Amazon Resource Names \(ARNs\), this is the ARN\.

For AWS resources that lack ARNs, this is the identifier as defined by the AWS service that created the resource\.

For non\-AWS resources, this is a unique identifier that is associated with the resource\.

**Example**

```
"Id": "arn:aws:s3:::example-bucket"
```

## Partition<a name="asff-resources-partition"></a>

The partition in which the resource is located\. A partition is a group of AWS Regions\. Each AWS account is scoped to one partition\.

The following partitions are supported:
+ `aws` – AWS Regions
+ `aws-cn` – China Regions
+ `aws-us-gov` – AWS GovCloud \(US\) Region

**Example**

```
"Partition": "aws"
```

## Region<a name="asff-resources-region"></a>

The code for the AWS Region where this resource is located\. For a list of Region codes, see [Regional endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints)\.

**Example**

```
"Region": "us-west-2"
```

## ResourceRole<a name="asff-resources-resourcerole"></a>

Identifies the role of the resource in the finding\. A resource is either the target of the finding activity or the actor that performed the activity\.

**Example**

```
"ResourceRole": "target"
```

## Tags<a name="asff-resources-tags"></a>

A list of AWS tags associated with a resource at the time the finding was processed\. You include the `Tags` attribute only for resources that have an associated tag\. If a resource has no associated tag, don't include a `Tags` attribute in the finding\.

The following basic restrictions apply to tags:
+ You can only provide tags that exist on an AWS resource in this field\. To provide data that isn't defined in the AWS Security Finding Format, use the `Other` details subfield\.
+ Values are limited to the following characters: A\-Z, a\-z, 0\-9, blank spaces, and \. : \+ = @ \_ / \- \(hyphen\)\.
+ Values are limited to the AWS tag value length of 256 characters max\.

**Example**

```
"Tags": {
    "billingCode": "Lotus-1-2-3",
    "needsPatching": "true"
}
```

## Type<a name="asff-resources-type"></a>

The type of resource that you are providing details for\.

Whenever possible, use one of the provided resource types, such as `AwsEc2Instance` or `AwsS3Bucket`\.

If the resource type does not match any of the provided resource types, then set the resource `Type` to `Other`, and use the `Other` details subfield to populate the details\.

Supported values are listed under [Resources](asff-resources.md)\.

**Example**

```
"Type": "AwsS3Bucket"
```