[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/jenkinsci/pipeline-aws-plugin)
[![Build Status](https://ci.jenkins.io/buildStatus/icon?job=Plugins/pipeline-aws-plugin/master)](https://ci.jenkins.io/job/Plugins/job/pipeline-aws-plugin/job/master/)

# Features

This plugins adds Jenkins pipeline steps to interact with the Aliyun OSS and OOS API.

* [ossUploadAndOosExec](#ossUploadAndOosExec)
* [oosStatusQuery](#oosStatusQuery)
* [oosExecuteNotify](#oosExecuteNotify)

[**see the changelog for release information**](#changelog)

# Primary/Agent setups

This plugin is not optimized to setups with a primary and multiple agents.
Only steps that touch the workspace are executed on the agents while the rest is executed on the master.

For the best experience make sure that primary and agents have the same global configuration of AK/SK and networking
capabilities.

# Usage / Steps

## ossUploadAndOosExec

Upload built project to OSS and execution OOS template download OSS file to smartly deploy on ECS instances.

```groovy
executeId = ossUploadAndOosExec(batchNumber: 3, mode: 'FailurePause', bucket: 'testBucket', destinationDir: '/root/test.zip', invokeScript: '', localPath: '/', objectName: 'test.zip', pausePolicy: 'EveryBatchPause', region: 'cn-hangzhou', resourceId: 'asg-bp15XXXXX', resourceType: 'ESS')
```

### oosStatusQuery

Query OOS template task status by OSS template task id.

```groovy
oosStatusQuery(executeId: "exec-XXXXXXXXX", region: 'cn-hangzhou')
```

### oosExecuteNotify

Oos template pause task execution next step,like Approve or Cancelled.

```groovy
oosExecuteNotify(executeId: "exec-XXXXXXXXX", region: 'cn-hangzhou', notifyType: "Approve")
```



