# 快速开始

## 采集主机日志

1\. 下载预编译的iLogtail包，解压后进入目录

```bash
wget https://ilogtail-community-edition.oss-cn-shanghai.aliyuncs.com/1.1.0/ilogtail-1.1.0.linux-amd64.tar.gz
tar -xzvf ilogtail-1.1.0.linux-amd64.tar.gz
cd ilogtail-1.1.0
```

2\. 复制示例配置

```
cp example_config/quick_start/ilogtail_config.json .
cp -a example_config/quick_start/user_yaml_config.d/* user_yaml_config.d
```

`ilogtail_config.json`是iLogtail的系统参数配置文件。

`user_yaml_config.d`是iLogtail的采集配置文件目录。

示例`user_yaml_config.d/file_simple.yaml`配置了采集simple.log文件并输出到标准输出。

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
