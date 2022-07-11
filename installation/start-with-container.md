# 容器使用

## 使用前提

已安装[docker](https://docs.docker.com/engine/install/)。

## 采集容器日志

1\. 下载预编译的iLogtail包，解压后进入目录

```bash
wget https://ilogtail-community-edition.oss-cn-shanghai.aliyuncs.com/1.1.0/ilogtail-1.1.0.linux-amd64.tar.gz
tar -xzvf ilogtail-1.1.0.linux-amd64.tar.gz
cd ilogtail-1.1.0
```

2\. 启动iLogtail容器，并挂载示例配置

```bash
docker run -d --name docker_ilogtail \
  -v /:/logtail_host:ro \
  -v /var/run:/var/run \
  -v /var/lib/docker_ilogtail/checkpoint:/usr/local/ilogtail/checkpoint \
  -v `pwd`/example_config/start_with_container/user_yaml_config.d:/usr/local/ilogtail/user_yaml_config.d \
  aliyun/ilogtail:latest
```

第2行将主机/目录挂载到iLogtail容器中，iLogtail依赖`logtail_host`路径采集容器日志。\
第3行将主机/var/run目录挂载到iLogtail容器中，iLogtail依赖/var/run目录与容器引擎通信。\
第4行将主机目录挂载到容器中iLogtail的checkpoint目录，使采集状态在容器重启时可恢复。\
第5行将示例配置挂载到iLogtail容器中。

`user_yaml_config.d/file_simple.yaml`配置了采集容器中的simple.log文件并输出到标准输出。\
`user_yaml_config.d/stdout_simple.yaml`配置了采集容器标准输出并输出到simple.stdout文件。

3\. 查看ilogtail\_docker容器自身标准输出日志

```bash
docker logs docker_ilogtail
```

4\. 进入iLogtail容器

```bash
docker exec -it docker_ilogtail bash
```

5\. 查看采集到的标准输出

```bash
cat /usr/local/ilogtail/simple.stdout
```

6\. 构造示例日志

```bash
echo 'Hello, iLogtail!' >> /root/simple.log
```

7\. 查看采集到的容器文件日志

```bash
docker logs docker_ilogtail
```
