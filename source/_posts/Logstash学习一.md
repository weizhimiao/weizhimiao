---
title: Logstash学习一
date: 2016-10-24 20:30:00
tags:
- Logstash
categories:
- Logstash
---

- Logstash简介
- Logstash入门

<!-- more -->


## Logstash简介

Logstash是具有实时流水线功能的开源数据收集引擎。 Logstash可以动态统一来自不同来源的数据，并将数据标准化为您选择的目的地。清理和民主化您的所有数据，用于各种高级下游分析和可视化用例。

尽管Logstash最初推动了日志收集的创新，但其功能远远超出了用例。任何类型的事件都可以用丰富的输入，过滤器和输出插件进行丰富和转换，其中许多本地编解码器进一步简化了摄取过程。 Logstash通过利用更大量和各种数据来加速您的洞察力。

### Logstashedit的特点

#### 摄取的主力为Elasticsearch和更多

具有强大的Elasticsearch和Kibana协同作用的水平可扩展的数据处理渠道



![img](http://n.sinaimg.cn/games/3ece443e/20161024/logstash.png)


#### 可插拔管线架构

混合，匹配和协调不同的输入，滤波器和输出以在管道和谐中播放

#### 社区可扩展和开发人员友好的插件生态系统

超过200个插件可用，加上创建和贡献自己的灵活性

### Logstash喜欢数据
收集更多，所以你可以知道更多。 Logstash欢迎各种形状和大小的数据。

### 日志和度量
这一切都开始了。

- 处理所有类型的日志数据
  - 轻松获取大量Web日志（如Apache）和应用程序日志（如log4j for Java）
  - 捕获许多其他日志格式，如syslog，Windows事件日志，网络和防火墙日志等
- 通过Filebeat获得补充的安全日志转发功能
- 通过TCP和UDP从Ganglia，collectd，NetFlow，JMX和许多其他基础架构和应用程序平台收集指标


### 网络
解锁万维网。

- 将HTTP请求转换为事件（博客）
  - 从web服务firehoses像Twitter的社会情绪分析
  - Webhook支持GitHub，HipChat，JIRA和无数其他应用程序
  - 启用许多Watcher警报用例
- 通过按需轮询HTTP端点来创建事件（博客）
  - 通常从Web应用程序接口捕获运行状况，性能，指标和其他类型的数据
  - 非常适合于轮询控制优于接收的情况

### 数据存储和流
从您已拥有的数据中发掘更多价值。

- 更好地了解您的数据从任何关系数据库或NoSQL存储与JDBC接口（博客）
- 统一来自消息队列的各种数据流，如Apache Kafka（博客），RabbitMQ，Amazon SQS和ZeroMQ

### 传感器和物联网
探索广泛的其他数据。

- 在这个技术进步的时代，大规模的IoT世界通过捕获和利用来自连接的传感器的数据来释放无尽的用例。
- Logstash是用于从移动设备向智能家庭，连接的车辆，医疗保健传感器以及许多其他行业特定应用程序发送数据的常见事件收集骨干网。
- 观看Logstash，结合更广泛的ELK堆栈，集中和丰富传感器数据，以获得有关住宅的更深入的知识。


### 轻松地丰富一切
数据越好，知识越好。 在提取期间清理并转换数据，以便在索引或输出时立即获取近实时的洞察信息。 Logstash包含许多聚合和突变以及模式匹配，地理位置映射和动态查找功能。

- Grok是Logstash过滤器的面包和黄油，并且无处不在地从非结构化数据中导出结构。 享受丰富的集成模式，旨在帮助快速解决网络，系统，网络和其他类型的事件格式。
- 通过从IP地址解密地理坐标，规范日期复杂性，简化键值对和CSV数据，隐藏敏感信息，以及使用本地查找或Elasticsearch查询进一步丰富您的数据，扩展您的视野。
- 编解码器通常用于简化JSON和多线事件等常见事件结构的处理。

### 选择您的stash
将数据路由到最重要的位置。 通过存储，分析和对您的数据采取行动，解锁各种下游分析和操作用例。


分析
- Elasticsearch
- 数据存储如MongoDB和Riak

存档
- HDFS
- S3
- Google云端存储

监控
- Nagios
- Ganglia
- Zabbix
- Graphite
- Datadog
- CloudWatch

警报
- Watcher with Elasticsearch
- Email
- Pagerduty
- HipChat
- IRC
- SNS


## Logstash入门

本节将指导您完成安装Logstash并验证一切正常运行的过程。 后面的章节讨论越来越复杂的配置，以解决选定的用例。 本节包括以下主题：

- 安装Logstash
- 保存您的第一个事件：基本Logstash示例
- 使用Logstash解析日志
- 停机检测
- Logstash处理管道

### 安装Logstash
> 注意: Logstash需要Java 7或更高版本。 使用官方Oracle发行版或开源发行版（如OpenJDK）。

要检查Java版本，请运行以下命令：
```
java -version
```
在安装了Java的系统上，此命令将生成类似于以下内容的输出：
```
java version "1.7.0_45"
Java(TM) SE Runtime Environment (build 1.7.0_45-b18)
Java HotSpot(TM) 64-Bit Server VM (build 24.45-b08, mixed mode)
```
#### 从下载的二进制文件安装
下载与您的主机环境匹配的Logstash安装文件。 解压缩文件。 不要将Logstash安装到包含冒号（:)字符的目录路径中。

在支持的Linux操作系统上，可以使用软件包管理器安装Logstash。

#### 从软件包存储库安装
我们还有可用于基于APT和YUM的发行版的存储库。 注意，我们只提供二进制包，但没有源包，因为这些包是作为Logstash构建的一部分创建的。

我们已将Logstash软件包存储库按版本拆分为单独的网址，以避免在主要版本或次要版本之间意外升级。 对于所有2.4.x版本使用2.4版本号，2.3.x使用2.3，等等。

我们使用PGP密钥D88E42B4，Elastic的签名密钥，用指纹
```
4609 5ACC 8548 582C 1A26 99A9 D27D 666C D88E 42B4
```
签署我们的所有包。 它可从https://pgp.mit.edu获得。

#### APT
下载并安装公共签名密钥：
```
wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```

将存储库定义添加到/etc/apt/sources.list文件中：
```
echo "deb https://packages.elastic.co/logstash/2.4/debian stable main" | sudo tee -a /etc/apt/sources.list
```
> 使用上述echo方法添加Logstash存储库。 不要使用add-apt-repository，因为它将添加一个deb-src条目，但我们不提供源包。 如果您已添加deb-src条目，您将看到类似如下的错误：
> `Unable to find expected entry 'main/source/Sources' in Release file (Wrong sources.list entry or malformed file)`
> 只需从/etc/apt/sources.list文件中删除deb-src条目，然后在按照正常程序进行安装。

运行sudo apt-get update并且存储库已准备就绪可以使用。 您可以安装：
```
sudo apt-get update && sudo apt-get install logstash
```

#### YUM
下载并安装公共签名密钥：
```
rpm --import https://packages.elastic.co/GPG-KEY-elasticsearch
```
将以下内容添加到具有.repo后缀的文件中的/etc/yum.repos.d/目录中，例如logstash.repo
```
[logstash-2.4]
name=Logstash repository for 2.4.x packages
baseurl=https://packages.elastic.co/logstash/2.4/centos
gpgcheck=1
gpgkey=https://packages.elastic.co/GPG-KEY-elasticsearch
enabled=1
```
您的存储库已准备就绪。 您可以安装：
```
yum install logstash
```

### 基本Logstash示例
要测试Logstash安装，运行最基本的Logstash管道：
```
cd logstash-2.4.0
bin/logstash -e 'input { stdin { } } output { stdout {} }'
```
-e标志使您能够直接从命令行指定配置。 在命令行中指定配置允许您快速测试配置，而无需在迭代之间编辑文件。 此管道从标准输入stdin接收输入，并以结构化格式将输入移动到标准输出stdout。

一旦显示“Pipeline main started”，在命令提示符下键入hello world以查看Logstash响应：
```
hello world
2013-11-21T01:22:14.405+0000 0.0.0.0 hello world
```

Logstash向消息添加时间戳和IP地址信息。 通过在Logstash运行的shell中发出CTRL-D命令，退出Logstash。

您已创建并运行基本的Logstash管道。 接下来，您将学习如何创建更加逼真的管道。

### 使用Logstash解析日志

在大多数使用情况下，Logstash管道具有一个或多个输入，过滤器和输出插件。 本节中的场景构建Logstash配置文件以指定这些插件，并讨论每个插件正在做什么。

Logstash配置文件定义了您的Logstash管道。 当您启动Logstash实例时，请使用 -f <path / to / file>选项指定定义该实例的管道的配置文件。

Logstash管道有两个必需的元素，输入和输出，以及一个可选元素，过滤器。 输入插件从源消耗数据，过滤器插件根据您指定的内容修改数据，输出插件将数据写入目标。

![img](http://n.sinaimg.cn/games/3ece443e/20161024/basic_logstash_pipeline.png)

在本节中，您将创建一个Logstash管道，它将Apache Web日志作为输入，解析这些日志以从日志中创建特定的命名字段，并将解析的数据写入Elasticsearch集群。 而不是在命令行定义管道配置，您将在配置文件中定义管道。

以下文本表示配置管道的骨架：
```
# The # character at the beginning of a line indicates a comment. Use
# comments to describe your configuration.
input {
}
# The filter part of this file is commented out to indicate that it is
# optional.
# filter {
#
# }
output {
}
```
此框架不起作用，因为输入和输出节没有定义任何有效选项。

要开始，请将骨架配置管道复制并粘贴到 Logstash home目录中名为first-pipeline.conf的文件中。 然后转到此处下载此示例中使用的示例数据集。 解压缩文件。

为文件输入配置Logstash
> 为了方便起见，本示例使用文件输入插件。 要在现实世界中拖拽文件，您将使用Filebeat将日志事件发送到Logstash。 您以后在构建更复杂的管道时学习如何配置Filebeat输入插件。

要开始Logstash管道，请将Logstash实例配置为通过使用文件输入插件从文件读取。

编辑first-pipeline.conf文件，并将整个输入节替换为以下文本：
```
input {
    file {
        path => "/path/to/file/*.log"
        start_position => beginning
        ignore_older => 0
    }
}
```

- 文件输入插件的默认行为是以类似于UNIX tail -f命令的方式监视文件的新信息。 要更改此默认行为并处理整个文件，我们需要指定Logstash开始处理文件的位置。

- 将ignore_older设置为0会禁用文件年龄检查，因此即使教程文件的时间已超过一天，也会对其进行处理。

将/ path / to / file替换为文件系统中logstash-tutorial.log所在位置的绝对路径。

#### 使用Grok Filter插件解析Web日志
grok过滤器插件是Logstash中默认提供的几个插件之一。 有关如何管理Logstash插件的详细信息，请参阅插件管理器的参考文档。

grok过滤器插件使您能够将非结构化日志数据解析为结构化和可查询的数据。

因为grok过滤器插件在传入日志数据中查找模式，配置需要您决定如何识别您的用例感兴趣的模式。 来自Web服务器日志示例的代表行如下所示：
```
83.149.9.216 - - [04/Jan/2015:05:13:42 +0000] "GET /presentations/logstash-monitorama-2013/images/kibana-search.png
HTTP/1.1" 200 203023 "http://semicomplete.com/presentations/logstash-monitorama-2013/" "Mozilla/5.0 (Macintosh; Intel
Mac OS X 10_9_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1700.77 Safari/537.36"
```

行开头的IP地址很容易识别，括号中的时间戳也很容易识别。 要解析数据，可以使用％{COMBINEDAPACHELOG} grok模式，该模式使用以下模式构建Apache日志中的行：

含义|字段
---|--------
IP地址|clientip
用户ID|ident
用户认证|auth
时间戳|timestamp
HTTP动词|verb
请求正文|request
HTTP版本|httpversion
HTTP状态码|response
字节数|bytes
Referrer URL|referrer
User agent|agent

编辑first-pipeline.conf文件，并用以下文本替换整个过滤器部分：
```
filter {
    grok {
        match => { "message" => "%{COMBINEDAPACHELOG}"}
    }
}
```
使用grok模式处理日志文件后，示例行将具有以下JSON表示形式：
```
{
"clientip" : "83.149.9.216",
"ident" : ,
"auth" : ,
"timestamp" : "04/Jan/2015:05:13:42 +0000",
"verb" : "GET",
"request" : "/presentations/logstash-monitorama-2013/images/kibana-search.png",
"httpversion" : "HTTP/1.1",
"response" : "200",
"bytes" : "203023",
"referrer" : "http://semicomplete.com/presentations/logstash-monitorama-2013/",
"agent" : "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1700.77 Safari/537.36"
}
```

#### 使用Geoip过滤插件增强您的数据
除了解析日志数据以获得更好的搜索外，过滤器插件还可以从现有数据中导出补充信息。 作为示例，geoip插件查找IP地址，从地址导出地理位置信息，并将该位置信息添加到日志。

通过将以下行添加到first-pipeline.conf文件的过滤器部分，将您的Logstash实例配置为使用geoip过滤器插件：

```
geoip {
    source => "clientip"
}
```
geoip插件配置要求您指定包含要查找的IP地址的源字段的名称。 在此示例中，clientip字段包含IP地址。

由于过滤器是按顺序评估的，请确保geoip部分位于配置文件的grok部分之后，并且grok和geoip部分嵌套在过滤器部分中，如下所示：
```
filter {
    grok {
        match => { "message" => "%{COMBINEDAPACHELOG}"}
    }
    geoip {
        source => "clientip"
    }
}
```
#### 将数据索引到Elasticsearch
现在，Web日志被细分为特定的字段，Logstash管道可以将数据索引到Elasticsearch集群中。 编辑first-pipeline.conf文件，并将整个输出部分替换为以下文本：
```
output {
    elasticsearch {
        hosts => [ "localhost:9200" ]
    }
}
```
使用此配置，Logstash使用http协议连接到Elasticsearch。 上面的例子假设Logstash和Elasticsearch在同一个实例上运行。 您可以通过使用hosts配置指定类似hosts => [“es-machine：9092”]的内容来指定远程Elasticsearch实例。

#### 测试您的初始流水线
此时，您的第一个pipeline.conf文件具有正确配置的输入，过滤器和输出节，并且如下所示：
```
input {
    file {
        path => "/Users/myusername/tutorialdata/*.log"
        start_position => beginning
        ignore_older => 0
    }
}
filter {
    grok {
        match => { "message" => "%{COMBINEDAPACHELOG}"}
    }
    geoip {
        source => "clientip"
    }
}
output {
    elasticsearch {
        hosts => [ "localhost:9200" ]
    }
}
```
要验证您的配置，请运行以下命令：
```
bin/logstash -f first-pipeline.conf --configtest
```
--configtest选项解析您的配置文件并报告任何错误。 当配置文件通过配置测试时，使用以下命令启动Logstash：
```
bin/logstash -f first-pipeline.conf
```
基于grok过滤器插件创建的字段，尝试对Elasticsearch进行测试查询：
```
curl -XGET 'localhost:9200/logstash-$DATE/_search?pretty&q=response=200'
```
将$ DATE替换为当前日期，格式为YYYY.MM.DD。

我们得到了多次点击。 例如：
```
{
  "took" : 4,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 98,
    "max_score" : 5.0091305,
    "hits" : [ {
      "_index" : "logstash-2016.08.30",
      "_type" : "logs",
      "_id" : "AVbd1HyuICXLyJ--dz7g",
      "_score" : 5.0091305,
      "_source" : {
        "message" : "83.149.9.216 - - [04/Jan/2015:05:13:45 +0000] \"GET /presentations/logstash-monitorama-2013/images/frontend-response-codes.png HTTP/1.1\" 200 52878 \"http://semicomplete.com/presentations/logstash-monitorama-2013/\" \"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1700.77 Safari/537.36\"",
        "@version" : "1",
        "@timestamp" : "2016-08-30T23:41:45.044Z",
        "path" : "/Users/myusername/tutorialdata/logstash-tutorial.log",
        "host" : "My-Macbook.local",
        "clientip" : "83.149.9.216",
        "ident" : "-",
        "auth" : "-",
        "timestamp" : "04/Jan/2015:05:13:45 +0000",
        "verb" : "GET",
        "request" : "/presentations/logstash-monitorama-2013/images/frontend-response-codes.png",
        "httpversion" : "1.1",
        "response" : "200",
        "bytes" : "52878",
        "referrer" : "\"http://semicomplete.com/presentations/logstash-monitorama-2013/\"",
        "agent" : "\"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1700.77 Safari/537.36\"",
        "geoip" : {
          "ip" : "83.149.9.216",
          "country_code2" : "RU",
          "country_code3" : "RUS",
          "country_name" : "Russian Federation",
          "continent_code" : "EU",
          "region_name" : "48",
          "city_name" : "Moscow",
          "latitude" : 55.75219999999999,
          "longitude" : 37.6156,
          "timezone" : "Europe/Moscow",
          "real_region_name" : "Moscow City",
          "location" : [ 37.6156, 55.75219999999999 ]
        }
      }
    },
    ...
```
尝试再次搜索从IP地址导出的地理位置信息：
```
curl -XGET 'localhost:9200/logstash-$DATE/_search?pretty&q=geoip.city_name=Buffalo'
```
将$ DATE替换为当前日期，格式为YYYY.MM.DD。

其中一个日志条目来自Buffalo，因此查询产生以下响应：
```
{
  "took" : 6,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 1,
    "max_score" : 1.0149983,
    "hits" : [ {
      "_index" : "logstash-2016.08.30",
      "_type" : "logs",
      "_id" : "AVbd1HyuICXLyJ--dz8u",
      "_score" : 1.0149983,
      "_source" : {
        "message" : "108.174.55.234 - - [04/Jan/2015:05:27:45 +0000] \"GET /?flav=rss20 HTTP/1.1\" 200 29941 \"-\" \"-\"",
        "@version" : "1",
        "@timestamp" : "2016-08-30T23:41:45.066Z",
        "path" : "/Users/myusername/tutorialdata/logstash-tutorial.log",
        "host" : "My-Macbook",
        "clientip" : "108.174.55.234",
        "ident" : "-",
        "auth" : "-",
        "timestamp" : "04/Jan/2015:05:27:45 +0000",
        "verb" : "GET",
        "request" : "/?flav=rss20",
        "httpversion" : "1.1",
        "response" : "200",
        "bytes" : "29941",
        "referrer" : "\"-\"",
        "agent" : "\"-\"",
        "geoip" : {
          "ip" : "108.174.55.234",
          "country_code2" : "US",
          "country_code3" : "USA",
          "country_name" : "United States",
          "continent_code" : "NA",
          "region_name" : "NY",
          "city_name" : "Buffalo",
          "postal_code" : "14221",
          "latitude" : 42.9864,
          "longitude" : -78.7279,
          "dma_code" : 514,
          "area_code" : 716,
          "timezone" : "America/New_York",
          "real_region_name" : "New York",
          "location" : [ -78.7279, 42.9864 ]
        }
      }
    } ]
  }
}
```

#### 多个输入和输出插件
您需要管理的信息通常来自多个不同的来源，用例可能需要多个目的地的数据。 您的Logstash管道可以使用多个输入和输出插件来处理这些要求。

在本节中，您将创建一个Logstash管道，它从Twitter feed和Filebeat客户端接收输入，然后将信息发送到Elasticsearch集群以及将信息直接写入文件。

#### 从Twitter feed阅读
要添加Twitter Feed，请使用twitter输入插件。 要配置插件，您需要几个信息：

- 消费者密钥，用于唯一标识您的Twitter应用。
- 消费者秘密，作为您的Twitter应用程序的密码。
- 在传入Feed中搜索的一个或多个关键字。
- oauth令牌，它使用此应用程序标识Twitter帐户。
- oauth令牌密钥，用作Twitter帐户的密码。

访问https://dev.twitter.com/apps以设置Twitter帐户，并生成您的用户密钥和密钥，以及您的访问令牌和密钥。 如果您不确定如何生成这些键，请参阅twitter输入插件的文档。

就像你以前在使用Logstash进行解析日志时一样，创建一个包含配置管道骨架的配置文件（称为second-pipeline.conf）。 如果需要，您可以重复使用之前创建的文件，但确保在运行Logstash时传递正确的配置文件名。

将以下行添加到second-pipeline.conf文件的输入部分，将您的值替换为如下所示的占位符值：
```
twitter {
    consumer_key => "enter_your_consumer_key_here"
    consumer_secret => "enter_your_secret_here"
    keywords => ["cloud"]
    oauth_token => "enter_your_access_token_here"
    oauth_token_secret => "enter_your_access_token_secret_here"
}
```

#### Filebeat客户端
Filebeat客户端是一个轻量级的，资源友好的工具，从服务器上的文件收集日志，并将这些日志转发到Logstash实例进行处理。 Filebeat设计用于可靠性和低延迟。 Filebeat使用托管源数据的计算机资源，Beats输入插件可最大限度地减少对Logstash实例的资源需求。

> 注意:在典型的使用情况下，Filebeat在运行Logstash实例的机器的单独机器上运行。为了本教程的目的，Logstash和Filebeat在同一台机器上运行。

默认的Logstash安装包括Beats输入插件。要在数据源计算机上安装Filebeat，请从Filebeat产品页面下载相应的软件包。

安装Filebeat后，您需要配置它。打开位于Filebeat安装目录中的filebeat.yml文件，并使用以下行替换内容。确保路径指向您的syslog：
```
filebeat:
  prospectors:
    -
      paths:
        - /var/log/*.log
      fields:
        type: syslog
output:
  logstash:
    hosts: ["localhost:5043"]
```
- Filebeat处理的文件的绝对路径。

- 在事件中添加一个名为syslog的名为type的字段。

保存更改。

为了保持配置简单，您不会像在真实场景中那样指定TLS / SSL设置。

通过将以下行添加到second-pipeline.conf文件的输入部分，将Logstash实例配置为使用Filebeat输入插件：
```
beats {
    port => "5043"
}
```
#### 将LogStash数据写入文件
您可以配置Logstash管道，使用文件输出插件将数据直接写入文件。

通过将以下行添加到second-pipeline.conf文件的输出部分，将Logstash实例配置为使用文件输出插件：
```
file {
    path => /path/to/target/file
}
```

#### 写入多个Elasticsearch节点
写入多个Elasticsearch节点可减轻给定Elasticsearch节点上的资源需求，以及在特定节点不可用时向集群提供冗余入口点。

要将Logstash实例配置为写入多个Elasticsearch节点，请编辑second-pipeline.conf文件的输出部分，以读取：
```
output {
    elasticsearch {
        hosts => ["IP Address 1:port1", "IP Address 2:port2", "IP Address 3"]
    }
}

```
在主机行中使用Elasticsearch集群中的三个非主节点的IP地址。 当hosts参数列出多个IP地址时，Logstash会跨地址列表对请求进行负载平衡。 另请注意，Elasticsearch的默认端口为9200，在上述配置中可以省略。

#### 测试管道
此时，您的second-pipeline.conf文件如下所示：

```
input {
    twitter {
        consumer_key => "enter_your_consumer_key_here"
        consumer_secret => "enter_your_secret_here"
        keywords => ["cloud"]
        oauth_token => "enter_your_access_token_here"
        oauth_token_secret => "enter_your_access_token_secret_here"
    }
    beats {
        port => "5043"
    }
}
output {
    elasticsearch {
        hosts => ["IP Address 1:port1", "IP Address 2:port2", "IP Address 3"]
    }
    file {
        path => "/path/to/target/file"
    }
}
```
Logstash正在使用您配置的Twitter源中的数据，从Filebeat接收数据，并将此信息索引到Elasticsearch集群中的三个节点以及写入文件。

在数据源计算机上，使用以下命令运行Filebeat：
```
sudo ./filebeat -e -c filebeat.yml -d "publish"
```
Filebeat将尝试在端口5403上连接。直到Logstash以活动的Beats插件启动，该端口将不会有任何答案，因此，您看到的有关无法在该端口上连接的任何消息是正常的。

要验证您的配置，请运行以下命令：
```
bin/logstash -f second-pipeline.conf --configtest
```
--configtest选项解析您的配置文件并报告任何错误。 当配置文件通过配置测试时，使用以下命令启动Logstash：
```
bin/logstash -f second-pipeline.conf
```
使用grep实用程序在目标文件中搜索以验证信息是否存在：
```
grep syslog /path/to/target/file
```
运行Elasticsearch查询以在Elasticsearch集群中查找相同的信息：
```
curl -XGET 'localhost:9200/logstash-$DATE/_search?pretty&q=fields.type:syslog'
```
将$ DATE替换为当前日期，格式为YYYY.MM.DD。

要查看Twitter Feed中的数据，请尝试以下查询：
```
curl -XGET 'http://localhost:9200/logstash-$DATE/_search?pretty&q=client:iphone'
```
同样，请记住用YYYY.MM.DD格式的当前日期替换$ DATE。

### 停机检测
关闭正在运行的Logstash实例涉及以下步骤：

- 停止所有输入，过滤器和输出插件
- 处理所有飞行中事件
- 终止Logstash进程

以下条件影响关闭过程：
- 输入插件以缓慢的速度接收数据。
- 慢速过滤器，如执行sleep（10000）的Ruby过滤器或执行非常繁重的查询的Elasticsearch过滤器。
- 正在等待重新连接以清除飞行中事件的已断开连接的输出插件。

这些情况使关闭过程的持续时间和成功不可预测。

Logstash有一个停止检测机制，它在关闭期间分析管道和插件的行为。 此机制生成有关内部队列中飞行事件计数的周期性信息和繁忙的工作线程列表。

要在停止关闭的情况下启用Logstash强制终止，请在启动Logstash时使用--allow-unsafe-shutdown标志。


#### 失速检测实例
在此示例中，慢速过滤器执行阻止管道干净关闭。 通过使用--allow-unsafe-shutdown标志启动Logstash，使用Ctrl + C退出会导致最终关闭，导致事件丢失。
```
bin/logstash -e 'input { generator { } } filter { ruby { code => "sleep 10000" } }
  output { stdout { codec => dots } }' -w 1 --allow-unsafe-shutdown
Settings: User set pipeline workers: 1, Default pipeline workers: 8
Pipeline main started
^CSIGINT received. Shutting down the agent. {:level=>:warn}
stopping pipeline {:id=>"main"}
Received shutdown signal, but pipeline is still waiting for in-flight events
to be processed. Sending another ^C will force quit Logstash, but this may cause
data loss. {:level=>:warn}
{"inflight_count"=>125, "stalling_thread_info"=>{["LogStash::Filters::Ruby",
{"code"=>"sleep 10000"}]=>[{"thread_id"=>17, "name"=>"[main]>worker0",
"current_call"=>"(ruby filter code):1:in `sleep'"}]}} {:level=>:warn}
The shutdown process appears to be stalled due to busy or blocked plugins.
Check the logs for more information. {:level=>:error}
{"inflight_count"=>125, "stalling_thread_info"=>{["LogStash::Filters::Ruby",
{"code"=>"sleep 10000"}]=>[{"thread_id"=>17, "name"=>"[main]>worker0",
"current_call"=>"(ruby filter code):1:in `sleep'"}]}} {:level=>:warn}
{"inflight_count"=>125, "stalling_thread_info"=>{["LogStash::Filters::Ruby",
{"code"=>"sleep 10000"}]=>[{"thread_id"=>17, "name"=>"[main]>worker0",
"current_call"=>"(ruby filter code):1:in `sleep'"}]}} {:level=>:warn}
Forcefully quitting logstash.. {:level=>:fatal}
```
当--allow-unsafe-shutdown未启用时，Logstash会继续运行并定期生成这些报告。

### Logstash处理管道

Logstash事件处理管道有三个阶段：输入→过滤器→输出。 输入生成事件，过滤器修改它们，并将输出发送到其他地方。 输入和输出支持编解码器，使您能够在数据进入或退出流水线时对其进行编码或解码，而无需使用单独的过滤器。

#### input
使用输入将数据导入Logstash。 一些更常用的输入是：

- file：从文件系统上的文件读取，很像UNIX命令尾-0F
- syslog：在公知的端口514上侦听syslog消息并根据RFC3164格式解析
- redis：从redis服务器读取，使用redis通道和redis列表。 Redis通常在集中式Logstash安装中用作“代理”，它会从远程Logstash“shippers”对Logstash事件进行排队。
- beats：处理Filebeat发送的事件。

有关可用输入的更多信息，请参阅input插件。

#### 过滤器
过滤器是Logstash管道中的中间处理设备。 您可以将过滤器与条件组合，以便在事件满足特定条件时对其执行操作。 一些有用的过滤器包括：

- grok：解析和结构任意文本。 Grok是目前Logstash将非结构化日志数据解析为结构化和可查询的最佳方式。 对于Logstash内置的120个模式，它更有可能找到一个满足您的需求！
- mutate：对事件字段执行常规转换。 您可以重命名，删除，替换和修改事件中的字段。
- drop：完全删除事件，例如，调试事件。
- clone：创建事件的副本，可能添加或删除字段。
- geoip：添加IP地址的地理位置信息（也显示在Kibana惊人的图表！）

有关可用过滤器的详细信息，请参阅过滤器插件。

#### Output
输出是Logstash管道的最后一个阶段。 事件可以传递多个输出，但是一旦所有输出处理完成，事件就完成了它的执行。 一些常用的输出包括：

- elasticsearch：将事件数据发送到Elasticsearch。 如果您打算以高效，方便，易于查询的格式保存您的数据... Elasticsearch是要走的路。 期。 是的，我们有偏见:)
- file：将事件数据写到磁盘上的文件。
- graphite：将事件数据发送到graphite，graphite是一种流行的开源工具，用于存储和绘制指标。 http://graphite.readthedocs.io/en/latest/
- statsd：将事件数据发送到statsd，该服务“监听通过UDP发送的统计信息（如计数器和计时器），并将聚合发送到一个或多个可插拔后端服务”。 如果你已经使用statsd，这可能对你有用！

有关可用输出的详细信息，请参阅Output插件。

#### 编解码器
编解码器基本上是可以作为输入或输出的一部分进行操作的流过滤器。 编解码器使您能够轻松地将消息的传输与序列化过程分离。 流行的编解码器包括json，msgpack和plain（text）。

- json：以JSON格式编码或解码数据。
- multiline：将多行文本事件（如java异常和stacktrace消息）合并为单个事件。

有关可用编解码器的详细信息，请参阅编解码器插件。

#### 容错
Logstash在处理期间将所有事件保留在主存储器中。 Logstash通过尝试暂停输入并等待挂起事件在关闭之前完成处理，来响应SIGTERM。 当管道由于卡住的输出或过滤器而无法刷新时，Logstash会无限期地等待。 例如，当管道将输出发送到Logstash实例无法访问的数据库时，实例在接收到SIGTERM后无限期等待。

要使Logstash能够检测这些情况并以停止的管道终止，请使用--allow-unsafe-shutdown标志。

> 警告:不安全的关闭，强制杀死Logstash进程或由于任何其他原因导致Logstash进程崩溃导致数据丢失。 尽可能安全地关闭Logstash。

#### 执行模型
Logstash管道协调输入，过滤器和输出的执行。 以下示意图描绘了流水线的数据流：
```
input threads | pipeline worker threads
```

管道在当前版本的Logstash进程过滤和输出在同一个线程。在2.2版本的Logstash之前，过滤和输出是由不同线程处理的不同阶段。对Logstash架构的这种更改可以提高性能并支持未来的持久性功能。新的流水线大大提高了线程活性，减少了资源使用，并增加了吞吐量。当前的Logstash管道是一个微批处理管道，其本质上比一次一个方法更有效。这些效率在许多地方出现，其中两个更突出的是减少争用和随之而来的线程活性的改善。这些效率在多核机器上尤其显着。

Logstash配置文件中的每个input{}语句都在其自己的线程中运行。将事件输入到公共Java同步队列。此队列不保留任何事件，而是将每个已推送事件转移到空闲工作线程，阻止所有工作线程忙。每个流水线工作线程从此队列中取出一批事件，为每个工人创建一个缓冲区，通过配置的过滤器运行该批事件，然后通过任何输出运行过滤的事件。批处理的大小和流水线工作线程的数量是可配置的。以下伪代码说明了过程流程：
```
synchronous_queue = SynchronousQueue.new
inputs.each do |input|
  Thread.new do
    input.run(synchronous_queue)
  end
end
num_pipeline_workers.times do
  Thread.new do
    while true
      batch = take_batch(synchronous_queue, batch_size, batch_delay)
      output_batch(filter_batch(batch))
    end
  end
end
wait_for_threads_to_terminate()
```

在管道中有三个可配置选项，--pipeline-workers，--pipeline-batch-size和--pipeline-batch-delay。

- --pipeline-workers或-w参数确定要为过滤器和输出处理运行多少线程。如果发现事件正在备份，或CPU未饱和，请考虑增加此参数的值以更好地利用可用的处理能力。好的结果甚至可以发现增加这个数字超过可用处理器的数量，因为这些线程在写入外部系统时可能在I / O等待状态中花费大量时间。此参数的合法值为正整数。

- --pipeline-batch-size或-b参数定义单个工作线程在尝试执行过滤器和输出之前收集的最大事件数。较大的批量大小通常更高效，但增加了内存开销。某些硬件配置要求您通过设置LS_HEAP_SIZE变量来增加JVM堆大小，以避免使用此选项导致性能下降。此参数的值超过最佳范围会导致由于频繁的垃圾回收或与内存不足异常相关的JVM崩溃而导致性能下降。输出插件可以将每个批处理作为逻辑单元处理。例如，Elasticsearch输出针对接收的每个批生产批量请求。调整-b参数可调整发送到Elasticsearch的批量请求的大小。

- --pipeline-batch-delay选项很少需要调整。此选项可调整Logstash管道的延迟。流水线批处理延迟是Logstash在当前管道工作线程中接收到事件后等待新消息的最大时间（毫秒）。在此时间过后，Logstash开始执行过滤器和输出.Logstash在接收事件和在过滤器中处理该事件之间等待的最大时间是pipeline_batch_delay和pipeline_batch_size设置的乘积。


#### 关于流水线配置和性能的注意事项
飞行事件的总数由pipeline_workers和pipeline_batch_size参数的乘积确定。本产品称为飞行计数。在调整pipeline_workers和pipeline_batch_size参数时，请记住飞行计数的值。以不规则间隔间歇接收大型事件的管道需要足够的内存来处理这些尖峰。相应地配置LS_HEAP_SIZE选项。

Logstash默认值是为大多数用户提供快速，安全的性能。要提高性能，请增加管道工作者的数量或批量大小，同时考虑以下建议：

测量每个更改以确保其性能提高，而不是降低。确保您留下足够的内存可用来应付突然增加的事件大小。例如，生成表示为大文本块的异常的应用程序。工作程序的数量可以设置为高于CPU核心的数量，因为输出经常在I / O等待条件中花费空闲时间。

Java中的线程具有名称，您可以使用jstack，top和VisualVM图形工具来确定给定线程使用的资源。

在Linux平台上，Logstash标记了所有可以描述的线程。例如，输入显示为[base] <inputname，过滤器/输出工作者显示为[base]> workerN，其中N是整数。在可能的情况下，还会标记其他线程以帮助您确定其目的。


#### 分析堆
当调整Logstash时，您可能需要调整堆大小。 您可以使用VisualVM工具来分析堆。 监视器窗格特别适用于检查堆分配是否足以满足当前工作负载。 下面的屏幕截图显示示例监视器窗格。 第一个窗格检查配置了太多飞行事件的Logstash实例。 第二个窗格检查配置有适当数量的飞行事件的Logstash实例。 请注意，此处使用的特定批量大小很可能不适用于您的特定工作负载，因为Logstash的内存需求在很大程度上取决于您要发送的消息类型。

![img](http://n.sinaimg.cn/games/3ece443e/20161024/pipeline_overload.png)

![img](http://n.sinaimg.cn/games/3ece443e/20161024/pipeline_correct_load.png)

在第一个例子中，我们看到CPU没有被非常有效地使用。 事实上，JVM经常需要停止VM的“完全GC”。 完全的垃圾收集是过度内存压力的常见症状。 这在CPU图表上的尖锐模式中可见。 在更高效配置的示例中，GC图形图案更光滑，并且CPU以更均匀的方式使用。 你还可以看到，在分配的堆大小和最大允许之间有足够的余量，给JVM GC一个很大的空间使用。

使用类似于优秀的VisualGC插件的工具来检查深入的GC统计数据表明，与在更资源密集型的“全”GC中花费的时间相比，过度分配的VM在高效的Eden GC中花费的时间非常少 。

> 只要GC模式可以接受，堆大小偶尔增加到最大是可以接受的。 这种堆大小尖峰响应于通过流水线的大事件的突发而发生。 在一般实践中，保持使用的堆内存量和最大值之间的差距。 本文档不是JVM GC调优的全面指南。 阅读官方Oracle指南有关该主题的更多信息。 我们还建议您阅读调试Java性能。
