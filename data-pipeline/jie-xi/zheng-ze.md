# 正则

## 简介

`processor_regex` `processor`插件，可以通过正则匹配的模式实现文本日志的字段提取。

## 配置参数



| 参数	          | 类型	      | 是否必选	 | 说明                                                                        |
| ------------ | -------- | ----- | ------------------------------------------------------------------------- |
| Type         | string   | 是     | 插件类型                                                                      |
| SourceKey    | string   | 是     | 原始字段名                                                                     |
| Regex        | string   | 是     | 正则表达式，使用()标注待提取的字段。                                                       |
| Keys         | String数组 | 是     | 提取的字段名，例如\["ip", "time", "method"]。                                       |
| NoKeyError   | Boolean  | 否     | 无匹配的原始字段时是否报错。如果未添加该参数，则默认使用false，表示不报错。                                  |
| NoMatchError | Boolean  | 否     | 正则表达式与原始字段的值不匹配时是否报错。如果未添加该参数，则默认使用false，表示不报错。                           |
| KeepSource   | Boolean  | 否     | 是否保留原始字段。如果未添加该参数，则默认使用false，表示不保留。                                       |
| FullMatch    | Boolean  | 否     | 如果未添加该参数，则默认使用true，表示只有字段完全匹配Regex参数中的正则表达式时才被提取。配置为false，表示部分字段匹配也会进行提取。 |

## 样例

采集`/home/test-dir/test_log`路径下的`reg.log`文件，日志内容按照提取字段`time`、`msg`字段。

```
enable: true
inputs:
  - Type: file_log
    LogPath: /home/test-dir/test_log
    FilePattern: reg.log
processors:
  - Type: processor_regex
    SourceKey: content
    Regex: (\d*-\d*-\d*)\s(.*)
    Keys:
      - time
      - msg
flushers:
  - Type: flusher_sls
    Endpoint: cn-xxx.log.aliyuncs.com
    ProjectName: test_project
    LogstoreName: test_logstore
  - Type: flusher_stdout
    OnlyStdout: true
```
