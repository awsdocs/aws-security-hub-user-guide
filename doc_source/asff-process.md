# Process<a name="asff-process"></a>

The `Process` object provides process\-related details about the finding\.

To view descriptions of `Process` attributes, see [ProcessDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_ProcessDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
"Process": {
    "Name": "syslogd",
    "Path": "/usr/sbin/syslogd",
    "Pid": 12345,
    "ParentPid": 56789,
    "LaunchedAt": "2018-09-27T22:37:31Z",
    "TerminatedAt": "2018-09-27T23:37:31Z"
}
```