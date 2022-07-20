# Table of contents

## 关于 <a href="#about" id="about"></a>

* [什么是iLogtail](README.md)
* [发展历史](about/brief-history.md)
* [产品优势](about/benefits.md)
* [开源协议](about/license.md)
* [社区版和企业版的对比说明](about/compare-editions.md)

## 安装 <a href="#installation" id="installation"></a>

* [快速开始](installation/quick-start.md)
* [Docker使用](installation/start-with-container.md)
* [Kubernetes使用](installation/start-with-k8s.md)
* [使用Supervised管理](installation/supervised.md)
* [发布记录](installation/release-notes.md)
* [支持的操作系统](installation/os.md)
* [源代码](installation/sources/README.md)
  * [下载](installation/sources/download.md)
  * [编译](installation/sources/build.md)
  * [Docker镜像](installation/sources/docker-image.md)
* [镜像站](installation/mirrors.md)

## 概念 <a href="#concepts" id="concepts"></a>

* [关键概念](concepts/key-concepts.md)
* [数据流水线](concepts/data-pipeline.md)

## 配置 <a href="#configuration" id="configuration"></a>

* [采集配置](configuration/collection-config.md)
* [系统参数](configuration/system-config.md)
* [日志](configuration/logging.md)

## 数据流水线 <a href="#data-pipeline" id="data-pipeline"></a>

* [概览](data-pipeline/overview.md)
* [输入](data-pipeline/input/README.md)
  * [文本日志](data-pipeline/input/file-log.md)
  * [容器标准输出](data-pipeline/input/input-docker-stdout.md)
* [处理](data-pipeline/processor/README.md)
  * [多行切分](data-pipeline/processor/split-log-regex.md)
  * [正则](data-pipeline/processor/regex.md)
  * [Json](data-pipeline/processor/json.md)
  * [分隔符](data-pipeline/processor/delimiter.md)
* [聚合](data-pipeline/aggregator.md)
* [输出](data-pipeline/flusher.md)
  * [标准输出/文件](data-pipeline/flusher/stdout.md)
  * [SLS](data-pipeline/flusher/sls.md)
  * [Kafka](data-pipeline/flusher/kafka.md)

## 工作原理 <a href="#principle" id="principle"></a>

* [文件发现](principle/file-discovery.md)

## 可观测性 <a href="#observability" id="observability"></a>

* [日志](observability/logs.md)

## 开发者指南 <a href="#developer-guide" id="developer-guide"></a>

* [CGO接口](developer-guide/cgo-interface.md)
* [插件编写指南](developer-guide/plugin-guide.md)
* [测试](developer-guide/test/README.md)
  * [单元测试](developer-guide/test/unit.md)
  * [E2E测试](developer-guide/test/e2e.md)

## 使用入门 <a href="#getting-started" id="getting-started"></a>

* [如何将业务日志采集到Kafka](getting-started/how-to-collect-to-kafka.md)
* [使用DaemonSet模式采集K8s容器日志](getting-started/k8s-daemonset-to-kafka.md)
* [主机环境采集业务日志到SLS](getting-started/hostlog-collect-to-sls.md)
* [K8s环境采集业务日志到SLS](getting-started/k8slog-collect-to-sls.md)
* [采集MySQL Binlog](getting-started/how-to-collect-binlog.md)