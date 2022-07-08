# Table of contents

## 关于

* [什么是iLogtail](README.md)
* [发展历史](guan-yu/fa-zhan-li-shi.md)
* [开源协议](guan-yu/kai-yuan-xie-yi.md)
* [产品优势](guan-yu/chan-pin-you-shi.md)
* [社区版和企业版的对比说明](guan-yu/she-qu-ban-he-qi-ye-ban-de-dui-bi-shuo-ming.md)

## 安装 <a href="#installation" id="installation"></a>

* [快速开始](an-zhuang/kuai-su-kai-shi.md)
* [容器使用](an-zhuang/rong-qi-shi-yong.md)
* [使用Supervised启动](an-zhuang/shi-yong-supervised-qi-dong.md)
* [发布记录](an-zhuang/fa-bu-ji-lu.md)
* [支持的操作系统](an-zhuang/zhi-chi-de-cao-zuo-xi-tong.md)
* [源代码](an-zhuang/yuan-dai-ma/README.md)
  * [下载](an-zhuang/yuan-dai-ma/xia-zai.md)
  * [编译](an-zhuang/yuan-dai-ma/bian-yi.md)
* [Docker](an-zhuang/docker.md)

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
