# AwsSageMaker<a name="asff-resourcedetails-awssagemaker"></a>

The following are examples of the AWS Security Finding Format for `AwsSageMaker` resources\.

## AwsSageMakerNotebookInstance<a name="asff-resourcedetails-awssagemakernotebookinstance"></a>

The `AwsSageMakerNotebookInstance` object provides information about a Amazon SageMaker notebook instance, which is a machine learning compute instance running the Jupyter Notebook App\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsSageMakerNotebookInstance` object\. To view descriptions of `AwsSageMakerNotebookInstance` attributes, see [AwsSageMakerNotebookInstanceDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsSageMakerNotebookInstanceDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"AwsSageMakerNotebookInstance": {
    "DirectInternetAccess": "Disabled",
    "InstanceMetadataServiceConfiguration": {
    	"MinimumInstanceMetadataServiceVersion": "1",
    },
    "InstanceType": "ml.t2.medium",
    "LastModifiedTime": "2022-09-09 22:48:32.012000+00:00",
    "NetworkInterfaceId": "eni-06c09ac2541a1bed3",
    "NotebookInstanceArn": "arn:aws:sagemaker:us-east-1:001098605940:notebook-instance/sagemakernotebookinstancerootaccessdisabledcomplia-8myjcyofzixm",
    "NotebookInstanceName": "SagemakerNotebookInstanceRootAccessDisabledComplia-8MYjcyofZiXm",
    "NotebookInstanceStatus": "InService",
    "PlatformIdentifier": "notebook-al1-v1",
    "RoleArn": "arn:aws:iam::001098605940:role/sechub-SageMaker-1-scenar-SageMakerCustomExecution-1R0X32HGC38IW",
    "RootAccess": "Disabled",
    "SecurityGroups": [
    	"sg-06b347359ab068745"
    ],
    "SubnetId": "subnet-02c0deea5fa64578e",
    "Url": "sagemakernotebookinstancerootaccessdisabledcomplia-8myjcyofzixm.notebook.us-east-1.sagemaker.aws",
    "VolumeSizeInGB": 5
}
```