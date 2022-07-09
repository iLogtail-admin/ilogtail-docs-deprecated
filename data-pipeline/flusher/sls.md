# SLS

## 简介

`flusher_sls` `flusher`插件可以实现将采集到的数据，经过处理后，发送到SLS。

## 配置参数

| 参数              | 类型      | 是否必选 | 说明                                                              |
| --------------- | ------- | ---- | --------------------------------------------------------------- |
| Type            | String  | 是    | 插件类型                                                            |
| Endpoint        | String  | 否    | [SLS接入点地址](https://help.aliyun.com/document\_detail/29008.html) |
| ProjectName     | String  | 否    | SLS Project名                                                    |
| LogstoreName    | String  | 否    | SLS Logstore名                                                   |
| EnableShardHash | Boolean | 否    |                                                                 |
| KeepShardHash   | Boolean | 否    |                                                                 |

## 样例

采集`/home/test-log/`路径下的所有文件名匹配`*.log`规则的文件，并将采集结果发送到SLS。

```
enable: true
inputs:
  - Type: file_log
    LogPath: /home/test-log/
    FilePattern: "*.log"
flushers:
  - Type: flusher_sls
    Endpoint: cn-xxx.log.aliyuncs.com
    ProjectName: test_project
    LogstoreName: test_logstore
```
