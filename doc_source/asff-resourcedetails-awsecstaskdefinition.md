# AwsEcsTaskDefinition<a name="asff-resourcedetails-awsecstaskdefinition"></a>

The `AwsEcsTaskDefinition` object contains details about a task definition\. A task definition describes the container and volume definitions of an Amazon Elastic Container Service task\.

The following example shows the AWS Security Finding Format \(ASFF\) for the `AwsEcsTaskDefinition` object\. To view descriptions of `AwsEcsTaskDefinition` attributes, see [AwsEcsTaskDefinitionDetails](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_AwsEcsTaskDefinitionDetails.html) in the *AWS Security Hub API Reference*\.

**Example**

```
    "AwsEcsTaskDefinition": {
        "ContainerDefinitions": [
            {
                "Command": ['ruby', 'hi.rb'],
                "Cpu":128,
                "Essential": true,
                "HealthCheck": {
                    "Command": ["CMD-SHELL", "curl -f http://localhost/ || exit 1"],
                    "Interval": 10,
                    "Retries": 3,
                    "StartPeriod": 5,
                    "Timeout": 20
                },
                "Image": "tongueroo/sinatra:latest",
                "Interactive": true,
                "Links": [],
                "LogConfiguration": {
                    "LogDriver": "awslogs",
                    "Options": {
                        "awslogs-group": "/ecs/sinatra-hi",
                        "awslogs-region": "ap-southeast-1",
                        "awslogs-stream-prefix": "ecs"
                    },
                    "SecretOptions": []
                    
                },
                "MemoryReservation": 128,
                "Name": "web",
                "PortMappings": [
                    {
                        "ContainerPort": 4567,
                        "HostPort":4567,
                        "Protocol": "tcp"
                    }
                ],
                "Privileged": true,
                "StartTimeout": 10,
                "StopTimeout": 100,
            }
        ],
        "Family": "sinatra-hi",
        "NetworkMode": "host",
        "RequiresCompatibilities": ["EC2"],
        "TaskRoleArn": "arn:aws:iam::111122223333:role/ecsTaskExecutionRole",
    }
```

The following is a list of valid value examples for `AwsEcsTaskDefinition` attributes:
+ `Cpu`

  Valid values for the Fargate launch type: `256 (.25 vCPU)` \| `512 (.5 vCPU)` \| `1024 (1 vCPU)` \| `2048 (2 vCPU)` \| `4096 (4 vCPU)`
+ `IpcMode`

  Valid values: `host` \| `task` \| `none`
+ `Memory`

  For the EC2 launch type, can provide either a task\-level memory value or a container\-level memory value\.

  For the Fargate launch type, the available values for memory are based on the value of the `Cpu` attribute\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/asff-resourcedetails-awsecstaskdefinition.html)
+ `NetworkMode`

  Valid values: `awsvpc` \| `bridge` \| `host` \| `none`
+ `PidMode`

  Valid values: `host` \| `task`
+ `ContainerDefinitions DependsOn Condition`

  Valid values: `START` \| `COMPLETE` \| `SUCCESS` \| `HEALTHY`
+ `ContainerDefinitions EnvironmentFiles Type`

  Valid value: `s3`
+ `ContainerDefinitions FirelensConfiguration Type`

  Valid values: `fluentd` \| `fluentbit`
+ `ContainerDefinitions LinuxParameters Capabilities Add`

  Valid values: `"ALL"` \| `"AUDIT_CONTROL"` \|` "AUDIT_WRITE"` \| `"BLOCK_SUSPEND"` \| `"CHOWN"` \| `"DAC_OVERRIDE"` \| `"DAC_READ_SEARCH"` \| `"FOWNER"` \| `"FSETID"` \| `"IPC_LOCK"` \| `"IPC_OWNER"` \| `"KILL"` \| `"LEASE"` \| `"LINUX_IMMUTABLE"` \| `"MAC_ADMIN"` \|` "MAC_OVERRIDE"` \| `"MKNOD"` \| `"NET_ADMIN"` \| `"NET_BIND_SERVICE"` \| `"NET_BROADCAST"` \| `"NET_RAW"` \| `"SETFCAP"` \| `"SETGID"` \| `"SETPCAP"` \| `"SETUID"` \| `"SYS_ADMIN"` \| `"SYS_BOOT"` \| `"SYS_CHROOT"` \| `"SYS_MODULE"` \| `"SYS_NICE"` \| `"SYS_PACCT"` \| `"SYS_PTRACE"` \| `"SYS_RAWIO"` \| `"SYS_RESOURCE"` \| `"SYS_TIME"` \| `"SYS_TTY_CONFIG"` \| `"SYSLOG"` \| `"WAKE_ALARM"`
+ `ContainerDefinitions LinuxParameters Capabilities Drop`

  Valid values: `"ALL"` \| `"AUDIT_CONTROL"` \|` "AUDIT_WRITE"` \| `"BLOCK_SUSPEND"` \| `"CHOWN"` \| `"DAC_OVERRIDE"` \| `"DAC_READ_SEARCH"` \| `"FOWNER"` \| `"FSETID"` \| `"IPC_LOCK"` \| `"IPC_OWNER"` \| `"KILL"` \| `"LEASE"` \| `"LINUX_IMMUTABLE"` \| `"MAC_ADMIN"` \|` "MAC_OVERRIDE"` \| `"MKNOD"` \| `"NET_ADMIN"` \| `"NET_BIND_SERVICE"` \| `"NET_BROADCAST"` \| `"NET_RAW"` \| `"SETFCAP"` \| `"SETGID"` \| `"SETPCAP"` \| `"SETUID"` \| `"SYS_ADMIN"` \| `"SYS_BOOT"` \| `"SYS_CHROOT"` \| `"SYS_MODULE"` \| `"SYS_NICE"` \| `"SYS_PACCT"` \| `"SYS_PTRACE"` \| `"SYS_RAWIO"` \| `"SYS_RESOURCE"` \| `"SYS_TIME"` \| `"SYS_TTY_CONFIG"` \| `"SYSLOG"` \| `"WAKE_ALARM"`
+ `ContainerDefinitions LinuxParameters Tmpfs MountOptions`

  Valid values: `"defaults"` \| `"ro"` \| `"rw"` \| `"suid"` \| `"nosuid"` \| `"dev"` \| `"nodev"` \|` "exec"` \| `"noexec"` \| `"sync"` \| `"async"` \| `"dirsync"` \| `"remount"` \| `"mand"` \| `"nomand"` \| `"atime"` \| `"noatime"` \| `"diratime"` \| `"nodiratime"` \| `"bind"` \| `"rbind"` \| `"unbindable"` \| `"runbindable"` \| `"private"` \| `"rprivate"` \| `"shared"` \| `"rshared"` \| `"slave"` \| `"rslave"` \| `"relatime"` \| `"norelatime"` \| `"strictatime"` \| `"nostrictatime"` \|` "mode"` \| `"uid"` \| `"gid"` \| `"nr_inodes"` \|` "nr_blocks"` \| `"mpol"`
+ `ContainerDefinitions LogConfiguration LogDriver`

  Valid values on AWS Fargate: `awslogs` \| `splunk` \| `awsfirelens`

  Valid values on EC2 instances: `awslogs` \| `fluentd` \| `gelf` \| `json-file` \| `journald` \| `logentries` \| `syslog` \| `splunk` \| `awsfirelens`
+ `ContainerDefinitions ResourceRequirements Type`

  Valid values: `GPU` \| `InferenceAccelerator`
+ `ContainerDefinitions Ulimits Name`

  Valid values: `core` \| `cpu` \| `data` \| `fsize` \| `locks` \| `memlock` \| `msgqueue` \| `nice` \| `nofile` \| `nproc` \| `rss` \| `rtprio` \| `rttime` \| `sigpending` \| `stack`
+ `Volumes DockerVolumeConfiguration Scope`

  Valid values: `shared` \| `task`