# Other<a name="asff-resourcedetails-other"></a>

The `Other` object allows you to provide custom fields and values\. You use the `Other` object in the following cases\.
+ The resource type does not have a corresponding `Details` object\. To provide details for the resource, you use the `Other` object\.
+ The `Details` object for the resource type does not include all of the attributes that you want to populate\. In this case, use the `Details` object for the resource type to populate the available attributes\. Use the `Other` object to populate the attributes that are not in the type\-specific object\.
+ The resource type is not one of the provided types\. In this case, you set `Resource.Type` to `Other`, and use the `Other` object to populate the details\.

**Type:** Map of up to 50 key\-value pairs

Each key\-value pair must meet the following requirements\.
+ The key must contain fewer than 128 characters\.
+ The value must contain fewer than 1,024 characters\.