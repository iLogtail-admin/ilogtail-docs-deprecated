# 分隔符

## 简介

`processor_split_char`插件可以通过单字符的分隔符提取字段，该方式支持使用引用符对分隔符进行包裹。

`processor_split_string`插件可以通过多字符的分隔符提取字段，该方式不支持使用引用符对分隔符进行包裹。

## 配置参数

### `processor_split_char`配置

| 参数	          | 类型	      | 是否必选	 | 说明                                       |
| ------------ | -------- | ----- | ---------------------------------------- |
| Type         | String   | 是     | 插件类型                                     |
| SourceKey    | String   | 是     | 原始字段名                                    |
| SplitSep     | String   | 是     | 分隔符。必须为单字符，可设置为不可见字符，例如\u0001。           |
| SplitKeys    | String数组 | 是     | 分割日志后设置的字段名，例如\["ip", "time", "method"]。 |
| QuoteFlag    | Boolean  | 否     | 是否使用引用符。如果未添加该参数，则默认使用false，表示不使用。       |
| Quote        | String   | 否     | 仅当QuoteFlag配置为true时有效。                   |
| NoKeyError   | Boolean  | 否     | 无匹配的原始字段时是否报错。如果未添加该参数，则默认使用false，表示不报错。 |
| NoMatchError | Boolean  | 否     | 分隔符不匹配时是否报错。如果未添加该参数，则默认使用false，表示不报错。   |
| KeepSource   | Boolean  | 否     | 是否保留原始字段。如果未添加该参数，则默认使用false，表示不保留。      |

### `processor_split_string`配置



| 参数	             | 类型	      | 是否必选	 | 说明                                                                |
| --------------- | -------- | ----- | ----------------------------------------------------------------- |
| Type            | String   | 是     | 插件类型                                                              |
| SourceKey       | String   | 是     | 原始字段名                                                             |
| SplitSep        | String   | 是     | 分隔符。可以设置不可见字符，例如\u0001\u0002。                                     |
| SplitKeys       | String数组 | 是     | 分割日志后设置的字段名，例如\["ip", "time", "method"]。                          |
| PreserveOthers  | Boolean  | 否     | 如果待分割的字段长度大于SplitKeys参数中的字段长度时是否保留超出部分。如果未添加该参数，则默认使用false，表示不保留。 |
| ExpandOthers    | Boolean  | 否     | 是否解析超出部分。如果未添加该参数，则默认使用false，表示不继续解析。                             |
| ExpandKeyPrefix | String   | 否     | 超出部分的命名前缀。例如配置expand\_，则Key为expand\_1、expand\_2。                  |
| NoKeyError      | Boolean  | 否     | 无匹配的原始字段时是否报错。如果未添加该参数，则默认使用false，表示不报错。                          |
| NoMatchError    | Boolean  | 否     | 分隔符不匹配时是否报错。如果未添加该参数，则默认使用false，表示不报错。                            |
| KeepSource      | Boolean  | 否     | 是否保留原始字段。如果未添加该参数，则默认使用false，表示不保留。                               |

## 样例

采集`/home/test-dir/test_log`路径下的`delimiter.log`文件，使用竖线`（|）`分隔符提取日志的字段值，并设置字段名为`time`、`k1`、`k2`。\


```
enable: true
inputs:
  - Type: file_log
    LogPath: /home/test-dir/test_log
    FilePattern: delimiter.log
processors:
  - Type: processor_split_char
    SourceKey: content
    SplitSep: "|"
    SplitKeys:
      - time
      - k1
      - k2
flushers:
  - Type: flusher_sls
    Endpoint: cn-xxx.log.aliyuncs.com
    ProjectName: test_project
    LogstoreName: test_logstore
  - Type: flusher_stdout
    OnlyStdout: true
```