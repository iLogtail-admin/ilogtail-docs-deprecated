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
* 定义ServiceExample结构体实现ServiceInput接口。这个例子里，我们用一个http server接收数据，可以使用`curl --header "test:val123" http://127.0.0.1:19000/data`命令来进行测试
```go
type ServiceExample struct {
	Address string
	server  *http.Server
	context ilogtail.Context
}
```

* Init方法会在运作前触发。在这个插件的例子中，我们只存储了logstore的config context，并且返回0来使用默认的触发间隔。

  
```go
func (s *ServiceExample) Init(context ilogtail.Context) (int, error) {
	s.context = context
	return 0, nil
}
```

* 设置插件说明。

```go
func (s *ServiceExample) Description() string {
	return "This is a service input example plugin, the plugin would show how to write a simple service input plugin."
}
```

* ServiceInput插件是一个阻塞式的方法，它会在一个单独的协程中启动，适用于接收外部输入数据。在演示中，我们实现了一个http server来接受指定的请求头。

```go
func (s *ServiceExample) Start(collector ilogtail.Collector) error {
	logger.Info(s.context.GetRuntimeContext(), "start the example plugin")
	mux := http.NewServeMux()
	mux.HandleFunc("/data", func(writer http.ResponseWriter, request *http.Request) {
		val := request.Header.Get("test")
		if val != "" {
			collector.AddDataArray(nil, []string{"test"}, []string{val})
		}
	})
	s.server = &http.Server{
		Addr:        s.Address,
		Handler:     mux,
		ReadTimeout: 5 * time.Second,
	}
	return s.server.ListenAndServe()
}
```

* 当关闭插件时，会触发Stop方法，终止Start方法阻塞的协程。

```go
func (s *ServiceExample) Stop() error {
	logger.Info(s.context.GetRuntimeContext(), "close the example plugin")
	return s.server.Shutdown(context.Background())
}
```

* 将该插件注册到ServiceInputs数组中，ServiceInputs插件的注册名（即json配置中的plugin_type）必须以"service_"开头。

```go
func init() {
	ilogtail.ServiceInputs["service_input_example"] = func() ilogtail.ServiceInput {
		return &ServiceExample{
			// here you could set default value.
			Address: ":19000",
		}
	}
}
```

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