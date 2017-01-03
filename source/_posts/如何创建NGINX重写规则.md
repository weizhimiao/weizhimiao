---
title: 如何创建NGINX重写规则
date: 2017-01-03 22:30:00
tags:
- rewrite
categories:
- Nginx
---

在这篇博文中，我们讨论如何创建NGINX重写规则（同样的方法适用于NGINX Plus和开源NGINX软件）。重写规则会更改客户请求中的部分或全部网址，通常用于以下两个目的之一：

- 通知客户端他们请求的资源现在位于不同的位置。示例用例是我们的网站的域名发生更改时，我们希望客户端使用规范网址格式（带或不带www前缀），以及当我们想要捕获和更正我们的域名的常见拼写错误时。返回和重写指令适合于这些目的。

- 控制NGINX和NGINX Plus中的处理流程，例如，在需要动态生成内容时，将请求转发到应用程序服务器。 try_files指令通常用于此目的。

**注意：** 要了解如何将Apache HTTP服务器重写规则转换为NGINX重写规则，请参阅我们的随附博客文章“[将Apache重写规则转换为NGINX重写规则](https://www.nginx.com/blog/converting-apache-to-nginx-rewrite-rules/?utm_source=creating-nginx-rewrite-rules&utm_medium=blog&utm_campaign=Core+Product)”。

我们假设你熟悉[HTTP响应代码](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)和正则表达式（NGINX和NGINX Plus使用Perl语法）。

<!-- more -->

## 比较return，rewrite 和try_files指令

通用NGINX重写的两个指令是返回和重写，而try_files指令是将请求定向到应用程序服务器的一种方便的方法。 让我们回顾一下指令的作用以及它们之间的区别。

### return 指令
返回指令是两个通用指令中的最简单的，因此我们建议在可能的情况下使用它而不是重写（更多的是为什么和什么时候）。 将返回值放在指定要重写的URL的服务器或位置上下文中，并定义客户端在将来对资源的请求中使用的已更正（重写）的URL。

这里有一个非常简单的例子，将客户端重定向到一个新的域名：

```
server {
    listen 80;
    listen 443 ssl;
    server_name www.old-name.com;
    return 301 $scheme://www.new-name.com$request_uri;
}
```

listen指令意味着服务器块应用于HTTP和HTTPS流量。 server_name指令匹配具有域名`www.old-name.com`的请求URL。 return指令告诉NGINX停止处理请求，并立即向客户端发送代码`301（Moved Permanently）`和指定的重写URL。 重写的URL使用两个NGINX变量来捕获和复制原始请求URL中的值：`$scheme`是协议（`http`或`https`），`$request_uri`是包含参数的完整URI。

对于3xx系列中的代码，url参数定义新的（重写的）URL。
```
return (301 | 302 | 303 | 307) url;
```

对于其他代码，我们可以选择定义一个显示在响应正文中的文本字符串（HTTP 状态码的标准文本，例如 404 的 Not Found，仍包含在header中）。 文本可以包含NGINX变量。
```
return (1xx | 2xx | 4xx | 5xx) ["text"];
```

例如，当我们需要拒绝没有有效身份验证令牌的请求时，此指令可能适用：
```
return 401 "Access denied because token is expired or invalid";
```

还有一些可以使用的快捷语法方式，例如省略302的代码; 请参阅返回指令的参考文档。

（在某些情况下，我们可能希望返回一个比在文本字符串中可以实现的更复杂或更细微的响应。使用`error_page`指令，我们可以为每个`HTTP 状态码`返回完整的自定义HTML页面，以及更改 响应代码或执行重定向。）

所以 `return` 指令使用简单，适合当重定向满足两个条件：重写的URL适合于每个匹配服务器或位置块的请求，我们可以使用标准的NGINX变量构建重写的URL。

### rewrite 指令

但是，如果我们需要测试更复杂的URL之间的区别，捕获原始URL中没有相对应的NGINX变量的元素，或者更改、添加路径中的元素，该怎么办？ 我们可以在这种情况下使用`rewrite`指令。

像`return`指令，我们将`rewrite`指令包含在`server`或`location`上下文中，定义要重写的URL。
除此以外，这两个指令还大有不同，`rewrite`指令使用更复杂。 它的语法很简单：
```
rewrite regex URL [flag];
```
第一个参数“regex”意味着NGINX Plus和NGINX只有在匹配指定的正则表达式（除了匹配“server”或“location”指令之外）才重写URL。 附加测试意味着NGINX必须做更多的处理。

第二个区别是rewrite指令只能返回代码`301`或`302`。 要返回其他代码，你需要在`rewrite`指令之后包含一个`return`指令（见下面的例子）。

最后，`rewrite`指令不一定会阻止NGINX对请求的处理，但`return`会，而且不一定会向客户端发送重定向。 除非我们明确指出（使用标志或URL的语法）希望NGINX停止处理或发送重定向，它会运行在整个配置寻找到的在Rewrite模块中定义的指令（`break，if`， `return`，`rewrite`和`set`），并按顺序处理它们。 如果重写的URL与重写模块中的后续指令匹配，NGINX对重写的URL执行指示的操作（通常再次重写）。

这种事情可能会变得比较复杂，我们需要仔细计划如何配置指令以获得所需的结果。 例如，如果原始的“location”块和利用NGINX重写规则重写的URL相匹配，NGINX就会进入循环，应用重写一遍又一遍直到内置的限制10次。 要了解所有详细信息，请参阅Rewrite模块的文档。 如前所述，所以我们建议尽可能使用`return`指令。

下面是一个使用`rewrite`指令的NGINX重写规则示例。 它匹配以字符串 `/download`开头的URL，，然后在稍后的路径中的某处包含`/media/`或`/audio/`目录。 它用`/ mp3 /`替换这些元素，并添加适当的文件扩展名`.mp3`或`.ra`。 `$1`和`$2`变量捕获不变的路径元素。 例如，`/download/cdn-west/media/file1`变成`/download/cdn-west/mp3/file1.mp3`。

```
server {
    ...
    rewrite ^(/download/.*)/media/(.*)\..*$ $1/mp3/$2.mp3 last;
    rewrite ^(/download/.*)/audio/(.*)\..*$ $1/mp3/$2.ra  last;
    return  403;
    ...
}
```

我们上面提到，我们可以添加标志到`rewrite`指令来控制处理的流程。 示例中的`last`标志是其中之一：它告诉NGINX跳过当前`server`或`location`块中的任何后续`Rewrite-module`指令，并开始搜索与重写的URL匹配的新`location` 。

在这个例子中的最终的返回指令意味着如果URL不匹配rewrite指令，则返回 403 状态码 到客户端。

### try_files 指令

像`return`和`rewrite`指令，`try_files`指令放在`server`或`location`块中。 作为参数，它需要一个或多个文件和目录以及最终URI的列表：
```
try_files file … uri;
```

NGINX按顺序检查文件和目录的存在（从`root`和`alias`指令的设置构造每个文件的完整路径）。如果要指定目录，则需要在元素名称的末尾添加一个斜杠。 如果没有文件或目录存在，NGINX将执行内部重定向到由最后一个元素（uri）定义的URI。

对于`try_files`指令的工作，还需要定义一个`location`块来捕获内部的重定向，如下面的例子所示。 最终元素可以是已经被命名的location，并由at符号（`@`）表示。

`try_files`指令通常使用`$uri`变量，它表示域名后的URL部分。

在以下示例中，如果客户端请求的文件不存在，则NGINX提供默认的GIF文件。 当客户端请求（例如）`http//www.domain.com/images/image1.gif`时，NGINX首先在`root`或`alias`指令指定的本地目录中查找`image1.gif` 适用于位置（未在代码段中显示）。 如果`image1.gif`不存在，NGINX寻找`image1.gif/`，如果不存在，它会重定向到`/images/default.gif`。 该值与第二个位置指令完全匹配，因此处理停止，NGINX提供该文件并将其标记为缓存30秒。

```
location /images/ {
    try_files $uri $uri/ /images/default.gif;
}

location = /images/default.gif {
    expires 30s;
}
```
## 示例 - 标准化域名

NGINX重写规则最常见的用途之一是捕获网站域名的弃用或非标准版本，并将其重定向到当前名称。 有几个相关的用例。

### 从前名称重定向到当前名称

该示例NGINX重写规则将来自`www.old-name.com`和`old-name.com`的请求永久地重定向到`www.new-name.com`，来从原始请求URL中使用两个NGINX变量
- `$scheme`是原始协议（`http`或`https`），
- `$request_uri`是完整的URI（域名后面），包括参数：
```
server {
    listen 80;
    listen 443 ssl;
    server_name www.old-name.com old-name.com;
    return 301 $scheme://www.new-name.com$request_uri;
}
```

因为`$request_uri`捕获域名后面的URL部分，所以如果新旧站点之间存在一对一的页面对应，这种重写是合适的（例如`www.new-name.com/about`与`www.old-name.com/about`具有相同的基本内容。 如果在更改域名之外重新整理了网站，则可以通过省略`$request_uri`将所有请求重定向到主页，这样更安全：
```
server {
    listen 80;
    listen 443 ssl;
    server_name www.old-name.com old-name.com;
    return 301 $scheme://www.new-name.com;
}
```

例如，一些其他关于在NGINX中重写URL的博客对这些用例使用rewrite指令，像这样：
```
# NOT RECOMMENDED
rewrite ^ $scheme://www.new-name.com$request_uri permanent;
```
这比等效的`return`指令效率低，因为它需要NGINX处理一个正则表达式，虽然是一个简单的（符号[`^`]，它匹配完整的原始URL）。 相应的`return`指令对于我们来说也更容易解释：`return 301`更清楚地表示NGINX返回代码`301`而不是`rewrite ... permanent`符号。


### 添加和删除www前缀

这些示例添加和删除www前缀：
```
# add 'www'
server {
    listen 80;
    listen 443 ssl;
    server_name domain.com;
    return 301 $scheme://www.domain.com$request_uri;
}

# remove 'www'
server {
    listen 80;
    listen 443 ssl;
    server_name www.domain.com;
    return 301 $scheme://domain.com$request_uri;
}
```

再次说明，`return`比等效的`rewrite`更好。 `rewrite`需要解释一个正则表达式 - `^(.*)$` - 并创建一个自定义变量（`$1`），事实上它相当于内置的`$request_uri`变量。

```
# NOT RECOMMENDED
rewrite ^(.*)$ $scheme://www.domain.com$1 permanent;
```

### 将所有流量重定向到正确的域名

这是一个特殊情况，当请求URL不匹配任何`server`和`location`块时，可能因为域名拼写错误，将入站流量重定向到网站的主页。 它的工作原理是将`default_server`参数与`listen`指令组合，并将下划线作为`server_name`指令的参数。

```
server {
    listen 80 default_server;
    listen 443 ssl default_server;
    server_name _;
    return 301 $scheme://www.domain.com;
}
```

我们使用下划线作为`server_name`的参数，以避免无意中匹配到真实的域名 - 可以安全地假设任何站点都不会有下划线作为其域名。 不匹配任何其他`server`块的配置中的请求在这里结束，而`default_server`参数`listen`告诉NGINX为它们使用这个块。 通过从重写的URL中省略`$request_uri`变量，我们将所有请求重定向到主页，这是一个好主意，因为具有错误域名的请求尤其可能使用网站上不存在的URI。

## 示例 - 强制所有请求使用 SSL/TLS

此`server`块强制所有访问者对我们的网站使用安全（`SSL/TLS`）连接。
```
server {
    listen 80;
    server_name www.domain.com;
    return 301 https://www.domain.com$request_uri;
}
```
一些关于NGINX重写规则的其他博客使用`if`测试和`rewrite`指令来处理这个用例，像这样：
```
# NOT RECOMMENDED
if ($scheme != "https") {
    rewrite ^ https://www.mydomain.com$uri permanent;
}
```
但是此方法需要额外的处理，因为NGINX必须同时评估`if`条件并处理`rewrite`指令中的正则表达式。

## 示例 - 为WordPress网站启用漂亮的固定链接

NGINX和NGINX Plus是使用WordPress的网站的非常受欢迎的应用交付平台。 下面的`try_files`指令告诉NGINX检查文件`$uri`和目录`$uri/`的存在。 如果文件或目录不存在，NGINX将返回一个重定向到`/index.php`，并传递query-string参数，这些参数由`$args`参数捕获。

```
location / {
    try_files $uri $uri/ /index.php?$args;
}
```

## 示例 - 删除不受支持的文件扩展名的请求

由于种种原因，我们的网站可能会收到以与我们未运行的应用程序服务器相对应的文件扩展名结尾的请求网址。 在本示例中，像Engine Yard博客，应用程序服务器是`Ruby on Rails`，因此无法处理由其他应用程序服务器（如ASP，PHP，CGI等）处理的文件类型的请求，并且需要拒绝它们。 在一个`server`块中，将对动态生成的资源的任何请求传递给应用程序，这个`location`指令会在非`Rails`文件类型的请求到达`Rails`队列之前丢弃这些请求。

```
location ~ \.(aspx|php|jsp|cgi)$ {
    return 410;
}
```

严格地说，响应代码410（Gone）意在用于 该URL所请求的资源不再是可用的情况，并且服务器不知道其当前位置（如果有的话）。 它相对于响应代码404的优点是它明确地指示资源永久不可用，因此客户端不会再次发送请求。

我们可能希望通过返回响应代码“403（Forbidden）`Server handles only Ruby requests` ，为客户端提供更准确的失败原因。 作为一个替代，`deny all`指令直接返回403：

```
location ~ \.(aspx|php|jsp|cgi)$ {
    deny all;
}
```
状态码403隐式地确认所请求的资源存在，因此如果想要通过向客户端提供尽可能少的信息来实现“security through obscurity”，则状态码404可能是更好的选择。 缺点是客户端可能会反复重试请求，因为404不会明确指出资源是失败是临时的还是永久的。


## 示例 - 配置自定义重新路由

在本示例中，从[MODXCloud](https://modxcloud.com/userguide/using-modx-cloud/tools-and-configuration/web-rules-rewrites-redirects-tweaks.html)，我们有一个资源，作为一组URL的控制器。 我们的用户可以为资源使用更易读的名称，并重写（不重定向）它由控制器在`listing.html`处理。

```
rewrite ^/listings/(.*)$ /listing.html?listing=$1 last;
```

作为示例，用户友好的URL `http://mysite.com/listings/123`被重写为由`listing.html`控制器处理的URL，`http://mysite.com/listing.html?listing=123`。


[【原文：https://www.nginx.com/blog/creating-nginx-rewrite-rules/】](https://www.nginx.com/blog/creating-nginx-rewrite-rules/)
