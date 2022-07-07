# 采集配置

`iLogtail`工作目录下`user_yaml_config.d`目录下可以配置数据流水线（`data-pipeline`），每个数据流水线对应一个配置文件，配置文件为`yaml`格式，以`.yaml`结尾。



一个典型的采集流水线以下部分组成：

* 输入（`Input`）：从数据源采集数据，数据源可以是文本、HTTP数据、Syslog等。
* 处理（`Processor`）：对采集的数据进行解析、过滤、加工等。
* 聚合（`Aggregator`）：`Pipeline`会自带默认聚合插件，一般不需要关注。
* 输出（`Flusher`）：将符合条件的数据发送到指定的存储系统。

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
