# 概览

## 输入

| 名称         | 提供方   | 贡献者                                                   | 简介   |
| ---------- | ----- | ----------------------------------------------------- | ---- |
| `file_log` | SLS官方 | [`messixukejia`](https://github.com/messixukejia) | 文本采集 |
|            |       |                                                       |      |
|            |       |                                                       |      |
|            |       |                                                       |      |
|            |       |                                                       |      |
|            |       |                                                       |      |

## 处理

| 名称                          | 提供方   | 贡献者 | 简介                    |
| --------------------------- | ----- | --- | --------------------- |
| `processor_default`         | SLS官方 | -   | 不做处理，采集原始数据。        |
| `processor_fields_with_conditions` | SLS官方 | -  | 根据日志部分字段的取值，动态进行字段扩展或删除。 |
| `processor_json`            | SLS官方 | -   | 实现对Json格式日志的解析。       |
| `processor_regex`           | SLS官方 | -   | 通过正则匹配的模式实现文本日志的字段提取。 |
| `processor_split_char`      | SLS官方 | -   | 通过单字符的分隔符提取字段。        |
| `processor_split_log_regex` | SLS官方 | -   | 实现多行日志（例如Java程序日志）的采集 |
| `processor_split_string`    | SLS官方 | -   | 通过多字符的分隔符提取字段。        |

## 聚合

## 输出

| 名称               | 提供方   | 贡献者 | 简介                 |
| ---------------- | ----- | --- | ------------------ |
| `flusher_stdout` | SLS官方 | -   | 将采集到的数据输出到标准输出或文件。 |
| `flusher_sls`    | SLS官方 | -   | 将采集到的数据输出到SLS。     |
| `flusher_kafka`  | 社区    | -   | 将采集到的数据输出到Kafka。   |
