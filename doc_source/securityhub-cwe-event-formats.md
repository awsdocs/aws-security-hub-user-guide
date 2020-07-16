# CloudWatch Events formats for Security Hub<a name="securityhub-cwe-event-formats"></a>

The CloudWatch events for the **Security Hub Findings \- Imported**, **Security Findings \- Custom Action**, and **Security Hub Insight Results** event types use the following formats\.

## Security Hub Findings \- Imported<a name="securityhub-cwe-event-formats-findings-imported"></a>

The CloudWatch event for the **Security Hub Findings \- Imported** event type is in the following format\.

```
{
   "version":"0",
   "id":"CWE-event-id",
   "detail-type":"Security Hub Findings - Imported",
   "source":"aws.securityhub",
   "account":"111122223333",
   "time":"2019-04-11T21:52:17Z",
   "region":"us-west-2",
   "resources":[
      "arn:aws:securityhub:us-west-2::product/aws/macie/arn:aws:macie:us-west-2:111122223333:integtest/trigger/6294d71b927c41cbab915159a8f326a3/alert/f2893b211841"
   ],
   "detail":{
      "findings”: [AMAZON_FINDING_JSON]
   }
}
```

For a complete list of parameters included in `AMAZON_FINDING_JSON`, see [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\.

## Security Hub Findings \- Custom Action<a name="securityhub-cwe-event-formats-findings-custom-action"></a>

The CloudWatch event for the **Security Hub Findings \- Custom Action** event type is in the following format\.

```
{
  "version": "0",
  "id": "1a1111a1-b22b-3c33-444d-5555e5ee5555",
  "detail-type": "Security Hub Findings - Custom Action",
  "source": "aws.securityhub",
  "account": "111122223333",
  "time": "2019-04-11T18:43:48Z",
  "region": "us-west-1",
  "resources": [
    "arn:aws:securityhub:us-west-1:111122223333:action/custom/custom-action-name"
  ],
  "detail": {
    "actionName":"custom-action-name",
    "actionDescription": "description of the action",
    "findings": [AMAZON_FINDING_JSON for each specified finding]
  }
}
```

For a complete list of parameters included in `AMAZON_FINDING_JSON`, see [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\.

## Security Hub Insight Results<a name="securityhub-cwe-event-formats-insight-results"></a>

The CloudWatch Events event for the **Security Hub Insight Results** event type has the following format\.

```
{ 
  "version": "0",
  "id": "1a1111a1-b22b-3c33-444d-5555e5ee5555",
  "detail-type": "Security Hub Insight Results",
  "source": "aws.securityhub",
  "account": "111122223333",
  "time": "2017-12-22T18:43:48Z",
  "region": "us-west-1",
  "resources": [
      "arn:aws:securityhub:us-west-1:111122223333::product/aws/macie:us-west-1:222233334444:test/trigger/1ec9cf700ef6be062b19584e0b7d84ec/alert/f2893b211841"
  ],
  "detail": {
    "actionName":"name of the action",
    "actionDescription":"description of the action",
    "insightArn":"ARN of the insight",
    "insightName":"Name of the insight",
    "resultType":"ResourceAwsIamAccessKeyUserName",
    "number of results":"number of results, max of 100",
    "insightResults": [
        {"result 1": 5},
        {"result 2": 6}
    ]
  }
}
```