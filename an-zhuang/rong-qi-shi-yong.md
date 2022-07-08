# 容器使用

## 使用前提

已安装docker

## 使用iLogtail采集容器日志

1\. 进入源代码根目录

2\. 启动iLogtail容器，并挂载示例配置

```bash
docker run -d --name docker_ilogtail \
  -v /:/logtail_host:ro \
  -v /var/run:/var/run \
  -v `pwd`/example_config/start_with_container/user_yaml_config.d:/usr/local/ilogtail/user_yaml_config.d \
  aliyun/ilogtail:latest
```

2\. 查看ilogtail\_docker容器自身标准输出日志

```
docker logs docker_ilogtail
```

3\. 进入iLogtail容器

```
docker exec -it docker_ilogtail bash
```

4\. 查看采集到的标准输出

```
cat /usr/local/ilogtail/simple.stdout
```

5\. 构造示例日志

```
echo 'Hello, iLogtail!' >> /root/simple.log
```

6\. 查看采集到的容器文件日志

```
docker logs docker_ilogtail
```
