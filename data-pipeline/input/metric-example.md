# MetricInput插件示例

## 简介
`metric_example` 插件是MetricInput样例插件，用于介绍讲解如何编写MetricInput插件。

## 配置参数
该插件不需要配置参数。

## MetricInput插件开发说明
### MetricInput接口说明
* Init：插件初始化接口，主要供插件做一些参数检查，并为其提供上下文对象 Context。 返回值的第一个参数表示调用周期（毫秒），插件系统会以该值作为数据获取周期。如果返回 0 的话，插件系统会使用全局的数据获取周期。 返回值的第二个参数表示初始化中发生的错误，一旦发生错误该插件实例将被忽略，插件系统不会向获取数据。
* Description：插件自描述接口。
* Collect： MetricInput 最关键的接口，插件系统通过此接口从插件实例中获取数据。插件系统会周期性地调用此接口，将数据收集到传入 Collector 中。
```go
// MetricInput ...
type MetricInput interface {
	// Init called for init some system resources, like socket, mutex...
	// return call interval(ms) and error flag, if interval is 0, use default interval
	Init(Context) (int, error)

	// Description returns a one-sentence description on the Input
	Description() string

	// Collect takes in an accumulator and adds the metrics that the Input
	// gathers. This is called every "interval"
	Collect(Collector) error
}
```

### MetricExample详解

完整文件请参考[metric_example.go](https://github.com/alibaba/ilogtail/blob/main/plugins/input/example/metric_example.go)，这里仅说明其主体部分。
* 定义MetricExample结构体实现MetricInput接口。这个例子里，我们设计了一个五秒递增一次的计数器counter，这也是我们要采集的metric数据。
```go
type MetricsExample struct {
	counter      int
	gauge        int
	commonLabels helper.KeyValues
	labels       string
}
```

* Init方法会在运作前触发。在这个例子中，我们将counter的初始值设置为100。
  
```go
func (m *MetricsExample) Init(context ilogtail.Context) (int, error) {
    // 初始化
	m.counter = 100
	// 使用helper.KeyValues来存储metric标签
	m.commonLabels.Append("hostname", util.GetHostName())
	m.commonLabels.Append("ip", util.GetIPAddress())
	// 将commonLabels转换为字符串，以减少内存成本，因为标签是固定的值
	m.labels = m.commonLabels.String()
    // 返回0，使用默认的触发间隔。
	return 0, nil
}
```

* 设置插件说明。

```go
func (m *MetricsExample) Description() string {
	return "This is a metric input example plugin, this plugin would show how to write a simple metric input plugin."
}
```

* 每次触发都会调用Collect来收集指标值，并将其发送到收集器中。

```go
func (m *MetricsExample) Collect(collector ilogtail.Collector) error {
	m.counter++
	// 这里用一个随机值作为指标值。
	m.gauge = rand.Intn(100)

	// 收集metric数据。
	helper.AddMetric(collector, "example_counter", time.Now(), m.labels, float64(m.counter))
	helper.AddMetric(collector, "example_gauge", time.Now(), m.labels, float64(m.gauge))
	return nil
}
```

* 将该插件注册到MetricInputs数组中，MetricInputs插件的注册名（即json配置中的plugin_type）必须以"metric_"开头。

```go
func init() {
	ilogtail.MetricInputs["metric_input_example"] = func() ilogtail.MetricInput {
		return &MetricsExample{
			// 这里可以设置一个默认值。
		}
	}
}
```

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
```