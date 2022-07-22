# ServiceInput插件示例

## 简介
`service_example` 插件是ServiceInput样例插件，用于介绍讲解如何编写ServiceInput插件。

## 配置参数
该插件不需要配置参数。

## ServiceInput插件开发说明
### ServiceInput接口说明
* Init：插件初始化接口，主要供插件做一些参数检查，并为其提供上下文对象 Context。 返回值的第一个参数表示调用周期（毫秒），插件系统会以该值作为数据获取周期。如果返回 0 的话，插件系统会使用全局的数据获取周期。 返回值的第二个参数表示初始化中发生的错误，一旦发生错误该插件实例将被忽略，插件系统不会向获取数据。但是 Init 的第一个返回值对于 ServiceInput 没有意义，因为它不会被周期性调用。
* Description：插件自描述接口。
* Start：由于 ServiceInput 的定位是常驻型输入，所以插件系统为此类型的插件实例都创建了独立的 goroutine，在 goroutine 中调用此接口来开始数据收集。Collector 的作用依旧是充当插件实例和插件系统之间的数据管道。
* Stop：提供终止插件的能力。插件必须正确地实现此接口，以避免 hang 住插件系统导致 Logtail 也无法正确退出。

```go
// ServiceInput ...
type ServiceInput interface {
	// Init called for init some system resources, like socket, mutex...
	// return interval(ms) and error flag, if interval is 0, use default interval
	Init(Context) (int, error)

	// Description returns a one-sentence description on the Input
	Description() string

	// Start starts the ServiceInput's service, whatever that may be
	Start(Collector) error

	// Stop stops the services and closes any necessary channels and connections
	Stop() error
}
```

### ServiceExample详解

完整文件请参考[service_example.go](https://github.com/alibaba/ilogtail/blob/main/plugins/input/example/service_example.go)，这里仅说明其主体部分。
* 定义ServiceExample结构体实现ServiceInput接口。这个例子里，我们设计了一个五秒递增一次的计数器counter，这也是我们要采集的metric数据。
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