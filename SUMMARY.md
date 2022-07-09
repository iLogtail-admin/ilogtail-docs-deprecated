# Table of contents

## 关于

* [什么是iLogtail](README.md)
* [发展历史](about/brief-history.md)
* [开源协议](about/license.md)
* [产品优势](about/benefits.md)
* [社区版和企业版的对比说明](about/compare-editions.md)

## 安装 <a href="#installation" id="installation"></a>

* [快速开始](installation/quick-start.md)
* [容器使用](installation/start-with-container.md)
* [使用Supervised管理](installation/supervised.md)
* [发布记录](installation/release-notes.md)
* [支持的操作系统](installation/os.md)
* [源代码](installation/sources/README.md)
  * [下载](installation/sources/download.md)
  * [编译](installation/sources/build.md)
* [Docker](installation/docker.md)

## 概念

* [关键概念](gai-nian/guan-jian-gai-nian.md)
* [数据流水线](gai-nian/shu-ju-liu-shui-xian/README.md)
  * [输入](gai-nian/shu-ju-liu-shui-xian/shu-ru.md)
  * [处理](gai-nian/shu-ju-liu-shui-xian/chu-li.md)
  * [聚合](gai-nian/shu-ju-liu-shui-xian/ju-he.md)
  * [输出](gai-nian/shu-ju-liu-shui-xian/shu-chu.md)

## 配置 <a href="#configuration" id="configuration"></a>

* [采集配置](configuration/collection-config.md)
* [系统参数](configuration/system-config.md)
* [日志](configuration/logging.md)

## 数据流水线 <a href="#data-pipeline" id="data-pipeline"></a>

* [概览](data-pipeline/overview.md)
* [输入](data-pipeline/input/README.md)
  * [文本日志](data-pipeline/input/file\_log.md)
* [处理](data-pipeline/processor/README.md)
  * [多行切分](data-pipeline/processor/split\_log\_regex.md)
  * [正则](data-pipeline/processor/regex.md)
  * [Json](data-pipeline/processor/json.md)
  * [分隔符](data-pipeline/processor/delimiter.md)
* [聚合](data-pipeline/aggregator.md)
* [输出](data-pipeline/flusher.md)
  * [标准输出/文件](data-pipeline/flusher/stdout.md)
  * [SLS](data-pipeline/flusher/sls.md)
  * [Kafka](data-pipeline/flusher/kafka.md)

## 工作原理

* [文件发现](gong-zuo-yuan-li/wen-jian-fa-xian.md)

## 可观测性

* [日志](ke-guan-ce-xing/ri-zhi.md)

## 开发者指南

* [CGO接口](kai-fa-zhe-zhi-nan/cgo-jie-kou.md)
* [插件编写指南](kai-fa-zhe-zhi-nan/cha-jian-bian-xie-zhi-nan.md)
* [测试](kai-fa-zhe-zhi-nan/ce-shi/README.md)
  * [单元测试](kai-fa-zhe-zhi-nan/ce-shi/dan-yuan-ce-shi.md)
  * [E2E测试](kai-fa-zhe-zhi-nan/ce-shi/e2e-ce-shi.md)
