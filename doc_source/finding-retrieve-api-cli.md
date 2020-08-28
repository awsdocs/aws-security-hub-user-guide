# Retrieving finding details \(Security Hub API, AWS CLI\)<a name="finding-retrieve-api-cli"></a>

To retrieve details for selected findings programmatically, you can use an API call or the AWS Command Line Interface\.

**To retrieve a list of findings \(Security Hub API, AWS CLI\)**
+ Security Hub API – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html) API operation\.
+ AWS CLI – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/get-findings.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/get-findings.html) command\.

  ```
  get-findings --filters <filter criteria JSON> --sort-criteria <sort criteria> --page-size <findings per page> --max-items <maximum number of results>
  ```

  **Example**

  ```
  aws securityhub get-findings --filters '{"GeneratorId":[{"Value": "aws-foundational","Comparison":"PREFIX"},"WorkflowStatus": {"Value": "NEW","Comparison":"EQUALS"},"Confidence": [{"Gte": 85}]}' --sort-criteria '{"Field": "LastObservedAt","SortOrder": "desc"}' --page-size 5 --max-items 100
  ```