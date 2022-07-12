# 什么是iLogtail

![](<.gitbook/assets/ilogtail-icon.png>)

iLogtail 为可观测场景而生，拥有的轻量级、高性能、自动化配置等诸多生产级别特性，在阿里巴巴以及外部数万家阿里云客户内部广泛应用。你可以将它部署于物理机，虚拟机，Kubernetes等多种环境中来采集遥测数据，例如logs、traces和metrics。

[![GitHub stars](https://camo.githubusercontent.com/674a26318ece2d770231086a733bebdbb174c15721f03714f5b79930574a800a/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f73746172732f616c69626162612f696c6f677461696c)](https://github.com/alibaba/ilogtail/stargazers) [![GitHub issues](https://camo.githubusercontent.com/4266ec67b48f666bc0d440f9d1399e4b56ffc4eca3af3764e062731be83b2873/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6973737565732f616c69626162612f696c6f677461696c)](https://github.com/alibaba/ilogtail/issues) [![GitHub license](https://camo.githubusercontent.com/608afe55a7ca2ed062304f89208d3b929fddcbde8923cd09ef40edb2d2c3bf76/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6963656e73652f616c69626162612f696c6f677461696c)](https://github.com/alibaba/ilogtail/blob/main/LICENSE)

## 核心优势

* 支持多种Logs、Traces、Metrics数据采集，尤其对容器、Kubernetes环境支持非常友好
* 数据采集资源消耗极低，相比同类遥测数据采集的Agent性能好5-20倍
* 高稳定性，在阿里巴巴以及数万阿里云客户生产中使用验证，部署量近千万，每天采集数十PB可观测数据
* 支持插件化扩展，可任意扩充数据采集、处理、聚合、发送模块
* 支持配置远程管理，支持以图形化、SDK、K8s Operator等方式进行配置管理，可轻松管理百万台机器的数据采集
* 支持自监控、流量控制、资源控制、主动告警、采集统计等多种高级特性

## 功能

**iLogtail** 支持收集多种遥测数据并将其传输到多种不同的后端，例如 [SLS可观测平台](https://help.aliyun.com/product/28958.html) 。 支持采集的数据主要如下:

* Logs
  * 收集静态日志文件
  * 在容器化环境中运行时动态收集文件
  * 在容器化环境中运行时动态收集 Stdout
* Traces
  * OpenTelemetry 协议
  * Skywalking V2 协议
  * Skywalking V3 协议
  * ...
* Metrics
  * Node指标
  * Process指标
  * GPU 指标
  * Nginx 指标
  * 支持获取Prometheus指标
  * 支持收集Telegraf指标
  * ...

## 联系我们

您可以通过[Github Issues](https://github.com/alibaba/ilogtail/issues) 报告bug、提出建议或参与讨论，或通过以下方式联系我们：

* 交流群请扫描

![](.gitbook/assets/chatgroup.png)

* 微信公众号：日志服务
* 哔哩哔哩：[阿里云SLS](https://space.bilibili.com/630680534?from=search\&seid=2845737427240690794\&spm\_id\_from=333.337.0.0)
* 知乎：[阿里云日志服务](https://www.zhihu.com/people/a-li-yun-ri-zhi-fu-wu)
