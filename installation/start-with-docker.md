# Docker使用

## 使用前提

已安装[docker](https://docs.docker.com/engine/install/)

## 采集Docker容器日志

1\. 准备iLogtail配置目录

新建配置目录`user_yaml_config.d`目，在目录中创建`file_simple.yaml`和`stdout_simple.yaml`。

在`file_simple.yaml`中配置采集容器中的simple.log到标准输出。

```yaml
enable: true
inputs:
  - Type: file_log
    LogPath: /root
    FilePattern: simple.log
    DockerFile: true
flushers:
  - Type: flusher_stdout
    OnlyStdout: true
```

在`stdout_simple.yaml`中配置采集容器标准输出并输出到simple.stdout文件。

```yaml
enable: true
inputs:
  - Type: service_docker_stdout # 容器标准输出流输入类型
    Stderr: false               # 不采集标准错误流
    Stdout: true                # 采集标准输出流
flushers:
  - Type: flusher_stdout        # 标准输出流输出类型
    FileName: simple.stdout     # 重定向文件名
```

您也可以直接从下面的地址下载示例配置。

```bash
wget https://raw.githubusercontent.com/alibaba/ilogtail/main/example_config/start_with_docker/user_yaml_config.d/file_simple.yaml
wget https://raw.githubusercontent.com/alibaba/ilogtail/main/example_config/start_with_docker/user_yaml_config.d/stdout_simple.yaml
```

2\. 启动iLogtail容器，并挂载iLogtail配置目录

```bash
docker run -d --name docker_ilogtail \
  -v /:/logtail_host:ro \
  -v /var/run:/var/run \
  -v /var/lib/docker_ilogtail/checkpoint:/usr/local/ilogtail/checkpoint \
  -v `pwd`/user_yaml_config.d:/usr/local/ilogtail/user_yaml_config.d \
  sls-opensource-registry.cn-shanghai.cr.aliyuncs.com/ilogtail-community-edition/ilogtail:1.1.0
```

第1行-d参数表示后台启动iLogtail容器，--name指定容器名称以便引用。\
第2行将主机/目录挂载到iLogtail容器中，iLogtail依赖`logtail_host`路径采集容器日志。\
第3行将主机/var/run目录挂载到iLogtail容器中，iLogtail依赖/var/run目录与容器引擎通信。\
第4行将主机目录挂载到容器中iLogtail的checkpoint目录，使采集状态在容器重启时可恢复。\
第5行将配置目录挂载到iLogtail容器中。

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
