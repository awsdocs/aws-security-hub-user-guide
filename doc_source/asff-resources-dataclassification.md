# DataClassification<a name="asff-resources-dataclassification"></a>

The `DataClassification` object contains information about sensitive data that was detected on the resource\.

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

## DataClassification attributes<a name="asff-resources-dataclassification-attributes"></a>

`DataClassification` can contain the following attributes\.

`DetailedResultsLocation`  
Optional  
The path to the folder or file that contains the sensitive data\.  
**Type:** String

[`Result`](#asff-resources-dataclassification-result)  
Optional  
The details about the sensitive data that was detected on the resource\.  
**Type:** Object

## Result<a name="asff-resources-dataclassification-result"></a>

The `Result` object contains the details about the sensitive data that was detected on the resource\.

`Result` can have the following attributes\.

`AdditionalOccurrences`  
Optional  
Indicates whether there are additional occurrences of sensitive data that are not included in the finding\. This occurs when the number of occurrences exceeds the maximum that can be included\.  
**Type:** Boolean

[`CustomDataIdentifiers`](#asff-resources-dataclassification-customdataidentifiers)  
Optional  
Provides details about sensitive data that was identified based on customer\-defined configuration\.  
**Type:** Object

`MimeType`  
Optional  
The type of content that the finding applies to\.  
**Type:** String  
**Required format:** Must be a MIME type\.  
**Examples**  
+ `application/gzip`, for a GNU Gzip compressed archive file
+ `application/pdf`, for an Adobe Portable Document Format \(`.pdf`\) file

[`SensitiveData`](#asff-resources-dataclassification-sensitivedata)  
Optional  
Provides details about sensitive data that was identified based on built\-in configuration\.  
**Type:** Object

`SizeClassified`  
Optional  
The total size in bytes of the affected data\.  
**Type:** Long

`Status`  
Optional  
Provides details about the current status of the detection\.  
**Type:** Object

`Status.Code`  
Optional  
The code that represents the status of the sensitive data detection\.  
**Type:** String

`Status.Reason`  
Optional  
A longer description of the current status of the sensitive data detection\.  
**Type:** String

## CustomDataIdentifiers<a name="asff-resources-dataclassification-customdataidentifiers"></a>

`CustomDataIdentifiers` contains instances of sensitive data that were detected by user\-defined identifiers\.

`CustomDataIdentifiers` can have the following attributes\.

[`Detections`](#asff-resources-dataclassification-detections)  
Optional  
The list of detected instances of sensitive data\.  
**Type:** Array of objects

`TotalCount`  
Optional  
The total number of occurrences of sensitive data\.  
**Type:** Integer

## SensitiveData<a name="asff-resources-dataclassification-sensitivedata"></a>

`SensitiveData` contains detected instances of sensitive data that are based on built\-in identifiers\.

`Category`  
Optional  
The category of sensitive data that was detected\. For example, the category might indicate that the sensitive data involved credentials, financial information, or personal information\.  
**Type:** String

[`Detections`](#asff-resources-dataclassification-detections)  
Optional  
The list of detected instances of sensitive data\.  
**Type:** Array of objects

`TotalCount`  
Optional  
The total number of occurrences of sensitive data\.  
**Type:** Integer

## Detections<a name="asff-resources-dataclassification-detections"></a>

`Detections` contains the details of the sensitive data that was detected\.

Each instance of detected sensitive data can have the following attributes\.

`Arn`  
Optional  
The ARN of the custom identifier that was used to detect the sensitive data\.  
`Arn` is only provided in `Detections` instances under `CustomDataIdentifiers` \. `Detections` instances under `SensitiveData` do not have the `Arn` attribute\.  
**Type:** String

`Count`  
Optional  
The total number of occurrences of sensitive data that were detected\.  
**Type:** Integer

`Name`  
Optional  
The name of the custom identifier that detected the sensitive data\.  
`Name` is only provided in `Detections` instances under `CustomDataIdentifiers`\. `Detections` instances under `SensitiveData` do not have the `Name` attribute\.  
**Type:** String

`Occurrences`  
Optional  
Details about the sensitive data that was detected\. `Occurrences` can contain the following objects\. Each of these objects contains an array of objects\.  
+ [`Cells`](#asff-resources-dataclassification-cells) – Contains occurrences of sensitive data detected in Microsoft Excel files, comma\-separated value \(`.csv`\) files, or tab\-separated value \(`.tsv`\) files
+ [`LineRanges`](#asff-resources-dataclassification-lineranges) – Contains occurrences of sensitive data detected in nonbinary text files or Microsoft Word files
+ [`OffsetRanges`](#asff-resources-dataclassification-offsetranges) – Contains occurrences of sensitive data detected in binary text files
+ [`Pages`](#asff-resources-dataclassification-pages) – Contains occurrences of sensitive data detected in Adobe Portable Document Format \(`.pdf`\) files
+ [`Records`](#asff-resources-dataclassification-records) – Contains occurrences of sensitive data detected in an Apache Avro object container or an Apache Parquet file
**Type:** Object

`Type`  
Optional  
The type of sensitive data that was detected\. For example, the type might indicate that the data is an email address\.  
`Type` is only provided in `Detections` instances under `SensitiveData` \. `Detections` instances under `CustomDataIdentifiers` do not have the `Type` attribute\.  
**Type:** String

## Cells<a name="asff-resources-dataclassification-cells"></a>

`Cells` contains occurrences of sensitive data detected in Microsoft Excel workbooks, comma\-separated value \(`.csv`\) files, or tab\-separated value \(`.tsv`\) files\.

For each occurrence, `Cells` identifies the cell that contains the sensitive data\.

Each occurrence can contain the following attributes\.

`CellReference`  
Optional  
For a Microsoft Excel workbook, provides the location of the cell, as an absolute cell reference, that contains the data\. For example, Sheet2\!C5 for cell C5 on Sheet2\.  
This attribute is null for `.csv` and `.tsv` files\.  
**Type:** String

`Column`  
Optional  
The column number of the column that contains the data\. For a Microsoft Excel workbook, the column number corresponds to the alphabetical column identifiers\. For example, a value of 1 for `Column` corresponds to the A column in the workbook\.  
**Type:** Integer

`ColumnName`  
Optional  
The name of the column that contains the data\.  
**Type:** String

`Row`  
Optional  
The row number of the row that contains the data\.  
**Type:** Integer

## LineRanges<a name="asff-resources-dataclassification-lineranges"></a>

`LineRanges` contains occurrences of sensitive data detected in a nonbinary text file or a Microsoft Word file\. Nonbinary text files include files such as `.html`, `.xml`, `.json`, and `.txt` files\.

For each occurrence, `LineRanges` provides the location of the sensitive data\. The location includes the line where the data is located and the position of the data on that line\.

Each occurrence can have the following attributes\.

`End`  
Optional  
The number of lines from the beginning of the file to the end of the sensitive data\.  
**Type:** Integer

`Start`  
Optional  
The number of lines from the beginning of the file to the end of the sensitive data\.  
**Type:** Integer

StartColumn  
Optional  
In the line where the sensitive data begins, the column within the line where the sensitive data starts\.  
**Type:** Integer

## OffsetRanges<a name="asff-resources-dataclassification-offsetranges"></a>

`OffsetRanges` contains occurrences of sensitive data detected in a binary text file\.

For each occurrence, `OffsetRanges` provides the location of the sensitive data\. The location is the number of characters relative to the beginning of the file\.

Each occurrence can have the following attributes\.

`End`  
Optional  
The number of characters from the beginning of the file to the end of the sensitive data\.  
**Type:** Integer

`Start`  
Optional  
The number of characters from the beginning of the file to the beginning of the sensitive data\.  
**Type:** Integer

`StartColumn`  
Optional  
The column where the sensitive data begins\.  
**Type:** Integer

## Pages<a name="asff-resources-dataclassification-pages"></a>

`Pages` provides occurrences of sensitive data in an Adobe Portable Document Format \(`.pdf`\) file\.

For each occurrence, `Pages` identifies the page that contains the data, and provides the position of the data on the page\. The position can be identified using either line numbers or numbers of characters\.

Each occurrence can have the following attributes\.

`LineRange`  
Optional  
Uses line numbers to identify the location of the sensitive data\.  
**Type:** Object

`LineRange.End`  
Optional  
The number of lines from the beginning of the file to the end of the sensitive data\.  
**Type:** Integer

`LineRange.Start`  
Optional  
The number of lines from the beginning of the file to the beginning of the sensitive data\.  
**Type:** Integer

`LineRange.StartColumn`  
Optional  
On the line where the sensitive data begins, the column number where the sensitive data begins\.  
**Type:** Integer

`OffsetRange`  
Optional  
Identifies the location of the sensitive data based on the number of characters\.  
**Type:** Object

`OffsetRange.End`  
Optional  
The number of characters from the beginning of the file to the end of the sensitive data\.  
**Type:** Integer

`OffsetRange.Start`  
Optional  
The number of characters from the beginning of the file to the beginning of the sensitive data\.  
**Type:** Integer

`OffsetRange.StartColumn`  
Optional  
On the line where the sensitive data starts, the column number where it starts\.  
**Type:** Integer

`PageNumber`  
Optional  
The page number of the page that contains the sensitive data\.  
**Type:** Integer

## Records<a name="asff-resources-dataclassification-records"></a>

`Records` identifies occurrences of sensitive data in an Apache Avro object container or an Apache Parquet file\.

For each occurrence, `Records` specifies the record index and the path to the field that contains the sensitive data\.

Each occurrence can have the following attributes\.

`JsonPath`  
Optional  
The path, as a JSONPath expression, to the field in the record that contains the data\. If the field name is longer than 20 characters, it is truncated\. If the path is longer than 250 characters, it is truncated\.  
**Type:** String

`RecordIndex`  
Optional  
The record index, starting from 0, for the record that contains the data\.  
**Type:** Integer