# Note<a name="asff-note"></a>

The `Note` object adds a user\-defined note to the finding\.

A finding provider can provide an initial note for a finding but cannot add notes after that\. A note can only be updated using [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

**Example**

```
"Note": {
    "Text": "Don't forget to check under the mat.",
    "UpdatedBy": "jsmith",
    "UpdatedAt": "2018-08-31T00:15:09Z"
}
```

The `Note` object can have the following attributes\.

**`Text`**  
Required  
The text of a finding note\.  
**Type:** String  
**Maximum length: ** 512  
**Example**  

```
"Text": "Example text."
```

**`UpdatedAt`**  
Required  
Indicates when the note was updated\.  
**Type:** String  
**Format:** Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  
**Example**  

```
"UpdatedAt": "2018-08-31T00:15:09Z"
```

**`UpdatedBy`**  
Required  
The principal that created a note\.  
**Type:** String or ARN  
**Maximum length:** 512  
**Example**  

```
"UpdatedBy": "jsmith"
```