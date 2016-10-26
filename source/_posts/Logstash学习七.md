---
title: Logstash学习七
date: 2016-10-26 21:30:00
tags:
- Logstash
categories:
- Logstash
---
- 贡献Logstash
- 专业术语


<!-- more -->

## 贡献Logstash

### Contributing to Logstash

在1.5版之前，Logstash包括每个版本中的所有插件。这使得使用任何插件很容易，但它复杂的插件开发 - 如果一个插件需要修补，Logstash的新版本是必要的。从版本1.5开始，所有插件都独立于Logstash核心。现在，您可以更容易地添加自己的输入，编解码器，过滤器或输出插件到Logstash！

### 添加插件
由于现在可以独立于Logstash核心开发和部署插件，因此有一些文档可以指导您完成编码和部署自己的插件的过程：

- [生成新的插件](https://www.elastic.co/guide/en/logstash/current/plugin-generator.html)
- [如何编写一个Logstash输入插件](http://www.elasticsearch.org/guide/en/logstash/current/_how_to_write_a_logstash_input_plugin.html)
- [如何编写一个Logstash编解码器插件](http://www.elasticsearch.org/guide/en/logstash/current/_how_to_write_a_logstash_codec_plugin.html)
- [如何写一个Logstash过滤器插件](http://www.elasticsearch.org/guide/en/logstash/current/_how_to_write_a_logstash_filter_plugin.html)
- [如何写一个Logstash输出插件](http://www.elasticsearch.org/guide/en/logstash/current/_how_to_write_a_logstash_output_plugin.html)
- [向Logstash插件提供修补程序](https://www.elastic.co/guide/en/logstash/current/contributing-patch-plugin.html)
- [社区维护者指南](https://www.elastic.co/guide/en/logstash/current/community-maintainer.html)
- [提交插件](https://www.elastic.co/guide/en/logstash/current/submitting-plugin.html)


### Plugin API Changes [2.0]于2.0中添加。
Logstash的2.0版本改变了输入插件的关闭方式，以提高关闭的可靠性。有三种方法用于插件关闭：stop, stop?, 和close。

从外部线程调用stop方法。此方法通知插件停止。
停止？方法在已为该插件调用stop方法时返回true。
close方法在插件的run方法和插件的线程都退出后执行最后的记事和清理。 close方法是在Logstash的早期版本中称为teardown的方法的新名称。
关机，完成，完成，运行？和终止？方法是多余的，不再存在于Plugin Base类中。

新插件关闭API的示例代码可用。


### 扩展Logstash核心
我们还欢迎对Logstash核心功能集的贡献和错误修复。

请阅读我们的[贡献指南](https://github.com/elastic/logstash/blob/master/CONTRIBUTING.md)和Logstash[自述文件](https://github.com/elastic/logstash/blob/master/README.md)。


## 专业术语

- `@metadata`
> 用于存储不希望包含在输出事件中的内容的特殊字段。例如，@metadata字段对于创建在条件语句中使用的临时字段很有用。


- `codec plugin`
> 用于更改事件的数据表示的Logstash插件。编解码器本质上是可以作为输入或输出的一部分操作的流过滤器。编解码器使您能够将消息的传输与序列化过程分离。流行的编解码器包括json，msgpack和plain（text）。

- `conditional`
> 基于语句（也称为条件）是真还是假执行某些操作的控制流。 Logstash支持if，else if和else语句。您可以使用条件语句根据您指定的条件应用过滤器和将事件发送到特定输出。

- `event`
> 单个信息单元，包含时间戳加上附加数据。事件通过输入到达，随后被解析，加时间戳并通过Logstash管道传递。

- `field`
> 事件属性。例如，apache访问日志中的每个事件具有诸如状态码（200,404），请求路径（“/”，“index.html”），HTTP动词（GET，POST），客户端IP地址，等等。 Logstash使用术语“fields”来引用这些属性。

- `field reference`
> 对事件字段的引用。此引用可能会出现在Logstash配置文件中的输出块或过滤器块中。字段引用通常包装在方括号（[]）中，例如[fieldname]。如果您要引用顶级字段，则可以省略[]，然后只需使用字段名称。要引用嵌套字段，请指定该字段的完整路径： \[top-level field][nested field].

- `filter plugin`
> 一个对事件执行中间处理的Logstash插件。通常，过滤器在事件数据已经通过输入被摄取之后，通过根据配置规则突变，丰富和/或修改数据来对事件数据进行操作。过滤器通常根据事件的特征有条件地应用。热门插件包括grok，mutate，drop，clone和geoip。过滤器级是可选的。

- `gem`
> 在RubyGems.org上托管的自包含代码包。 Logstash插件包装为Ruby Gems。您可以使用Logstash插件管理器来管理Logstash gem。

- `hot thread`
> 具有高CPU使用率并且执行时间长于正常时间的Java线程。

- `input plugin`
> 一个用于从特定源读取事件数据的Logstash插件。输入插件是Logstash事件处理管道的第一个阶段。热门输入插件包括 file, syslog, redis, and beats.

- `indexer`
> 一个Logstash实例，负责与Elasticsearch集群连接，以便索引事件数据。

- `message broker`
> 也称为消息缓冲区或消息队列，消息代理是外部软件（例如Redis，Kafka或RabbitMQ），它将来自Logstash运输程序实例的消息存储为中间存储，等待由Logstash索引器实例处理。

- `output plugin`
> 一个用于将事件数据写入特定目标的Logstash插件。输出是事件管道中的最后一个阶段。热门输出插件包括elasticsearch，file，graphite和statsd。

- `pipeline`
> 用于描述通过Logstash工作流的事件流的术语。流水线通常由一系列输入，滤波器和输出级组成。输入阶段从源获取数据并生成事件，过滤阶段（可选），修改事件数据，输出阶段将数据写入目标。输入和输出支持编解码器，使您能够在数据进入或退出流水线时对其进行编码或解码，而无需使用单独的过滤器。

- `plugin`
> 一个自包含的软件包，实现Logstash事件处理管道中的一个阶段。可用插件列表包括输入插件，输出插件，编解码器插件和过滤器插件。这些插件实现为Ruby gem并且托管在RubyGems.org上。通过配置插件来定义事件处理管道的阶段。

- `plugin manager`
> 通过bin / logstash-plugin脚本访问，插件管理器使您能够管理Logstash部署中的插件的生命周期。您可以使用插件管理器命令行界面（CLI）安装，卸载和升级插件。

- `shipper`
> 将事件发送到Logstash的另一个实例或其他一些应用程序的Logstash实例。

- `worker`
> Logstash使用的过滤器线程模型，其中每个工作程序接收事件并按顺序应用所有过滤器，然后将事件发送到输出队列。这允许CPU之间的可扩展性，因为许多过滤器是CPU密集型。
