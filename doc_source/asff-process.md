# Process<a name="asff-process"></a>

The `Process` object provides process\-related details about the finding\.

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

The `Process` object can have the following attributes\.

**`LaunchedAt`**  
Optional  
Indicates when the process was launched\.  
**Type: **String  
**Format:** Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  
**Example**  

```
"LaunchedAt": "2018-09-27T22:37:31Z"
```

**`Name`**  
Optional  
The name of the process\.  
**Type:** String  
**Maximum length:** 64  
**Example**  

```
"Name": "syslogd"
```

**`ParentPid`**  
Optional  
The parent process ID\.  
**Type:** Number  
**Example**  

```
"ParentPid": 56789
```

**`Path`**  
Optional  
The path to the process executable\.   
**Type:** String  
**Maximum length:** 512  
**Example**  

```
"Path": "/usr/sbin/syslogd"
```

**`Pid`**  
Optional  
The process ID\.   
**Type:** Number  
**Example**  

```
"Pid": 12345
```

**`TerminatedAt`**  
Optional  
Indicates when the process was terminated\.  
**Type:** String  
**Format:** Uses the `date-time` format specified in [RFC 3339 section 5\.6, Internet Date/Time Format](https://tools.ietf.org/html/rfc3339#section-5.6)\. The value cannot contain spaces\.  
**Example**  

```
"TerminatedAt": "2018-09-27T23:37:31Z"
```