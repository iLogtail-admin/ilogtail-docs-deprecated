# ServiceInput插件示例

## 简介
`service_example` 插件是ServiceInput样例插件，用于介绍讲解如何编写ServiceInput插件。

## 配置参数
该插件不需要配置参数。

## 样例

* 采集配置
```yaml
enable: true
inputs:
  - Type: service_input_example
flushers:
  - Type: flusher_stdout
    OnlyStdout: true  
```

* 输入
```
curl --header "test:val123" http://127.0.0.1:19000/data
```

* 输出
```
{
	"test":"val123",
	"__time__":"1658495321"
}
```