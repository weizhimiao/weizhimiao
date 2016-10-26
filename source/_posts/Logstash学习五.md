---
title: Logstash学习五
date: 2016-10-26 20:30:00
tags:
- Logstash
categories:
- Logstash
---




## 过滤插件

过滤器插件对事件执行中间处理。 过滤器通常根据事件的特征有条件地应用。

以下过滤器插件可用：


**aggregate**

> 聚合来自单个任务的多个事件的信息

[logstash-filter-aggregate](https://github.com/logstash-plugins/logstash-filter-aggregate)

**alter**

> 对mutate过滤器不处理的字段执行常规更改

[logstash-filter-alter](https://github.com/logstash-plugins/logstash-filter-alter)

**anonymize**

> 将字段值替换为一致的散列

[logstash-filter-anonymize](https://github.com/logstash-plugins/logstash-filter-anonymize)

**collate**

> 按时间或计数整理事件

[logstash-filter-collate](https://github.com/logstash-plugins/logstash-filter-collate)

**csv**

> 将逗号分隔的值数据解析为单个字段

[logstash-filter-csv](https://github.com/logstash-plugins/logstash-filter-csv)

**cidr**

> 根据网络块列表检查IP地址

[logstash-filter-cidr](https://github.com/logstash-plugins/logstash-filter-cidr)

**clone**

> 复制事件

[logstash-filter-clone](https://github.com/logstash-plugins/logstash-filter-clone)

**cipher**

> 应用或删除事件的密码

[logstash-filter-cipher](https://github.com/logstash-plugins/logstash-filter-cipher)

**checksum**

> 基于事件中的字段创建校验和

[logstash-filter-checksum](https://github.com/logstash-plugins/logstash-filter-checksum)

**date**

> 解析从用作事件的Logstash时间戳的字段开始

[logstash-filter-date](https://github.com/logstash-plugins/logstash-filter-date)

**de_dot**

> 计算上昂贵的过滤器，从字段名称中删除点

[logstash-filter-de_dot](https://github.com/logstash-plugins/logstash-filter-de_dot)

**dns**

> 执行标准或反向DNS查找

[logstash-filter-dns](https://github.com/logstash-plugins/logstash-filter-dns)

**drop**

> 删除所有事件

[logstash-filter-drop](https://github.com/logstash-plugins/logstash-filter-drop)

**elasticsearch**

> 将字段从Elasticsearch中的先前日志事件复制到当前事件

[logstash-filter-elasticsearch](https://github.com/logstash-plugins/logstash-filter-elasticsearch)

**extractnumbers**

> 从字符串中提取数字

[logstash-filter-extractnumbers](https://github.com/logstash-plugins/logstash-filter-extractnumbers)

**environment**

> 将环境变量存储为元数据子字段

[logstash-filter-environment](https://github.com/logstash-plugins/logstash-filter-environment)

**elapsed**

> 计算一对事件之间经过的时间

[logstash-filter-elapsed](https://github.com/logstash-plugins/logstash-filter-elapsed)

**fingerprint**

> 通过用一致的哈希替换值来指纹字段

[logstash-filter-fingerprint](https://github.com/logstash-plugins/logstash-filter-fingerprint)

**geoip**

> 添加有关IP地址的地理信息

[logstash-filter-geoip](https://github.com/logstash-plugins/logstash-filter-geoip)

**grok**

> 将非结构化事件数据解析到字段中

[logstash-filter-grok](https://github.com/logstash-plugins/logstash-filter-grok)

**i18n**

> 从字段中删除特殊字符

[logstash-filter-i18n](https://github.com/logstash-plugins/logstash-filter-i18n)

**json**

> 将字段序列化为JSON

[logstash-filter-json](https://github.com/logstash-plugins/logstash-filter-json)

**json_encode**

> 将字段序列化为JSON


[logstash-filter-json_encode](https://github.com/logstash-plugins/logstash-filter-json_encode)

**kv**

> 解析键值对


[logstash-filter-kv](https://github.com/logstash-plugins/logstash-filter-kv)

**mutate**

> 在字段上执行突变


[logstash-filter-mutate](https://github.com/logstash-plugins/logstash-filter-mutate)

**metrics**

> 汇总指标


[logstash-filter-metrics](https://github.com/logstash-plugins/logstash-filter-metrics)

**multiline**

> 将多行合并成一个事件

[logstash-filter-multiline](https://github.com/logstash-plugins/logstash-filter-multiline)

**metaevent**

> 将任意字段添加到事件

[logstash-filter-metaevent](https://github.com/logstash-plugins/logstash-filter-metaevent)

**prune**

>将基于字段列表的事件数据修剪为黑名单或白名单

[logstash-filter-prune](https://github.com/logstash-plugins/logstash-filter-prune)

**punct**

> 从字段中删除所有非标点符号内容

[logstash-filter-punct](https://github.com/logstash-plugins/logstash-filter-punct)

**ruby**

> 执行任意Ruby代码

[logstash-filter-ruby](https://github.com/logstash-plugins/logstash-filter-ruby)

**range**

> 检查指定的字段是否保持在给定的大小或长度限制内

[logstash-filter-range](https://github.com/logstash-plugins/logstash-filter-range)

**syslog_pri**

> 解析系统日志消息的PRI（优先级）字段

[logstash-filter-syslog_pri](https://github.com/logstash-plugins/logstash-filter-syslog_pri)

**sleep**

>睡眠指定的时间跨度

[logstash-filter-sleep](https://github.com/logstash-plugins/logstash-filter-sleep)

**split**

> 将多行消息拆分为不同的事件

[logstash-filter-split](https://github.com/logstash-plugins/logstash-filter-split)

**throttle**

> 调节事件数

[logstash-filter-throttle](https://github.com/logstash-plugins/logstash-filter-throttle)

**translate**

> 基于散列或YAML文件替换字段内容

[logstash-filter-translate](https://github.com/logstash-plugins/logstash-filter-translate)

**uuid**

> 向事件添加UUID

[logstash-filter-uuid](https://github.com/logstash-plugins/logstash-filter-uuid)

**urldecode**

> 解码网址编码字段

[logstash-filter-urldecode](https://github.com/logstash-plugins/logstash-filter-urldecode)

**useragent**

> 将用户代理字符串解析为字段

[logstash-filter-useragent](https://github.com/logstash-plugins/logstash-filter-useragent)

**xml**

> 将XML解析成字段

[logstash-filter-xml](https://github.com/logstash-plugins/logstash-filter-xml)

**zeromq**

> 将事件发送到ZeroMQ

[logstash-filter-zeromq](https://github.com/logstash-plugins/logstash-filter-zeromq)


### csv
CSV过滤器接收包含CSV数据的事件字段，对其进行解析，并将其存储为单个字段（可以选择指定名称）。 此过滤器还可以使用任何分隔符解析数据，而不仅仅是逗号。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
csv {
}
```
可用配置选项：

|Setting	|Input type	|Required	|Default value
|--------|-----------|---------|-------------
|add_field|hash|No|{}
|add_tag|array|No|[]
|autogenerate_column_names|boolean|No|true
|columns|array|No|[]
|convert|hash|No|{}
|periodic_flush|boolean|No|false
|quote_char|string|No|"\""
|remove_field|array|No|[]
|remove_tag|array|No|[]
|separator|string|No|","
|skip_empty_columns|boolean|No|false
|source|string|No|"message"
|target|string|No|


#### 详情

**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用`％{field}`包括事件的部分。

例：
```
filter {
  csv {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  csv {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。

**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  csv {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  csv {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**autogenerate_column_names**
- 值类型是布尔值
- 默认值为true

定义列名称是否应自动生成。默认为true。如果设置为false，将不会解析不具有指定的头的列。

**columns**
- 值类型是数组
- 默认值为[]

定义列名称列表（按照它们在CSV中显示的顺序，就像它是标题行一样）。如果未配置列，或没有指定足够的列，则默认列名称为“column1”，“column2”等。如果数据中的列超过此列列表中指定的列数，自动编号：（例如，“user_defined_1”，“user_defined_2”，“column3”，“column4”等）

**convert**
- 值类型是哈希
- 默认值为{}

定义要应用于列的一组数据类型转换。可能的转换是整数，浮点，日期，date_time，布尔值

示例：
```
filter {
  csv {
    convert => { "column1" => "integer", "column2" => "boolean" }
  }
}
```

**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。

**quote_char**
- 值类型是字符串
- 默认值为“`\`”“

定义用于报告CSV字段的字符。如果未指定此属性，则默认值为双引号“。可选。

**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：

```
filter {
  csv {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  csv {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。

**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  csv {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  csv {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。

**separator**
- 值类型是字符串
- 默认值为“，”

定义列分隔符值。如果未指定此选项，则默认值为逗号，。可选的。

**skip_empty_columns**
- 值类型是布尔值
- 默认值为false

定义是否应跳过空列。默认为false。如果设置为true，将不会设置不包含值的列。


**source**
- 值类型是字符串
- 默认值为“message”

源字段值中的CSV数据将扩展为数据结构。

**target**
- 值类型是字符串
- 此设置没有默认值。

定义用于放置数据的目标字段。默认为写入事件的根。

### alter

> 这是一个社区维护的插件！ 它默认不随Logstash一起提供，但它很容易安装通过运行bin / logstash-plugin install logstash-filter-alter。

alter过滤器允许您对不包括在正常mutate过滤器中的字段进行常规更改。

> 注意: 此插件提供的功能可能会在未来版本中合并到mutate过滤器中。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
alter {
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
coalesce|array|No |
condrewrite|array|No |
condrewriteother|array|No|
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]


#### 详情


**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  alter {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  alter {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。

**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  alter {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  alter {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**coalesce**
- 值类型是数组
- 此设置没有默认值。

将field_name的值设置为其参数中的第一个非空表达式。

例：
```
filter {
  alter {
    coalesce => [
         "field_name", "value1", "value2", "value3", ...
    ]
  }
}
```

**condrewrite**
- 值类型是数组
- 此设置没有默认值。

如果实际内容等于预期值，请将字段的内容更改为指定值。

例：
```
filter {
  alter {
    condrewrite => [
         "field_name", "expected_value", "new_value",
         "field_name2", "expected_value2, "new_value2",
         ....
       ]
  }
}
```

**condrewriteother**
- 值类型是数组
- 此设置没有默认值。

如果另一个字段的内容等于预期值，请将字段的内容更改为指定的值。

例：

```
filter {
  alter {
    condrewriteother => [
         "field_name", "expected_value", "field_name_to_change", "value",
         "field_name2", "expected_value2, "field_name_to_change2", "value2",
         ....
    ]
  }
}
```

**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。



**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  alter {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  alter {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。


**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  alter {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  alter {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。

### date

日期过滤器用于解析字段中的日期，然后使用该日期或时间戳作为事件的logstash时间戳。

例如，syslog事件通常具有如下所示的时间戳：
```
“Apr 17 09:32:01”
```
您将使用日期格式MMM dd HH：mm：ss解析此。

日期过滤器对排序事件和回填旧数据尤为重要。 如果您在活动中没有得到正确的日期，那么稍后再搜索这些日期可能会出现乱序。

在没有此过滤器的情况下，如果时间戳尚未在事件中设置，则logstash将基于第一次看到事件（在输入时间）时选择时间戳。 例如，对于文件输入，时间戳设置为每次读取的时间。


#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
date {
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
locale|string|No|
match|array|No|[]
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]
tag_on_failure|array|No|`["_dateparsefailure"]`
target|string|No|"`@timestamp`"
timezone|string|No|

#### 详情


**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  date {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  date {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。

**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  date {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  date {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**locale**
- 值类型是字符串
- 此设置没有默认值。

使用IETF-BCP47或POSIX语言标记指定用于日期解析的区域设置。简单示例是en，en-US for BCP47或en_US for POSIX。

对于解析月份名称（使用MMM的模式）和工作日名称（使用EEE的模式），区域设置几乎是必需的。

如果未指定，则将使用平台默认值，但对于非英语平台默认值，英语解析器也将用作回退机制。


**match**
- 值类型是数组
- 默认值为[]

允许的日期格式是Joda-Time允许的任何日期格式（java时间库）。您可以在此处查看此格式的文档：
```
joda.time.format.DateTimeFormat
```

一个字段名称为first的数组，其后面的格式类型为[field，formats ...]

如果您的时间字段有多种可能的格式，您可以这样做：

```
match => [ "logdate", "MMM dd YYY HH:mm:ss",
          "MMM  d YYY HH:mm:ss", "ISO8601" ]
```
以上将匹配syslog（rfc3164）或iso8601时间戳。

有一些特殊的例外。存在以下格式字面值以帮助您节省时间并确保日期解析的正确性。

- ISO8601 - 应解析任何有效的ISO8601时间戳，例如2011-04-19T03：44：01.103Z
- UNIX - 将解析float或int值，表示自从时代以来的以秒为单位的unix时间，如1326149001.132以及1326149001
- UNIX_MS - 将解析int值表示自从纪元以来的毫秒数的unix时间，如1366125117000
- TAI64N - 将解析tai64n时间值

例如，如果您有一个字段logdate，其值类似于Aug 13 2010 00:03:44，您将使用此配置：
```
filter {
  date {
    match => [ "logdate", "MMM dd YYYY HH:mm:ss" ]
  }
}
```
如果您的字段嵌套在您的结构中，则可以使用嵌套语法[foo] [bar]来匹配其值。有关详细信息，请参阅“字段引用”一节，

有关语法的更多详细信息

用于解析日期和时间文本的语法使用字母表示时间值（月，分钟等）的类型，以及重复的字母以指示该值的形式（2位数月份，完整月份名称等） 。

以下是您可以用来解析日期和时间：

- y,year
  - yyyy,full year number. Example: 2015.
  - yy,two-digit year. Example: 15 for the year 2015.

- M,month of the year
  - M,minimal-digit month. Example: 1 for January and 12 for December.
  - MM,two-digit month. zero-padded if needed. Example: 01 for January and 12 for December
  - MMM,abbreviated month text. Example: Jan for January. Note: The language used depends on your locale. See the locale setting for how to change the language.
  - MMMM,full month text, Example: January. Note: The language used depends on your locale.

- d,day of the month
  - d,minimal-digit day. Example: 1 for the 1st of the month.
  - dd,two-digit day, zero-padded if needed. Example: 01 for the 1st of the month.

- H,hour of the day (24-hour clock)
  - H,minimal-digit hour. Example: 0 for midnight.
  - HH,two-digit hour, zero-padded if needed. Example: 00 for midnight.

- m,minutes of the hour (60 minutes per hour)
  - m,minimal-digit minutes. Example: 0.
  - mm,two-digit minutes, zero-padded if needed. Example: 00.

- s,seconds of the minute (60 seconds per minute)
  - s,minimal-digit seconds. Example: 0.
  - ss,two-digit seconds, zero-padded if needed. Example: 00.

- S,fraction of a second Maximum precision is milliseconds (SSS). Beyond that, zeroes are appended.
  - S,tenths of a second. Example: 0 for a subsecond value 012
  - SS,hundredths of a second. Example: 01 for a subsecond value 01
  - SSS,thousandths of a second. Example: 012 for a subsecond value 012

- Z,time zone offset or identity
  - Z,Timezone offset structured as HHmm (hour and minutes offset from Zulu/UTC). Example: -0700.
  - ZZ,Timezone offset structured as HH:mm (colon in between hour and minute offsets). Example: -07:00.
  - ZZZ,Timezone identity. Example: America/Los_Angeles. Note: Valid IDs are listed on the Joda.org available time zones page.

- z,time zone names. Time zone names (z) cannot be parsed.

- w,week of the year
  - w,minimal-digit week. Example: 1.
  - ww,two-digit week, zero-padded if needed. Example: 01.

- D,day of the year

- e,day of the week (number)

- E,day of the week (text)
  - E, EE, EEE,    Abbreviated day of the week. Example: Mon, Tue, Wed, Thu, Fri, Sat, Sun. Note: The actual language of this will depend on your locale.
  - EEEE, The full text day of the week. Example: Monday, Tuesday, … Note: The actual language of this will depend on your locale.


对于非格式化语法，您需要在值周围加上单引号字符。 例如，如果您正在解析ISO8601时间，“2015-01-01T01：12：23”，小的“T”不是有效的时间格式，并且您想说“字面上，一个T”，您的格式将是 这个：“yyyy-MM-dd'T'HH：mm：ss”

其他不太常见的日期单位，如时代（G），世纪（C），上午/下午（a）和＃更多，可以了解关于[joda时间文档](http://www.joda.org/joda-time/key_format.html)。




**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。


**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  date {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  date {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。


**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  date {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  date {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。



**tag_on_failure**
- 值类型是数组
- 默认值为[“`_dateparsefailure`”]

当没有成功匹配时，将值附加到标记字段


**target**
- 值类型是字符串
- 默认值为“@timestamp”

将匹配的时间戳存储到给定的目标字段中。如果未提供，则默认更新事件的@timestamp字段。


**timezone**
- 值类型是字符串
- 此设置没有默认值。

指定要用于日期解析的时区标准ID。有效ID列在Joda.org可用时区页上。这在时区无法从值中提取，而不是平台默认值的情况下非常有用。如果未指定，将使用平台默认值。规范ID是好的，因为它照顾夏令时您例如，美洲/ Los_Angeles或欧洲/巴黎是有效的ID。此字段可以是动态的，并使用％{字段}语法包括事件的部分


### drop

丢弃过滤器。

丢弃所有到这个过滤器的东西。

这最好与条件组合使用，例如：
```
filter {
  if [loglevel] == "debug" {
    drop { }
  }
}
```
如果loglevel字段是debug，上述操作只会将事件传递给drop过滤器。 这将导致所有匹配的事件被删除。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
drop {
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
percentage|number|No|100
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]

#### 详情


**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  drop {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  drop {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。


**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  drop {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  drop {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**percentage**
- 值类型是数字
- 默认值为100

删除预配置百分比内的所有事件。

这是有用的，如果你只需要一个百分比，但不是整体。

例如，只有大约40％的具有字段loglevel值为“debug”的事件。
```
filter {
  if [loglevel] == "debug" {
    drop {
      percentage => 40
    }
  }
}
```

**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。


**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  drop {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  drop {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。


**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  drop {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  drop {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。


### geoip

GeoIP过滤器根据Maxmind数据库中的数据添加有关IP地址的地理位置的信息。

从Logstash的1.3.0版本开始，如果GeoIP查询返回纬度和经度，则会创建一个[geoip] [location]字段。 该字段存储为GeoJSON格式。 此外，弹性搜索输出提供的默认Elasticsearch模板将[geoip] [location]字段映射到Elasticsearch geo_point。

由于此字段是geo_point，它仍然有效GeoJSON，您将获得Elasticsearch的地理空间查询，构面和过滤器功能的强大功能，以及为所有其他应用程序（如Kibana的地图可视化）使用GeoJSON的灵活性。

Logstash发行版随附带有CCA-ShareAlike 3.0许可证的Maxmind提供的GeoLiteCity数据库。 有关GeoLite的更多详细信息，请参见http://www.maxmind.com/en/geolite。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
geoip {
    source => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
database|a valid filesystem path|No|
fields|array|No|
lru_cache_size|number|No|1000
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]
source|string|Yes|
target|string|No|"geoip"

#### 详情


**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  geoip {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  geoip {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。


**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  geoip {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  geoip {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**database**
- 值类型为路径
- 此设置没有默认值。

查找缓存的地图，由geoip_type锁定LogStash应使用的GeoIP数据库文件的路径。支持国家，城市，ASN，ISP和组织数据库。

如果未指定，这将默认为LogStash附带的GeoLiteCity数据库。可以从这里下载最新的数据库：https://dev.maxmind.com/geoip/legacy/geolite/请务必下载旧版格式数据库。


**fields**
- 值类型是数组
- 此设置没有默认值。

要包含在事件中的geoip字段数组。

可能的字段取决于数据库类型。默认情况下，所有地理位置字段都包含在事件中。

对于内置的GeoLiteCity数据库，以下是可用的： city_name, continent_code, country_code2, country_code3, country_name, dma_code, ip, latitude, longitude, postal_code, region_name and timezone.


**lru_cache_size**
- 值类型是数字
- 默认值为1000

GeoIP查找令人惊讶的昂贵。此过滤器使用LRU缓存来利用IP代理经常在日志文件中彼此相邻并且很少具有随机分布的事实。设置的越高，项目在缓存中的可能性越大，并且此过滤器运行的速度越快。但是，如果您设置太高，您可以使用比所需的更多的内存。

为此选项尝试不同的值，以便为数据集找到最佳性能。

这必须设置为值> 0。真的没有理由不想要这种行为，开销是最小的，速度增益很大。

请注意，此配置值对geoip_type是全局的。也就是说，同一geoip_type的geoip过滤器的所有实例共享相同的缓存。最后声明的缓存大小将赢。这样做的原因是，对于在流水线中的不同点处的不同实例具有多个高速缓存将没有益处，这只会增加高速缓存未命中和浪费存储器的数量。


**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。


**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：

```
filter {
  geoip {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  geoip {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。


**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  geoip {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  geoip {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。


**source**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

包含要通过geoip映射的IP地址或主机名的字段。如果此字段是数组，则仅使用第一个值。

**target**
值类型是字符串
默认值为“geoip”
指定Logstash应存储geoip数据的字段。这可能很有用，例如，如果您有`src\_ip`和`dst\_ip`字段，并且想要两个IP的GeoIP信息。

如果将数据保存到除geoip以外的目标字段，并且希望使用Elasticsearch中的`geo\_point`相关函数，则需要更改Elasticsearch输出提供的模板，并将输出配置为使用新模板。

即使您不使用`geo\_point`映射，[target] [location]字段仍然有效GeoJSON。


### grok
解析任意文本和结构。

Grok是目前在logstash中将糟糕的非结构化日志数据解析为结构化和可查询的最佳方式。

这个工具是完美的syslog日志，apache和其他webserver日志，mysql日志，一般，任何日志格式，一般为人而不是计算机消费。

默认情况下，Logstash附带约120个模式。 你可以在这里找到他们：https：//github.com/logst-plugins/logstash-patterns-core/tree/master/patterns。 你可以添加自己的trivially。 （请参阅patterns_dir设置）

如果您需要帮助构建模式以匹配您的日志，您会发现http://grokdebug.herokuapp.com和http://grokconstructor.appspot.com/应用程序非常有用！

#### Grok基础
Grok通过将文本模式组合成与您的日志匹配的东西。

grok模式的语法为％{SYNTAX：SEMANTIC}

SYNTAX是将匹配您的文本的模式的名称。 例如，3.44将匹配NUMBER模式，55.3.244.1将匹配IP模式。 语法是如何匹配。

SEMANTIC是您给匹配的文本片段的标识符。 例如，3.44可以是事件的持续时间，因此您可以将其称为持续时间。 此外，字符串55.3.244.1可以标识发出请求的客户端。

对于上面的例子，你的grok过滤器看起来像这样：
```
%{NUMBER:duration} %{IP:client}
```
或者，您可以向grok模式添加数据类型转换。 默认情况下，所有语义都保存为字符串。 如果希望转换语义的数据类型，例如将字符串更改为整数，然后使用目标数据类型进行后缀。 例如％{NUMBER：num：int}，它将num语义从字符串转换为整数。 目前唯一支持的转换是int和float。

示例：有了语法和语义的想法，我们可以从示例日志中提取有用的字段，就像这个虚构的http请求日志：
```
55.3.244.1 GET /index.html 15824 0.043
```

这种模式可以是：
```
%{IP:client} %{WORD:method} %{URIPATHPARAM:request} %{NUMBER:bytes} %{NUMBER:duration}
```
一个更现实的例子，让我们从文件中读取这些日志：
```
input {
  file {
    path => "/var/log/http.log"
  }
}
filter {
  grok {
    match => { "message" => "%{IP:client} %{WORD:method} %{URIPATHPARAM:request} %{NUMBER:bytes} %{NUMBER:duration}" }
  }
}
```
在grok过滤器之后，事件将有一些额外的字段：

- client: 55.3.244.1
- method: GET
- request: /index.html
- bytes: 15824
- duration: 0.043

#### 正则表达式
Grok位于正则表达式的顶部，因此任何正则表达式在grok中都有效。 正则表达式库是Oniguruma，您可以在Oniguruma站点上看到完整支持的regexp语法。

自定义Patternsedit
有时logstash没有你需要的模式。 为此，您有几个选项。

首先，您可以使用Oniguruma语法进行命名捕获，它将让您匹配一段文本并将其保存为字段：
```
(?<field_name>the pattern here)
```
例如，后缀日志具有为10或11个字符的十六进制值的队列ID。 我可以很容易地捕捉到这样：
```
(?<queue_id>[0-9A-F]{10,11})
```
或者，您可以创建自定义模式文件。

创建一个名为patterns的模式，其中包含一个名为extra的文件（文件名不重要，但为自己命名）
在该文件中，写所需的模式作为模式名称，一个空格，然后是该模式的正则表达式。
例如，执行postfix队列id示例如上：
```
# contents of ./patterns/postfix:
POSTFIX_QUEUEID [0-9A-F]{10,11}
```
然后使用这个插件中的patterns_dir设置告诉logstash您的自定义模式目录在哪里。 这里有一个示例日志的完整示例：
```
Jan  1 06:25:43 mailserver14 postfix/cleanup[21403]: BEF25A72965: message-id=<20130101142543.5828399CCAF@mailserver14.example.com>
filter {
  grok {
    patterns_dir => ["./patterns"]
    match => { "message" => "%{SYSLOGBASE} %{POSTFIX_QUEUEID:queue_id}: %{GREEDYDATA:syslog_message}" }
  }
}
```
以上将匹配并导致以下字段：

- timestamp: Jan 1 06:25:43
- logsource: mailserver14
- program: postfix/cleanup
- pid: 21403
- queue_id: BEF25A72965
- syslog_message: message-id=<20130101142543.5828399CCAF@mailserver14.example.com>

The timestamp, logsource, program, and pid 字段来自SYSLOGBASE模式，该模式本身由其他模式定义。


#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
grok {
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
break_on_match|boolean|No|true
keep_empty_captures|boolean|No|false
match|hash|No|{}
named_captures_only|boolean|No|true
overwrite|array|No|[]
patterns_dir|array|No|[]
patterns_files_glob|string|No|"`*`"
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]
tag_on_failure|array|No|["`_grokparsefailure`"]

#### 详情


**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  grok {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  grok {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。


**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  grok {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  grok {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。




**break_on_match**
- 值类型是布尔值
- 默认值为true

打破第一场比赛。 grok的第一次成功匹配将导致过滤器完成。如果你想让grok尝试所有的模式（也许你正在解析不同的东西），然后设置为false。


**keep_empty_captures**
- 值类型是布尔值
- 默认值为false

如果为true，请将空捕获保留为事件字段。



**match**
- 值类型是哈希
- 默认值为{}

field ⇒ value 的匹配散列

例如：
```
filter {
  grok { match => { "message" => "Duration: %{NUMBER:duration}" } }
}
```
如果您需要针对单个字段匹配多个模式，则该值可以是模式数组
```
filter {
  grok { match => { "message" => [ "Duration: %{NUMBER:duration}", "Speed: %{NUMBER:speed}" ] } }
}
```

**named_captures_only**
- 值类型是布尔值
- 默认值为true

如果为true，则只存储从grok命名的捕获。


**overwrite**
值类型是数组
默认值为[]
要覆盖的字段。

这允许您覆盖已存在的字段中的值。

例如，如果消息字段中有syslog行，则可以使用部分匹配覆盖消息字段，如下所示：

```
filter {
  grok {
    match => { "message" => "%{SYSLOGBASE} %{DATA:message}" }
    overwrite => [ "message" ]
  }
}
```
在这种情况下，一行像May 29 16:37:11悲伤日志：hello world将被解析，hello world将覆盖原始消息。

**pattern (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是数组
- 此设置没有默认值。

指定要解析的模式。这将匹配消息字段。

如果要匹配消息之外的其他字段，请使用匹配设置。多种模式是好的。


**patterns_dir**
值类型是数组
默认值为[]
Logstash默认带有一堆模式，所以你不一定需要自己定义，除非你添加额外的模式。您可以使用此设置指向多个模式目录请注意，Grok将读取与patterns_files_glob匹配的目录中的所有文件，并假定其模式文件（包括任何波形字符备份文件）
```
patterns_dir => ["/opt/logstash/patterns", "/opt/logstash/extra_patterns"]
```
模式文件是带有格式的纯文本：
```
NAME PATTERN
```
示例
```
NUMBER \d+
```

**patterns_files_glob**
- 值类型是字符串
- 默认值为“`*`”

Glob模式，用于选择patterns_dir指定的目录中的模式文件


**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。


**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  grok {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  grok {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。


**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  grok {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  grok {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。


**singles (DEPRECATED)**
- DEPRECATED WARNING：此配置项目已弃用，并且可能在将来的版本中不可用。
- 值类型是布尔值
- 默认值为true

如果为true，则将单值字段设置为该值，而不是包含该值的数组。

**tag_on_failure**
- 值类型是数组
- 默认值为[“`_grokparsefailure`”]

当没有成功匹配时，将值附加到标记字段

### json

这是一个JSON解析过滤器。 它需要一个包含JSON的现有字段，并在Logstash事件中将其扩展为实际的数据结构。

默认情况下，它会将解析的JSON放在Logstash事件的根（顶级）中，但是可以配置此过滤器以使用目标配置将JSON放入任意事件字段。


#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
json {
    source => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]
source|string|Yes|
target|string|No|

#### 详情


**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  json {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  json {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。


**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  json {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  json {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。


**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  json {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  json {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。


**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  json {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  json {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。


**source**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

JSON过滤器的配置：

```
source => source_field
```
例如，如果您在消息字段中有JSON数据：
```
filter {
  json {
    source => "message"
  }
}
```
上面将解析从消息字段的json


**target**
- 值类型是字符串
- 此设置没有默认值。

定义放置解析数据的目标字段。如果省略此设置，JSON数据将存储在事件的根（顶级）。

例如，如果您想将数据放在doc字段中：
```
filter {
  json {
    target => "doc"
  }
}
```
在源字段的值中的JSON将在目标字段中展开为数据结构。

> 注意: 如果目标字段已经存在，它将被覆盖！

### json_encode

这是一个社区维护的插件！ 它默认不随Logstash一起提供，但它很容易安装通过运行bin / logstash-plugin install logstash-filter-json_encode。

JSON编码过滤器。 获取字段并将其序列化为JSON

如果未指定目标，源字段将被JSON文本覆盖。

例如，如果您有一个名为foo的字段，并且您想要在bar中存储JSON编码的字符串，请执行以下操作：
```
filter {
  json_encode {
    source => "foo"
    target => "bar"
  }
}
```

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
json_encode {
    source => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]
source|string|Yes|
target|string|No|

#### 详情


**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  json_encode {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  json_encode {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。

**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  json_encode {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  json_encode {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。


**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  json_encode {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  json_encode {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。

**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  json_encode {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  json_encode {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。

**source**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

要转换为JSON的字段。


**target**
- 值类型是字符串
- 此设置没有默认值。

将JSON写入的字段。如果未指定，源字段将被覆盖。

### ruby

执行ruby代码。

例如，要取消90％的事件，您可以执行以下操作：
```
filter {
  ruby {
    # Cancel 90% of events
    code => "event.cancel if rand <= 0.90"
  }
}
```

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
ruby {
    code => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
code|string|Yes|
init|string|No|
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]

#### 详情



**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  ruby {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  ruby {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。

**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  ruby {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  ruby {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**code**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

为每个事件执行的代码。您将有一个事件变量可用，它是事件本身。

**init**
- 值类型是字符串
- 此设置没有默认值。

在logstash启动时执行的任何代码


**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。

**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  ruby {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  ruby {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。

**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  ruby {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  ruby {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。


### split

分割过滤器通过拆分其中一个字段并将分割后的每个值放入原始事件的克隆中来克隆事件。 要分割的字段可以是字符串或数组。

此过滤器的一个示例用例是从exec输入插件获取输出，该输出为命令的整个输出发出一个事件，并通过换行分割该输出 - 使每行成为事件。

每个拆分的最终结果是事件的完整副本，只有给定字段的当前拆分部分已更改。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
split {
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
field|string|No|"message"
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]
target|string|No|
terminator|string|No|"\\n"

#### 详情



**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  split {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  split {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。


**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  split {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  split {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**field**
- 值类型是字符串
- 默认值为“message”

其值由终止符拆分的字段。

**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。

**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  split {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  split {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。

**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  split {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  split {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。

**target**
- 值类型是字符串
- 此设置没有默认值。

新事件中的值将被分割为的字段。如果未设置，目标字段默认为拆分字段名称。

**terminator**
- 值类型是字符串
- 默认值为“`\n`”

要拆分的字符串。这通常是行终止符，但可以是任何字符串。


### uuid
uuid过滤器允许您生成UUID，并将其作为字段添加到每个已处理的事件。

如果您需要生成每个事件唯一的字符串，即使同一个输入被处理多次，这也很有用。 如果要生成每次处理具有给定内容的事件（即哈希）时相同的字符串，则应使用指纹过滤器。

生成的UUID遵循RFC 4122中的版本4定义），并且将被表示为标准十六进制字符串格式，例如。 “e08806fe-02af-406c-bbde-8a5ae4475e57”。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
uuid {
    target => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
overwrite|boolean|No|false
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]
target|string|Yes|

#### 详情


**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  uuid {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
您也可以一次添加多个字段：
```
filter {
  uuid {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。


**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  uuid {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
您也可以一次添加多个代码：
```
filter {
  uuid {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**overwrite**
- 值类型是布尔值
- 默认值为false

如果当前字段中的值（如果有）应该被生成的UUID覆盖。默认为false（即，如果字段存在，具有ANY值，则不会被覆盖）

例：
```
filter {
   uuid {
     target    => "@uuid"
     overwrite => true
   }
}
```

**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。


**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  uuid {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
您也可以一次删除多个字段：
```
filter {
  uuid {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。


**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  uuid {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
您也可以一次移除多个标记：
```
filter {
  uuid {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。


**target**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

向字段添加UUID。

例：
```
filter {
  uuid {
    target => "@uuid"
  }
}
```


### urldecode

urldecode过滤器用于解码被urlencoded的字段。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
urldecode {
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
all_fields|boolean|No|false
charset|string, one of ["ASCII-8BIT", "Big5", "Big5-HKSCS", "Big5-UAO", "CP949", "Emacs-Mule", "EUC-JP", "EUC-KR", "EUC-TW", "GB18030", "GBK", "ISO-8859-1", "ISO-8859-2", "ISO-8859-3", "ISO-8859-4", "ISO-8859-5", "ISO-8859-6", "ISO-8859-7", "ISO-8859-8", "ISO-8859-9", "ISO-8859-10", "ISO-8859-11", "ISO-8859-13", "ISO-8859-14", "ISO-8859-15", "ISO-8859-16", "KOI8-R", "KOI8-U", "Shift_JIS", "US-ASCII", "UTF-8", "UTF-16BE", "UTF-16LE", "UTF-32BE", "UTF-32LE", "Windows-1251", "GB2312", "Windows-31J", "IBM437", "IBM737", "IBM775", "CP850", "IBM852", "CP852", "IBM855", "CP855", "IBM857", "IBM860", "IBM861", "IBM862", "IBM863", "IBM864", "IBM865", "IBM866", "IBM869", "Windows-1258", "GB1988", "macCentEuro", "macCroatian", "macCyrillic", "macGreek", "macIceland", "macRoman", "macRomania", "macThai", "macTurkish", "macUkraine", "CP950", "CP951", "stateless-ISO-2022-JP", "eucJP-ms", "CP51932", "EUC-JIS-2004", "GB12345", "ISO-2022-JP", "ISO-2022-JP-2", "CP50220", "CP50221", "Windows-1252", "Windows-1250", "Windows-1256", "Windows-1253", "Windows-1255", "Windows-1254", "TIS-620", "Windows-874", "Windows-1257", "MacJapanese", "UTF-7", "UTF8-MAC", "UTF-16", "UTF-32", "UTF8-DoCoMo", "SJIS-DoCoMo", "UTF8-KDDI", "SJIS-KDDI", "ISO-2022-JP-KDDI", "stateless-ISO-2022-JP-KDDI", "UTF8-SoftBank", "SJIS-SoftBank", "BINARY", "CP437", "CP737", "CP775", "IBM850", "CP857", "CP860", "CP861", "CP862", "CP863", "CP864", "CP865", "CP866", "CP869", "CP1258", "Big5-HKSCS:2008", "eucJP", "euc-jp-ms", "EUC-JISX0213", "eucKR", "eucTW", "EUC-CN", "eucCN", "CP936", "ISO2022-JP", "ISO2022-JP2", "ISO8859-1", "CP1252", "ISO8859-2", "CP1250", "ISO8859-3", "ISO8859-4", "ISO8859-5", "ISO8859-6", "CP1256", "ISO8859-7", "CP1253", "ISO8859-8", "CP1255", "ISO8859-9", "CP1254", "ISO8859-10", "ISO8859-11", "CP874", "ISO8859-13", "CP1257", "ISO8859-14", "ISO8859-15", "ISO8859-16", "CP878", "MacJapan", "ASCII", "ANSI_X3.4-1968", "646", "CP65000", "CP65001", "UTF-8-MAC", "UTF-8-HFS", "UCS-2BE", "UCS-4BE", "UCS-4LE", "CP932", "csWindows31J", "SJIS", "PCK", "CP1251", "external", "locale"]|No|"UTF-8"
field|string|No|"message"
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_tag|array|No|[]


#### 详情


**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  urldecode {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# 您也可以一次添加多个字段
filter {
  urldecode {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。


**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  urldecode {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  urldecode {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**all_fields**
- 值类型是布尔值
- 默认值为false

Urldecode所有字段


**charset**
- 值可以是以下任何一个：ASCII-8BIT，Big5，Big5-HKSCS，Big5-UAO，CP949，Emacs-Mule，EUC-JP，EUC-KR，EUC-TW，GB18030，GBK，ISO-8859-1，ISO- ISO-8859-3，ISO-8859-4，ISO-8859-5，ISO-8859-6，ISO-8859-7，ISO-8859-8，ISO-8859-9，ISO- 10，ISO-8859-11，ISO-8859-13，ISO-8859-14，ISO-8859-15，ISO-8859-16，KOI8-R，KOI8-U，Shift_JIS，US-ASCII，UTF- UT85，IBM855，IBM855，IBM857，IBM860，IBM861，IBM862，IBM853，UT86，UTF-16BE，UTF-16LE，UTF-32BE，UTF-32LE，Windows-1251，GB2312，Windows-31J，IBM437，IBM737，IBM775， IBM863，IBM864，IBM865，IBM866，IBM869，Windows-1258，GB1988，macCentEuro，macCroatian，macCyrillic，macGreek，macIlandland，macRoman，macRomania，macThai，macTurkish，macUkraine，CP950，CP951，stateless-ISO-2022-JP，eucJP- ms，CP51932，EUC-JIS-2004，GB12345，ISO-2022-JP，ISO-2022-JP-2，CP50220，CP50221，Windows-1252，Windows-1250，Windows-1256，Windows-1253， Windows-1254，TIS-620，Windows-874，Windows-1257，MacJapanese，UTF-7，UTF8-MAC，UTF-16，UTF-32，UTF8-DoCoMo，SJIS-DoCoMo，UTF8-KDDI，SJIS- ISO-2022-JP-KDDI，无状态ISO-2022-JP-KDDI，UTF8-软银行，SJIS-软银行，BINARY，CP437，CP737，CP775，IBM850，CP857，CP860，CP861，CP862，CP863，CP864，CP865， CP866，CP869，CP1258，Big5-HKSCS：2008，eucJP，euc-jp-ms，EUC-JISX0213，eucKR，eucTW，EUC-CN，eucCN，CP936，ISO2022-JP，ISO2022-JP2，ISO8859-1， ISO8859-3，ISO8859-4，ISO8859-5，ISO8859-6，CP1256，ISO8859-7，CP1253，ISO8859-8，CP1255，ISO8859-9，CP1254，ISO8859-10，ISO8859-11， CP874，ISO8859-13，CP1257，ISO8859-14，ISO8859-15，ISO8859-16，CP878，MacJapan，ASCII，ANSI_X3.4-1968,646，CP65000，CP65001，UTF-8-MAC，UTF-8-HFS， UCS-2BE，UCS-4BE，UCS-4LE，CP932，csWindows31J，SJIS，PCK，CP1251，external，locale
- 默认值为“UTF-8”

此过滤器中使用的字符编码。例子包括UTF-8和cp1252

如果您的url已解码的字符串是Latin-1（又名cp1252）或除UTF-8之外的其他字符集，此设置很有用。


**field**
- 值类型是字符串
- 默认值为“message”

值被urldecoded的字段


**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。

**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：

```
filter {
  urldecode {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  urldecode {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。

**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  urldecode {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  urldecode {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。


### useragent

基于BrowserScope数据将用户代理字符串解析为结构化数据

UserAgent过滤器，添加有关用户代理的信息，如系列，操作系统，版本和设备

Logstash发行版随附了使用Apache 2.0许可证从ua-parser提供的regexes.yaml数据库。 有关ua-parser的更多详细信息，请参见https://github.com/tobie/ua-parser/。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
useragent {
    source => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
lru_cache_size|number|No|1000
periodic_flush|boolean|No|false
prefix|string|No|""
regexes|string|No|
remove_field|array|No|[]
remove_tag|array|No|[]
source|string|Yes|
target|string|No|

#### 详情


**add_field**
- 值类型是哈希
- 默认值为{}

如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  useragent {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# 您也可以一次添加多个字段：
filter {
  useragent {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。


**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  useragent {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  useragent {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**lru_cache_size**
- 值类型是数字
- 默认值为1000

UA解析是惊人的昂贵。此过滤器使用LRU缓存来利用这样的事实：用户代理经常在日志文件中彼此相邻，并且很少具有随机分布。设置的越高，项目在缓存中的可能性越大，并且此过滤器运行的速度越快。但是，如果您设置太高，您可以使用比所需的更多的内存。

为此选项尝试不同的值，以便为数据集找到最佳性能。

这必须设置为值> 0。真的没有理由不想要这种行为，开销是最小的，速度增益很大。

重要的是注意这个配置值是全局的。也就是说，用户代理过滤器的所有实例共享同一缓存。最后声明的缓存大小将赢。这样做的原因是，对于在流水线中的不同点处的不同实例具有多个高速缓存将没有益处，这只会增加高速缓存未命中和浪费存储器的数量。


**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。


**prefix**
- 值类型是字符串
- 默认值为“”

预先附加到所有提取的键的字符串


**regexes**
- 值类型是字符串
- 此设置没有默认值。

regexes.yaml文件使用

如果不指定，这将默认为与logstash一起提供的regexes.yaml。

您可以在这里找到最新版本：https：//github.com/tobie/ua-parser/blob/master/regexes.yaml


**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  useragent {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  useragent {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。


**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  useragent {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  useragent {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。


**source**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

包含用户代理字符串的字段。如果此字段是数组，则仅使用第一个值。

**target**
- 值类型是字符串
- 此设置没有默认值。

要将用户代理数据分配到的字段的名称。

如果没有指定，用户代理数据将存储在事件的根中。


### xml

XML过滤器。 获取包含XML的字段，并将其扩展为实际的数据结构。

#### 概述
此插件支持以下配置选项：

所需的配置选项：
```
xml {
    source => ...
}
```
可用配置选项：

Setting	|Input type	|Required	|Default value
--------|-----------|---------|-------------
add_field|hash|No|{}
add_tag|array|No|[]
force_array|boolean|No|true
namespaces|hash|No|{}
periodic_flush|boolean|No|false
remove_field|array|No|[]
remove_namespaces|boolean|No|false
remove_tag|array|No|[]
source|string|Yes|
store_xml|boolean|No|true
target|string|No|
xpath|hash|No|{}


#### 详情


**add_field**
值类型是哈希
默认值为{}
如果此过滤器成功，请将任意字段添加到此事件。字段名称可以是动态的，并使用％{field}包括事件的部分。

例：
```
filter {
  xml {
    add_field => { "foo_%{somefield}" => "Hello world, from %{host}" }
  }
}
```
```
# You can also add multiple fields at once:
filter {
  xml {
    add_field => {
      "foo_%{somefield}" => "Hello world, from %{host}"
      "new_field" => "new_static_value"
    }
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将添加字段foo_hello，如果它存在，与上面的值和％{host}块替换的事件中的值。第二个例子也将添加一个硬编码字段。

**add_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请向事件中添加任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  xml {
    add_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also add multiple tags at once:
filter {
  xml {
    add_tag => [ "foo_%{somefield}", "taggedy_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”这个过滤器，在成功时，将添加一个标签foo_hello（第二个例子当然会添加一个taggedy_tag标签）。


**force_array**
- 值类型是布尔值
- 默认值为true

默认情况下，过滤器会强制单个元素为数组。将此设置为false将阻止在数组中存储单个元素。

**namespaces**
- 值类型是哈希
- 默认值为{}

默认情况下，只考虑根元素上的命名空间声明。这允许配置所有命名空间声明来解析XML文档。

例：
```
filter {
  xml {
    namespaces => {
      "xsl" => "http://www.w3.org/1999/XSL/Transform"
      "xhtml" => http://www.w3.org/1999/xhtml"
    }
  }
}
```

**periodic_flush**
- 值类型是布尔值
- 默认值为false

定期调用过滤器flush方法。可选的。

**remove_field**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从此事件中删除任意字段。例：
```
filter {
  xml {
    remove_field => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple fields at once:
filter {
  xml {
    remove_field => [ "foo_%{somefield}", "my_extraneous_field" ]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除名为foo_hello的字段（如果存在）。第二个示例将删除一个附加的非动态字段。


**remove_namespaces**
- 值类型是布尔值
- 默认值为false

从文档中的所有节点中删除所有命名空间。当然，如果文档具有相同名称但不同命名空间的节点，它们现在将是不明确的。


**remove_tag**
- 值类型是数组
- 默认值为[]

如果此过滤器成功，请从事件中删除任意标记。标签可以是动态的，并使用％{字段}语法包括事件的部分。

例：
```
filter {
  xml {
    remove_tag => [ "foo_%{somefield}" ]
  }
}
```
```
# You can also remove multiple tags at once:
filter {
  xml {
    remove_tag => [ "foo_%{somefield}", "sad_unwanted_tag"]
  }
}
```
如果事件有字段“somefield”==“hello”此过滤器，如果成功，将删除标签foo_hello如果它存在。第二个例子也会删除一个悲伤的，不需要的标签。


**source**
- 这是必需的设置。
- 值类型是字符串
- 此设置没有默认值。

配置xml到哈希是：

```
source => source_field
```
例如，如果您在消息字段中具有整个XML文档
```
filter {
  xml {
    source => "message"
  }
}
```
上面将解析消息字段中的XML。


**store_xml**
- 值类型是布尔值
- 默认值为true

默认情况下，过滤器会将整个解析的XML存储在目标字段中，如上所述。设置为false将阻止。

**target**
- 值类型是字符串
- 此设置没有默认值。

定义放置数据的目标

例如，如果您希望将数据放在doc字段中：
```
filter {
  xml {
    target => "doc"
  }
}
```
源字段值中的XML将扩展为目标字段中的数据结构。注意：如果目标字段已存在，它将被覆盖。如果store_xml为true（这是缺省值），那么是必需的。


**xpath**
- 值类型是哈希
- 默认值为{}

xpath将使用解析的XML（使用上述方法定义的每个源字段）另外选择字符串值（非字符串将使用Ruby的to_s函数转换为字符串），并将这些值放在目标字段中。组态：Configuration:
```
xpath => [ "xpath-syntax", "destination-field" ]
```
XPath从xpath语法解析返回的值将放在目标字段中。返回的多个值将作为数组推送到目标字段。因此，跨多个源字段的多个匹配将在字段中产生重复条目。

更多关于XPath：http：//www.w3schools.com/xml/xml_xpath.asp

XPath函数特别强大：http://www.w3schools.com/xsl/xsl_functions.asp
