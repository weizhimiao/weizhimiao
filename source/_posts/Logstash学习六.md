---
title: Logstash学习六
date: 2016-10-26 20:30:00
tags:
- Logstash
categories:
- Logstash
---

- 编解码器插件

<!-- more -->

## 编解码器插件

编解码器插件更改事件的数据表示。编解码器本质上是可以作为输入或输出的一部分操作的流过滤器。

以下编解码器插件可用：



**avro**

> 将序列化的Avro记录读取为Logstash事件

[logstash-codec-avro](https://github.com/logstash-plugins/logstash-codec-avro)

**cef**

> 读取ArcSight公共事件格式（CEF）。

[logstash-codec-cef](https://github.com/logstash-plugins/logstash-codec-cef)

**cloudtrail**

> 读取AWS Cloudtrail事件

[logstash-codec-cloudtrail](https://github.com/logstash-plugins/logstash-codec-cloudtrail)

**cloudfront**

> 阅读AWS CloudFront报告

[logstash-codec-cloudfront](https://github.com/logstash-plugins/logstash-codec-cloudfront)

**collectd**

> 使用UDP从collectd二进制协议读取事件。

[logstash-codec-collectd](https://github.com/logstash-plugins/logstash-codec-collectd)

**compress_spooler**

> 将事件压缩为假脱机批处理

[logstash-codec-compress_spooler](https://github.com/logstash-plugins/logstash-codec-compress_spooler)

**dots**

> 每个事件发送1个点到stdout用于性能跟踪

[logstash-codec-dots](https://github.com/logstash-plugins/logstash-codec-dots)

**edn**

> 读取EDN格式数据

[logstash-codec-edn](https://github.com/logstash-plugins/logstash-codec-edn)

**edn_lines**

> 读取换行分隔的EDN格式数据

[logstash-codec-edn_lines](https://github.com/logstash-plugins/logstash-codec-edn_lines)

**es_bulk**

> 将Elasticsearch批量格式读取为单独的事件以及元数据

[logstash-codec-es_bulk](https://github.com/logstash-plugins/logstash-codec-es_bulk)

**fluent**

> 读取fluentd msgpack模式

[logstash-codec-fluent](https://github.com/logstash-plugins/logstash-codec-fluent)

**graphite**

> 读取graphite格式的行

[logstash-codec-graphite](https://github.com/logstash-plugins/logstash-codec-graphite)

**gzip_lines**

> 读取gzip编码内容

[logstash-codec-gzip_lines](https://github.com/logstash-plugins/logstash-codec-gzip_lines)

**json**

> 读取JSON格式的内容，在JSON数组中为每个元素创建一个事件

[logstash-codec-json](https://github.com/logstash-plugins/logstash-codec-json)

**json_lines**

> 读取以换行符分隔的JSON

[logstash-codec-json_lines](https://github.com/logstash-plugins/logstash-codec-json_lines)

**line**

> 读取面向行的文本数据

[logstash-codec-line](https://github.com/logstash-plugins/logstash-codec-line)

**msgpack**

[logstash-codec-msgpack](https://github.com/logstash-plugins/logstash-codec-msgpack)

**multiline**

> 将多行消息合并为单个事件

[logstash-codec-multiline](https://github.com/logstash-plugins/logstash-codec-multiline)

**netflow**

> 读取Netflow v5和Netflow v9数据

[logstash-codec-netflow](https://github.com/logstash-plugins/logstash-codec-netflow)

**nmap**

> 以XML格式读取Nmap数据

[logstash-codec-nmap](https://github.com/logstash-plugins/logstash-codec-nmap)

**oldlogstashjson**

> 在Logstash 1.2.0之前版本中使用的模式中读取Logstash JSON

[logstash-codec-oldlogstashjson](https://github.com/logstash-plugins/logstash-codec-oldlogstashjson)

**plain**

> 读取纯文本，而不在事件之间进行分隔

[logstash-codec-plain](https://github.com/logstash-plugins/logstash-codec-plain)

**rubydebug**

> 将Ruby Awesome打印库应用于Logstash事件

[logstash-codec-rubydebug](https://github.com/logstash-plugins/logstash-codec-rubydebug)

**s3_plain**

> 提供与早期版本的S3输出的向后兼容性

[logstash-codec-s3_plain](https://github.com/logstash-plugins/logstash-codec-s3_plain)

**spool**

> 收集事件并批量传输

[logstash-codec-spool](https://github.com/logstash-plugins/logstash-codec-spool)


### edn_lines

#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
edn_lines {
}
```

### es_bulk
此编解码器会将Elasticsearch批量格式解码为单个事件，并将元数据解码为@metadata字段。

目前不支持编码，因为Elasticsearch输出以批量格式提交Logstash事件。

#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
es_bulk {
}
```

### gzip_lines

> 这是一个社区维护的插件！ 默认情况下它不随Logstash一起提供，但通过运行`bin/logstash-plugin install logstash-codec-gzip_lines` 可以很容易地安装。

此编解码器将读取gzip编码的内容

#### 概述
这个插件支持下列配置选项：

所需的配置选项：
```
gzip_lines {
  }
```
可用的配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
charset|string, one of ["ASCII-8BIT", "Big5", "Big5-HKSCS", "Big5-UAO", "CP949", "Emacs-Mule", "EUC-JP", "EUC-KR", "EUC-TW", "GB18030", "GBK", "ISO-8859-1", "ISO-8859-2", "ISO-8859-3", "ISO-8859-4", "ISO-8859-5", "ISO-8859-6", "ISO-8859-7", "ISO-8859-8", "ISO-8859-9", "ISO-8859-10", "ISO-8859-11", "ISO-8859-13", "ISO-8859-14", "ISO-8859-15", "ISO-8859-16", "KOI8-R", "KOI8-U", "Shift_JIS", "US-ASCII", "UTF-8", "UTF-16BE", "UTF-16LE", "UTF-32BE", "UTF-32LE", "Windows-1251", "GB2312", "Windows-31J", "IBM437", "IBM737", "IBM775", "CP850", "IBM852", "CP852", "IBM855", "CP855", "IBM857", "IBM860", "IBM861", "IBM862", "IBM863", "IBM864", "IBM865", "IBM866", "IBM869", "Windows-1258", "GB1988", "macCentEuro", "macCroatian", "macCyrillic", "macGreek", "macIceland", "macRoman", "macRomania", "macThai", "macTurkish", "macUkraine", "CP950", "CP951", "stateless-ISO-2022-JP", "eucJP-ms", "CP51932", "EUC-JIS-2004", "GB12345", "ISO-2022-JP", "ISO-2022-JP-2", "CP50220", "CP50221", "Windows-1252", "Windows-1250", "Windows-1256", "Windows-1253", "Windows-1255", "Windows-1254", "TIS-620", "Windows-874", "Windows-1257", "MacJapanese", "UTF-7", "UTF8-MAC", "UTF-16", "UTF-32", "UTF8-DoCoMo", "SJIS-DoCoMo", "UTF8-KDDI", "SJIS-KDDI", "ISO-2022-JP-KDDI", "stateless-ISO-2022-JP-KDDI", "UTF8-SoftBank", "SJIS-SoftBank", "BINARY", "CP437", "CP737", "CP775", "IBM850", "CP857", "CP860", "CP861", "CP862", "CP863", "CP864", "CP865", "CP866", "CP869", "CP1258", "Big5-HKSCS:2008", "eucJP", "euc-jp-ms", "EUC-JISX0213", "eucKR", "eucTW", "EUC-CN", "eucCN", "CP936", "ISO2022-JP", "ISO2022-JP2", "ISO8859-1", "CP1252", "ISO8859-2", "CP1250", "ISO8859-3", "ISO8859-4", "ISO8859-5", "ISO8859-6", "CP1256", "ISO8859-7", "CP1253", "ISO8859-8", "CP1255", "ISO8859-9", "CP1254", "ISO8859-10", "ISO8859-11", "CP874", "ISO8859-13", "CP1257", "ISO8859-14", "ISO8859-15", "ISO8859-16", "CP878", "MacJapan", "ASCII", "ANSI_X3.4-1968", "646", "CP65000", "CP65001", "UTF-8-MAC", "UTF-8-HFS", "UCS-2BE", "UCS-4BE", "UCS-4LE", "CP932", "csWindows31J", "SJIS", "PCK", "CP1251", "external", "locale"]|No|"UTF-8"

#### 详情
**charset**
- 值可以是以下任何一个：ASCII-8BIT，Big5，Big5-HKSCS，Big5-UAO，CP949，Emacs-Mule，EUC-JP，EUC-KR，EUC-TW，GB18030，GBK，ISO-8859-1，ISO- ISO-8859-3，ISO-8859-4，ISO-8859-5，ISO-8859-6，ISO-8859-7，ISO-8859-8，ISO-8859-9，ISO- 10，ISO-8859-11，ISO-8859-13，ISO-8859-14，ISO-8859-15，ISO-8859-16，KOI8-R，KOI8-U，Shift_JIS，US-ASCII，UTF- UT85，IBM855，IBM855，IBM857，IBM860，IBM861，IBM862，IBM853，UT86，UTF-16BE，UTF-16LE，UTF-32BE，UTF-32LE，Windows-1251，GB2312，Windows-31J，IBM437，IBM737，IBM775， IBM863，IBM864，IBM865，IBM866，IBM869，Windows-1258，GB1988，macCentEuro，macCroatian，macCyrillic，macGreek，macIlandland，macRoman，macRomania，macThai，macTurkish，macUkraine，CP950，CP951，stateless-ISO-2022-JP，eucJP- ms，CP51932，EUC-JIS-2004，GB12345，ISO-2022-JP，ISO-2022-JP-2，CP50220，CP50221，Windows-1252，Windows-1250，Windows-1256，Windows-1253， Windows-1254，TIS-620，Windows-874，Windows-1257，MacJapanese，UTF-7，UTF8-MAC，UTF-16，UTF-32，UTF8-DoCoMo，SJIS-DoCoMo，UTF8-KDDI，SJIS- ISO-2022-JP-KDDI，无状态ISO-2022-JP-KDDI，UTF8-软银行，SJIS-软银行，BINARY，CP437，CP737，CP775，IBM850，CP857，CP860，CP861，CP862，CP863，CP864，CP865， CP866，CP869，CP1258，Big5-HKSCS：2008，eucJP，euc-jp-ms，EUC-JISX0213，eucKR，eucTW，EUC-CN，eucCN，CP936，ISO2022-JP，ISO2022-JP2，ISO8859-1， ISO8859-3，ISO8859-4，ISO8859-5，ISO8859-6，CP1256，ISO8859-7，CP1253，ISO8859-8，CP1255，ISO8859-9，CP1254，ISO8859-10，ISO8859-11， CP874，ISO8859-13，CP1257，ISO8859-14，ISO8859-15，ISO8859-16，CP878，MacJapan，ASCII，ANSI_X3.4-1968,646，CP65000，CP65001，UTF-8-MAC，UTF-8-HFS， UCS-2BE，UCS-4BE，UCS-4LE，CP932，csWindows31J，SJIS，PCK，CP1251，external，locale
- 默认值为“UTF-8”

此编解码器中使用的字符编码。实例包括“UTF-8”和“CP1252”

JSON需要有效的UTF-8字符串，但在某些情况下，发出JSON的软件在另一种编码（例如nxlog）中也是如此。在这样的奇怪的情况下，你可以设置charset设置为文本的实际编码，logstash会为你转换它。

对于nxlog用户，您需要将其设置为“CP1252”
