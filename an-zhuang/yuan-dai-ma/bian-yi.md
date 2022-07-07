# 编译

## 编译前准备

安装docker

## 编译

ilogtail依赖了诸多第三方库（详见附录），为了简化编译流程ilogtail提供了预编译依赖的镜像辅助编译。

1.创建编译容器，并挂载代码和编译产出目录。

```bash
docker run --name ilogtail-build -d 、
  -v `pwd`:/src -v `pwd`/docker-core-build:/src/core/build \
  sls-registry.cn-beijing.cr.aliyuncs.com/sls-microservices/ilogtail-build-linux-amd64:latest \
  bash -c "sleep infinity"
```

2.进入容器

```bash
docker exec -it ilogtail-build bash3
```

3.在容器内编译

```bash
cd /src/core/build
cmake ..
make -sj${nproc}
```

需要编译UT的话，可以打开开关。替换上述第2行为

```bash
cmake -DBUILD_LOGTAIL_UT=ON ..
```

4.编译产出

编译产出在容器的`/src/core/build`目录下，即主机代码根目录的`docker-core-build`下。
