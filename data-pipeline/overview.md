# 概览

## 输入

| 名称               | 提供方  | 贡献者                                            | 简介         |
| ------------------ | ------- | ------------------------------------------------- | ------------ |
| `file_log`         | SLS官方 | [`messixukejia`](https://github.com/messixukejia) | 文本采集     |
| `metric_meta_host` | SLS官方 | -                                                 | 主机Meta数据 |


## 处理

| 名称                        | 提供方  | 贡献者 | 简介                                       |
| --------------------------- | ------- | ------ | ------------------------------------------ |
| `processor_split_log_regex` | SLS官方 | -      | 实现多行日志（例如Java程序日志）的采集     |
| `processor_regex`           | SLS官方 | -      | 通过正则匹配的模式实现文本日志的字段提取。 |
| `processor_json`            | SLS官方 | -      | 实现对Json格式日志的解析。                 |
| `processor_split_char`      | SLS官方 | -      | 通过单字符的分隔符提取字段。               |
| `processor_split_string`    | SLS官方 | -      | 通过多字符的分隔符提取字段。               |
| `processor_split_key_value` | SLS官方 | -      | 通过切分键值对的方式提取字段。             |
| `processor_rename`          | SLS官方 | -      | 重命名字段。                               |
| `processor_drop`            | SLS官方 | -      | 丢弃字段。                                 |
| `processor_add_fields`      | SLS官方 | -      | 添加字段。                                 |


## 聚合

## 输出

| 名称             | 提供方  | 贡献者 | 简介                                 |
| ---------------- | ------- | ------ | ------------------------------------ |
| `flusher_stdout` | SLS官方 | -      | 将采集到的数据输出到标准输出或文件。 |
| `flusher_sls`    | SLS官方 | -      | 将采集到的数据输出到SLS。            |
| `flusher_kafka`  | 社区    | -      | 将采集到的数据输出到Kafka。          |
