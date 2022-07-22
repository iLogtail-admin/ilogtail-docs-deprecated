# MetricInput插件示例

## 简介
`metric_example` 插件是MetricInput样例插件，用于介绍讲解如何编写MetricInput插件。

## 配置参数
该插件不需要配置参数。

## 样例

* 采集配置
```yaml
enable: true
inputs:
  - Type: metric_input_example
flushers:
  - Type: flusher_stdout
    OnlyStdout: true  
```

* 输出
```
{
    "__name__":"example_counter",
    "__labels__":"hostname#$#************************|ip#$#172.***.***.***",
    "__time_nano__":"1658491078378371632",
    "__value__":"101",
    "__time__":"1658491078"
}
```