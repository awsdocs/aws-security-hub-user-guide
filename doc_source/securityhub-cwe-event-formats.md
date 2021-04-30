# EventBridge event formats for Security Hub<a name="securityhub-cwe-event-formats"></a>

The **Security Hub Findings \- Imported**, **Security Findings \- Custom Action**, and **Security Hub Insight Results** event types use the following event formats\.

The event format is the format that is used when Security Hub sends an event to EventBridge\.

## Security Hub Findings \- Imported<a name="securityhub-cwe-event-formats-findings-imported"></a>

**Security Hub Findings \- Imported** events that are sent from Security Hub to EventBridge use the following format\.

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
      "findings": {
         <finding content>
       }
   }
}
```

`<finding content>` is the content, in JSON format, of the finding that is sent by the event\.

For a complete list of finding attributes, see [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\.

For information about how to configure EventBridge rules that are triggered by these events, see [Configuring an EventBridge rule for automatically sent findings](securityhub-cwe-all-findings.md)\.

## Security Hub Findings \- Custom Action<a name="securityhub-cwe-event-formats-findings-custom-action"></a>

**Security Hub Findings \- Custom Action** events that are sent from Security Hub to EventBridge use the following format\.

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
    "findings": {
        <finding content>
    }
  }
}
```

`<finding content>` is the content, in JSON format, of the finding that is sent by the event\.

For a complete list of finding attributes, see [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\.

For information about how to configure EventBridge rules that are triggered by these events, see [Using custom actions to send findings and insight results to EventBridge](securityhub-cwe-custom-actions.md)\.

## Security Hub Insight Results<a name="securityhub-cwe-event-formats-insight-results"></a>

**Security Hub Insight Results** events that are sent from Security Hub to EventBridge use the following format\.

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

For information about how to create an EventBridge rule that is triggered by these events, see [Using custom actions to send findings and insight results to EventBridge](securityhub-cwe-custom-actions.md)\.