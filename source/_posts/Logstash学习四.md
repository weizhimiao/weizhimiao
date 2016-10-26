---
title: Logstash学习四
date: 2016-10-25 20:30:00
tags:
- Logstash
categories:
- Logstash
---

- 输出插件

<!-- more -->

## 输出插件
输出插件将事件数据发送到特定目标。 输出是事件管道中的最后一个阶段。

以下输出插件可用：


**boundary**

> 基于Logstash事件将注释发送到Boundary

[logstash-output-boundary](https://github.com/logstash-plugins/logstash-output-boundary)

**circonus**

> 基于Logstash事件向Circonus发送注释

[logstash-output-circonus](https://github.com/logstash-plugins/logstash-output-circonus)

**csv**

> 以分隔格式将事件写入磁盘

[logstash-output-csv](https://github.com/logstash-plugins/logstash-output-csv)

**cloudwatch**

> 聚合并将度量标准数据发送到AWS CloudWatch

[logstash-output-cloudwatch](https://github.com/logstash-plugins/logstash-output-cloudwatch)

**datadog**

> 基于Logstash事件将事件发送到DataDogHQ

[logstash-output-datadog](https://github.com/logstash-plugins/logstash-output-datadog)

**datadog_metrics**

> 基于Logstash事件将度量标准发送到DataDogHQ

[logstash-output-datadog_metrics](https://github.com/logstash-plugins/logstash-output-datadog_metrics)

**email**

> 收到输出时将电子邮件发送到指定的地址

[logstash-output-email](https://github.com/logstash-plugins/logstash-output-email)

**elasticsearch**

> 将日志存储在Elasticsearch中

[logstash-output-elasticsearch](https://github.com/logstash-plugins/logstash-output-elasticsearch)

**elasticsearch_java**

> 使用节点和传输协议将日志存储在Elasticsearch中

[logstash-output-elasticsearch_java](https://github.com/logstash-plugins/logstash-output-elasticsearch_java)

**exec**

> 为匹配的事件运行命令

[logstash-output-exec](https://github.com/logstash-plugins/logstash-output-exec)

**file**

> 将事件写入磁盘上的文件

[logstash-output-file](https://github.com/logstash-plugins/logstash-output-file)

**google_bigquery**

> 将事件写入Google BigQuery

[logstash-output-google_bigquery](https://github.com/logstash-plugins/logstash-output-google_bigquery)

**google_cloud_storage**

> 将活动写入Google云端存储

[logstash-output-google_cloud_storage](https://github.com/logstash-plugins/logstash-output-google_cloud_storage)

**ganglia**

> 写指标到Ganglia的gmond

[logstash-output-ganglia](https://github.com/logstash-plugins/logstash-output-ganglia)

**gelf**

> 为Graylog2生成GELF格式化输出

[logstash-output-gelf](https://github.com/logstash-plugins/logstash-output-gelf)

**graphtastic**

> 在Windows上发送度量标准数据

[logstash-output-graphtastic](https://github.com/logstash-plugins/logstash-output-graphtastic)

**graphite**

> 向Graphite写入指标

[logstash-output-graphite](https://github.com/logstash-plugins/logstash-output-graphite)

**hipchat**

> 将事件写入HipChat

[logstash-output-hipchat](https://github.com/logstash-plugins/logstash-output-hipchat)

**http**

> 将事件发送到通用HTTP或HTTPS端点

[logstash-output-http](https://github.com/logstash-plugins/logstash-output-http)

**irc**

> 将事件写入IRC

[logstash-output-irc](https://github.com/logstash-plugins/logstash-output-irc)

**influxdb**

> 将指标写入InfluxDB

[logstash-output-influxdb](https://github.com/logstash-plugins/logstash-output-influxdb)

**juggernaut**

> 将消息推送到Juggernaut websockets服务器

[logstash-output-juggernaut](https://github.com/logstash-plugins/logstash-output-juggernaut)

**jira**

> 将结构化JSON事件写入JIRA

[logstash-output-jira](https://github.com/logstash-plugins/logstash-output-jira)

**kafka**

将事件写入Kafka

[logstash-output-kafka](https://github.com/logstash-plugins/logstash-output-kafka)

**lumberjack**

> 使用lumberjack协议发送事件

[logstash-output-lumberjack](https://github.com/logstash-plugins/logstash-output-lumberjack)

**librato**

> 基于Logstash事件向Librato发送度量，注释和警报

[logstash-output-librato](https://github.com/logstash-plugins/logstash-output-librato)

**loggly**

> 将日志发送到Loggly

[logstash-output-loggly](https://github.com/logstash-plugins/logstash-output-loggly)

**mongodb**

> 将事件写入MongoDB

[logstash-output-mongodb](https://github.com/logstash-plugins/logstash-output-mongodb)

**metriccatcher**

> 将指标写入MetricCatcher

[logstash-output-metriccatcher](https://github.com/logstash-plugins/logstash-output-metriccatcher)

**nagios**

> 将被动检查结果发送到Nagios

[logstash-output-nagios](https://github.com/logstash-plugins/logstash-output-nagios)

**nagios_nsca**

> 使用NSCA协议将被动检查结果发送到Nagios

[logstash-output-nagios_nsca](https://github.com/logstash-plugins/logstash-output-nagios_nsca)

**null**

> 用于测试的null输出

[logstash-output-null](https://github.com/logstash-plugins/logstash-output-null)

**opentsdb**

> 将指标写入OpenTSDB

[logstash-output-opentsdb](https://github.com/logstash-plugins/logstash-output-opentsdb)

**pagerduty**

> 根据预配置的服务和上报策略发送通知

[logstash-output-pagerduty](https://github.com/logstash-plugins/logstash-output-pagerduty)

**pipe**

> 将事件管道传送到另一个程序的标准输入

[logstash-output-pipe](https://github.com/logstash-plugins/logstash-output-pipe)

**riemann**

>向Riemann发送指标

[logstash-output-riemann](https://github.com/logstash-plugins/logstash-output-riemann)

**redmine**

> 使用Redmine API创建票证

[logstash-output-redmine](https://github.com/logstash-plugins/logstash-output-redmine)

**rackspace**

> 将事件发送到Rackspace云队列服务

[logstash-output-rackspace](https://github.com/logstash-plugins/logstash-output-rackspace)

**rabbitmq**

> 将事件推送到RabbitMQ

[logstash-output-rabbitmq](https://github.com/logstash-plugins/logstash-output-rabbitmq)

**redis**

> 使用RPUSH命令将事件发送到Redis队列

[logstash-output-redis](https://github.com/logstash-plugins/logstash-output-redis)

**riak**

> 将事件写入Riak分布式键/值存储

[logstash-output-riak](https://github.com/logstash-plugins/logstash-output-riak)

**s3**

> 将Logstash事件发送到Amazon Simple Storage Service

[logstash-output-s3](https://github.com/logstash-plugins/logstash-output-s3)

**sqs**

> 将事件推送到Amazon Web服务简单队列Serice队列

[logstash-output-sqs](https://github.com/logstash-plugins/logstash-output-sqs)

**stomp**

> 使用STOMP协议写入事件

[logstash-output-stomp](https://github.com/logstash-plugins/logstash-output-stomp)

**statsd**

> 使用statsd网络守护程序发送指标

[logstash-output-statsd](https://github.com/logstash-plugins/logstash-output-statsd)

**solr_http**

> 在Solr中存储和索引日志

[logstash-output-solr_http](https://github.com/logstash-plugins/logstash-output-solr_http)

**sns**

> 将事件发送到Amazon的简单通知服务

[logstash-output-sns](https://github.com/logstash-plugins/logstash-output-sns)

**syslog**

> 将事件发送到系统日志服务器

[logstash-output-syslog](https://github.com/logstash-plugins/logstash-output-syslog)

**stdout**

> 将事件打印到标准输出

[logstash-output-stdout](https://github.com/logstash-plugins/logstash-output-stdout)

**tcp**

> 通过TCP套接字写事件

[logstash-output-tcp](https://github.com/logstash-plugins/logstash-output-tcp)

**udp**

> 通过UDP发送事件

[logstash-output-udp](https://github.com/logstash-plugins/logstash-output-udp)

**webhdfs**

> 使用webhdfs REST API将Logstash事件发送到HDFS

[logstash-output-webhdfs](https://github.com/logstash-plugins/logstash-output-webhdfs)

**websocket**

> 将消息发布到websocket

[logstash-output-websocket](https://github.com/logstash-plugins/logstash-output-websocket)

**xmpp**

> 通过XMPP上传事件

[logstash-output-xmpp](https://github.com/logstash-plugins/logstash-output-xmpp)

**zabbix**

> 将事件发送到Zabbix服务器

[logstash-output-zabbix](https://github.com/logstash-plugins/logstash-output-zabbix)

**zeromq**

> 将事件写入ZeroMQ PUB套接字

[logstash-output-zeromq](https://github.com/logstash-plugins/logstash-output-zeromq)


### elasticsearch
此插件是在Elasticsearch中存储日志的推荐方法。 如果计划使用Kibana Web界面，您将需要使用此输出。

此输出仅讲HTTP协议。 HTTP是从Logstash 2.0开始与Elasticsearch交互的首选协议。 我们强烈建议在节点协议上使用HTTP有很多原因。 HTTP只是稍微减慢，但更容易管理和使用。 当使用HTTP协议时，可以升级Elasticsearch版本，而不必在锁定步骤中升级Logstash。 对于那些仍然希望使用节点或传输协议的用户，请参阅elasticsearch_java输出插件。

您可以在https://www.elastic.co/products/elasticsearch了解有关Elasticsearch的更多信息

#### 重试策略
重试策略在2.2.0版本中发生了显着更改。 此插件使用Elasticsearch批量API来优化其导入Elasticsearch。 这些请求可能会部分或全部失败。

以下错误无限重试：

- 网络错误（无法连接）
- 429（请求过多）和
- 503（服务不可用）错误

> 注意: 409异常不再重试。 如果遇到409异常，请设置更高的retry_on_conflict值。 Elasticsearch比这个插件重试这些异常更有效率。

#### DNS缓存
此插件使用JVM来查找DNS条目，并受networkaddress.cache.ttl的值（即JVM的全局设置）的约束。

例如，要将DNS TTL设置为1秒，您应将LS_JAVA_OPTS环境变量设置为-Dnetwordaddress.cache.ttl = 1。

请记住，启用keepalive的连接将不会在keepalive有效时重新评估其DNS值。

#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
elasticsearch {
}
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
action |  string, one of ["index", "delete", "create", "update"] |  No |  "index"
cacert |  a valid filesystem path |  No|
codec |  codec |  No |  "plain"
doc_as_upsert |  boolean |  No |  false
document_id |  string |  No|
document_type |  string |  No|
flush_size |  number |  No |  500
hosts |  array |  No |  ["127.0.0.1"]
idle_flush_time |  number |  No |  1
index |  string |  No |  "logstash-%{+YYYY.MM.dd}"
keystore |  a valid filesystem path |  No|
keystore_password |  password |  No|
manage_template |  boolean |  No |  true
max_retries |  number |  No |  3
parent |  string |  No |  nil
password |  password |  No|
path |  string |  No |  "/"
proxy |  <<,>> |  No|
retry_max_interval |  number |  No |  2
routing |  string |  No|
script |  string |  No |  ""
script_lang |  string |  No |  ""
script_type |  string, one of ["inline", "indexed", "file"] |  No |  ["inline"]
script_var_name |  string |  No |  "event"
scripted_upsert |  boolean |  No |  false
sniffing |  boolean |  No |  false
sniffing_delay |  number |  No |  5
ssl |  boolean |  No|
ssl_certificate_verification |  boolean |  No |  true
template |  a valid filesystem path |  No
template_name |  string |  No |  "logstash"
template_overwrite |  boolean |  No |  false
timeout |  number |  No|
truststore |  a valid filesystem path |  No|
truststore_password |  password |  No|
upsert |  string |  No |  ""
user |  string |  No|
workers |  number |  No |  1

#### 详情

**action**
- 值可以是以下任何值：index，delete，create，update
- 默认值为“index”

要执行的Elasticsearch操作。有效操作是：

- index：索引文档（来自Logstash的事件）。
- delete：按id删除文档（此操作需要id）
- create：索引文档，如果该id的文档已经存在于索引中，则失败。
- update：按id更新文档。更新有一个特殊情况，你可以upsert - 更新文档，如果还没有。请参见upsert选项
- 基于事件内容更改操作的sprintf样式字符串。值％{[foo]}将使用foo字段作为操作

有关操作的更多详细信息，请参阅[Elasticsearch批量API文档](http://www.elastic.co/guide/en/elasticsearch/reference/current/docs-bulk.html)

**cacert**
- 值类型为路径
- 此设置没有默认值。

.cer或.pem文件以验证服务器的证书

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输出数据的编解码器。输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**doc_as_upsert**
- 值类型是布尔值
- 默认值为false

为更新模式启用doc_as_upsert。如果Elasticsearch中不存在document_id，请使用源代码创建新文档

**document_id**
- 值类型是字符串
- 此设置没有默认值。

索引的文档ID。用于使用相同的ID覆盖Elasticsearch中的现有条目。

**document_type**
- 值类型是字符串
- 此设置没有默认值。

要将事件写入的文档类型。一般来说，你应该尝试只写相似类型的事件。字符串扩展％{foo}在这里工作。除非设置document_type，否则将使用事件类型（如果存在），否则将为文档类型分配日志值

**flush_size**
- 值类型是数字
- 默认值为500

此插件使用批量索引API提高索引性能。在Logstashes> = 2.2中，此设置定义了Logstash会创建的最大大小的批量请求。您可能希望将其增加到与管道的批量大小一致。如果您指定的数字大于管道的批处理大小，则不会生效，除非过滤器通过输出事件来增加飞动批处理的大小。

在Logstashes 2.1中，这个插件使用自己的内部事件缓冲区。此配置选项设置该大小。在这些较旧的logstash中，这个大小可能对堆使用有重大影响，而在2.2+以上它永远不会增加它。为了进行有效的批量API调用，我们将缓冲一定数量的事件，然后将其刷新到Elasticsearch。此设置控制在发送一批事件之前将缓冲的事件数。增加flush_size对Logstash的堆大小有影响。如果要发送大文档或将flush_size增加到更高的值，请记住也使用LS_HEAP_SIZE增加堆大小。

**hosts**
- 值类型是数组
- 默认值为[“127.0.0.1”]

设置远程实例的主机。如果给定一个数组，它将在hosts参数中指定的主机上负载均衡请求。请记住，http协议使用http地址（例如，9200，而不是9300）。 “127.0.0.1”[“127.0.0.1:9200","127.0.0.2:9200”] [“https://127.0.0.1:9200”] [“https://127.0.0.1:9200/mypath”] （如果在子路径上使用代理）重要的是从主机列表中排除专用主节点，以防止LS向主节点发送批量请求。因此，此参数应仅引用Elasticsearch中的数据或客户端节点。

**idle_flush_time**
- 值类型是数字
- 默认值为1

强制刷新之前自上次刷新以来的时间量。

此设置有助于确保缓慢的事件率不会陷入Logstash。例如，如果您的flush_size为100，并且已经收到10个事件，并且自上次刷新以来已经超过idle_flush_time秒，Logstash将自动刷新这10个事件。

这有助于保持快速和慢速日志流几乎实时地移动。

**index**
- 值类型是字符串
- 默认值为“logstash - ％{+ YYYY.MM.dd}”

将事件写入的索引。这可以是使用％{foo}语法的动态。默认值将按日划分索引，以便您可以更轻松地删除旧数据或仅搜索特定日期范围。索引不能包含大写字符。对于每周索引，建议使用ISO 8601格式，例如。 logstash - ％{+ xxxx.ww}

**keystore**
- 值类型为路径
- 此设置没有默认值。

用于向服务器提供证书的密钥库。它可以是.jks或.p12

**keystore_password**
- 值类型为密码
- 此设置没有默认值。

设置信任库密码

**manage_template**
- 值类型是布尔值
- 默认值为true

从Logstash 1.3开始（除非将option_template选项设置为false），如果您还没有一个集合来匹配定义的索引模式（默认为logstash - ％{+ YYYY.MM.dd），将应用Elasticsearch的默认映射模板}），减去任何变量。例如，在这种情况下，模板将应用于所有索引，从logstash- *

如果您有动态模板（例如，根据字段名称创建索引），则应将manage_template设置为false，并使用REST API手动上传模板。

**max_retries**
- 值类型是数字
- 默认值为3

＃DEPRECATED此设置不再有任何作用。它将在以后的版本中标记为过时。

**parent**
- 值类型是字符串
- 默认值为nil

对于子文档，相关父级的ID。这可以是使用％{foo}语法的动态。

**password**
- 值类型为密码
- 此设置没有默认值。

用于向安全Elasticsearch群集进行身份验证的密码

**path**
- 值类型是字符串
- 默认值为“/”

HTTP Elasticsearch服务器所在的路径。如果必须在代理之后运行Elasticsearch，重新映射Elasticsearch HTTP API的根路径，请使用此选项。

**proxy**
```
<li> Value type is <<string,string>>
* There is no default value for this setting.
```

设置转发HTTP代理的地址。可以是字符串，例如http：// localhost：123，也可以是{host：'proxy.org'port：80 scheme：'http'}形式的哈希。注意，这不是SOCKS代理，而是纯HTTP代理


**retry_max_interval**
- 值类型是数字
- 默认值为2

设置批量重试之间的最大间隔。

**retry_max_items (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是数字
- 默认值为500

**routing**
- 值类型是字符串
- 此设置没有默认值。

要应用于所有已处理事件的路由覆盖。这可以是使用％{foo}语法的动态。

**script**
- 值类型是字符串
- 默认值为“”

设置脚本更新模式的脚本名称


**script_lang**
- 值类型是字符串
- 默认值为“”

设置使用的脚本的语言

**script_type**
- 值可以是以下任何值：inline, indexed, file
- 默认值为[“inline”]

定义由“script”变量引用的脚本类型inline：“script”包含索引的内联脚本：“script”包含在elasticsearch文件中直接索引的脚本的名称：“script”包含存储在elasticseach的config目录中的脚本的名称


**script_var_name**
- 值类型是字符串
- 默认值为“event”

设置变量名传递给脚本（脚本更新）

**scripted_upsert**
- 值类型是布尔值
- 默认值为false

如果启用，脚本负责创建不存在的文档（脚本式更新）

**sniffing**
- 值类型是布尔值
- 默认值为false

此设置要求Elasticsearch查找所有集群节点的列表，并将它们添加到主机列表中。注意：这将返回所有节点启用HTTP（包括主节点！）。如果将此与主节点一起使用，则可能希望通过在elasticsearch.yml中将http.enabled设置为false来禁用HTTP。您可以使用sniffing选项，也可以使用hosts参数手动输入多个Elasticsearch主机。

**sniffing_delay**
- 值类型是数字
- 默认值为5

在嗅探尝试之间等待几秒钟

**ssl**
- 值类型是布尔值
- 此设置没有默认值。

启用到Elasticsearch群集的SSL / TLS安全通信。留下此未指定将使用在主机中列出的URL中指定的任何方案。如果没有指定明确的协议，将使用纯HTTP。如果在此处显式禁用SSL，则如果在主机中指定了HTTPS URL，插件将拒绝启动

**ssl_certificate_verification**
- 值类型是布尔值
- 默认值为true

用于验证服务器证书的选项。禁用此操作会严重危及安全性。有关禁用证书验证的详细信息，请参阅https://www.cs.utexas.edu/~shmat/shmat_ccs12.pdf


**template**
- 值类型为路径
- 此设置没有默认值。

你可以在这里设置你自己的模板的路径，如果你愿意的话。如果未设置，将使用包含的模板。

**template_name**
- 值类型是字符串
- 默认值为“logstash”

此配置选项定义模板在Elasticsearch中的命名方式。请注意，如果您已使用模板管理功能并随后更改此设置，则需要手动修剪旧模板，例如。
```
curl -XDELETE <http://localhost:9200/_template/OldTemplateName?pretty>
```
其中OldTemplateName是以前的设置。

**template_overwrite**
- 值类型是布尔值
- 默认值为false

template_overwrite选项将始终使用模板或包含的模板指示的模板覆盖Elasticsearch中指示的模板。默认情况下，此选项设置为false。如果你总是想保持最新的Logstash提供的模板，这个选项可能对你非常有用。同样，如果你有自己的模板文件由puppet管理，例如，你想要能够定期更新，这个选项也可以帮助那里。

请注意，如果您使用自己的自定义版本的Logstash模板（logstash），将其设置为true将使Logstash覆盖“logstash”模板（即删除所有自定义设置）

**timeout**
- 值类型是数字
- 此设置没有默认值。

设置发送Elasticsearch的网络操作和请求的超时。如果发生超时，将重试请求。

**truststore**
- 值类型为路径
- 此设置没有默认值。

JKS信任库以验证服务器的证书。使用：truststore或：cacert

**truststore_password**
- 值类型为密码
- 此设置没有默认值。

设置信任库密码

**upsert**
- 值类型是字符串
- 默认值为“”

设置更新模式的内容。使用此参数创建一个新文档作为json字符串（如果document_id不存在）

**user**
- 值类型是字符串
- 此设置没有默认值。

用于向安全Elasticsearch集群进行身份验证的用户名

**workers**
- 值类型是数字
- 默认值为1

用于此输出的工人数。请注意，此设置可能不适用于所有输出。


### exec
此输出将运行任何匹配的事件的命令。例：
```
output {
  exec {
    type => abuse
    command => "iptables -A INPUT -s %{clientip} -j DROP"
  }
}
```
通过系统ruby函数运行子进程

> 警告: 如果你想要它的非阻塞，你应该使用＆或分离或其他这样的技术

#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
exec {
    command => ...
}
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
codec|codec|No|"plain"
command|string|Yes|
workers|number|No|1

#### 详情

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输出数据的编解码器。 输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**command**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

通过子进程执行的命令行。 使用dtach或屏幕使它不阻塞

**workers**
- 值类型为数字
- 默认值为1

用于此输出的工人数。 请注意，此设置可能不适用于所有输出。

### file
此输出将事件写入磁盘上的文件。 您可以使用事件中的字段作为文件名和/或路径的一部分。

默认情况下，此输出以json格式每行写入一个事件。 您可以使用线路编解码器自定义线路格式
```
output {
 file {
   path => ...
   codec => line { format => "custom format: %{message}"}
 }
}
```

##### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
file {
    path => ...
}
```
可用的配置选项:

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
codec | codec | No | "json_lines"
create_if_deleted | boolean | No | true
dir_mode | number | No | -1
file_mode | number | No | -1
filename_failure | string | No | "\_filepath_failures"
flush_interval | number | No | 2
gzip | boolean | No | false
path | string | Yes|
workers | number | No | 1


#### 详情
**codec**
- 值类型是编解码器
- 默认值为“json_lines”

用于输出数据的编解码器。输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**create_if_deleted**
- 值类型是布尔值
- 默认值为true

如果一个文件被删除，但事件正在进行，需要存储在这样的文件，插件将创建一个增益这个文件。 Default ⇒ true

**dir_mode**
- 值类型是数字
- 默认值为-1

使用的dir访问模式。注意，由于jruby系统中的错误umask在linux上被忽略：https://github.com/jruby/jruby/issues/3426将其设置为-1使用默认操作系统值。示例：“dir_mode”=> 0750

**file_mode**
- 值类型是数字
- 默认值为-1

要使用的文件访问模式。注意，由于jruby系统中的错误umask在linux上被忽略：https://github.com/jruby/jruby/issues/3426将其设置为-1使用默认操作系统值。示例：“file_mode”=> 0640

**filename_failure**
- 值类型是字符串
- 默认值为“`_filepath_failures`”

如果生成的路径无效，则事件将保存到此文件和定义的路径内。

**flush_interval**
- 值类型是数字
- 默认值为2

刷新间隔（以秒为单位）刷新写入日志文件。 0将刷新每条消息。

**gzip**
- 值类型是布尔值
- 默认值为false

在写入磁盘之前将输出流压缩。

**message_format (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是字符串
- 此设置没有默认值。

将事件写入文件时使用的格式。此值支持任何字符串，并且可以包括％{name}和其他动态字符串。

如果省略此设置，事件的完整json表示将写为单行。

**path**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

要写入的文件的路径。可以在这里使用事件字段，如`/var/log/logstash/%{host}/%{application}`也可以通过joda时间格式使用路径选项进行基于日期的日志轮换。这将使用事件时间戳。例如：`path => "./test-%{+YYYY-MM-dd}.txt"`创建./test-2013-05-29.txt

如果使用绝对路径，则不能以动态字符串开头。例如：`/%{myfield}/`，`/test-%{myfield}/`不是有效的路径

**workers**
- 值类型是数字
- 默认值为1

用于此输出的工人数。请注意，此设置可能不适用于所有输出。

### http

#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
http {
    http_method => ...
    url => ...
}
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
automatic_retries | number | No | 1
cacert | a valid filesystem path | No|
client_cert | a valid filesystem path | No|
client_key | a valid filesystem path | No|
codec | codec | No | "plain"
connect_timeout | number | No | 10
content_type | string | No|
cookies | boolean | No | true
follow_redirects | boolean | No | true
format | string, one of ["json", "form", "message"] | No | "json"
headers | hash | No|
http_method | string, one of ["put", "post", "patch", "delete", "get", "head"] | Yes|
keepalive | boolean | No | true
keystore | a valid filesystem path | No|
keystore_password | password | No|
keystore_type | string | No | "JKS"
mapping | hash | No|
message | string | No|
pool_max | number | No | 50
pool_max_per_route | number | No | 25
proxy | <<,>> | No|
request_timeout | number | No | 60
retry_non_idempotent | boolean | No | false
socket_timeout | number | No | 10
ssl_certificate_validation | boolean | No | true
truststore | a valid filesystem path | No|
truststore_password | password | No|
truststore_type | string | No | "JKS"
url | string | Yes|
workers | number | No | 1

#### 详情

**automatic_retries**
- 值类型是数字
- 默认值为1

**cacert**
- 值类型为路径
- 此设置没有默认值。

**client_cert**
- 值类型为路径
- 此设置没有默认值。

**client_key**
- 值类型为路径
- 此设置没有默认值。

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输出数据的编解码器。输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**connect_timeout**
- 值类型是数字
- 默认值为10

**content_type**
- 值类型是字符串
- 此设置没有默认值。

内容类型

如果未指定，则默认为以下内容：

- 如果格式为“json”，"application/json"
- 如果格式是“form”，"application/x-www-form-urlencoded"

**cookies**
- 值类型是布尔值
- 默认值为true

**follow_redirects**
- 值类型是布尔值
- 默认值为true

**format**
- 值可以是以下任何值：json，form，message
- 默认值为“json”

设置http主体的格式。

如果是form，那么主体将映射（或整个事件）转换为查询参数字符串，例如。 `foo=bar&baz=fizz...`

如果消息，那么正文将根据消息格式化事件的结果

否则，事件将作为json发送。


**headers**
- 值类型是哈希
- 此设置没有默认值。

要使用格式的自定义标头是headers => ["X-My-Header", "%{host}"]

**http_method**
- 这是必需的设置。
- 值可以是任何：put，post，patch，delete，get，head
- 此设置没有默认值。

HTTP动词“put”，“post”，“patch”，“delete”，“get”，“head”

**keepalive**
- 值类型是布尔值
- 默认值为true

**keystore**
- 值类型为路径
- 此设置没有默认值。

**keystore_password**
- 值类型为密码
- 此设置没有默认值。

**keystore_type**
- 值类型是字符串
- 默认值为“JKS”

**mapping**
- 值类型是哈希
- 此设置没有默认值。

这允许您选择发送的事件的结构和部分。

例如：
```
mapping => {"foo", "%{host}", "bar", "%{type}"}
```

**message**
- 值类型是字符串
- 此设置没有默认值。

**pool_max**
- 值类型是数字
- 默认值为50

**pool_max_per_route**
- 值类型是数字
- 默认值为25

**proxy**
- 值类型为string
- 此设置没有默认值


**request_timeout**
- 值类型是数字
- 默认值为60

**retry_non_idempotent**
- 值类型是布尔值
- 默认值为false

**socket_timeout**
- 值类型是数字
- 默认值为10

**ssl_certificate_validation**
- 值类型是布尔值
- 默认值为true

**truststore**
- 值类型为路径
- 此设置没有默认值。

**truststore_password**
- 值类型为密码
- 此设置没有默认值。

**truststore_type**
- 值类型是字符串
- 默认值为“JKS”

**url**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

此输出允许您将事件发送到通用HTTP（S）端点

此输出将并行执行pool_max请求以提高性能。在调整此插件的性能时，请考虑这一点。

此外，请注意，当使用并行执行时，不能保证事件的严格排序！

当心，这个gem还不支持编解码器。请立即使用格式选项。要使用的网址

**verify_ssl (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是布尔值
- 默认值为true

DEPRECATED。请改为设置ssl_certificate_validation

**workers**
- 值类型是数字
- 默认值为1

用于此输出的工人数。请注意，此设置可能不适用于所有输出。


### kafka
将事件写入Kafka主题。 这使用Kafka Producer API将消息写入代理上的主题。

这里有一个兼容性矩阵，显示与每个Logstash和Kafka输出插件组合兼容的Kafka客户端版本：

Kafka Client Version	|Logstash Version	|Plugin Version	|Security Features	|Why?
----------------------|-----------------|---------------|-------------------|-----
0.8|2.0.0 - 2.x.x|<3.0.0||Legacy, 0.8 is still popular
0.9|2.0.0 - 2.3.x|3.x.x|Basic Auth, SSL|Works with the old Ruby Event API (event['product']['price'] = 10)
0.9|2.4.0 - 5.0.x|4.x.x|Basic Auth, SSL|Works with the new getter/setter APIs (event.set('[product][price]', 10))
0.10|2.4.0 - 5.0.x|5.x.x|Basic Auth, SSL|Not compatible with the 0.9 broker

> 建议： 我们建议您使用匹配的Kafka客户端和代理版本。 在升级期间，您应该在客户端之前升级代理，因为代理的目标向后兼容。 例如，0.9代理与0.8消费者API和0.9消费者API兼容，但不是相反。

唯一需要的配置是主题名称。 默认编解码器是json，所以事件将以json格式保存在代理上。 如果您选择一个纯文本编码，Logstash将编码您的消息不仅消息，而且与时间戳和主机名。 如果你不想要任何东西，但你的消息传递，你应该使输出配置：

```
    output {{
      kafka {{
        codec => plain {=> plain {
           format => "%{message}"=> "%{message}"
        }}
      }}
    }}
For more information see http://kafka.apache.org/documentation.html#theproducerFor more information see http://kafka.apache.org/documentation.html#theproducer
```
Kafka 配置详情: http://kafka.apache.org/documentation.html#newproducerconfigs

#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
kafka {{
    topic_id => ...=> ...
}}
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
acks| string, one of ["0", "1", "all"]| No| "1"
batch_size| number| No| 16384
block_on_buffer_full| boolean| No| true
bootstrap_servers| string| No| "localhost:9092"
buffer_memory| number| No| 33554432
client_id| string| No|
codec| codec| No| "json"
compression_type| string, one of ["none", "gzip", "snappy"]| No| "none"
key_serializer| string| No| "org.apache.kafka.common.serialization.StringSerializer"
linger_ms| number| No| 0
max_request_size| number| No| 1048576
message_key| string| No|
metadata_fetch_timeout_ms| number| No| 60000
metadata_max_age_ms| number| No| 300000
receive_buffer_bytes| number| No| 32768
reconnect_backoff_ms| number| No| 10
retries| number| No| 0
retry_backoff_ms| number| No| 100
send_buffer_bytes| number| No| 131072
timeout_ms| number| No| 30000
topic_id| string| Yes|
value_serializer| string| No| "org.apache.kafka.common.serialization.StringSerializer"
workers| number| No| 1


#### 详情

**acks**
- 值可以是以下任意值：0，1，all
- 默认值为“1”

生产者需要领导者在考虑请求完成之前已接收的确认的数目。

acks = 0，生产者将不会等待来自服务器的任何确认。 acks = 1，这将意味着领导者将记录写入其本地日志，但将在不等待所有跟随者的完全确认的情况下进行响应。 acks = all，这意味着领导将等待完整的同步副本集合来确认记录。

**batch_size**
- 值类型是数字
- 默认值为16384

每当多个记录被发送到同一分区时，生产者将尝试将批记录一起分成较少的请求。这有助于客户端和服务器上的性能。此配置控制默认批量大小（以字节为单位）。

**block_on_buffer_full**
- 值类型是布尔值
- 默认值为true

当我们的内存缓冲区用尽时，我们必须停止接受新的记录（块）或抛出错误。默认情况下，此设置为true，我们阻止，但是在某些情况下阻塞是不可取的，最好立即给出错误。

**bootstrap_servers**
- 值类型是字符串
- 默认值为“localhost：9092”

这是用于引导，生产者将只使用它来获取元数据（主题，分区和副本）。用于发送实际数据的套接字连接将基于元数据中返回的代理信息来建立。格式为host1：port1，host2：port2，并且列表可以是代理的子集或指向代理子集的VIP。

**buffer_memory**
- 值类型是数字
- 默认值为33554432

生产者可以用来缓冲等待发送到服务器的记录的内存的总字节数。

**client_id**
- 值类型是字符串
- 此设置没有默认值。

在发出请求时传递给服务器的id字符串。这样做的目的是通过允许逻辑应用程序名称包含在请求中来跟踪超出ip / port的请求源

**codec**
- 值类型是编解码器
- 默认值为“json”

用于输出数据的编解码器。输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**compression_type**
- 值可以是以下任何值：none，gzip，snappy
- 默认值为“none”

生产者生成的所有数据的压缩类型。默认值为none（即不压缩）。有效值为none，gzip或snappy。

**key_serializer**
- 值类型是字符串
- 默认值为“org.apache.kafka.common.serialization.StringSerializer”

用于消息的密钥的序列化程序类

**linger_ms**
- 值类型是数字
- 默认值为0

生成器将在请求传输之间到达的任何记录集合到单个成批请求中。通常这仅在负载下发生，当记录到达比它们可以被发送时快。然而在某些情况下，即使在中等负载下，客户端也可能希望减少请求的数量。该设置通过添加少量的人为延迟来实现这一点，即，不是立即发出记录，而是生产者将等待给定的延迟，以允许发送其他记录，使得发送可以被批处理在一起。

**max_request_size**
- 值类型是数字
- 默认值为1048576

请求的最大大小

**message_key**
- 值类型是字符串
- 此设置没有默认值。

消息的键

**metadata_fetch_timeout_ms**
- 值类型是数字
- 默认值为60000

用于获取主题元数据的初始元数据请求的超时设置。

**metadata_max_age_ms**
- 值类型是数字
- 默认值为300000

强制元数据刷新之前的最长时间（以毫秒为单位）。

**receive_buffer_bytes**
- 值类型是数字
- 默认值为32768

读取数据时使用的TCP接收缓冲区的大小

**reconnect_backoff_ms**
- 值类型是数字
- 默认值为10

连接失败时尝试重新连接到给定主机之前等待的时间。

**retries**
- 值类型是数字
- 默认值为0

设置大于零的值将导致客户端重新发送任何发送失败且可能存在临时错误的记录。

**retry_backoff_ms**
- 值类型是数字
- 默认值为100

在尝试对给定主题分区重试失败的产生请求之前等待的时间量。

**send_buffer_bytes**
- 值类型是数字
- 默认值为131072

发送数据时使用的TCP发送缓冲区的大小。

**timeout_ms**
- 值类型是数字
- 缺省值为30000

配置控制服务器等待来自跟随者的确认以满足生产者使用ack配置指定的确认要求的最大时间量。如果在超时过期时未满足所请求的确认数量，则将返回错误。此超时在服务器端测量，不包括请求的网络延迟。

**topic_id**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

产生消息的主题

**value_serializer**
- 值类型是字符串
- 默认值为“org.apache.kafka.common.serialization.StringSerializer”

用于消息值的Serializer类

**workers**
- 值类型是数字
- 默认值为1

用于此输出的工人数。请注意，此设置可能不适用于所有输出。

### nagios

> 这是一个社区维护的插件！

Nagios输出用于通过Nagios命令文件将被动检查结果发送到Nagios。 此输出目前支持Nagios 3。

要使此输出正常工作，您的事件必须具有以下Logstash事件字段：

- nagios_host
- nagios_service

支持这些Logstash事件字段，但可选：

- nagios_annotation
- nagios_level (覆盖nagios级别配置选项)

有两个配置选项：

- commandfile - Nagios外部命令文件的位置。 默认为/var/lib/nagios3/rw/nagios.cmd
- nagios_level - 指定要发送的检查的级别。 默认为CRITICAL，可以通过将“nagios_level”字段设置为“OK”，“WARNING”，“CRITICAL”或“UNKNOWN”之一
```
output{
  if [message] =~ /(error|ERROR|CRITICAL)/ {
    nagios {
      # your config here
    }
  }
}
```
#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
nagios {
}
```

可用的配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
codec|codec|No|"plain"
commandfile|<<,>>|No|"/var/lib/nagios3/rw/nagios.cmd"
nagios_level|string, one of ["0", "1", "2", "3"]|No|"2"
workers|number|No|1

#### 详情

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输出数据的编解码器。 输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**commandfile**
- 值类型是字符串
- 默认值为“/var/lib/nagios3/rw/nagios.cmd”`

Nagios命令文件的完整路径。

**nagios_level**
- 值可以是以下任意值：0，1，2，3
- 默认值为“2”

Nagios检查级别。 应为0 =正常，1 =警告，2 =严重，3 =未知。 默认为2 - CRITICAL。

**workers**
- 值类型为数字
- 默认值为1

用于此输出的工人数。 请注意，此设置可能不适用于所有输出。

### pipe
> 这是一个社区维护的插件！

管道输出。

管道事件到另一个程序的stdin。 您可以使用事件中的字段作为命令的一部分。 警告：如果你不关心per-event命令行，这个功能可以导致logstash分叉多个孩子。

#### 概述

这个插件支持下列配置选项：

所需的配置选项：
```
pipe {
    command => ...
}
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
codec|codec|No|"plain"
command|string|Yes|
message_format|string|No|
ttl|number|No|10
workers|number|No|1


#### 详情

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输出数据的编解码器。 输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**command**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

命令行启动和管道

**message_format**
- 值类型是字符串
- 此设置没有默认值。

将事件写入管道时使用的格式。 此值支持任何字符串，并且可以包括％{name}和其他动态字符串。

如果省略此设置，事件的完整json表示将写为单行。

**ttl**
- 值类型为数字
- 默认值为10

关闭尚未用于TTL秒的管道。 -1或0表示永不关闭。

**workers**
- 值类型为数字
- 默认值为1

用于此输出的工人数。 请注意，此设置可能不适用于所有输出。



### rabbitmq
将事件推送到RabbitMQ交换。 需要RabbitMQ 2.x或更高版本（建议使用3.x）。

相关链接：

- [RabbitMQ](http://www.rabbitmq.com/)
- [March Hare](http://rubymarchhare.info/)

#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
rabbitmq {
    exchange => ...
    exchange_type => ...
    host => ...
}
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
arguments| array| No| {}
automatic_recovery| boolean| No| true
codec| codec| No| "json"
connect_retry_interval| number| No| 1
connection_timeout| number| No|
durable| boolean| No| true
exchange| string| Yes|
exchange_type| string, one of ["fanout", "direct", "topic"]| Yes|
heartbeat| number| No|
host| string| Yes|
key| string| No| "logstash"
passive| boolean| No| false
password| password| No| "guest"
persistent| boolean| No| true
port| number| No| 5672
ssl| boolean| No| false
user| string| No| "guest"
verify_ssl| boolean| No| false
vhost| string| No| "/"
workers| number| No| 1

#### 详情


**arguments**
- 值类型是数组
- 默认值为{}

**automatic_recovery**
- 值类型是布尔值
- 默认值为true

**codec**
- 值类型是编解码器
- 默认值为“json”

用于输出数据的编解码器。输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。


**connect_retry_interval**
- 值类型是数字
- 默认值为1

**connection_timeout**
- 值类型是数字
- 此设置没有默认值。

**debug (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是布尔值
- 默认值为false

启用或禁用日志记录


**durable**
- 值类型是布尔值
- 默认值为true

这种交换是否耐用？ （aka;它应该存活经纪人重新启动吗？）


**exchange**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

交换的名称


**exchange_type**
- 这是必需的设置。
- 值可以是以下任意值：fanout，direct，topic
- 此设置没有默认值。

交换类型（fanout，topic，direct）


**heartbeat**
- 值类型是数字
- 此设置没有默认值。

**host**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

**key**
- 值类型是字符串
- 默认值为“logstash”

默认路由到的键。默认为logstash

在fanout交换上忽略路由密钥。

**passive**
- 值类型是布尔值
- 默认值为false

**password**
- 值类型为密码
- 默认值为“guest”

**persistent**
- 值类型是布尔值
- 默认值为true

RabbitMQ应该将消息持久化到磁盘吗？


**port**
- 值类型是数字
- 默认值为5672

**ssl**
- 值类型是布尔值
- 默认值为false

**user**
- 值类型是字符串
- 默认值为“guest”

**verify_ssl**
- 值类型是布尔值
- 默认值为false

验证SSL证书


**vhost**
- 值类型是字符串
- 默认值为“/”

要使用的vhost。如果你不知道这是什么，离开默认。


**workers**
- 值类型是数字
- 默认值为1

用于此输出的工人数。请注意，此设置可能不适用于所有输出。

### redis
此输出将使用RPUSH将事件发送到Redis队列。 Redis v0.0.7 +中支持RPUSH命令。 对一个频道使用PUBLISH至少需要v1.3.8 +。 虽然你可以使这些Redis版本工作，最好的性能和稳定性将在最近的稳定版本中找到。 建议使用2.6.0+版本。

有关更多信息，请参阅[Redis主页](http://redis.io/)

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
redis {
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
batch|boolean|No|false
batch_events|number|No|50
batch_timeout|number|No|5
codec|codec|No|"plain"
congestion_interval|number|No|1
congestion_threshold|number|No|0
data_type|string, one of ["list", "channel"]|No|
db|number|No|0
host|array|No|["127.0.0.1"]
key|string|No|
password|password|No|
port|number|No|6379
reconnect_interval|number|No|1
shuffle_hosts|boolean|No|true
timeout|number|No|5
workers|number|No|1

#### 详情

**batch**
- 值类型是布尔值
- 默认值为false

如果希望Redis对值进行批处理并发送1个RPUSH命令而不是每个值的一个命令来推送列表，请设置为true。注意，这只适用于data_type =“list”模式。

如果为true，我们发送一个RPUSH每“batch_events”事件或“batch_timeout”秒（以先到者为准）。只支持data_type为“list”。

**batch_events**
- 值类型是数字
- 默认值为50

如果batch设置为true，我们为RPUSH排队的事件数。

**batch_timeout**
- 值类型是数字
- 默认值为5

如果batch设置为true，则在有待清除事件时RPUSH命令之间的最大时间量。

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输出数据的编解码器。输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。


**congestion_interval**
- 值类型是数字
- 默认值为1

检查拥塞的频率。默认值为1秒。零意味着检查每个事件。

**congestion_threshold**
- 值类型是数字
- 默认值为0

如果Redis data_type是列表并且具有多于`@congestion_threshold`项，阻塞直到有人使用它们并减少拥塞，否则如果没有消费者，Redis将耗尽内存，除非它配置了OOM保护。但是即使使用OOM保护，单个Redis列表也可以阻止Redis的所有其他用户，直到Redis CPU消耗达到允许的最大RAM大小。默认值为0表示禁用此限制。仅支持列表Redis data_type。

**data_type**
值可以是以下任何值：list，channel
此设置没有默认值。
列表或频道。如果redis_type是list，那么我们将设置RPUSH为key。如果redis_type是channel，那么我们将PUBLISH改为key。

**db**
- 值类型是数字
- 默认值为0

Redis数据库号。

**host**
- 值类型是数组
- 默认值为[“127.0.0.1”]

您的Redis服务器的主机名。端口可以​​在任何主机名上指​​定，这将覆盖全局端口配置。

例如：
```
"127.0.0.1"
["127.0.0.1", "127.0.0.2"]
["127.0.0.1:6380", "127.0.0.1"]
```

**key**
- 值类型是字符串
- 此设置没有默认值。

Redis列表或通道的名称。动态名称在此处有效，例如, `logstash-%{type}`.

**name (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是字符串
- 默认值为“default”

名称用于在有多个实例的情况下进行日志记录。

**password**
- 值类型为密码
- 此设置没有默认值。

要验证的密码。默认情况下没有身份验证。

**port**
- 值类型是数字
- 默认值为6379

要连接的默认端口。可以覆盖任何主机名。

**queue (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是字符串
- 此设置没有默认值。

Redis队列的名称（我们将在此使用RPUSH）。动态名称在此有效，例如,`logstash-%{type}`

**reconnect_interval**
- 值类型是数字
- 默认值为1

重新连接到失败的Redis连接的间隔

**shuffle_hosts**
- 值类型是布尔值
- 默认值为true

在Logstash启动期间洗牌主机列表。

**timeout**
- 值类型是数字
- 默认值为5

Redis初始连接超时（以秒为单位）。


**workers**
- 值类型是数字
- 默认值为1

用于此输出的工人数。请注意，此设置可能不适用于所有输出。

### stdout

一个简单的输出，打印到运行Logstash的shell的STDOUT。 当调试插件配置时，通过允许在事件数据通过输入和过滤器之后立即访问该事件数据，此输出可以非常方便。

例如，以下输出配置与Logstash -e命令行标志一起，将允许您查看事件管道的结果，以便快速迭代。
```
output {
  stdout {}
}
```
有用的编解码器包括：

rubydebug: 使用ruby“awesome_print”库输出事件数据
```
output {
  stdout { codec => rubydebug }
}
```
json: 以结构化JSON格式输出事件数据
```
output {
  stdout { codec => json }
}
```
#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
stdout {
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
codec|codec|No|"line"
workers|number|No|1

#### 详情

**codec**
- 值类型是编解码器
- 默认值为“line”

用于输出数据的编解码器。 输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**workers**
- 值类型为数字
- 默认值为1

用于此输出的工人数。 请注意，此设置可能不适用于所有输出。

### tcp
通过TCP套接字写事件。

每个事件json由换行符分隔。

可以接受来自客户端的连接或连接到服务器，具体取决于模式。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
tcp {
    host => ...
    port => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
codec|codec|No|"json"
host|string|Yes|
mode|string, one of ["server", "client"]|No|"client"
port|number|Yes|
reconnect_interval|number|No|10
workers|number|No|1

#### 详情
**codec**
- 值类型是编解码器
- 默认值为“json”

用于输出数据的编解码器。输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**host**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

当模式是服务器时，地址要监听。当模式为客户端时，连接的地址。

**message_format (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是字符串
- 此设置没有默认值。

将事件写入文件时使用的格式。此值支持任何字符串，并且可以包括％{name}和其他动态字符串。

**mode**
- 值可以是以下任意值：server, client
- 默认值为“client”

模式操作。服务器侦听客户端连接，客户端连接到服务器。

**port**
- 这是必需的设置。
- 值类型是数字
- 此设置没有默认值。

当模式是服务器时，端口要监听。当模式为客户端时，连接到的端口。

**reconnect_interval**
- 值类型是数字
- 默认值为10

当连接失败时，请以秒为单位重试间隔。

**workers**
- 值类型是数字
- 默认值为1

用于此输出的工人数。请注意，此设置可能不适用于所有输出。

### udp
通过UDP发送事件

请记住，UDP将丢失消息。
#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
udp {
    host => ...
    port => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
codec|codec|No|"json"
host|string|Yes|
port|number|Yes|
workers|number|No|1

#### 详情

**codec**
- 值类型是编解码器
- 默认值为“json”

用于输出数据的编解码器。 输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**host**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

发送邮件的地址

**port**
- 这是必需的设置。
- 值类型为数字
- 此设置没有默认值。

发送邮件的端口

**workers**
- 值类型为数字
- 默认值为1

用于此输出的工人数。 请注意，此设置可能不适用于所有输出。


### websocket
这是一个社区维护的插件！ 它默认不随Logstash一起提供，但它很容易安装通过运行bin / logstash-plugin install logstash-output-websocket。

此输出运行websocket服务器并将所有消息发布到所有连接的websocket客户端。

您可以使用`ws://<host\>:<port\>/`

如果没有连接客户端，则忽略接收的任何消息。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
websocket {
}
```
可用配置选项：

|Setting	|Input type	|Required	|Default value
|--------|-----------|---------|-------------
|codec|codec|No|"plain"
|host|string|No|"0.0.0.0"
|port|number|No|3232
|workers|number|No|1

#### 详情

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输出数据的编解码器。 输出编解码器是一种方便的方法，用于在离开输出之前对数据进行编码，而无需在Logstash管道中使用单独的过滤器。

**host**
- 值类型是字符串
- 默认值为“0.0.0.0”

从中提供websocket数据的地址

**port**
- 值类型为数字
- 默认值为3232

从中提供websocket数据的端口

**workers**
- 值类型为数字
- 默认值为1

用于此输出的工人数。 请注意，此设置可能不适用于所有输出。
