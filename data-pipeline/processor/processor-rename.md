# 重命名字段

## 简介

`processor_rename processor`插件可以将日志字段重命名。

## 配置参数

| 参数       | 类型    | 是否必选 | 说明                                                                 |
| ---------- | ------- | -------- | -------------------------------------------------------------------- |
| Type       | String  | 是       | 插件类型。                                                           |
| NoKeyError | Map     | 否       | 待添加字段和字段值。键值对格式，支持添加多个。                       |
| SourceKeys | Boolean | 是       | 当Key相同时是否忽略。如果未添加该参数，则默认使用false，表示不忽略。 |
| DestKeys   | Boolean | 是       | 当Key相同时是否忽略。如果未添加该参数，则默认使用false，表示不忽略。 |




## 样例

采集`/home/test-log/`路径下的`json.log`文件，并按照`Json`格式进行日志解析，然后对解析后的字段进行重命名。

* 输入

```
echo '{"key1": 123456, "key2": "abcd"}' >> /home/test-log/json.log
```

* 采集配置

```
enable: true
inputs:
  - Type: file_log
    LogPath: /home/test-log/
    FilePattern: key_value.log
processors:
  - Type: processor_json
    SourceKey: content
    KeepSource: false
    ExpandDepth: 1
    ExpandConnector: ""
  - Type: processor_rename
    SourceKeys: 
      - key1
    DestKeys:
      - new_key1
flushers:
  - Type: flusher_sls
    Endpoint: cn-xxx.log.aliyuncs.com
    ProjectName: test_project
    LogstoreName: test_logstore
  - Type: flusher_stdout
    OnlyStdout: true
```

* 输出

```
{
    "__tag__:__path__": "/home/test_log/key_value.log",
    "new_key1": "123456",
    "key2": "abcd",
    "__time__": "1657354602"
}
``` 