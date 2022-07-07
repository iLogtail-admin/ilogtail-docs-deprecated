# 日志

完整的iLogtail由`C++`开发的主程序及`Golang`开发的插件组成，因此iLogtail的运行日志也有两部分组成。

## iLogtail主程序日志

日志控制文件：`apsara_log_conf.json，`该文件`iLogtail`首次运行时会自动生成。日志级别分别为：`TRACE`、`DEBUG`、`INFO`、`WARNING`、`ERROR`、`FATAL`。



```
{
	"Loggers" :
	{
		"/" :
		{
			"AsyncFileSink" : "WARNING"
		},
		"/apsara/sls/ilogtail" :
		{
			"AsyncFileSink" : "INFO"
		},
		"/apsara/sls/ilogtail/profile" :
		{
			"AsyncFileSinkProfile" : "INFO"
		},
		"/apsara/sls/ilogtail/status" :
		{
			"AsyncFileSinkStatus" : "INFO"
		}
	},
	"Sinks" :
	{
		"AsyncFileSink" :
		{
			"Compress" : "Gzip",
			"LogFilePath" : "${ilogtail运行路径}/ilogtail.LOG",
			"MaxDaysFromModify" : 300,
			"MaxLogFileNum" : 10,
			"MaxLogFileSize" : 20000000,
			"Type" : "AsyncFile"
		},
		"AsyncFileSinkProfile" :
		{
			"Compress" : "",
			"LogFilePath" : "${ilogtail运行路径}/snapshot/ilogtail_profile.LOG",
			"MaxDaysFromModify" : 1,
			"MaxLogFileNum" : 61,
			"MaxLogFileSize" : 1,
			"Type" : "AsyncFile"
		},
		"AsyncFileSinkStatus" :
		{
			"Compress" : "",
			"LogFilePath" : "${ilogtail运行路径}/snapshot/ilogtail_status.LOG",
			"MaxDaysFromModify" : 1,
			"MaxLogFileNum" : 61,
			"MaxLogFileSize" : 1,
			"Type" : "AsyncFile"
		}
	}
}
```

## iLogtail插件日志

日志控制文件：`logtail_plugin.LOG`
