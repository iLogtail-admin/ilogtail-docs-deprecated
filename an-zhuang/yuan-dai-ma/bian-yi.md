# 编译

## 编译前准备

下载源代码

安装docker

## C++核心编译

ilogtail依赖了诸多第三方库（详见附录），为了简化编译流程ilogtail提供了预编译依赖的镜像辅助编译。

1\. 进入源代码顶层目录

2\. 创建编译容器，并挂载代码目录。

```bash
docker run --name ilogtail-build -d
  -v `pwd`:/src -w /src \
  sls-registry.cn-beijing.cr.aliyuncs.com/sls-microservices/ilogtail-build-linux-amd64:latest \
  bash -c "sleep infinity"
```

3\. 进入容器

```bash
docker exec -it ilogtail-build bash
```

4\. 在容器内编译

```bash
mkdir -p /src/core/build
cd /src/core/build
cmake ..
make -sj${nproc}
```

需要编译UT的话，可以打开开关。替换上述第2行为

```bash
cmake -DBUILD_LOGTAIL_UT=ON ..
```

5\. 编译产出

编译产出在容器的`/src/core/build`目录下。

`/src/core/build`目录的结构如下

```
/src/core/build
├── ilogtail (主程序）
├── plugin (主程序）
│   ├── libPluginAdapter.so（插件接口）
│   └── ...
├── unittest (单元测试程序）
└── ...
```

## Golang插件编译

可以在镜像内继续编译Golang插件（即从上面的3开始）。

1\. 在容器内编译

```
cd /src
./scripts/plugin_build.sh vendor c-shared
```

2\. 编译产出

编译产出在容器的`/src/bin`目录下。

`/src/bin`目录的结构如下

```
/src/bin
├── libPluginBase.h
└── libPluginBase.so (插件lib）
```

## 组装构建结果

当C++核心和Golang插件都编译完成后，可以将C++核心的构建结果拷贝到`/src/bin`目录组装出完整的构建结果。

```
cp -a /src/core/build/ilogtail /src/bin
cp -a /src/core/build/plugin/libPluginAdapter.so /src/bin
```

`/src/bin`目录的结构如下

```
/src/bin
├── ilogtail (主程序）
├── libPluginAdapter.so（插件接口）
├── libPluginBase.h
└── libPluginBase.so (插件lib）
```

由于容器挂载了主机的源代码目录，因此源代码目录下的`bin`目录与之完全相同。
