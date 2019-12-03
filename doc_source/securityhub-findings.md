# Findings in AWS Security Hub<a name="securityhub-findings"></a>

AWS provides a highly secure cloud computing environment where you can run your workloads\. When you use AWS services, you can also access various security, identity, and compliance tools from AWS and its partners\. These tools include firewalls, endpoint, and intrusion detection applications, as well as database security, vulnerability, and compliance scanners\. These tools can generate thousands of security findings daily\. Findings from these tools might have different finding formats and might be stored and viewed across different platforms\.

In this context, it can be difficult to get a complete understanding of your overall security and compliance state\. To do so, you would have to either continuously and manually process the output from all of these tools or develop ways to aggregate and analyze the generated findings\. With large workloads and environments, processing and analyzing this data can take hundreds of hours of building parsers, transformers, custom compliance rules, and data enrichment pipelines\. Even then, the volume of the findings can sometimes be more than you can effectively process\. Therefore, it can be difficult to separate potential security issues from noise, to prioritize the findings that matter most to you, and to ensure that you aren’t missing any critical findings\. AWS Security Hub eliminates this complexity and reduces the effort required to manage and improve the security and compliance of all of your AWS accounts, resources, and workloads\.

Security Hub imports findings from AWS security services and from the third\-party product integrations that you enable\. Security Hub consumes these findings using a standard findings format called AWS Security Finding Format, which eliminates the need for time\-consuming data conversion efforts\. Security Hub then correlates the findings across integrated products to prioritize the most important ones\. For more information about the findings format, see [AWS Security Finding Format](securityhub-findings-format.md)\.

**Topics**
+ [Working with Findings in Security Hub](#securityhub-managing-findings)
+ [AWS Security Finding Format](securityhub-findings-format.md)

## Working with Findings in Security Hub<a name="securityhub-managing-findings"></a>

After findings are imported in to Security Hub, you can filter finding results and create insights based on findings\.

**Note**  
Findings are kept for 90 days from the last update to the finding\. After 90 days without an update, findings are deleted\.

**To view and manage findings**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Findings**\.

   By default, the **Findings** page lists all of your active findings that Security Hub has processed and generated\. Archived findings are not displayed by default\.

   The **Record state** filter attribute is preselected by default, and its value is `ACTIVE`\. You can update the value of the **Record state** filter attribute to `ARCHIVED` to view only your archived findings\. You can also remove this filter attribute to view all of your active and archived findings\.

1. To query your findings, use the **Filter** field to select one attribute for the **Group by** aggregator and one or more filter attributes from the available attribute list\. There are different filters available for different attributes\. For example, EQUALS and PREFIX operaters are avaiable for string values, such as names and account numbers\. If you create a filter for a date field, you can choose a range of days to retrieve findings for\. When you filter on Criticality, you select a numeric value or range of values to sue as a filter\. Only finidngs that match the criteia you add to the filter are displayed when you apply the filter\.
**Important**  
Filter values are case\-senstive\. When you enter values for a filter, the exact value you enter is used to filter the displayed findings\. For example, to view the findings in your environment that were generated from Security Hub you could create a filter using the **Product name** attribute\. If you use **EQUALS** as an operator, you must enter "Security Hub" to see findings from Security Hub\. If you enter "security hub", no findings are displayed because the value in the finding is *Security Hub*\. Similarly, if you choose **PREFIX** as an operator, which is like a "Starts with" filter, you must enter a partial name using the same casing\. If you enter only *Sec*, Security Hub findings are returned because Security Hub starts with the exact text "Sec"\. If you enter only "sec", no Security Hub findings are displayed\.

   You can use one of the following attributes as the **Group by** aggregator:
   + **Aws account Id**
   + **Company name**
   + **Compliance status**
   + **Generator ID**
   + **Malware name**
   + **Process name**
   + **Threat intel type**
   + **Product ARN**
   + **Product name**
   + **Record state**
   + **EC2 instance image ID**
   + **EC2 instance IPv4**
   + **EC2 instance IPv6**
   + **EC2 instance key name**
   + **EC2 instance subnet ID**
   + **EC2 instance type**
   + **EC2 instance VPC ID**
   + **IAM access key user name**
   + **S3 bucket owner name**
   + **Container image ID**
   + **Container image name**
   + **Container name**
   + **Resource ID**
   + **Resource type**
   + **Severity label**
   + **Source URL**
   + **Type**
   + **Verification state**
   + **Workflow state**

   You can use all of the AWS Security Finding format's attributes as filters to query through your findings\.
**Note**  
For optional filters, AND logic is applied to your specified collection of filters to query your findings\. However, OR logic is applied to multiple filters that use the same attribute set to different values\.

   For the complete list of AWS Security Finding attributes and their descriptions, see [AWS Security Finding Format](securityhub-findings-format.md)\.

1. Choose a finding's title to view the finding's detail pane\. In the detail pane, choose the finding ID to view the complete details JSON of that finding\.
**Note**  
You can apply an action to a maximum of 20 findings at a time\.

1. To apply default \(**Archive**\) and custom actions to findings, select one or more findings' check boxes\. Then expand the **Actions** menu and choose either **Archive** or one of the existing custom actions\. When you **Archive** findings, the `Recordstate` of the selected findings is set to `ARCHIVED`\.
**Note**  
You can create Security Hub custom actions to automate Security Hub with Amazon CloudWatch Events\. For more information and detailed steps on creating custom actions, see [Automating AWS Security Hub with CloudWatch Events](securityhub-cloudwatch-events.md)\.

To update finding details, you can also use the [UpdateFinding](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_UpdateFindings.html) operation of the Security Hub API\.