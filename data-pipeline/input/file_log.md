# 文本日志

## 简介

`file_log` `input`插件可以实现从文本文件中采集日志。

## 配置参数

| 参数          | 类型     | 是否必选 | 说明                                                                                         |
| ----------- | ------ | ---- | ------------------------------------------------------------------------------------------ |
| Type        | String | 是    | 插件类型                                                                                       |
| LogPath     | String | 是    | <p>采集文本日志所在的目录，支持完整目录和通配符两种模式。</p><p>日志文件查找模式为多层目录匹配，即指定目录（包含所有层级的目录）下所有符合条件的文件都会被查找到。</p> |
| FilePattern | String | 是    | 采集文本日志的文件名，支持完整文件名和通配符两种模式。                                                                |
| MaxDepth    | Int    | 否    | <p>设置日志目录被监控的最大深度。最大深度范围：0~1000，0代表只监控本层目录。</p><p>默认取值为0。</p>                              |
| DockerFile  | Boolen | 否    | 是否为Docker文件。                                                                               |

## 样例

采集`/home/test_log/`路径下的所有文件名匹配`*.log`规则的文件。

```
enable: true
inputs:
  - Type: file_log
    LogPath: /home/test_log
    FilePattern: "*.log"
flushers:
  - Type: flusher_stdout
    OnlyStdout: true
```
