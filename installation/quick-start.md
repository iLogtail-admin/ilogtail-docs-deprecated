# 快速开始

## 采集主机日志

1\. 下载预编译的iLogtail包，解压后进入目录，该目录下文均称为部署目录。

```bash
wget https://ilogtail-community-edition.oss-cn-shanghai.aliyuncs.com/1.1.0/ilogtail-1.1.0.linux-amd64.tar.gz
tar -xzvf ilogtail-1.1.0.linux-amd64.tar.gz
cd ilogtail-1.1.0
```

2\. 对iLogtail进行配置

部署目录中`ilogtail_config.json`是iLogtail的系统参数配置文件。`user_yaml_config.d`是iLogtail的采集配置目录。

这里我们在采集配置目录中创建`file_simple.yaml`文件，配置采集当前目录simple.log文件并输出到标准输出：

```yaml
enable: true
inputs:
  - Type: file_log          # 文件输入类型
    LogPath: .              # 文件路径Glob匹配规则
    FilePattern: simple.log # 文件名Glob匹配规则
flushers:
  - Type: flusher_stdout    # 标准输出流输出类型
    OnlyStdout: true
```

您也可以直接从下面的地址下载示例配置。

```bash
wget https://raw.githubusercontent.com/alibaba/ilogtail/main/example_config/quick_start/user_yaml_config.d/file_simple.yaml
```

3\. 后台启动iLogtail

```bash
nohup ./ilogtail > stdout.log 2> stderr.log &
```

以上命令将标准输出重定向到stdout.log以便观察。

4\. 构造示例日志

```bash
echo 'Hello, iLogtail!' >> simple.log
```

5\. 查看采集到的文件日志

```bash
cat stdout.log
```
