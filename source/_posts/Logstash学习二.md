---
title: Logstash学习二
date: 2016-10-24 22:30:00
tags:
- Logstash
categories:
- Logstash
---

- 版本的变化
- 升级Logstash
- 配置Logstash
<!-- more -->


## 版本的变化
本节讨论在将应用程序从一个版本的Logstash迁移到另一个版本时需要注意的更改。

### 2.4的变化
#### Beats输入配置更改
Beats输入已经使用Netty重新实现，Netty是Java的异步IO框架。这种重写性能使插件符合Logstash转发器+ LS组合。作为Beats重构器的一部分，我们现在仅支持PKCS＃8格式的私钥。您可以通过使用OpenSSL工具包轻松地将现有密钥转换为使用PKCS＃8格式。请参阅OpenSSL文档。

### 2.2
尽管2.2与旧版本的配置完全兼容，但是在部署到生产环境之前，用户需要考虑到管道的一些架构更改。这些更改在语义版本意义上不会严格“打破”，但是它们使Logstash在运行时的行为不同，并且也会影响性能。我们在升级Logstash中编译了这样的列表到2.2部分。请在部署2.2版本之前查看它。

### 2.0中的更改
Logstash的2.0版本有一些与先前版本的Logstash不兼容的更改。本节讨论迁移到此版本时需要注意的事项。

#### Elasticsearch输出默认值
从Logstash的2.0版本开始，Elasticsearch的默认Logstash输出是HTTP。 要使用节点或传输协议，请下载Elasticsearch Java插件。 Logstash到Elasticsearch的HTTP输出现在支持嗅探。

> 注意:elasticsearch_java插件有两个特定于底层Elasticsearch集群版本的版本。 请务必在安装期间为--version选项指定正确的值：\*对于2.0之前的Elasticsearch版本，请使用命令bin / plugin install --version 1.5.x logstash-output-elasticsearch_java \*对于Elasticsearch版本2.0及更高版本，请使用 命令bin / plugin install --version 2.0.0 logstash-output-elasticsearch_java

#### Elasticsearch输出配置更改
Elasticsearch输出插件配置具有以下更改：

- 主机配置选项现在是主机，允许您在myhost：9200格式中指定多个主机和关联端口
- 新选项：bind_host，bind_port，cluster，embedded，embedded_http_port，port，sniffing_delay
- max_inflight_requests选项（在1.5版本中已弃用）现已删除
- 由于hosts选项允许为主机指定端口，因此现在将删除冗余端口选项
- node_name和协议选项已移至elasticsearch_java插件

#### 已删除插件配置设置
在此版本中删除以下弃用的配置设置：

- 输入插件配置设置：debug，format，charset，message_format
- 输出插件配置设置：type，tags，exclude_tags。
- 过滤器插件配置设置：type，tags，exclude_tags。
- 具有这些设置的配置文件无效，并防止Logstash启动。

#### Kafka输出配置更改
Logstash的2.0版本包括一个新版本的Kafka输出插件，并进行了重大的配置更改。 请比较Logstash 1.5和Logstash 2.0版本的Kafka输出插件的文档页面，并相应地更新配置文件。

#### 指标过滤器更改
以前的指标过滤器插件的实现使用点字段名称。 Elasticsearch不允许字段名称有从2.0版开始的点，所以更改使用子字段而不是在此插件中的点。 请注意，这些更改使得版本3.0.0的指标过滤器插件与以前的版本不兼容。

#### 过滤器工作者默认更改
从Logstash的2.0版本开始，过滤器插件的filter_workers配置选项的默认值是可用CPU内核的一半，而不是1.此更改增加了资源密集型过滤操作的过滤器执行的并行性。 您可以继续使用-w标志来手动设置此选项的值，如在以前的版本中。


## 升级Logstash
**重要** 升级Logstash之前：

请参阅最新更改文档。
在升级生产集群之前在开发环境中测试升级。

### 使用软件包管理器升级

此过程使用包管理器来升级Logstash。

1. 关闭Logstash管道，包括将事件发送到Logstash的任何输入。
2. 使用“软件包存储库”部分中的说明，将存储库链接更新为指向2.0存储库，而不是先前的版本。
3. 针对您的操作系统，运行apt-get upgrade logstash或yum update logstash命令。
4. 使用logstash --configtest -f <configuration-file>命令测试配置文件。 某些Logstash插件的配置选项在2.0版本中已更改。
5. 更新配置文件后重新启动Logstash管道。

### 使用直接下载升级
此过程直接从Elastic下载相关的Logstash二进制文件。

1. 关闭Logstash管道，包括将事件发送到Logstash的任何输入。
2. 下载与您的主机环境匹配的Logstash安装文件。
3. 将安装文件解包到Logstash目录中。
4. 使用logstash --configtest -f <configuration-file>命令测试配置文件。 某些Logstash插件的配置选项在2.0版本中已更改。
5. 更新配置文件后重新启动Logstash管道。

### 将Logstash和Elasticsearch升级到2.0

如果您使用Elasticsearch作为输出，并希望升级到Elasticsearch 2.0，请注意在升级之前的更改。 此外，升级到Elasticsearch 2.0后需要执行以下步骤：

**映射更改：** 用户可能有自定义模板更改，因此默认情况下，Logstash升级将保留模板。 即使您没有自定义模板，默认情况下Logstash也不会覆盖现有模板。

使用需要手动更新模板的GeoIP过滤器有一个已知问题（删除路径）。

注意：如果您有自定义模板更改，请务必保存并合并所有更改。 您可以通过运行以下命令获取现有模板：
```
curl -XGET localhost:9200/_template/logstash
```
下列选项添加到您的Logstash配置：
```
output {
        elasticsearch {
                template_overwrite => true
        }
}
```
重新启动Logstash。

**字段中的点：** Elasticsearch 2.0不允许字段名包含。 字符。 有关此更改的更多详细信息。 某些插件已经更新，以补偿此中断更改，包括logstash-filter-metrics和logstash-filter-elapsed。 这些插件更新可用于Logstash 2.0。 要升级到这些插件的最新版本，命令是：
```
bin/logstash-plugin update <plugin_name>
```

**多行过滤器：** 如果您在配置中使用多行过滤器并升级到Logstash 2.0，则会出现错误。 确保显式设置过滤器工作程序（-w）的数目为1.您可以通过传递命令行标志来设置工作程序的数目，例如：
```
bin/logstash -w 1
```
### 将Logstash升级到2.2
Logstash 2.2重新构建了流水线阶段，以提供更多的性能，并帮助未来增强弹性。 新管道引入了微批次，一次处理一组事件。 默认批处理大小为每个工作程序125。 此外，过滤器和输出级在相同的线程中执行，但仍然，作为不同的级。 CLI标志--pipeline-workers或-w控制执行线程的数量，默认情况下将其设置为内核数。

**Elasticsearch输出的注意事项** 管道的默认批处理大小为每个工作程序125个事件。 默认情况下，这也将是用于弹性搜索输出的批量大小。 Elasticsearch输出的flush_size现在仅作为最大批量大小（仍默认为500）。 例如，如果您的管道批处理大小为3000个事件，Elasticsearch输出将在6个单独的批量请求中一次发送500个事件。 换句话说，对于Elasticsearch输出，批量请求大小基于flush_size和--pipeline-batch-size进行分块。 如果flush_size设置为大于--pipeline-batch-size，则会被忽略，并将使用--pipeline-batch-size。

Logstash 2.2中的输出工作程序的默认数目现在等于管道工作程序的数目（-w），除非在Logstash配置文件中被覆盖。 这对于一些用户可能是有问题的，因为额外的工作者可能消耗诸如文件句柄的额外资源，尤其是在Elasticsearch输出的情况下。 具有多个Elasticsearch主机的用户可能想在其Logstash配置中覆盖Elasticsearch输出的workers设置，以将该数字限制为1到4之间的较小值。

**2.2中的性能调优** 由于过滤器和输出工作程序都在同一个线程上，这可能导致线程在I / O等待状态中空闲。 因此，在2.2中，您可以安全地将-w设置为一个数字，该数字是计算机上核心数的倍数。 调整性能的一种常用方法是，不断增加-w超过核心数，直到性能不再提高。 注意注意 - 确保您还记住大小，因为正在进行的事件的数量是#workers * batch_size * average_event大小。 更多的飞行中事件可能会增加内存压力，最终导致内存不足错误。 您可以通过设置LS_HEAP_SIZE更改Logstash中的堆大小

## 配置Logstash

要配置Logstash，请创建一个配置文件，指定要使用的插件和每个插件的设置。 您可以引用配置中的事件字段，并使用条件来处理满足特定条件的事件。 当您运行logstash时，您使用-f指定您的配置文件。

让我们通过创建一个简单的配置文件并使用它来运行Logstash。 创建一个名为“logstash-simple.conf”的文件，并将其保存在与Logstash相同的目录中。

```
input { stdin { } }
output {
  elasticsearch { hosts => ["localhost:9200"] }
  stdout { codec => rubydebug }
}
```
然后，运行logstash并指定使用-f标志的配置文件。
```
bin/logstash -f logstash-simple.conf
```
Logstash读取指定的配置文件，并输出到Elasticsearch和stdout。 在我们继续讨论一些更复杂的例子之前，让我们仔细看看配置文件中的内容。

### 配置文件的结构
Logstash配置文件对于要添加到事件处理管道的每种类型的插件都有一个单独的部分。 例如：
```
# This is a comment. You should use comments to describe
# parts of your configuration.
input {
  ...
}

filter {
  ...
}

output {
  ...
}
```
每个部分包含一个或多个插件的配置选项。 如果指定多个过滤器，它们将按照其在配置文件中的显示顺序应用。

#### 插件配置
插件的配置包括插件名称，后面是该插件的一组设置。 例如，此输入节配置两个文件输入：

```
input {
  file {
    path => "/var/log/messages"
    type => "syslog"
  }

  file {
    path => "/var/log/apache/access.log"
    type => "apache"
  }
}
```
在此示例中，为每个文件输入配置了两个设置：路径和类型。

您可以配置的设置因插件类型而异。 有关每个插件的信息，请参阅输入插件，输出插件，过滤器插件和编解码器插件。

#### 值类型
插件可以要求设置的值为某种类型，例如布尔值，列表或哈希。 支持以下值类型。

1. 数组

这种类型现在大多已被废弃，赞成使用标准类型，如字符串与插件定义：更多类型检查：list => true属性。 它仍然需要处理哈希或混合类型的列表，其中不需要类型检查。

例：
```
 users => [ {id => 1, name => bob}, {id => 2, name => jane} ]
```
2. 列表
不是一个类型本身，而是一个属性类型可以有。 这使得可以键入检查多个值。 插件作者可以通过在声明参数时指定：list => true来启用列表检查。

例：
```
path => [ "/var/log/messages", "/var/log/*.log" ]
 uris => [ "http://elastic.co", "http://example.net" ]
```
此示例配置path，它是一个字符串，它是一个包含三个字符串中每个字符串的元素的列表。 它还将配置uris参数为URI列表，如果提供的任何URI无效，则失败。


3. 布尔值
布尔值必须为true或false。 请注意，true和false关键字不用引号括起来。

例：
```
 ssl_enable => true
```
4. 字节
字节字段是表示有效字节单位的字符串字段。 在插件选项中声明特定大小是一种方便的方法。 支持SI（k M G T P E Z Y）和二进制（Ki Mi Gi Ti Pi Ei Zi Yi）单位。 二进制单位以base-1024为单位，SI单位为base-1000。 此字段不区分大小写，并接受值和单位之间的空格。 如果未指定单位，则整数字符串表示字节数。

例子：
```
 my_bytes => "1113"   # 1113 bytes
 my_bytes => "10MiB"  # 10485760 bytes
 my_bytes => "100kib" # 102400 bytes
 my_bytes => "180 mb" # 180000000 bytes
```
5. 编解码器
编解码器是用于表示数据的Logstash编解码器的名称。 编解码器可用于输入和输出。

输入编解码器提供了一种方便的方式在数据进入输入之前对其进行解码。 输出编解码器提供了一种方便的方式在离开输出之前对数据进行编码。 使用输入或输出编解码器无需在Logstash管道中使用单独的过滤器。

可在Codec插件页面找到可用编解码器的列表。

例：
```
 codec => "json"
```
6. 哈希
散列是以格式“field1”=>“value1”指定的键值对的集合。 请注意，多个键值值条目之间用空格分隔，而不是逗号。

例：
```
match => {
  "field1" => "value1"
  "field2" => "value2"
  ...
}
```
7. 数值
数字必须是有效的数字值（浮点数或整数）。

例：
```
  port => 33
```

8. 密码
密码是具有未记录或打印的单个值的字符串。

例：
```
  my_password => "password"
```
9. URI
URI可以是从完整URL（如http://elastic.co/）到简单标识符（如foobar）的任何内容。 如果URI包含密码，例如http：// user：pass@example.net，则不会记录或打印URI的密码部分。

例：
```
  my_uri => "http://foo:bar@example.net"
```
10. 路径
路径是表示有效操作系统路径的字符串。

例：
```
  my_path => "/tmp/logstash"
```

11. 字符串
字符串必须是单个字符序列。 请注意，字符串值用双引号或单引号括起来。 字符串中的字面引号需要使用反斜杠转义，如果它们与字符串分隔符相同，即单引号字符串中的单引号需要转义，以及双引号字符串中的双引号。

例：
```
name => "Hello world"
name => 'It\'s a beautiful day'
```

#### 注释
注释与perl，ruby和python中的注释相同。 注释以＃字符开头，不需要在行的开头。 例如：
```
# this is a comment

input { # comments can appear at the end of a line, too
  # ...
}
```

### 事件相关配置
logstash代理是一个具有3个阶段的处理流水线：输入→过滤器→输出。 输入生成事件，过滤器修改它们，输出发送到其他地方。

所有事件都有属性。 例如，apache访问日志将具有诸如状态代码（200,404），请求路径（“/”，“index.html”），HTTP动词（GET，POST），客户端IP地址等的东西.Logstash调用这些 属性“字段。

Logstash中的一些配置选项需要存在字段才能运行。 因为输入生成事件，所以在输入块中没有要计算的字段 - 它们不存在！

由于它们依赖于事件和字段，因此以下配置选项只能在过滤器和输出块中使用。

> 重要: 下面描述的字段引用，sprintf格式和条件不会在输入块中工作。

#### 字段引用
通过名称引用字段通常很有用。 为此，可以使用Logstash字段引用语法。

访问字段的语法是[fieldname]。 如果您要引用顶级字段，则可以省略[]，只需使用fieldname。 要引用嵌套字段，请指定该字段的完整路径：[顶级字段] [嵌套字段]。

例如，以下事件有五个顶级字段（代理，ip，请求，响应，ua）和三个嵌套字段（状态，字节，os）。
```
{
  "agent": "Mozilla/5.0 (compatible; MSIE 9.0)",
  "ip": "192.168.24.44",
  "request": "/index.html"
  "response": {
    "status": 200,
    "bytes": 52353
  },
  "ua": {
    "os": "Windows 7"
  }
}
```
要引用os字段，请指定[ua] [os]。 要引用顶级字段（如请求），您只需指定字段名称即可。

#### sprintf格式
字段引用格式也用于Logstash调用sprintf格式。 此格式允许您引用其他字符串中的字段值。 例如，statsd输出具有增量设置，使您能够通过状态代码保留apache日志的计数：
```
output {
  statsd {
    increment => "apache.%{[response][status]}"
  }
}
```
您还可以使用此sprintf格式来格式化时间。 而不是指定字段名称，请使用+ FORMAT语法，其中FORMAT是时间格式。

例如，如果要使用文件输出根据小时和类型字段写入日志：
```
output {
  file {
    path => "/var/log/%{type}.%{+yyyy.MM.dd.HH}"
  }
}
```

#### 条件
有时您只想在特定条件下过滤或输出事件。 为此，您可以使用条件。

Logstash中的条件看起来和行为方式与在编程语言中相同。 条件支持if，else if和else语句并且可以嵌套。

条件语法是：
```
if EXPRESSION {
  ...
} else if EXPRESSION {
  ...
} else {
  ...
}
```
什么是表达式？ 比较测试，布尔逻辑等等！

您可以使用以下比较运算符：
- equality：==，！=，<，>，<=，> =
- regex：=〜，！〜（在左边检查一个字符串值的模式）
- 包含：in，not in

支持的布尔运算符为：
- and, or, nand, xor

支持的一元运算符是：
- !

表达式可以长而复杂。 表达式可以包含其他表达式，可以使用！否定表达式，并且可以使用括号（...）将它们分组。

例如，如果字段操作的值为login，则以下条件使用mutate过滤器删除字段secret：
```
filter {
  if [action] == "login" {
    mutate { remove_field => "secret" }
  }
}
```
您可以指定单个条件的多个表达式：
```
output {
  # Send production errors to pagerduty
  if [loglevel] == "ERROR" and [deployment] == "production" {
    pagerduty {
    ...
    }
  }
}
```
您可以使用in运算符来测试字段是否包含特定字符串，键或（对于lists）元素：
```
filter {
  if [foo] in [foobar] {
    mutate { add_tag => "field in field" }
  }
  if [foo] in "foo" {
    mutate { add_tag => "field in string" }
  }
  if "hello" in [greeting] {
    mutate { add_tag => "string in field" }
  }
  if [foo] in ["hello", "world", "foo"] {
    mutate { add_tag => "field in list" }
  }
  if [missing] in [alsomissing] {
    mutate { add_tag => "shouldnotexist" }
  }
  if !("foo" in ["hello", "world"]) {
    mutate { add_tag => "shouldexist" }
  }
}
```
你使用不是在条件相同的方式。 例如，当grok成功时，您可以使用not in仅将事件路由到Elasticsearch：
```
output {
  if "_grokparsefailure" not in [tags] {
    elasticsearch { ... }
  }
}
```
您可以检查特定字段的存在，但是目前没有办法区分不存在的字段和简单为false的字段。 表达式if [foo]在以下情况下返回false：

- [foo]在事件中不存在，
- [foo]存在于事件中，但是为false，或
- [foo]存在于事件中，但是无


有关更复杂的示例，[请参阅使用条件](https://www.elastic.co/guide/en/logstash/current/config-examples.html#using-conditionals)。

#### \@metadata字段
在Logstash 1.5和更高版本中，有一个称为@metadata的特殊字段。 @metadata的内容在输出时不会成为任何事件的一部分，这使得它非常适合用于条件语句，或扩展和构建具有字段引用和sprintf格式的事件字段。

以下配置文件将从STDIN产生事件。 无论键入什么将成为事件中的消息字段。 过滤器块中的mutate事件将添加几个字段，一些嵌套在@metadata字段中。
```
input { stdin { } }

filter {
  mutate { add_field => { "show" => "This data will be in the output" } }
  mutate { add_field => { "[@metadata][test]" => "Hello" } }
  mutate { add_field => { "[@metadata][no_show]" => "This data will not be in the output" } }
}

output {
  if [@metadata][test] == "Hello" {
    stdout { codec => rubydebug }
  }
}
```
让我们看看出来：
```
$ bin/logstash -f ../test.conf
Settings: Default pipeline workers: 8
Pipeline main started
asdf
{
       "message" => "asdf",
      "@version" => "1",
    "@timestamp" => "2016-06-30T02:08:03.148Z",
          "host" => "example.com",
          "show" => "This data will be in the output"
}
```
输入的“asdf”成为消息字段内容，条件成功地评估嵌套在@metadata字段中的测试字段的内容。 但是输出没有显示一个称为@metadata或其内容的字段。

rubydebug编解码器允许您显示@metadata字段的内容，如果添加配置标志，metadata => true：
```
    stdout { codec => rubydebug { metadata => true } }
```
让我们看看这个变化的输出：
```
$ bin/logstash -f ../test.conf
Settings: Default pipeline workers: 8
Pipeline main started
asdf
{
       "message" => "asdf",
      "@version" => "1",
    "@timestamp" => "2016-06-30T02:10:25.044Z",
          "host" => "example.com",
          "show" => "This data will be in the output",
     "@metadata" => {
           "test" => "Hello",
        "no_show" => "This data will not be in the output"
    }
}
```
现在，您可以看到@metadata字段及其子字段。

> 重要: 只有rubydebug编解码器允许您显示@metadata字段的内容。

每当您需要一个临时字段，但不希望它在最终输出中时，使用@metadata字段。

也许这个新字段最常见的用例之一是使用日期过滤器并具有临时时间戳。

此配置文件已经过简化，但使用Apache和Nginx Web服务器通用的时间戳格式。 在过去，您必须自己删除时间戳字段，在使用它覆盖@timestamp字段后。 使用@metadata字段，不再需要：
```
input { stdin { } }

filter {
  grok { match => [ "message", "%{HTTPDATE:[@metadata][timestamp]}" ] }
  date { match => [ "[@metadata][timestamp]", "dd/MMM/yyyy:HH:mm:ss Z" ] }
}

output {
  stdout { codec => rubydebug }
}
```
请注意，此配置将提取的数据放入grok过滤器中的[\@metadata] [timestamp]字段中。 让我们给这个配置一个示例日期字符串，看看什么出来：
```
$ bin/logstash -f ../test.conf
Settings: Default pipeline workers: 8
Pipeline main started
{
       "message" => "02/Mar/2014:15:36:43 +0100",
      "@version" => "1",
    "@timestamp" => "2014-03-02T14:36:43.000Z",
          "host" => "example.com"
}
```
而已！ 在输出中没有额外的字段，并且更干净的配置文件，因为您不必在日期过滤器中转换后删除“时间戳”字段。

另一个用例是CouchDB Changes输入插件（请参阅https://github.com/logstash-plugins/logstash-input-couchdb_changes）。 此插件会自动将CouchDB文档字段元数据捕获到输入插件本身的@metadata字段中。 当事件通过以由Elasticsearch索引时，Elasticsearch输出插件允许您指定操作（删除，更新，插入等）和document_id，如下所示：

```
output {
  elasticsearch {
    action => "%{[@metadata][action]}"
    document_id => "%{[@metadata][_id]}"
    hosts => ["example.com"]
    index => "index_name"
    protocol => "http"
  }
}
```

### 在配置中使用环境变量
此功能是实验性的，要启用它，您将需要使用--allow-env标志运行logstash。

#### 概述
- 您可以使用${var}在Logstash插件的配置中设置环境变量引用。
- 在Logstash启动时，每个引用将由环境变量的值替换。
- 替换是区分大小写的。
- 对未定义变量的引用引发Logstash配置错误。
- 您可以使用${var：default value}形式提供默认值。 如果环境变量未定义，Logstash使用默认值。
- 您可以在任何插件选项类型中添加环境变量引用：string，number，boolean，array或hash。
- 环境变量是不可变的。 如果更新环境变量，则必须重新启动Logstash以获取更新的值。

#### 例子
以下示例说明如何使用环境变量设置一些常用配置选项的值。


##### 设置TCP端口
下面是一个使用环境变量设置TCP端口的示例：
```
input {
  tcp {
    port => "${TCP_PORT}"
  }
}
```
现在让我们设置TCP_PORT的值：
```
export TCP_PORT=12345
```
在启动时，Logstash使用以下配置：
```
input {
  tcp {
    port => 12345
  }
}
```
如果未设置TCP_PORT环境变量，则Logstash返回配置错误。

您可以通过指定默认值来解决此问题：
```
input {
  tcp {
    port => "${TCP_PORT:54321}"
  }
}
```
现在，如果变量未定义，而不是返回配置错误，Logstash使用默认值：
```
input {
  tcp {
    port => 54321
  }
}
```
如果定义了环境变量，Logstash将使用为变量指定的值，而不是默认值。



##### 设置标签的值
以下是使用环境变量设置标记值的示例：
```
filter {
  mutate {
    add_tag => [ "tag1", "${ENV_TAG}" ]
  }
}
```
我们设置ENV_TAG的值：
```
export ENV_TAG="tag2"
```
在启动时，Logstash使用以下配置：
```
filter {
  mutate {
    add_tag => [ "tag1", "tag2" ]
  }
}
```

#####  设置文件路径
下面是一个使用环境变量设置日志文件路径的示例：
```
filter {
  mutate {
    add_field => {
      "my_path" => "${HOME}/file.log"
    }
  }
}
```
让我们设置HOME的值：
```
export HOME="/path"
```
在启动时，Logstash使用以下配置：
```
filter {
  mutate {
    add_field => {
      "my_path" => "/path/file.log"
    }
  }
}
```

### Logstash配置示例
以下示例说明如何配置Logstash以过滤事件，处理Apache日志和syslog消息，以及使用条件控制过滤器或输出处理哪些事件。


#### 配置过滤器
过滤器是一种内联处理机制，可以灵活地根据您的需要对数据进行切片和切片。 让我们来看看一些行动中的过滤器。 以下配置文件设置grok和日期过滤器。

```
input { stdin { } }

filter {
  grok {
    match => { "message" => "%{COMBINEDAPACHELOG}" }
  }
  date {
    match => [ "timestamp" , "dd/MMM/yyyy:HH:mm:ss Z" ]
  }
}

output {
  elasticsearch { hosts => ["localhost:9200"] }
  stdout { codec => rubydebug }
}
```
使用此配置运行Logstash：
```
bin/logstash -f logstash-filter.conf
```
现在，将以下行粘贴到您的终端，以便它将被stdin输入处理：
```
127.0.0.1 - - [11/Dec/2013:00:01:45 -0800] "GET /xampp/status.php HTTP/1.1" 200 3891 "http://cadenza/xampp/navi.php" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:25.0) Gecko/20100101 Firefox/25.0"
```
你应该看到一些返回到stdout的东西，看起来像这样：
```
{
        "message" => "127.0.0.1 - - [11/Dec/2013:00:01:45 -0800] \"GET /xampp/status.php HTTP/1.1\" 200 3891 \"http://cadenza/xampp/navi.php\" \"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:25.0) Gecko/20100101 Firefox/25.0\"",
     "@timestamp" => "2013-12-11T08:01:45.000Z",
       "@version" => "1",
           "host" => "cadenza",
       "clientip" => "127.0.0.1",
          "ident" => "-",
           "auth" => "-",
      "timestamp" => "11/Dec/2013:00:01:45 -0800",
           "verb" => "GET",
        "request" => "/xampp/status.php",
    "httpversion" => "1.1",
       "response" => "200",
          "bytes" => "3891",
       "referrer" => "\"http://cadenza/xampp/navi.php\"",
          "agent" => "\"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:25.0) Gecko/20100101 Firefox/25.0\""
}
```
如您所见，Logstash（在grok过滤器的帮助下）能够解析日志行（恰巧是以“组合日志”格式），并将其分解成许多不同的离散信息位。当您开始查询和分析我们的日志数据时，这是非常有用的。例如，您可以轻松地生成有关HTTP响应代码，IP地址，引荐来源网址等的报告。 Logstash包含了很多grok模式，所以很可能如果你需要解析一个通用的日志格式，有人已经为你做了工作。有关更多信息，请参阅GitHub上的Logstash grok模式列表。

在此示例中使用的其他过滤器是日期过滤器。此过滤器解析时间戳，并将其用作事件的时间戳（无论您何时接收日志数据）。您会注意到，此示例中的@timestamp字段设置为2013年12月11日，即使Logstash之后在某个时间点获取了事件。这在回填日志时很方便。它使您能够告诉Logstash“将此值用作此事件的时间戳”。

#### 处理Apache日志
让我们做一些实际有用的事情：process apache2 access log files！ 我们将从localhost上的文件中读取输入，并使用条件来根据我们的需要处理事件。 首先，创建一个名为logstash-apache.conf的文件，其中包含以下内容（您可以更改日志的文件路径以满足您的需要）：

```
input {
  file {
    path => "/tmp/access_log"
    start_position => "beginning"
  }
}

filter {
  if [path] =~ "access" {
    mutate { replace => { "type" => "apache_access" } }
    grok {
      match => { "message" => "%{COMBINEDAPACHELOG}" }
    }
  }
  date {
    match => [ "timestamp" , "dd/MMM/yyyy:HH:mm:ss Z" ]
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
  }
  stdout { codec => rubydebug }
}
```
然后，使用以下日志条目（或使用自己的Web服务器中的一些）创建上面配置的输入文件（在本例中为“/ tmp / access log”）：
```
71.141.244.242 - kurt [18/May/2011:01:48:10 -0700] "GET /admin HTTP/1.1" 301 566 "-" "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.9.2.3) Gecko/20100401 Firefox/3.6.3"
134.39.72.245 - - [18/May/2011:12:40:18 -0700] "GET /favicon.ico HTTP/1.1" 200 1189 "-" "Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 5.1; Trident/4.0; .NET CLR 2.0.50727; .NET CLR 3.0.4506.2152; .NET CLR 3.5.30729; InfoPath.2; .NET4.0C; .NET4.0E)"
98.83.179.51 - - [18/May/2011:19:35:08 -0700] "GET /css/main.css HTTP/1.1" 200 1837 "http://www.safesand.com/information.htm" "Mozilla/5.0 (Windows NT 6.0; WOW64; rv:2.0.1) Gecko/20100101 Firefox/4.0.1"

```
现在，使用-f标志运行Logstash以传递配置文件：
```
bin/logstash -f logstash-apache.conf
```
现在你应该在Elasticsearch中看到你的apache日志数据！ Logstash打开并读取指定的输入文件，处理遇到的每个事件。 记录到此文件的任何其他行也将被捕获，由Logstash作为事件处理，并存储在Elasticsearch中。 作为附加的好处，它们被存储为字段“type”设置为“apache_access”（这通过输入配置中的类型⇒“apache_access”行来完成）。

在此配置中，Logstash只监视apache access_log，但通过更改上述配置中的一行，可以轻松查看access_log和error_log（实际上，任何匹配* log的文件）：
```
input {
  file {
    path => "/tmp/*_log"
...
```
当您重新启动Logstash时，它将处理错误日志和访问日志。 但是，如果您检查数据（可能使用elasticsearch-kopf），您会看到access_log被分解为离散字段，但error_log不是。 这是因为我们使用一个grok过滤器来匹配标准的组合apache日志格式，并自动将数据分割成单独的字段。 如果我们可以控制一行是如何解析的，根据它的格式不是很好吗？ 好吧，我们可以...

注意，Logstash没有重新处理已经在access_log文件中看到的事件。 当从文件读取时，Logstash保存其位置，并且只有在添加新行时才处理新行。 整齐！

#### 使用条件
您可以使用条件控制过滤器或输出处理哪些事件。 例如，您可以根据出现在哪个文件（access_log，error_log和以“log”结尾的其他随机文件）标记每个事件。
```
input {
  file {
    path => "/tmp/*_log"
  }
}

filter {
  if [path] =~ "access" {
    mutate { replace => { type => "apache_access" } }
    grok {
      match => { "message" => "%{COMBINEDAPACHELOG}" }
    }
    date {
      match => [ "timestamp" , "dd/MMM/yyyy:HH:mm:ss Z" ]
    }
  } else if [path] =~ "error" {
    mutate { replace => { type => "apache_error" } }
  } else {
    mutate { replace => { type => "random_logs" } }
  }
}

output {
  elasticsearch { hosts => ["localhost:9200"] }
  stdout { codec => rubydebug }
}
```
此示例使用类型字段标记所有事件，但实际上不会解析错误或随机文件。 有这么多类型的错误日志，他们应该如何标记真的取决于你正在使用什么日志。

类似地，您可以使用条件将事件定向到特定输出。 例如，您可以：

- 警报任何具有状态5xx的apache事件的nagios
- 将任何4xx状态记录到Elasticsearch
- 通过statsd记录所有状态码的命中

要告诉nagios任何具有5xx状态代码的http事件，您首先需要检查类型字段的值。 如果是apache，那么您可以检查状态字段是否包含5xx错误。 如果是，请将其发送到nagios。 如果不是5xx错误，请检查状态字段是否包含4xx错误。 如果是，请将其发送到Elasticsearch。 最后，无论状态字段包含以下内容，将所有apache状态代码发送到statsd：

```
output {
  if [type] == "apache" {
    if [status] =~ /^5\d\d/ {
      nagios { ...  }
    } else if [status] =~ /^4\d\d/ {
      elasticsearch { ... }
    }
    statsd { increment => "apache.%{status}" }
  }
}
```
#### 处理Syslog消息
Syslog是Logstash最常见的用例之一，它处理得非常好（只要日志行大致符合RFC3164）。 Syslog是事实上的UNIX网络日志记录标准，通过rsyslog将消息从客户端计算机发送到本地文件或集中式日志服务器。 对于这个例子，你不需要一个正常的syslog实例; 我们将从命令行中伪造它，以便您可以感觉到发生了什么。

首先，让我们为Logstash + syslog创建一个简单的配置文件，称为logstash-syslog.conf。
```
input {
  tcp {
    port => 5000
    type => syslog
  }
  udp {
    port => 5000
    type => syslog
  }
}

filter {
  if [type] == "syslog" {
    grok {
      match => { "message" => "%{SYSLOGTIMESTAMP:syslog_timestamp} %{SYSLOGHOST:syslog_hostname} %{DATA:syslog_program}(?:\[%{POSINT:syslog_pid}\])?: %{GREEDYDATA:syslog_message}" }
      add_field => [ "received_at", "%{@timestamp}" ]
      add_field => [ "received_from", "%{host}" ]
    }
    date {
      match => [ "syslog_timestamp", "MMM  d HH:mm:ss", "MMM dd HH:mm:ss" ]
    }
  }
}

output {
  elasticsearch { hosts => ["localhost:9200"] }
  stdout { codec => rubydebug }
}
```
使用此新配置运行Logstash：
```
bin/logstash -f logstash-syslog.conf
```
通常，客户端机器将连接到端口5000上的Logstash实例并发送其消息。 对于这个例子，我们将telnet到Logstash并输入日志行（类似于我们之前输入的日志行到STDIN）。 打开另一个shell窗口以与Logstash syslog输入进行交互并输入以下命令：
```
telnet localhost 5000
```
复制并粘贴以下行作为示例。 （随意尝试一些自己的，但记住，如果grok过滤器不正确的数据，他们可能不会解析）。
```
Dec 23 12:11:43 louis postfix/smtpd[31499]: connect from unknown[95.75.93.154]
Dec 23 14:42:56 louis named[16000]: client 199.48.164.7#64817: query (cache) 'amsterdamboothuren.com/MX/IN' denied
Dec 23 14:30:01 louis CRON[619]: (www-data) CMD (php /usr/share/cacti/site/poller.php >/dev/null 2>/var/log/cacti/poller-error.log)
Dec 22 18:28:06 louis rsyslogd: [origin software="rsyslogd" swVersion="4.2.0" x-pid="2253" x-info="http://www.rsyslog.com"] rsyslogd was HUPed, type 'lightweight'.
```
现在，在处理和解析消息时，您应该在原始shell中看到Logstash的输出！
```
{
                 "message" => "Dec 23 14:30:01 louis CRON[619]: (www-data) CMD (php /usr/share/cacti/site/poller.php >/dev/null 2>/var/log/cacti/poller-error.log)",
              "@timestamp" => "2013-12-23T22:30:01.000Z",
                "@version" => "1",
                    "type" => "syslog",
                    "host" => "0:0:0:0:0:0:0:1:52617",
        "syslog_timestamp" => "Dec 23 14:30:01",
         "syslog_hostname" => "louis",
          "syslog_program" => "CRON",
              "syslog_pid" => "619",
          "syslog_message" => "(www-data) CMD (php /usr/share/cacti/site/poller.php >/dev/null 2>/var/log/cacti/poller-error.log)",
             "received_at" => "2013-12-23 22:49:22 UTC",
           "received_from" => "0:0:0:0:0:0:0:1:52617",
    "syslog_severity_code" => 5,
    "syslog_facility_code" => 1,
         "syslog_facility" => "user-level",
         "syslog_severity" => "notice"
}
```


### 重新加载配置文件
从Logstash 2.3开始，您可以将Logstash设置为自动检测和重新加载配置更改。

要启用自动配置重新加载，请使用指定的--auto-reload（或-r）命令行选项启动Logstash。 例如：
```
bin/logstash –f apache.config --auto-reload
```
> 当您从命令行指定要在配置设置中传递的-e标志时，--auto-reload选项不可用。

默认情况下，Logstash每3秒检查一次配置更改。 要更改此时间间隔，请使用--reload-interval <seconds>选项，其中seconds指定Logstash检查配置文件以进行更改的频率。

如果Logstash已在运行但未启用自动重新加载，则可以强制Logstash重新加载配置文件，并通过向运行Logstash的进程发送SIGHUP（信号挂断）来重新启动管道。 例如：
```
kill -1 14175
```
其中14175是运行Logstash的进程的ID。

##### 自动配置重新加载的工作原理
当Logstash检测到配置文件中的更改时，它会通过停止所有输入来停止当前管道，并尝试创建使用更新配置的新管道。 在验证新配置的语法后，Logstash验证所有输入和输出都可以初始化（例如，所有需要的端口都打开）。 如果检查成功，Logstash将使用新管道交换现有管道。 如果检查失败，旧的管道继续运行，并且错误传播到控制台。

在自动配置重新加载期间，JVM不会重新启动。 管道的创建和交换都发生在同一过程中。

### 命令行标志
Logstash有以下标志。 您可以使用--help标志来显示此信息。

- -f, --config CONFIG_PATH
从特定文件或目录加载Logstash配置。 如果给定目录，那个目录中的所有文件将按字典顺序连接，然后解析为单个配置文件。 您还可以指定通配符（globs）和任何匹配的文件将按照上述顺序加载。

- -e CONFIG_STRING
使用给定的字符串作为配置数据。 与配置文件相同的语法。 如果未指定输入，则使用以下命令作为默认输入：input {stdin {type => stdin}}，如果未指定输出，则使用以下命令作为默认输出：output {stdout {codec = rubydebug}}。 如果您希望使用两个默认值，请使用空字符串作为-e标志。 默认值为“”。

- -w, --pipeline-workers COUNT
设置要运行的管道工作线程的数量。 默认值为8。

- -b, --pipeline-batch-size SIZE
管道工作的批次大小。默认值为125.此参数定义单个工作线程在尝试执行其过滤器和输出之前将收集的最大事件数。 较大的批量大小通常更有效，但是以增加的内存开销为代价。 您可能必须通过设置LS_HEAP_SIZE变量来有效地使用该选项来增加JVM堆大小。

- -u, --pipeline-batch-delay DELAY_IN_MS
在创建管道事件批处理时，在轮询下一个事件时等待的时间。 默认值为5ms。

- -w, --filterworkers COUNT
DEPRECATED。 现在是--pipeline-workers和-w的别名。

- -l, --log FILE
将Logstash内部日志写入给定文件。 没有这个标志，Logstash会将日志发送到标准输出。

- -v
DEPRECATED。 增加Logstash内部日志的详细程度。 指定一次将显示信息日志。 指定两次会显示调试日志。 此标志已弃用。 您应该使用--verbose或--debug。

- --quiet
Quieter Logstash日志记录。 这仅仅导致错误被发出。

- --verbose
更详细的日志记录。 这导致发出信息级日志。

- --debug
最详细的日志记录。 这将导致发出调试级日志。

- --debug-config
将编译的配置ruby代码打印为调试日志（您还必须启用--debug）。 警告：这将包括传递到插件配置为明文的任何密码选项，并可能导致明文密码出现在您的日志！ 默认值为false。

- -V, --version
发出Logstash及其朋友的版本，然后退出。

- -p, --pluginpath PATH
一个在哪里找到插件的路径。 此标志可以多次提供以包括多个路径。 插件应该在特定的目录层次结构中：PATH / logstash / TYPE / NAME.rb其中TYPE是输入，过滤器，输出或编解码器，NAME是插件的名称。

- -t, --configtest
检查配置的有效语法，然后退出。 注意，不使用此标志检查grok模式的正确性。 Logstash可以从目录中读取多个配置文件。 如果将此标志与--debug组合，Logstash将记录组合的配置文件，注释各个配置块与源文件。

- --[no-]allow-unsafe-shutdown
强制Logstash在关机期间退出，即使内存中仍然存在飞行事件。 默认情况下，Logstash将拒绝退出，直到所有接收到的事件都被推送到输出。 默认值为false。

- -r, --[no-]auto-reload
监视配置更改，并在配置更改时重新加载。 NOT：使用SIGHUP手动重新加载配置默认值为false。

- --reload-interval RELOAD_INTERVAL
轮询轮询配置位置的频率（以秒为单位）。 默认值为3秒。

- --allow-env
[实验性]此功能是实验性功能，可能会在将来的版本中完全更改或删除。 启用环境变量值的模板。 字符串中的$ {VAR}实例将替换为各自的名为“VAR”的环境变量值。 默认值为false。

- --[no-]log-in-json
指定Logstash应以JSON格式写入自己的日志 - 每行一个事件。 如果为false，Logstash将使用Ruby的Object＃inspect（不容易进行机器解析）进行日志记录。 默认值为false。

- -h, --help
打印帮助

### 管理多行事件

几个用例生成跨越多行文本的事件。 为了正确处理这些多行事件，Logstash需要知道如何分辨哪些行是单个事件的一部分。

多线事件处理是复杂的，并且依赖于正确的事件排序。 保证有序日志处理的最好方法是尽可能早地在流水线中实现处理。 Logstash管道中的首选工具是多行编解码器，它使用一组简单的规则从单个输入合并行。

配置多线插件的最重要的方面如下：

- pattern选项指定正则表达式。 与指定的正则表达式匹配的行被视为上一行的连续或新的多行事件的开始。 您可以使用grok正则表达式模板与此配置选项。
- what选项有两个值：previous或next。 上一个值指定与pattern选项中的值匹配的行是上一行的一部分。 下一个值指定与pattern选项中的值匹配的行是以下行的一部分。* negate选项将多行编解码器应用于与pattern选项中指定的正则表达式不匹配的行。

有关配置选项的更多信息，请参阅多线编解码器或多线滤波器插件的完整文档。

> 注意： 对于更复杂的需求，多线过滤器在处理的过滤阶段执行类似的任务，其中Logstash实例聚合多个输入。 多线过滤器插件不是线程安全的。 避免对多行过滤器使用多个过滤器工作。 您可以在此Github问题上跟踪升级多行编解码器功能的进度。

#### Multiline插件配置示例
本节中的示例涵盖以下用例：

- 将Java堆栈跟踪合并到单个事件中
- 将C风格的线延续组合成单个事件
- 组合来自时间戳事件的多个行


##### Java堆栈跟踪
Java堆栈跟踪由多行组成，每行后面以空格开头，如下例所示：
```
Exception in thread "main" java.lang.NullPointerException
        at com.example.myproject.Book.getTitle(Book.java:16)
        at com.example.myproject.Author.getBookTitles(Author.java:25)
        at com.example.myproject.Bootstrap.main(Bootstrap.java:14)
```
要将这些行合并到Logstash中的单个事件中，请对多行编解码器使用以下配置：
```
input {
  stdin {
    codec => multiline {
      pattern => "^\s"
      what => "previous"
    }
  }
}
```
此配置将以空格开头的任何行合并到上一行。


##### 连续的行
一些编程语言使用行尾的\\字符来表示行继续，如下例所示：
```
printf ("%10.10ld  \t %10.10ld \t %s\
  %f", w, x, y, z );
```
要将这些行合并到Logstash中的单个事件中，请对多行编解码器使用以下配置：
```
input {
  stdin {
    codec => multiline {
      pattern => "\\$"
      what => "next"
    }
  }
}
```
此配置将以\\字符结尾的任何行合并到以下行。


##### 时间戳
来自服务（例如Elasticsearch）的活动日志通常以时间戳开头，后跟有关特定活动的信息，如下例所示：
```
[2015-08-24 11:49:14,389][INFO ][env                      ] [Letha] using [1] data paths, mounts [[/
(/dev/disk1)]], net usable_space [34.5gb], net total_space [118.9gb], types [hfs]
```
要将这些行合并到Logstash中的单个事件中，请对多行编解码器使用以下配置：
```
input {
  file {
    path => "/var/log/someapp.log"
    codec => multiline {
      pattern => "^%{TIMESTAMP_ISO8601} "
      negate => true
      what => previous
    }
  }
}
```
此配置使用negate选项指定不以时间戳开头的任何行属于上一行。

### 部署和扩展Logstash
随着Logstash的用例不断发展，给定规模的首选架构将发生变化。 本节从复杂性的增加顺序讨论一系列Logstash体系结构，从最小安装和向系统添加元素开始。 本节中的示例部署写入Elasticsearch集群，但Logstash可以写入大量的端点。

#### 最小安装
最小Logstash安装具有一个Logstash实例和一个Elasticsearch实例。 这些实例是直接连接的。 Logstash使用输入插件来接收数据，并使用Elasticsearch输出插件来索引Elasticsearch中的数据，跟在Logstash处理管道之后。 Logstash实例具有基于实例的配置文件在启动时构建的固定管道。 您必须指定输入插件。 输出默认为stdout，并且管道的过滤部分（在下一部分中讨论）是可选的。

![img](http://n.sinaimg.cn/games/3ece443e/20161024/deploy_1.png)

#### 使用过滤器
日志数据通常是非结构化的，通常包含与您的用例无关的无关信息，有时缺少可从日志内容导出的相关信息。您可以使用过滤器插件来解析日志到字段，删除不必要的信息，并从现有字段中导出其他信息。例如，过滤器可以从IP地址导出地理位置信息，并将该信息添加到日志，或者使用grok过滤器解析和构造任意文本。

添加过滤器插件可能会显着影响性能，具体取决于过滤器插件执行的计算量，以及正在处理的日志的卷。 grok过滤器的正则表达式计算特别是资源密集型。解决这种对计算资源的增加的需求的一种方式是在多核机器上使用并行处理。使用-w开关设置Logstash过滤任务的执行线程数。例如，bin / logstash -w 8命令使用八个不同的线程进行过滤器处理。


![img](http://n.sinaimg.cn/games/3ece443e/20161024/deploy_2.png)

#### 使用Filebeat
Filebeat是一个轻量级的，资源友好的工具，在Go中编写，从服务器上的文件收集日志，并将这些日志转发到其他机器进行处理。 Filebeat使用Beats协议与集中式Logstash实例通信。 配置接收Beats数据的Logstash实例以使用Beats输入插件。

Filebeat使用托管源数据的机器的计算资源，Beats输入插件将对Logstash实例的资源需求最小化，使得此架构对于具有资源约束的用例非常有吸引力。

![img](http://n.sinaimg.cn/games/3ece443e/20161024/deploy_3.png)

#### 缩放到较大的Elasticsearch群集
通常，Logstash不与单个Elasticsearch节点通信，而是与包含多个节点的集群通信。默认情况下，Logstash使用HTTP协议将数据移入集群。

您可以使用Elasticsearch HTTP REST API将数据索引到Elasticsearch集群中。这些API表示JSON中的索引数据。使用REST API不需要Java客户端类或任何其他JAR文件，并且与传输或节点协议相比没有性能上的缺点。您可以使用支持SSL和HTTP基本身份验证的Shield插件来保护使用HTTP REST API的通信。

使用HTTP协议时，您可以配置Logstash Elasticsearch输出插件，以自动在Elasticsearch集群中的指定主机集上负载平衡索引请求。指定多个Elasticsearch节点还通过将流量路由到活动的Elasticsearch节点来为Elasticsearch集群提供高可用性。

您还可以使用Elasticsearch Java API将数据序列化为二进制表示，使用传输协议。传输协议可以侦听请求的端点，并在Elasticsearch集群中选择任意客户端或数据节点。

使用HTTP或传输协议使Logstash实例与Elasticsearch集群分离。相反，节点协议使运行Logstash实例的机器加入Elasticsearch集群，运行Elasticsearch实例。需要索引的数据从此节点传播到集群的其余部分。由于机器是集群的一部分，因此集群拓扑可用，使得节点协议非常适合使用相对较少数量的持久连接的用例。

您还可以使用第三方硬件或软件负载平衡器来处理Logstash和外部应用程序之间的连接。

> 注意: 请确保您的Logstash配置不直接连接到执行专用群集管理的Elasticsearch专用主节点。将Logstash连接到客户端或数据节点以保护Elasticsearch集群的稳定性。

![img](http://n.sinaimg.cn/games/3ece443e/20161024/deploy_4.png)


#### 管理吞吐量峰值与消息队列
当进入Logstash管道的数据超过Elasticsearch集群获取数据的能力时，可以使用消息队列作为缓冲区。默认情况下，当索引器使用率低于传入数据速率时，Logstash控制传入事件。由于此限制可能导致事件在数据源中缓冲，因此防止消息队列的背压成为管理部署的重要部分。

向Logstash部署添加消息队列还提供了防止数据丢失的级别。当从消息队列中消耗数据的Logstash实例失败时，数据可以从消息队列重播到活动Logstash实例。

存在多个第三方消息队列，例如Redis，Kafka或RabbitMQ。 Logstash提供输入和输出插件来与其中几个第三方消息队列集成。当Logstash部署配置了消息队列时，Logstash在功能上分为两个阶段：运送实例（用于处理消息队列中的数据提取和存储）和索引实例（从消息队列检索数据），应用任何配置的过滤，以及将过滤的数据写入Elasticsearch索引。

![img](http://n.sinaimg.cn/games/3ece443e/20161024/deploy_5.png)


#### 多个连接用于Logstash高可用性
要使Logstash部署对单个实例故障更具弹性，您可以在数据源计算机和Logstash集群之间设置负载均衡器。 负载平衡器处理与Logstash实例的各个连接，以确保即使在单个实例不可用时，数据提取和处理的连续性。

![img](http://n.sinaimg.cn/games/3ece443e/20161024/deploy_6.png)

如果专用于该输入类型的Logstash实例不可用，则上图中的体系结构无法处理来自特定类型（例如RSS源或文件）的输入。 为了更稳健的输入处理，请为多个输入配置每个Logstash实例，如下图所示：
![img](http://n.sinaimg.cn/games/3ece443e/20161024/deploy_7.png)

此架构根据您配置的输入来并行化Logstash工作负载。 使用更多输入，您可以添加更多Logstash实例以水平缩放。 独立的并行管道还通过消除单点故障来提高堆栈的可靠性。


#### 缩放Logstash
成熟的Logstash部署通常具有以下管道：

- 输入层使用来自源的数据，并由具有正确输入插件的Logstash实例组成。
- 消息队列用作缓冲区以保存所接收的数据，并用作故障转移保护。
- 过滤器层对从消息队列消耗的数据应用解析和其他处理。
- 索引层将处理的数据移动到Elasticsearch中。

这些层中的任何层可以通过添加计算资源来缩放。 随着用例的发展和根据需要添加资源，定期检查这些组件的性能。 当Logstash常规地限制传入事件时，请考虑为消息队列添加存储。 或者，通过添加更多Logstash索引实例来增加Elasticsearch集群的数据消耗速率。
