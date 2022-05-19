# Remediation<a name="asff-remediation"></a>

The `Remediation` object provides information about recommended remediation steps to address the finding\.

**Example**

```
"Remediation": {
    "Recommendation": {
        "Text": "Run sudo yum update and cross your fingers and toes.",
        "Url": "http://myfp.com/recommendations/dangerous_things_and_how_to_fix_them.html"
    }
}
```

## Remediation attributes<a name="asff-remediation-attributes"></a>

The `Remediation` object can have the following attributes\.

**[`Recommendation`](#asff-remediation-recommendation)**  
Optional  
A recommendation on how to remediate the issue identified within a finding\.  
The `Recommendation` field is meant to facilitate manual instructions or details to resolve a finding\.  
If the recommendation object is present, then either the `Text` or `Url` field must be present and populated\. Both fields can be present and populated\.  
**Type:** Object  
**Example**  

```
"Recommendation": {
    "Text": "Example text.",
    "Url": "http://myfp.com/recommendations/dangerous_things_and_how_to_fix_them.html"
}
```

## Recommendation<a name="asff-remediation-recommendation"></a>

The `Recommendation` object can have the following attributes\.

**`Text`**  
Optional  
A free\-form string that is the recommendation of what to do about the finding when presented to a user\. This field can contain nonspecific boilerplate text or details that are specific to this instance of the finding\.  
**Type:** String  
**Maximum length:** 512  
**Example**  

```
"Text": "Example text."
```

**`Url`**  
Optional  
A URL to link to general remediation information for the finding type of a finding\.  
This URL must not require credentials to access\. It must be accessible from the public internet and must not expect any context or session\.  
**Type:** URL  
**Example**  

```
"Url": "http://myfp.com/recommendations/example_domain.html"
```