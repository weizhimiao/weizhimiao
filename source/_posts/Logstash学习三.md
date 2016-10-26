---
title: Logstash学习三
date: 2016-10-25 20:30:00
tags:
- Logstash
categories:
- Logstash
---

- 性能故障排除指南
- 使用插件
- 输入插件

<!-- more -->

## 性能故障排除指南
您可以使用此故障排除指南快速诊断和解决Logstash性能问题。 对管线内部的高级知识不需要理解本指南。 然而，如果你想超越本指南，建议阅读管道文档。

您可能会试图前进并更改设置，如-w作为第一次尝试提高性能。 根据我们的经验，更改此设置使得更难以排除性能问题，因为您增加了正在使用的变量数。 相反，每次进行一次更改并测量结果。 从这个列表的末尾开始是一个确定的方式来创建一个混乱的情况。

### 性能清单

1. 检查输入源和输出目的地的性能：
  - Logstash只有它连接的服务一样快。 Logstash只能消耗和产生数据，因为它的输入和输出目的地可以！


2. 检查系统统计信息：
  - CPU
    - 请注意CPU是否被大量使用。在Linux / Unix上，您可以运行top -H以查看线程分解的进程统计信息，以及总CPU统计信息。
    - 如果CPU使用率很高，请跳到有关检查JVM堆的部分，然后阅读有关调整Logstash工作线程设置的部分。
  - Memory
    - 请注意Logstash在Java VM上运行的事实。这意味着Logstash将始终使用您分配给它的最大内存量。
    - 查找使用大量内存的其他应用程序，并可能导致Logstash切换到磁盘。如果应用程序使用的总内存超过物理内存，则会发生这种情况。
  - I / O利用率
    - 监视磁盘I / O以检查磁盘饱和。
      - 如果您使用Logstash插件（例如文件输出），可能会使存储饱和，则可能会出现磁盘饱和。
      - 磁盘饱和也可能发生，如果你遇到很多错误，强制Logstash生成大的错误日志。
      - 在Linux上，可以使用iostat，dstat或类似于监视磁盘I / O的东西。
    - 监视网络I / O以实现网络饱和。
      - 如果您使用执行大量网络操作的输入/输出，则可能发生网络饱和。
      - 在Linux上，可以使用诸如dstat或iftop之类的工具来监视网络。

3. 检查JVM堆：
  - 通常情况下，如果堆大小太低，CPU利用率可以通过屋顶，导致JVM不断进行垃圾回收。
  - 检查此问题的快速方法是将堆大小加倍，并查看性能是否提高。 不要增加超过物理内存量的堆大小。 为操作系统和其他进程保留至少1GB的空闲空间。
  - 您可以使用随Java分发的jmap命令行实用程序或使用VisualVM对JVM堆进行更准确的度量。

4. 调整Logstash工作线程设置：
  - 首先使用-w标志扩大管道工作线程的数量。 这将增加可用于过滤器和输出的线程数。 如果需要，可以安全地将其扩展到多个CPU内核，因为线程可以在I / O上变为空闲。
  - 默认情况下，每个输出只能在单个管道工作线程中处于活动状态。 您可以通过更改每个输出的配置块中的workers设置来增加此值。 不要使此值大于管道工人的数量。
  - 您还可以调整输出批处理大小。 对于许多输出，例如Elasticsearch输出，此设置将对应于I / O操作的大小。 在Elasticsearch输出的情况下，此设置对应于批处理大小。


## 使用插件

Logstash有丰富的输入，过滤器，编解码器和输出插件。 插件可以作为自包含的包称为gems并托管在RubyGems.org上。 通过bin / logstash-plugin脚本访问的插件管理器用于管理Logstash部署中的插件的生命周期。 您可以使用下面描述的命令行界面（CLI）调用来安装，卸载和升级插件。

### 使用插件
#### 查看插件
Logstash发行包捆绑公共插件，以便您可以立即使用它们。 要列出部署中当前可用的插件：
```
bin/logstash-plugin list
bin/logstash-plugin list --verbose
bin/logstash-plugin list '*namefragment*'
bin/logstash-plugin list --group output
```
- 将列出所有已安装的插件
- 将列出已安装的插件与版本信息
- 将列出所有已安装的包含namefragment的插件
- 将列出特定组的所有已安装的插件（输入，过滤器，编解码器，输出）

#### 向部署中添加插件
处理插件安装时最常见的情况是您可以访问互联网。 使用此方法，您将能够检索托管在公共存储库（RubyGems.org）上的插件，并安装在Logstash安装之上。
```
bin / logstash-plugin install logstash-output-kafka
```
插件成功安装后，您可以开始在配置文件中使用它。

##### 高级：添加本地构建的插件
在某些情况下，您想要安装尚未发布并且未托管在RubyGems.org上的插件。 Logstash提供了安装本地构建的插件的选项，该插件包装为ruby gem。 使用文件位置：
```
bin / logstash-plugin install /path/to/logstash-output-kafka-1.0.0.gem
```
##### 高级：使用--pluginpath
使用--pluginpath标志，可以加载位于文件系统上的插件源代码。 通常，这是由开发人员使用的迭代在一个自定义插件，并希望在创建ruby宝石之前测试。
```
bin / logstash --pluginpath /opt/shared/lib/logstash/input/my-custom-plugin-code.rb
```

#### 更新插件
插件有自己的发布周期，通常独立于Logstash的核心发布周期发布。 使用update子命令，您可以获取最新的或更新到特定版本的插件。
```
bin / logstash-plugin更新
bin / logstash-plugin update logstash-output-kafka
```
- 将更新所有已安装的插件
- 将只更新此插件

#### 删除插件
如果您需要从Logstash安装中删除插件：
```
bin / logstash-plugin卸载logstash-output-kafka
```

#### 代理支持
前面的部分依赖于Logstash能够与RubyGems.org通信。 在某些环境中，转发代理用于处理HTTP请求。 通过设置HTTP_PROXY环境变量，可以通过代理安装和更新Logstash插件：
```
export HTTP_PROXY=http://127.0.0.1:3128

bin/logstash-plugin install logstash-output-kafka
```
一旦设置，插件命令安装，更新可以通过这个代理使用。

### 生成插件
现在，您可以在几秒钟内创建自己的Logstash插件！ bin / logstash-plugin的generate子命令为带有模板化文件的新Logstash插件创建基础。 它创建正确的目录结构，gemspec文件和依赖关系，以便您可以开始添加自定义代码以使用Logstash处理数据。

用法示例
```
bin/logstash-plugin generate --type input --name xkcd --path ~/ws/elastic/plugins
```
--type：插件的类型 - input(输入), filter(过滤器), output(输出), or codec(编解码器)
--name：新插件的名称
--path：将创建新插件结构的目录路径。 如果未指定，它将在当前目录中创建。

### 离线插件管理
Logstash插件管理器在1.5版本中引入。 本节讨论设置插件的本地存储库，以便在无法访问Internet的系统上使用。

本节中的过程需要运行Logstash的暂存机器，该Logstash可以访问公共或私有Rubygems服务器。 此暂存计算机下载并打包用于脱机安装的文件。

有关设置您自己的专用Rubygems服务器的信息，请参阅私有Gem Repositories部分。

可以使用更大的Logstash工件大小的用户可以使用Logstash产品页面中的Logstash（所有插件）下载链接下载与所有可用插件的最新版本捆绑在一起的Logstash。 您可以将此捆绑包分发到所有节点，而无需进一步插件分级。

#### 构建离线包
使用离线插件需要您创建一个离线包，这是一个压缩文件，包含您的离线Logstash安装所需的所有插件，以及这些插件的依赖关系。
使用bin / logstash-plugin pack子命令创建脱机包。

1. 当您运行bin / logstash-plugin pack子命令时，Logstash会创建一个压缩包，其中包含当前安装的所有插件以及这些插件的依赖关系。 默认情况下，当您在UNIX计算机上运行bin / logstash-plugin pack子命令时，压缩包是一个GZipped TAR文件。 默认情况下，在Windows计算机上运行bin / logstash-plugin pack子命令时，压缩包是ZIP文件。 有关更改这些默认行为的详细信息，请参阅管理插件包。
> 注意: 下载指定插件的所有依赖关系可能需要一些时间，具体取决于列出的插件。

2. 将压缩包移动到作为脱机插件安装源的脱机计算机，然后使用bin / logstash-plugin unpack子命令使打包的插件可用。


#### 安装或更新本地插件
要安装或更新本地插件，请在安装和更新命令中使用--local选项，如以下示例所示：

示例1。 安装本地插件
```
bin/logstash-plugin install --local logstash-input-jdbc
```

示例2.更新本地插件
```
bin/logstash-plugin update --local logstash-input-jdbc
```

示例3.在一个命令中更新所有本地插件
```
bin/logstash-plugin update --local
```

#### 管理插件包

`bin / logstash-plugin` 的pack和unpack子命令采用以下选项：

- --tgz
> 生成脱机包作为GZipped TAR文件。 UNIX系统上的默认行为。

- --zip
> 生成脱机包为ZIP文件。 Windows系统上的默认行为。

- [packname] --override
> 生成新的脱机包，使用指定的名称覆盖现有脱机包。 [packname] - [no-] clean：删除与指定名称匹配的脱机包。

### Private Gem库
Logstash插件管理器连接到Ruby gems资源库以安装和更新Logstash插件。 默认情况下，此存储库为http://rubygems.org。

某些用例无法使用默认存储库，如以下示例所示：

- 防火墙阻止对默认存储库的访问。
- 您正在本地开发自己的插件。
- 气隙对本地系统的要求。

当您使用自定义gem存储库时，请确保提供插件依赖。

几个开源项目使您能够运行自己的插件服务器，其中包括：
- [Geminabox](https://github.com/geminabox/geminabox)
- [Gemirro](https://github.com/PierreRambaud/gemirro)
- [Gemfury](https://gemfury.com/)
- [Artifactory](http://www.jfrog.com/open-source/)

#### 编辑Gemfile
gemfile是一个配置文件，指定插件管理所需的信息。 每个gem文件都有一个源行，用于指定插件内容的位置。

默认情况下，gemfile的源代码行为：

```
# This is a Logstash generated Gemfile.
# If you modify this file manually all comments and formatting will be lost.

source "https://rubygems.org"
```
要更改源，请编辑源行以包含首选源，如以下示例所示：
```
# This is a Logstash generated Gemfile.
# If you modify this file manually all comments and formatting will be lost.

source "https://my.private.repository"
```
保存新版本的gemfile后，正常使用插件管理命令。

以下链接包含有关设置一些常用存储库的其他资料：

- [Geminabox](https://github.com/geminabox/geminabox/blob/master/README.markdown)
- [Artifactory](https://www.jfrog.com/confluence/display/RTF/RubyGems+Repositories)
- Running a [rubygems mirror](http://guides.rubygems.org/run-your-own-gem-server/)

## 输入插件

输入插件使得Logstash可以读取特定的事件源。

提供以下输入插件：

**beats**

> 从Elastic Beats框架接收事件

[logstash-input-beats](https://github.com/logstash-plugins/logstash-input-beats)

**couchdb_changes**

> 从CouchDB流的事件_changes URI

[logstash-input-couchdb_changes](https://github.com/logstash-plugins/logstash-input-couchdb_changes)

**drupal_dblog**

> 从启用DBLog的Drupal安装中检索看门狗日志事件

[logstash-input-drupal_dblog](https://github.com/logstash-plugins/logstash-input-drupal_dblog)

**elasticsearch**

> 从Elasticsearch集群读取查询结果

[logstash-input-elasticsearch](https://github.com/logstash-plugins/logstash-input-elasticsearch)

**exec**

> 捕获shell命令的输出作为事件

[logstash-input-exec](https://github.com/logstash-plugins/logstash-input-exec)

**eventlog**

> 从Windows事件日志中提取事件

[logstash-input-eventlog](https://github.com/logstash-plugins/logstash-input-eventlog)

**file**

> 从文件流流式传输事件

[logstash-input-file](https://github.com/logstash-plugins/logstash-input-file)

**ganglia**

> 通过UDP读取Ganglia数据包

[logstash-input-ganglia](https://github.com/logstash-plugins/logstash-input-ganglia)

**gelf**

> 从Graylog2读取GELF格式的消息作为事件

[logstash-input-gelf](https://github.com/logstash-plugins/logstash-input-gelf)

**generator**

> 生成用于测试目的的随机日志事件

[logstash-input-generator](https://github.com/logstash-plugins/logstash-input-generator)

**graphite**

> 从graphite工具读取指标

[logstash-input-graphite](https://github.com/logstash-plugins/logstash-input-graphite)

**github**

> 从GitHub webhook读取事件

[logstash-input-github](https://github.com/logstash-plugins/logstash-input-github)

**heartbeat**

> 生成测试用的心跳事件

[logstash-input-heartbeat](https://github.com/logstash-plugins/logstash-input-heartbeat)

**heroku**

> 从Heroku应用程序的日志中流式传输事件

[logstash-input-heroku](https://github.com/logstash-plugins/logstash-input-heroku)

**http**

> 通过HTTP或HTTPS接收事件

[logstash-input-http](https://github.com/logstash-plugins/logstash-input-http)

**http_poller**

> 将HTTP API的输出解码为事件

[logstash-input-http_poller](https://github.com/logstash-plugins/logstash-input-http_poller)

**irc**

> 从IRC服务器读取事件

[logstash-input-irc](https://github.com/logstash-plugins/logstash-input-irc)

**imap**

> 从IMAP服务器读取电子邮件

[logstash-input-imap](https://github.com/logstash-plugins/logstash-input-imap)

**jdbc**

> 从JDBC数据创建事件

[logstash-input-jdbc](https://github.com/logstash-plugins/logstash-input-jdbc)

**jmx**

> 通过JMX从远程Java应用程序检索指标

[logstash-input-jmx](https://github.com/logstash-plugins/logstash-input-jmx)

**kafka**

> 读取Kafka主题的事件

[logstash-input-kafka](https://github.com/logstash-plugins/logstash-input-kafka)

**log4j**

> 从Log4j SocketAppender对象通过TCP套接字读取事件

[logstash-input-log4j](https://github.com/logstash-plugins/logstash-input-log4j)

**lumberjack**

> 使用Lumberjack协议接收事件

[logstash-input-lumberjack](https://github.com/logstash-plugins/logstash-input-lumberjack)

**meetup**

> 作为事件捕获命令行工具的输出

[logstash-input-meetup](https://github.com/logstash-plugins/logstash-input-meetup)

**pipe**

> 从长时间运行的命令管道流出事件

[logstash-input-pipe](https://github.com/logstash-plugins/logstash-input-pipe)

**puppet_facter**

> 从Puppet服务器接收事实

[logstash-input-puppet_facter](https://github.com/logstash-plugins/logstash-input-puppet_facter)

**relp**

> 通过TCP套接字接收RELP事件

[logstash-input-relp](https://github.com/logstash-plugins/logstash-input-relp)

**rss**

> 作为事件捕获命令行工具的输出

[logstash-input-rss](https://github.com/logstash-plugins/logstash-input-rss)

**rackspace**

> 从Rackspace Cloud Queue服务接收事件

[logstash-input-rackspace](https://github.com/logstash-plugins/logstash-input-rackspace)

**rabbitmq**

> 从RabbitMQ交换中提取事件

[logstash-input-rabbitmq](https://github.com/logstash-plugins/logstash-input-rabbitmq)

**redis**

> 从Redis实例读取事件

[logstash-input-redis](https://github.com/logstash-plugins/logstash-input-redis)

**salesforce**

> 基于Salesforce SOQL查询创建事件

[logstash-input-salesforce](https://github.com/logstash-plugins/logstash-input-salesforce)

**snmptrap**

> 基于SNMP陷阱消息创建事件

[logstash-input-snmptrap](https://github.com/logstash-plugins/logstash-input-snmptrap)

**stdin**

> 从标准输入读取事件

[logstash-input-stdin](https://github.com/logstash-plugins/logstash-input-stdin)

**sqlite**

> 基于SQLite数据库中的行创建事件

[logstash-input-sqlite](https://github.com/logstash-plugins/logstash-input-sqlite)

**s3**

> 从S3存储桶中的文件流传输事件

[logstash-input-s3](https://github.com/logstash-plugins/logstash-input-s3)

**sqs**

> 从Amazon Web Services简单队列服务队列中提取事件

[logstash-input-sqs](https://github.com/logstash-plugins/logstash-input-sqs)

**stomp**

> 创建使用STOMP协议接收的事件

[logstash-input-stomp](https://github.com/logstash-plugins/logstash-input-stomp)

**syslog**

> 将syslog消息读为事件

[logstash-input-syslog](https://github.com/logstash-plugins/logstash-input-syslog)

**tcp**

> 从TCP套接字读取事件

[logstash-input-tcp](https://github.com/logstash-plugins/logstash-input-tcp)

**twitter**

> 从Twitter Streaming API读取事件

[logstash-input-twitter](https://github.com/logstash-plugins/logstash-input-twitter)

**unix**

> 通过UNIX套接字读取事件

[logstash-input-unix](https://github.com/logstash-plugins/logstash-input-unix)

**udp**

> 通过UDP读取事件

[logstash-input-udp](https://github.com/logstash-plugins/logstash-input-udp)

**varnishlog**

> 从varnish缓存中读取共享内存日志

[logstash-input-varnishlog](https://github.com/logstash-plugins/logstash-input-varnishlog)

**wmi**

> 基于WMI查询的结果创建事件

[logstash-input-wmi](https://github.com/logstash-plugins/logstash-input-wmi)

**websocket**

> 从websocket读取事件

[logstash-input-websocket](https://github.com/logstash-plugins/logstash-input-websocket)

**xmpp**

> 通过XMPP / Jabber协议接收事件

[logstash-input-xmpp](https://github.com/logstash-plugins/logstash-input-xmpp)

**zenoss**

> 从fanout交换机读取Zenoss事件

[logstash-input-zenoss](https://github.com/logstash-plugins/logstash-input-zenoss)

**zeromq**

> 从ZeroMQ SUB插槽读取事件

[logstash-input-zeromq](https://github.com/logstash-plugins/logstash-input-zeromq)


### beats
这个输入插件使Logstash能够接收来自Elastic Beats框架的事件。

以下示例显示如何配置Logstash在端口5044上侦听传入的Beats连接并索引到Elasticsearch：
```
input {
  beats {
    port => 5044
  }
}

output {
  elasticsearch {
    hosts => "localhost:9200"
    manage_template => false
    index => "%{[@metadata][beat]}-%{+YYYY.MM.dd}"
    document_type => "%{[@metadata][type]}"
  }
}
```
“beats”会自动在事件上设置类型字段。 您不能在Logstash配置中覆盖此设置。 如果在Logstash中为类型配置选项指定了一个设置，则会被忽略。

#### 概要
此插件支持以下配置选项：

所需的配置选项：
```
beats {
    port => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
------------|-------------|--------|-----------
add_field   |hash         |No      |{}
cipher_suites|array       |No      |
client_inactivity_timeout|number|No|15
codec       |codec        |No      | "plain"
congestion_threshold|number|No     |5
host        |string       |No      |"0.0.0.0"
include_codec_tag|boolean |No      |true
port        |number       |Yes     |
ssl         |boolean      |No      |false
ssl_certificate|a valid filesystem path|No|
ssl_certificate_authorities|array|No|[]
ssl_handshake_timeout|number|No    |10000
ssl_key|a valid filesystem path|No |
ssl_key_passphrase|password|No     |
ssl_verify_mode|string, one of ["none", "peer", "force_peer"]|No|"none"
tags        |array        |No      |
tls_max_version|number    |No      |1.2
tls_min_version|number    |No      |1
type        |string       |No      |


##### 详情
 

**add_field**
- 值类型是哈希
- 默认值为{}
向事件添加字段

**cipher_suites**
- 值类型是数组
- 默认值为java.lang.String [TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA38，TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384，TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256，TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256，TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384，TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384，TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256] // @ 210af31f

要使用的密码套件列表，按优先级列出。



**client_inactivity_timeout**
- 值类型是数字
- 默认值为15

在X秒钟不活动后关闭空闲客户端。


**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。


**congestion_threshold**

- 值类型是数字
- 默认值为5

在我们提出超时之前的秒数。此选项很有用控制多少时间来等待，如果事情是阻止管道。



**host**
- 值类型是字符串
- 默认值为“0.0.0.0”

要监听的IP地址。



**include_codec_tag**
- 值类型是布尔值
- 默认值为true

**port**
- 这是必需的设置。
- 值类型是数字
- 此设置没有默认值。

要监听的端口。

**ssl**
- 值类型是布尔值
- 默认值为false

事件默认情况下以纯文本发送。你可以通过设置SSL为true，并配置ssl_certificate和ssl_key选项启用加密。

**ssl_certificate**
- 值类型为路径
- 此设置没有默认值。
要使用的SSL证书。

**ssl_certificate_authorities**
- 值类型是数组
- 默认值为[]

根据这些权限验证客户端证书。您可以定义多个文件或路径。将读取所有证书并将其添加到信任存储区。您需要配置ssl_verify_mode同行或force_peer启用验证。

此功能只支持直接通过你的根CA签署的证书当前不支持中间CA.


**ssl_handshake_timeout**
- 值类型是数字
- 缺省值为10000

时间以毫秒为单位一个不完整的SSL握手超时

**ssl_key****
- 值类型为路径
- 此设置没有默认值。

要使用的SSL密钥。

**ssl_key_passphrase**
- 值类型为密码
- 此设置没有默认值。

要使用的SSL密钥密码。

**ssl_verify_mode**
- 值可以是以下任何值：none，peer，force_peer
- 默认值为“none”

默认情况下，服务器不执行任何客户端验证。

同行就会使服务器要求客户提供证书。如果客户端提供证书，它将被验证。

force_peer将使服务器要求客户端提供证书。如果客户端不提供证书，连接将关闭。

此选项需要与ssl_certificate_authorities和定义的CA列表一起使用。

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。


**target_field_for_codec (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是字符串
- 默认值为“message”

这是将应用指定的编解码器的默认字段。

**tls_max_version**
- 值类型是数字
- 默认值为1.2

加密连接允许的最大TLS版本。该值必须为以下值之一：TLS 1.0为1.0，TLS 1.1为1.1，TLS 1.2为1.2

**tls_min_version**
- 值类型是数字
- 默认值为1

加密连接允许的最低TLS版本。该值必须为以下值之一：TLS 1.0为1.0，TLS 1.1为1.1，TLS 1.2为1.2

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

### couchdb_changes
此CouchDB输入允许您从CouchDB \_changes URI自动流事件。 此外，任何“未来”更改将自动流式传输，以便轻松将CouchDB数据与任何目标目标同步

＃Upsert和delete可以使用事件元数据来允许删除文档。 所有非删除操作都被视为上行插入

＃从特定序列开始CouchDB输入存储由sequence_path定义的位置中的最后序列号值。 您可以使用此事实以特定顺序启动或恢复流。

#### 概要
此插件支持以下配置选项：
所需的配置选项：
```
couchdb_changes {
    db => ...
}
```
可用配置选项：

Setting	         |Input type       	|Required|Default value
-----------------|-------------------|------|-------
add_field        |hash               |No    |{}
always_reconnect |boolean            |No    |true
ca_file          |a valid filesystem path|No|
codec            |odec               |No    |"plain"
db               |string             |Yes   |
heartbeat        |number             |No    |1000
host             |string             |No    |"localhost"
ignore_attachments|boolean           |No    |true
initial_sequence |number             |No    |
keep_revision    |boolean            |No    |false
password         |password           |No    |nil
port             |number             |No    |5984
reconnect_delay  |number             |No    |10
secure           |boolean            |No    |false
sequence_path    |string             |No    |
tags             |array              |No    |
timeout          |number             |No    |
type             |string             |No    |
username         |string             |No    |nil

##### 详情

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**always_reconnect**
- 值类型是布尔值
- 默认值为true

重新连接标志。当为true时，总是尝试在失败后重新连接

**ca_file**
- 值类型为路径
- 此设置没有默认值。

CA证书文件的路径，用于验证证书

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**db**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

要连接到的CouchDB数据库。必需参数。

**heartbeat**
- 值类型是数字
- 默认值为1000

Logstash连接到CouchDB的_changes with feed = continuous心跳是多久（以毫秒为单位）Logstash将ping CouchDB以确保连接被维护。不建议更改此设置，除非您知道您在做什么。

**host**
- 值类型是字符串
- 默认值为“localhost”
- IP或CouchDB实例的主机名

**ignore_attachments**
- 值类型是布尔值
- 默认值为true

未来功能！直到实现，改变这个从默认不会做任何事情。

忽略与CouchDB文档关联的附件。

**initial_sequence**
- 值类型是数字
- 此设置没有默认值。

如果未指定，Logstash将尝试从sequence_path文件读取最后一个序列号。如果它是空的或不存在，它将从0开始。

如果指定此值，则预计您将只在特殊情况下进行初始读取，并且此后您将取消设置此值。

**keep_revision**
- 值类型是布尔值
- 默认值为false

保留输出中的CouchDB文档版本“`_rev`”值。

**password**
- 值类型为密码
- 默认值为nil

密码，如果需要认证以连接到CouchDB

**port**
- 值类型是数字
- 默认值为5984

您的CouchDB实例的端口。

**reconnect_delay**
- 值类型是数字
- 默认值为10

重新连接延迟：重新连接尝试之间的时间（以秒为单位）。

**secure**
- 值类型是布尔值
- 默认值为false

安全地连接到CouchDB的_changes订阅源（通过https）默认值：false（通过http）


**sequence_path**
- 值类型是字符串
- 此设置没有默认值。

存储_changes流中最后一个序列号的文件路径。如果取消设置，它将写入$ HOME / .couchdb_seq


**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**timeout**
- 值类型是数字
- 此设置没有默认值。

超时：在终止连接之前等待新数据的毫秒数。如果设置了超时，它将禁用心跳配置选项。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

**username**
- 值类型是字符串
- 默认值为nil

用户名，如果需要认证以连接到CouchDB


### elasticsearch

从Elasticsearch群集中根据搜索查询结果读取。 这对于重放测试日志，重建索引等非常有用。

例：
```
input {
  # Read all documents from Elasticsearch matching the given query
  elasticsearch {
    hosts => "localhost"
    query => '{ "query": { "match": { "statuscode": 200 } }, "sort": [ "_doc" ] }'
  }
}
```
这将创建具有以下格式的Elasticsearch查询：
```
curl 'http://localhost:9200/logstash-*/_search?&scroll=1m&size=1000' -d '{
  "query": {
    "match": {
      "statuscode": 200
    }
  },
  "sort": [ "_doc" ]
}'
```
#### 概要
此插件支持以下配置选项：

所需的配置选项：
```
elasticsearch {
}
```
可用的配置选项：

Setting	      |Input type	| Required	|  Default value
--------------|-----------|-----------|--------------------
add_field     | hash      | No        | {}
ca_file       | a valid filesystem path| No |
codec         | codec     | No        |"json"
docinfo       | boolean   | No        | false
docinfo_fields| array     | No        |["\_index", "\_type", "\_id"]
docinfo_target| string    | No        |"\@metadata"
hosts         | array     | No        |
index         | string    | No        |"logstash-\*"
password      | password  | No        |
query         | string    | No        |"{ \"sort\": [ \"\_doc\" ] }"
scroll        | string    | No        |"1m"
size          | number    | No        | 1000
ssl           | boolean   | No        | false
tags          | array     | No        |
type          | string    | No        |
user          | string    | No        |


#### 详细

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**ca_file**
- 值类型为路径
- 此设置没有默认值。

SSL证书授权文件

**codec**
- 值类型是编解码器
- 默认值为“json”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**docinfo**
- 值类型是布尔值
- 默认值为false

如果设置，请在事件中包括Elasticsearch文档信息，如索引，类型和ID。

关于元数据，可能需要注意的是，如果你正在接收文档，并且想要重新索引它们（或者只是更新它们），那么弹性搜索输出中的操作选项想要知道如何处理这些事情。它可以动态分配一个添加到元数据的字段。

例
```
input {
  elasticsearch {
    hosts => "es.production.mysite.org"
    index => "mydata-2018.09.*"
    query => "*"
    size => 500
    scroll => "5m"
    docinfo => true
  }
}
output {
  elasticsearch {
    index => "copy-of-production.%{[@metadata][_index]}"
    index_type => "%{[@metadata][_type]}"
    document_id => "%{[@metadata][_id]}"
  }
}
```

**docinfo_fields**
- 值类型是数组
- 默认值为`[“_index”，“_type”，“_id”]`

要移动到docinfo_target字段的文档元数据列表要了解有关Elasticsearch元数据字段的详细信息，请阅读http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/_document_metadata.html

**docinfo_target**
- 值类型是字符串
- 默认值为“@metadata”

默认情况下，在哪里移动Elasticsearch文档信息，我们使用@metadata字段。

**hosts**
- 值类型是数组
- 此设置没有默认值。

用于查询的elasticsearch主机列表。每个主机可以是IP，HOST，IP：端口或HOST：端口端口默认为9200

如果你不明确设置这个变量，Logstash会生成一个唯一的名字。

**index**
- 值类型是字符串
- 默认值为“`logstash-*`”

要搜索的索引或别名。

**password**
- 值类型为密码
- 此设置没有默认值。

Basic Auth - password

**query**
- 值类型是字符串
- 默认值为“`{\”sort \“：[\”_ doc \“]}`”

要执行的查询。有关详细信息，请阅读Elasticsearch查询DSL文档https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html

**scroll**
- 值类型是字符串
- 默认值为“1m”

此参数控制滚动请求的保持活动时间（以秒为单位），并启动滚动过程。每次往返（即，在上一个滚动请求与下一个滚动请求之间）应用超时。

**size**
- 值类型是数字
- 默认值为1000

这允许您设置每次滚动返回的最大命中数。

**ssl**
- 值类型是布尔值
- 默认值为false

SSL

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

**user**
- 值类型是字符串
- 此设置没有默认值。

Basic Auth - username

### exec

定期运行shell命令并将整个输出捕获为事件。

笔记：
- 此事件的命令字段将是命令运行。
- 此事件的消息字段将是命令的整个stdout。

#### 概要
此插件支持以下配置选项：

所需的配置选项：
```
exec {
    command => ...
    interval => ...
}
```
可用配置选项：

Setting	  |Input type	|Required	|Default value
----------|-----------|---------|-------------
add_field |hash       |No       |{}
codec     |codec      |No       |"plain"
command   |string     |Yes      |
interval  |number     |Yes      |
tags      |array      |No       |
type      |string     |No       |


#### Details


**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**command**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

命令运行。例如，uptime

**debug (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是布尔值
- 默认值为false

将此设置为true可对输入启用调试。

**interval**
- 这是必需的设置。
- 值类型是数字
- 此设置没有默认值。

运行命令的间隔。值以秒为单位。

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

### file
从文件流事件，通常通过拖尾它们以类似于尾-0F的方式，但可选地从开始读取它们。

默认情况下，每个事件假定为一行。 如果您希望将多个日志行连接到一个事件中，则需要使用多行编解码器或过滤器。

该插件旨在跟踪更改的文件，并发出新内容，因为它附加到每个文件。 它不太适合从头到尾读取文件，并将其存储在单个事件中（即使使用多线编解码器或过滤器）。

#### 监视文件中当前位置的跟踪
插件通过将其记录在名为sincedb的单独文件中来跟踪每个文件中的当前位置。这使得可以停止和重新启动Logstash，并让它从停止的位置选择，而不会丢失在Logstash停止时添加到文件的行。

默认情况下，sincedb文件放置在运行Logstash的用户的主目录中，文件名基于被监视的文件名模式（即路径选项）。因此，更改文件名模式将导致使用新的sincedb文件，并且任何现有的当前位置状态将丢失。如果你用任何频率改变模式，用sincedb_path选项显式选择一个sincedb路径可能是有意义的。

每个输入必须使用不同的sincedb_path。使用相同的路径将导致问题。每个输入的读取检查点必须存储在不同的路径中，因此信息不会覆盖。

Sincedb文件是具有四列的文本文件：
- inode号（或等效值）。
- 文件系统（或等效的）的主设备号。
- 文件系统的次设备号（或等效设备号）。
- 文件中当前的字节偏移量。

在非Windows系统上，您可以获取文件的索引节点号。 ls -li。


#### 文件旋转
文件旋转由此输入检测和处理，无论文件是通过重命名还是复制操作旋转。 要支持在旋转之后写入旋转文件一段时间的程序，请在文件名模式中包括原始文件名和旋转文件名（例如/ var / log / syslog和/var/log/syslog.1） 观看（路径选项）。 请注意，旋转的文件名将被视为一个新文件，因此如果start_position设置为开始旋转的文件将被重新处理。

使用默认值start_position（end）将任何写入文件末尾的消息（在旋转之前的最后一个读取操作和在新名称下重新打开之间的间隔（由stat_interval和discover_interval选项确定的间隔））将不会被拾取 。


#### 概要
此插件支持以下配置选项：

所需的配置选项：
```
file {
    path => ...
}
```
可用配置选项：

Setting	        |Input type	|Required	|Default value
----------------|-----------|---------|-----------
add_field       | hash      | No      |{}
close_older     | number    | No      | 3600
codec           | codec     | No      |"plain"
delimiter       | string    | No      |"\n"
discover_interval| number   | No      | 15
exclude         | array     | No      |
ignore_older    | number    | No      | 86400
max_open_files  | number    | No      |
path            | array     | Yes     |
sincedb_path    | string    | No      |
sincedb_write_interval| number| No    | 15
start_position  | string, one of ["beginning", "end"]| No"end"
stat_interval   | number    | No      | 1
tags            | array     | No      |
type            | string    | No      |


#### 细节


**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**close_older**
- 值类型是数字
- 默认值为3600

文件输入关闭上次在几秒钟前读取指定时间跨度的任何文件。这具有不同的含义，这取决于文件是否被拖尾或读取。如果拖尾，并且在传入数据中存在大的时间间隔，则可以关闭文件（允许打开其他文件），但是当检测到新数据时将排队等待重新打开。如果读取，该文件将在从读取最后一个字节后的closed_older秒后关闭。默认值为1小时

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**delimiter**
- 值类型是字符串
- 默认值为“\\n”

设置新的行分隔符，默认为“\\n”

**discover_interval**
- 值类型是数字
- 默认值为15

我们扩展路径选项中的文件名模式以发现新文件以观察的频率（以秒为单位）。

**exclude**
- 值类型是数组
- 此设置没有默认值。

排除（与文件名匹配，而不是完整路径）。文件名模式也在这里有效。例如，如果你有
```
path => "/var/log/*"
```
您可能希望排除gzip压缩文件：
```
exclude => "*.gz"
```

**ignore_older**
- 值类型是数字
- 默认值为86400

当文件输入发现在指定的时间间隔（以秒为单位）之前最后一次修改的文件时，该文件将被忽略。发现后，如果忽略的文件被修改，它不再被忽略，任何新的数据被读取。默认值为24小时。

**max_open_files**
- 值类型是数字
- 此设置没有默认值。

此输入在任何时间消耗的file_handles的最大数量是多少。如果需要处理比此数字更多的文件，请使用close_older关闭某些文件。这不应该设置为操作系统可以做的最大值，因为其他LS插件和OS进程需要文件句柄。在filewatch中设置默认值4095。

**path**
这是必需的设置。
值类型是数组
此设置没有默认值。
要用作输入的文件的路径。您可以在此处使用文件名模式，例如`/var/log/**/*.log`。如果使用类似`/var/log/**/*.log`的模式，将对所有`* .log`文件执行`/var/log `的递归搜索。路径必须是绝对的，不能是相对的。

您还可以配置多个路径。请参见Logstash配置页面上的示例。


**sincedb_path**
- 值类型是字符串
- 此设置没有默认值。

将写入磁盘的sincedb数据库文件的路径（记录被监视日志文件的当前位置）。默认情况下会将sincedb文件写入与`$HOME/.sincedb*`匹配的路径注意：它必须是文件路径，而不是目录路径

**sincedb_write_interval**
值类型是数字
默认值为15
使用受监视日志文件的当前位置写入自从数据库的频率（以秒为单位）。

**start_position**
- 值可以是以下任意值：beginning, end
- 默认值为“end”

选择Logstash最初开始读取文件的位置：开始或结束。默认行为处理像直播流这样的文件，因此从结束处开始。如果您有要导入的旧数据，请将其设置为开始。

此选项仅修改文件是新的且之前不可见的“第一接触”情况，即，没有当前位置的文件记录在由Logstash读取的sincedb文件中。如果以前已经看过一个文件，该选项不起作用，并且将使用记录在sincedb文件中的位置。

**stat_interval**
- 值类型是数字
- 默认值为1

stat文件的频率（以秒为单位），以查看它们是否已被修改。增加此间隔将减少我们进行的系统调用的数量，但增加检测新日志行的时间。

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。


### heartbeat

生成心跳消息。

这个的一般意图是测试Logstash的性能和可用性。

 

#### 概要
此插件支持以下配置选项：

所需的配置选项：
```
heartbeat {
}
```
可用的配置选项：

Setting	 |Input type	|Required	|Default value
---------|------------|---------|------------
add_field| hash       | No      |{}
codec    | codec      | No      |"plain"
count    | number     | No      |-1
interval | number     | No      | 60
message  | string     | No      |"ok"
tags     | array      | No      |
threads  | number     | No      | 1
type     | string     | No      |



#### 细节


**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**count**
- 值类型是数字
- 默认值为-1

迭代次数。这通常仅用于测试目的。

**interval**
- 值类型是数字
- 默认值为60

设置应发送邮件的频率。

默认值为60，表示每60秒发送一条消息。

**message**
- 值类型是字符串
- 默认值为“ok”

要在事件中使用的消息字符串。

如果将此设置为epoch，则此插件将使用unix时间戳（根据定义，UTC）中的当前时间戳。它将该值输出到称为时钟的字段

如果你设置为序列，然后这个插件将发送从0开始的序列号，并增加每个间隔。它将该值输出到称为时钟的字段

否则，此值将被逐字用作事件消息。它将该值输出到一个名为message的字段

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**threads**
- 值类型是数字
- 默认值为1

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。


### http
使用此输入，您可以通过http（s）接收单行或多行事件。应用程序可以向由此输入启动的端点发送具有正文的HTTP POST请求，Logstash会将其转换为事件以供后续处理。用户可以传递纯文本，JSON或任何格式的数据，并使用相应的编解码器与此输入。对于Content-Type application / json，使用json编解码器，但对于所有其他数据格式，使用纯编解码器。

此输入还可用于接收Webhook请求以与其他服务和应用程序集成。通过利用Logstash中可用的大量插件生态系统，您可以直接从应用程序触发可操作的事件。

#### 安全
此插件支持标准HTTP基本认证头以标识请求者。您可以在向此输入发送数据时传递用户名，密码组合

您还可以设置SSL并通过https安全地发送数据，并具有验证客户端证书的选项。目前，证书设置是通过Java Keystore格式



#### 概要
此插件支持以下配置选项：

所需的配置选项：
```
http {
}
```
可用配置选项：

Setting	          |Input type	|Required	|Default value
------------------|-----------|---------|--------------
add_field         |  hash     |  No     |  {}
additional_codecs |  hash     |  No     |  {"application/json"=>"json"}
codec             |  codec    |  No     |  "plain"
host              |  string   |  No     |  "0.0.0.0"
keystore          |  a valid filesystem path |  No|
keystore_password |  password |  No     |
password          |  password |  No     |
port              |  number   |  No     |  8080
response_headers  |  hash     |  No     |  {"Content-Type"=>"text/plain"}
ssl               |  boolean  |  No     |  false
tags              |  array    |  No     |
threads           |  number   |  No     |  4
type              |  string   |  No     |
user              |  string   |  No     |
verify_mode       |  string, one of ["none", "peer", "force_peer"] |  No |  "none"



#### 细节


**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**additional_codecs**
- 值类型是哈希
- 默认值为{“application / json”=>“json”}

为特定内容类型应用特定的编解码器。默认编解码器将仅在此列表选中并且未找到请求的内容类型的编解码器之后才应用

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**host**
- 值类型是字符串
- 默认值为“0.0.0.0”

编解码器用于解码输入数据。如果在“additional_codecs”散列中找不到内容类型，则此编解码器将用作后退。主机或ip绑定

**keystore**
- 值类型为路径
- 此设置没有默认值。

JKS密钥库用于验证客户端的证书

**keystore_password**
- 值类型为密码
- 此设置没有默认值。

设置信任库密码

**password**
- 值类型为密码
- 此设置没有默认值。

基本授权密码

**port**
- 值类型是数字
- 默认值为8080

要绑定的TCP端口

**response_headers**
- 值类型是哈希
- 默认值为{“Content-Type”=>“text / plain”}

指定一组自定义的响应头

**ssl**
- 值类型是布尔值
- 默认值为false

SSL配置

启用S​​SL

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**threads**
- 值类型是数字
- 默认值为4

要使用的最大线程数

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

**user**
- 值类型是字符串
- 此设置没有默认值。

基本授权的用户名

**verify_mode**
- 值可以是以下任何值：none，peer，force_peer
- 默认值为“none”

设置客户端证书验证方法。有效方法：none, peer, force_peer

### kafka
此输入将读取来自Kafka主题的事件。 它使用Kafka提供的高级消费者API从代理读取消息。 它还维护使用Zookeeper消耗的状态。 默认输入编解码器是json。

这里有一个兼容性矩阵，显示与Logstash和Kafka输入插件的每个组合兼容的Kafka客户端版本：

Kafka Client Version	|Logstash Version	|Plugin Version	|Security Features	|Why?
----------------------|-----------------|---------------|-------------------|-----
0.8                   |2.0.0 - 2.x.x    |<3.0.0         |                   |Legacy, 0.8 is still popular
0.9                   |2.0.0 - 2.3.x    |3.x.x          |Basic Auth, SSL    |Works with the old Ruby Event API (event['product']['price'] = 10)
0.9                   |2.4.0 - 5.0.x    |4.x.x          |Basic Auth, SSL    |Works with the new getter/setter APIs (event.set('[product][price]', 10))
0.10                  |2.4.0 - 5.0.x    |5.x.x          |Basic Auth, SSL    |Not compatible with the 0.9 broker

`nitice：`我们建议您使用匹配的Kafka客户端和代理版本。 在升级期间，您应该在客户端之前升级代理，因为代理的目标向后兼容。 例如，0.9代理与0.8消费者API和0.9消费者API兼容，但不是相反。

您必须配置topic_id，white_list或black_list。 默认情况下，它将连接到在localhost上运行的Zookeeper。 所有代理信息从Zookeeper状态读取。

理想情况下，您应该具有与分区数目一样多的线程以实现完美平衡 - 比分区更多的线程意味着某些线程将是空闲的

有关详细信息，请参阅http://kafka.apache.org/documentation.html#theconsumer

Kafka使用者配置：http://kafka.apache.org/documentation.html#consumerconfigs


#### 概要
此插件支持以下配置选项：

所需的配置选项：
```
kafka {
}
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|--------------
add_field| hash| No| {}
auto_offset_reset| string, one of ["largest", "smallest"]| No| "largest"
black_list| string| No| nil
codec| codec| No| "json"
consumer_id| string| No| nil
consumer_restart_on_error| boolean| No| true
consumer_restart_sleep_ms| number| No| 0
consumer_threads| number| No| 1
consumer_timeout_ms| number| No| -1
decoder_class| string| No| "kafka.serializer.DefaultDecoder"
decorate_events| boolean| No| false
fetch_message_max_bytes| number| No| 1048576
group_id| string| No| "logstash"
key_decoder_class| string| No| "kafka.serializer.DefaultDecoder"
queue_size| number| No| 20
rebalance_backoff_ms| number| No| 2000
rebalance_max_retries| number| No| 4
reset_beginning| boolean| No| false
tags| array| No |
topic_id| string| No |
nil| type| string| No |
white_list| string| No| nil
zk_connect| string| No| "localhost:2181"


#### 细节


**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**auto_offset_reset**
- 值可以是以下任意值：最大，最小
- 默认值为“最大”

最小或最大 - （可选，默认最大）如果消费者没有已建立的偏移量或偏移量无效，请从日志中最早的消息（最小）或日志中最后一个消息（最大）开始。

**black_list**
- 值类型是字符串
- 默认值为nil

从消费中排除的主题黑名单。

**codec**
- 值类型是编解码器
- 默认值为“json”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**consumer_id**
- 值类型是字符串
- 默认值为nil

消费者的唯一ID;如果未设置则自动生成。

**consumer_restart_on_error**
- 值类型是布尔值
- 默认值为true

选项在出错时重新启动使用者循环

**consumer_restart_sleep_ms**
- 值类型是数字
- 默认值为0

以毫为单位等待消费者在出现错误后重新启动的时间

**consumer_threads**
- 值类型是数字
- 默认值为1

从分区读取的线程数。理想情况下，您应该具有与分区数量一样多的线程以实现完美平衡。比分区更多的线程意味着一些线程将是空闲的。较少的线程意味着单个线程可能正在从多个分区消耗

**consumer_timeout_ms**
- 值类型是数字
- 默认值为-1

如果在指定的时间间隔后没有消息可用，则向使用者抛出超时异常

**decoder_class**


- 值类型是字符串
- 默认值为“kafka.serializer.DefaultDecoder”

消息的序列化类。默认解码器接受一个字节[]并返回相同的字节[]

**decorate_events**
- 值类型是布尔值
- 默认值为false

选项添加Kafka元数据，如主题，消息大小到事件。这将在logstash事件中添加一个名为kafka的字段，其中包含以下属性：msg_size：此消息的完整序列化大小（以字节为单位）（包括crc，头属性等）主题：此消息与consumer_group关联的主题：用于读取此事件分区：此消息与分区相关联的键：包含消息键的ByteBuffer

**fetch_message_max_bytes**
- 值类型是数字
- 默认值为1048576

尝试在每个抓取请求中为每个主题分区获取的消息的字节数。这些字节将被读入每个分区的内存，因此这有助于控制消费者使用的内存。获取请求大小必须至少与服务器允许的最大消息大小一样大，否则生产者可能发送大于客户可以提取的消息。

**group_id**
- 值类型是字符串
- 默认值为“logstash”

唯一标识此消费者所属的消费者进程组的字符串。通过设置相同的组ID，多个进程指示它们都是同一使用者组的一部分。

**key_decoder_class**
- 值类型是字符串
- 默认值为“kafka.serializer.DefaultDecoder”

键的序列化类（默认与消息的默认值相同）

**queue_size**
- 值类型是数字
- 默认值为20

内部Logstash队列大小，用于在从Kafka读取事件后将事件保存在内存中

**rebalance_backoff_ms**
- 值类型是数字
- 默认值为2000
在重新平衡期间重试之间的退避时间。

**rebalance_max_retries**
- 值类型是数字
- 默认值为4

当新消费者加入消费者组时，该组消费者尝试“重新平衡”负载以向每个消费者分配分区。如果在进行此分配时，消费者集合发生变化，则重新平衡将失败并重试。此设置控制放弃之前的最大尝试次数。

**reset_beginning**
- 值类型是布尔值
- 默认值为false

通过清除存储在Zookeeper中的组的任何偏移量，将使用者组重置为从日志中存在的最早消息开始。这是破坏性的！必须与auto_offset_reset⇒smallest 结合使用

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**topic_id**
- 值类型是字符串
- 默认值为nil

使用消息的主题

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

**white_list**
- 值类型是字符串
- 默认值为nil

包括消费的主题的白名单。

**zk_connect**

- 值类型是字符串
- 默认值为“localhost：2181”

指定ZooKeeper连接字符串，格式为hostname：port，其中host和port是ZooKeeper服务器的主机和端口。您还可以指定多个主机，格式为hostname1：port1，hostname2：port2，hostname3：port3。

服务器也可能有一个ZooKeeper chroot路径作为其ZooKeeper连接字符串的一部分，该连接字符串将其数据放在全局ZooKeeper命名空间中的某个路径下。如果是这样，消费者应在其连接字符串中使用相同的chroot路径。例如，要给出/ chroot / path的chroot路径，您将给出连接字符串为hostname1：port1，hostname2：port2，hostname3：port3 / chroot / path。


### pipe

> 这是一个社区维护的插件！

从长时间运行的命令管道流事件。

默认情况下，每个事件假定为一行。 如果要连接线，您将需要使用多行过滤器。

 

#### 概要
此插件支持以下配置选项：

所需的配置选项：
```
pipe {
    command => ...
}
```
可用的配置选项：

Setting   	|Input type	|Required	|Default value
------------|-----------|---------|--------------
add_field   |hash       |No       |{}
codec       |codec      |No       |"plain"
command     |string     |Yes      |
tags        |array      |No       |
type        |string     |No       |


#### 细节


**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**command**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

TODO（sissel）：我们应该切换到默认使用行编解码器，一旦我们从执行readline命令开始运行和读取事件，一次一行。

Example:
```
command => "echo hello world"
```

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。


### rabbitmq

从RabbitMQ队列拉取事件。

默认设置将创建一个完全暂时的队列并默认侦听所有消息。 如果您需要耐久性或任何其他高级设置，请设置相应的选项

此插件使用March Hare库与RabbitMQ服务器进行交互。 大多数配置选项直接映射到标准RabbitMQ和AMQP概念。 AMQP 0-9-1参考指南和RabbitMQ文档的其他部分有助于更深入的理解。

如果选中@metadata_enabled设置，接收的邮件的属性将存储在[\@metadata] [rabbitmq_properties]字段中。 请注意，存储元数据可能会降低性能。 以下属性可用（在大多数情况下，取决于它们是否由发件人设置）：

- app-id
- cluster-id
- consumer-tag
- content-encoding
- content-type
- correlation-id
- delivery-mode
- exchange
- expiration
- message-id
- priority
- redeliver
- reply-to
- routing-key
- timestamp
- type
- user-id

例如，要将RabbitMQ消息的timestamp属性导入Logstash事件的@timestamp字段，请使用日期过滤器解析[\@metadata]\[rabbitmq_properties] [timestamp]字段：
```
filter {
  if [@metadata][rabbitmq_properties][timestamp] {
    date {
      match => ["[@metadata][rabbitmq_properties][timestamp]", "UNIX"]
    }
  }
}
```
此外，任何邮件标头都将保存在[\@metadata]\[rabbitmq_headers]字段中。


#### 概要

此插件支持以下配置选项：
所需的配置选项：
```
rabbitmq {
    host => ...
    subscription_retry_interval_seconds => ...
}
```
可用的配置选项：

Setting	    |Input type	|Required	|Default value
------------|-----------|---------|------------
ack| boolean| No| true
add_field| hash| No| {}
arguments| array| No| {}
auto_delete| boolean| No| false
automatic_recovery| boolean| No| true
codec| codec| No| "json"
connect_retry_interval| number| No| 1
connection_timeout| number| No
durable| boolean| No| false
exchange| string| No
exclusive| boolean| No| false
heartbeat| number| No
host| string| Yes|
key| string| No| "logstash"
metadata_enabled| boolean| No| false
passive| boolean| No| false
password| password| No| "guest"
port| number| No| 5672
prefetch_count| number| No| 256
queue| string| No| ""
ssl| boolean| No| false
subscription_retry_interval_seconds| number| Yes| 5
tags| array| No|
threads| number| No| 1
type| string| No|
user| string| No| "guest"
verify_ssl| boolean| No| false
vhost| string| No| "/"


#### 细节

**ack**
- 值类型是布尔值
- 默认值为true

启用消息确认。如果Logstash关闭，由Logstash获取但尚未发送到Logstash管道中的确认消息将由服务器重新排队。然而，确认将损害消息吞吐量。

这将只发送一个回来每个prefetch_count消息。批量工作在这里提供了性能提升。

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**arguments**
- 值类型是数组
- 默认值为{}

额外的队列参数作为数组。要使RabbitMQ队列镜像，请使用：{“x-ha-policy”=>“all”}

**auto_delete**
- 值类型是布尔值
- 默认值为false

当最后一个消费者断开连接时，应该在代理上删除队列吗？如果希望队列保留在代理上，将消息排队等待消费者消费，则将此选项设置为false。


**automatic_recovery**
- 值类型是布尔值
- 默认值为true

将此设置为从断开的连接自动恢复。你几乎肯定不想覆盖这个！


**codec**
- 值类型是编解码器
- 默认值为“json”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**connect_retry_interval**
- 值类型是数字
- 默认值为1

重试连接前等待的时间（以秒为单位）


**connection_timeout**
- 值类型是数字
- 此设置没有默认值。

默认连接超时（以毫秒为单位）。如果没有指定超时是无限的。

**debug (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是布尔值
- 默认值为false

启用或禁用日志记录

**durable**
- 值类型是布尔值
- 默认值为false

这个队列是否持久？ （aka;它应该存活经纪人重新启动吗？）

**exchange**
- 值类型是字符串
- 此设置没有默认值。

绑定队列的交换机的名称。

**exclusive**
- 值类型是布尔值
- 默认值为false

队列是独占吗？独占队列只能由声明它们的连接使用，并且在关闭时会被删除（例如，由于Logstash重新启动）。

**heartbeat**
- 值类型是数字
- 此设置没有默认值。

心跳延迟（以秒为单位）。如果未指定，则不发送心跳

**host**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

RabbitMQ服务器地址

**key**
- 值类型是字符串
- 默认值为“logstash”

将队列绑定到交换机时使用的路由密钥。这只与直接或主题交换有关。

- 在扇出交换上忽略路由密钥。
- 通配符在直接交换上无效。


**metadata_enabled**
- 值类型是布尔值
- 默认值为false

启用@metadata中邮件标头和属性的存储。这可能会影响性能

**passive**
- 值类型是布尔值
- 默认值为false

如果为true，队列将被动地声明，这意味着它必须已经存在于服务器上。要使Logstash创建队列（如果需要），将此选项保留为false。如果主动声明一个已经存在的队列，该插件的队列选项（持久等）必须与现有队列的队列选项匹配。

**password**
- 值类型为密码
- 默认值为“guest”

RabbitMQ密码

**port**
- 值类型是数字
- 默认值为5672

RabbitMQ端口连接

**prefetch_count**
- 值类型是数字
- 默认值为256

预取计数。如果使用ack选项启用确认，请指定未确认的未确认数量

**queue**
- 值类型是字符串
- 默认值为“”

Logstash队列的名称将消耗事件。如果为空，将创建具有随机选择的名称的瞬时队列。

**ssl**
- 值类型是布尔值
- 默认值为false

启用或禁用SSL

**subscription_retry_interval_seconds**
- 这是必需的设置。
- 值类型是数字
- 默认值为5

重试前失败的订阅请求后等待的时间（秒）。如果服务器离开然后返回，订阅可能会失败

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**threads**
- 值类型是数字
- 默认值为1


**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

**user**
- 值类型是字符串
- 默认值为“guest”

RabbitMQ用户名

**verify_ssl**
- 值类型是布尔值
- 默认值为false

验证SSL证书

**vhost**
- 值类型是字符串
- 默认值为“/”

要使用的vhost。如果你不知道这是什么，离开默认。

### redis

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
redis {
}
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-----------
add_field | hash | No | {}
batch_count | number | No | 1
codec | codec | No | "json"
data_type | string, one of ["list", "channel", "pattern_channel"] | No |
db | number | No | 0
host | string | No | "127.0.0.1"
key | string | No |
password | password | No |
port | number | No | 6379
tags | array | No |
threads | number | No | 1
timeout | number | No | 5
type | string | No |


#### 详细

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**batch_count**
- 值类型是数字
- 默认值为1

使用EVAL从Redis返回的事件数。

**codec**
- 值类型是编解码器
- 默认值为“json”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**data_type**
- 值可以是以下任何值：list，channel，pattern_channel
- 此设置没有默认值。

指定列表或通道。如果`redis\_type` 是list，那么我们将BLPOP的键。如果`redis\_type`是channel，那么我们将SUBSCRIBE给key。如果`redis\_type`是pattern_channel，那么我们将PSUBSCRIBE给键。


**db**
- 值类型是数字
- 默认值为0

Redis数据库号。

**host**
- 值类型是字符串
- 默认值为“127.0.0.1”

Redis服务器的主机名。

**key**
- 值类型是字符串
- 此设置没有默认值。

Redis列表或通道的名称。

**name (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是字符串
- 默认值为“default”

`class LogStash::Inputs::Redis < LogStash::Inputs::Threadable `名称配置用于在有多个实例的情况下进行日志记录。此功能没有实际功能，将在以后的版本中删除。

**password**
- 值类型为密码
- 此设置没有默认值。

要验证的密码。默认情况下没有身份验证。

**port**
- 值类型是数字
- 默认值为6379

要连接的端口。

**queue (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是字符串
- 此设置没有默认值。

Redis队列的名称（我们将使用BLPOP）。

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**threads**
- 值类型是数字
- 默认值为1


**Timeout**
- 值类型是数字
- 默认值为5

初始连接超时（以秒为单位）。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

### stdin

从标准输入读取事件。

默认情况下，每个事件假定为一行。 如果要连接线，您将需要使用多行过滤器。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
stdin {
}
```
可用的配置选项：

Setting	  |Input type	|Required	|Default value
----------|-----------|---------|-------------
add_field |hash       |No       |{}
codec     |codec      |No       |"line"
tags      |array      |No       |
type      |string     |No       |


#### 细节

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**codec**
- 值类型是编解码器
- 默认值为“line”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**type**
- 值类型是字符串
- 此设置没有默认值。
向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

### sqlite
> 这是一个社区维护的插件！ 它默认不随Logstash一起提供，但它很容易安装通过运行bin / logstash-plugin install logstash-input-sqlite。

从sqlite数据库读取行。

这在您直接记录到表的情况下最有用。 任何被监视的表必须有一个单调增加的id列。

默认读取所有表，除了：

- 匹配`sqlite_％`的那些 - 这些是sqlite的内部/管理表
- since_table - 此插件用于跟踪状态。

示例：
```
% sqlite /tmp/example.db
sqlite> CREATE TABLE weblogs (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    ip STRING,
    request STRING,
    response INTEGER);
sqlite> INSERT INTO weblogs (ip, request, response)
    VALUES ("1.2.3.4", "/index.html", 200);
```
然后用这个logstash配置：
```
input {
  sqlite {
    path => "/tmp/example.db"
    type => weblogs
  }
}
output {
  stdout {
    debug => true
  }
}
```
输出示例：
```
{
  "@source"      => "sqlite://sadness/tmp/x.db",
  "@tags"        => [],
  "@fields"      => {
    "ip"       => "1.2.3.4",
    "request"  => "/index.html",
    "response" => 200
  },
  "@timestamp"   => "2013-05-29T06:16:30.850Z",
  "@source_host" => "sadness",
  "@source_path" => "/tmp/x.db",
  "@message"     => "",
  "@type"        => "foo"
}
```
#### 概要

这个插件支持下列配置选项：

所需的配置选项：
```
sqlite {
    path => ...
}
```
可用的配置选项：

Setting	  |Input type	|Required	|Default value
----------|-----------|---------|------------
add_field |  hash     |  No |  {}
batch     |  number   |  No |  5
codec     |  codec    |  No |  "plain"
exclude_tables |array |  No |  []
path      |  string   |  Yes|
tags      |  array    |  No |
type      |  string   |  No |

#### 详情

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**batch**
- 值类型是数字
- 默认值为5

每次SELECT调用时一次获取多少行。

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。


**exclude_tables**
- 值类型是数组
- 默认值为[]

按名称排除的任何表。默认情况下，将遵循所有表。

**path**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

sqlite数据库文件的路径。

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

### syslog
通过网络将syslog消息读为事件。

如果你今天已经使用syslog，这个输入是一个不错的选择。 如果要从不能运行自己的日志收集器的设备和网络设备接收日志，这也是一个不错的选择。

当然，syslog是一个非常泥泞的术语。 此输入仅支持具有一些小修改的RFC3164 syslog。 日期格式允许为RFC3164样式或ISO8601。 否则，必须遵守RFC3164的其余部分。 如果不使用RFC3164，请不要使用此输入。

有关详细信息，请参阅[RFC3164页](http://www.ietf.org/rfc/rfc3164.txt)。

注意：此输入将在TCP和UDP上启动侦听器。

#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
syslog {
}
```
可用的配置选项：

Setting	        |Input type	|Required	|Default value
----------------|-----------|---------|------------
add_field | hash | No | {}
codec | codec | No | "plain"
facility_labels | array | No | ["kernel", "user-level", "mail", "system", "security/authorization", "syslogd", "line printer", "network news", "UUCP", "clock", "security/authorization", "FTP", "NTP", "log audit", "log alert", "clock", "local0", "local1", "local2", "local3", "local4", "local5", "local6", "local7"]
host | string | No | "0.0.0.0"
locale | string | No |
port | number | No | 514
severity_labels | array | No | ["Emergency", "Alert", "Critical", "Error", "Warning", "Notice", "Informational", "Debug"]
tags | array | No |
timezone | string | No |
type | string | No |
use_labels | boolean | No | true


#### 详情

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**facility_labels**
- 值类型是数组
- 默认值是[“内核”，“用户级”，“邮件”，“系统”，“安全/授权”，“syslogd”，“行式打印机”，“网络新闻”，“UUCP” “security / authorization”，“FTP”，“NTP”，“log audit”，“log alert”，“clock”，“local0”，“local1”，“local2”，“local3”，“local4”，“local5 “，”local6“，”local7“]

设施级别的标签。这些在RFC3164中定义。

**host**
- 值类型是字符串
- 默认值为“0.0.0.0”

要听的地址。

**locale**
- 值类型是字符串
- 此设置没有默认值。

使用IETF-BCP47或POSIX语言标记指定用于日期解析的区域设置。简单示例是en，en-US for BCP47或en_US for POSIX。如果未指定，将使用平台默认值。

对于解析月份名称（使用MMM的模式）和工作日名称（使用EEE的模式），区域设置几乎是必需的。

**port**
- 值类型是数字
- 默认值为514

要监听的端口。记住小于1024的端口（特权端口）可能需要root才能使用。

**severity_labels**
- 值类型是数组
- 默认值为[“Emergency”，“Alert”，“Critical”，“Error”，“Warning”，“Notice”，“Informational”，“Debug”]

严重性级别的标签。这些在RFC3164中定义。


**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**timezone**
- 值类型是字符串
- 此设置没有默认值。

指定要用于日期解析的时区标准ID。有效ID列在[Joda.org可用时区页面]（http://joda-time.sourceforge.net/timezones.html）上。这在时区无法从值中提取，而不是平台默认值的情况下非常有用。如果未指定，将使用平台默认值。标准ID是好的，因为它照顾您的夏令时例如，美洲/ Los_Angeles或欧洲/法国是有效的ID。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

**use_labels**
- 值类型是布尔值
- 默认值为true

对严重性和设施级别使用标签解析。

### tcp

通过TCP套接字读取事件。

与标准输入和文件输入一样，每个事件假定为一行文本。

可以接受来自客户端的连接或连接到服务器，具体取决于模式。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
tcp {
    port => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field | hash | No | {}
codec | codec | No | "line"
host | string | No | "0.0.0.0"
mode | string, one of ["server", "client"] | No | "server"
port | number | Yes |
ssl_cert | a valid filesystem path | No |
ssl_enable | boolean | No | false
ssl_extra_chain_certs | array | No | []
ssl_key | a valid filesystem path | No |
ssl_key_passphrase | password | No | nil
ssl_verify | boolean | No | true
tags | array | No |
type | string | No |


#### 详情

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**codec**
- 值类型是编解码器
- 默认值为“line”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**data_timeout (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是数字
- 默认值为-1

**host**
- 值类型是字符串
- 默认值为“0.0.0.0”

当模式是服务器时，地址要监听。当模式为客户端时，连接的地址。

**mode**
- 值可以是以下任意值：服务器，客户端
- 默认值为“server”

模式操作。服务器侦听客户端连接，客户端连接到服务器。

**port**
- 这是必需的设置。
- 值类型是数字
- 此设置没有默认值。

当模式是服务器时，端口要监听。当模式为客户端时，连接到的端口。

**ssl_cacert (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型为路径
- 此设置没有默认值。

SSL CA证书，chainfile或CA路径。将自动包括系统CA路径。

**ssl_cert**
- 值类型为路径
- 此设置没有默认值。

SSL证书路径

**ssl_enable**
- 值类型是布尔值
- 默认值为false

启用S​​SL（必须设置为使其他ssl_选项生效）。

**ssl_extra_chain_certs**
- 值类型是数组
- 默认值为[]

要添加到证书链的额外X509证书的数组。当系统存储中不需要CA链时很有用。

**ssl_key**
- 值类型为路径
- 此设置没有默认值。

SSL密钥路径

**ssl_key_passphrase**
- 值类型为密码
- 默认值为nil

SSL密钥密码

**ssl_verify**
- 值类型是布尔值
- 默认值为true

验证SSL连接的另一端与CA的身份。对于输入，将字段sslsubject设置为客户端证书的字段。

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**type**
值类型是字符串
此设置没有默认值。
向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

### unix

> 这是一个社区维护的插件！

通过UNIX套接字读取事件。

与标准输入和文件输入一样，每个事件假定为一行文本。

可以接受来自客户端的连接或连接到服务器，具体取决于模式。

 

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
unix {
    path => ...
}
```
可用配置选项：

Setting	 |Input type	|Required	|Default value
---------|------------|---------|-------------
add_field|hash|No|{}
codec|codec|No|"line"
data_timeout|number|No|-1
force_unlink|boolean|No|false
mode|string, one of ["server", "client"]|No|"server"
path|string|Yes|
tags|array|No|
type|string|No|

#### 详情
 
**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**codec**
- 值类型是编解码器
- 默认值为“line”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**data_timeout**
- 值类型是数字
- 默认值为-1

读取超时（以秒为单位）。如果特定连接空闲超过此超时时间，我们将假定它已经死了并关闭它。

如果你不想超时，请使用-1。

**force_unlink**
- 值类型是布尔值
- 默认值为false

在EADDRINUSE故障的情况下删除套接字文件

**mode**
- 值可以是以下任意值：服务器，客户端
- 默认值为“server”

模式操作。服务器侦听客户端连接，客户端连接到服务器。

**path**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

当模式是服务器时，要监听的路径。当模式为客户端时，连接到的路径。

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

### udp

通过udp将消息作为事件读取。 唯一需要的配置项是port，它指定logstash将侦听事件流的udp端口。


#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
udp {
    port => ...
}
```
可用的配置选项:

Setting	    |Input type	|Required	|Default value
------------|-----------|---------|-------------
add_field   |    hash   |    No   |    {}
buffer_size |    number |    No   |    8192
codec       |    codec  |    No   |    "plain"
host        |    string |    No   |    "0.0.0.0"
port        |    number |    Yes  |
queue_size  |    number |    No   |    2000
tags        |    array  |    No   |
type        |    string |    No   |
workers     |    number |    No   |    2


#### 详情

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**buffer_size**
- 值类型是数字
- 默认值为8192

要从网络读取的最大数据包大小

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**host**
- 值类型是字符串
- 默认值为“0.0.0.0”

logstash将侦听的地址。

**port**
- 这是必需的设置。
- 值类型是数字
- 此设置没有默认值。

logstash将侦听的端口。记住小于1024的端口（特权端口）可能需要root或提升权限才能使用。

**queue_size**
- 值类型是数字
- 默认值为2000

这是在数据包开始丢弃之前可以在内存中保存的未处理UDP数据包的数量。

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

**workers**
- 值类型是数字
- 默认值为2

处理数据包的线程数


### varnishlog

> 这是一个社区维护的插件！ 它默认不随Logstash一起提供，但它很容易安装通过运行bin / logstash-plugin install logstash-input-varnishlog。

从varnish缓存的共享内存日志中读取

#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
varnishlog {
}
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
------|------|------|------
add_field|hash|No|{}
codec|codec|No|"plain"
tags|array|No|
threads|number|No|1
type|string|No|

#### 详情

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**codec**
- 值类型是编解码器
- 默认值为“plain”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**threads**
- 值类型是数字
- 默认值为1

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

### websocket

> 这是一个社区维护的插件！ 它默认不随Logstash一起提供，但它很容易安装通过运行bin / logstash-plugin install logstash-input-websocket。

通过websocket协议读取事件。


#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
websocket {
}
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
------|------|------|------
add_field|hash|No|{}
codec|codec|No|"json"
mode|string, one of ["server", "client"]|No|"client"
tags|array|No|
type|string|No|
url|string|No|"0.0.0.0"


#### 详情

**add_field**
- 值类型是哈希
- 默认值为{}

向事件添加字段

**codec**
- 值类型是编解码器
- 默认值为“json”

用于输入数据的编解码器。输入的编解码器是用于在进入输入之前，无需一个单独的过滤器中的Logstash管道解码数据的简便方法。

**mode**
- 值可以是以下任意值：server, client
- 默认值为“client”

作为客户端或服务器运行。

客户端模式导致此插件作为websocket客户端连接到给定的URL。它期望接收事件作为websocket消息。

（NOT IMPLEMENTED YET）服务器模式导致此插件侦听websocket客户端的给定URL。它期望从这些客户端接收作为websocket消息的事件。


**tags**
- 值类型是数组
- 此设置没有默认值。

向您的活动添加任意数量的任意标签。

这可以帮助稍后处理。

**type**
- 值类型是字符串
- 此设置没有默认值。

向此输入处理的所有事件添加一个类型字段。

类型主要用于过滤器激活。

类型存储为事件本身的一部分，因此您也可以使用类型在Kibana中搜索它。

如果您尝试在已有一个事件的事件上设置类型（例如，当您将事件从发件人发送到索引器时），则新输入不会覆盖现有类型。发货人设置的类型即使在发送到另一个Logstash服务器时也会保持该事件的有效期。

**url**

- 值类型是字符串
- 默认值为“0.0.0.0”

连接到或服务于的网址
