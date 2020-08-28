# Viewing details about a control finding and finding resource<a name="control-finding-resource-details"></a>

For each finding, AWS Security Hub provides access to details to help you investigate the finding\.

You can display details about the finding resource and the related configuration rule\.

You can also view any notes added to the finding\.

## Viewing the complete \.json for a finding<a name="control-finding-json"></a>

You can display and download the full `.json` of a finding\.

To display the `.json`, in the **Finding \.json ** column, choose the icon\.

On the** Finding JSON** panel, to download the `.json`, choose **Download**\.

## Viewing information about a finding resource<a name="control-finding-resource"></a>

The **Resource** column contains the resource type and resource identifier\.

To display information about the resource, choose the resource identifier\.

If you have permission to view the resource in its original service, then the resource identifier displays a link to the service\. For example, for an AWS user, the resource details provide a link to the view the user details in IAM\.

## Viewing the configuration timeline for a finding resource<a name="control-finding-config-timeline"></a>

One avenue of investigation is the configuration timeline for the resource in AWS Config\.

If you have permission to view the configuration timeline for the finding resource, then the finding list provides a link to the timeline\.

**To navigate to the configuration timeline in AWS Config**

1. In the **Investigate** column, choose the icon\.

1. On the menu, choose **Configuration timeline**\. If you do not have access to the configuration timeline, then the link does not appear\.

## Viewing the AWS Config rule for a finding resource<a name="control-finding-view-config-rule"></a>

If the control is based on an AWS Config rule, then you might also want to view the details for the AWS Config rule\. The AWS Config rule information can help you to get a better understanding why a check passed or failed\.

If you have permission to view the AWS Config rule for the control, then the finding list provides a link to the AWS Config rule in AWS Config\.

**To navigate to the AWS Config rule**

1. In the **Investigate** column, choose the icon\.

1. On the menu, choose **Config rule**\. If you do not have access to the AWS Config rule, then **Config rule** is not linked\.

## Viewing notes for findings<a name="control-finding-view-note"></a>

If a finding has an associated note, then the **Updated** column displays a note icon\.

**To display the note that is associated with a finding**  
In the **Updated** column, choose the note icon\.