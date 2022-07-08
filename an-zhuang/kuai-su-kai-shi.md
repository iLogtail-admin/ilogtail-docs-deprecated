# 快速开始

## 使用前提

## 采集主机日志

1\. 下载预编译的iLogtail包，解压，进入解压目录

2\. 使用示例配置

```
cp -a example_config/quick_start/* .
```

3\. 后台启动iLogtail

```
cd bin
nohup ./ilogtail > stdout.log 2> stderr.log &
```

4\. 构造示例日志

```
echo 'hello world!' >> simple.log
```

5\. 查看采集到的文件日志

```
cat stdout.log
```
