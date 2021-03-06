HTTP协议的状态消息都有哪些?
===========================

`"ruby\lib\ruby\2.0\webrick\httpstatus.rb"`

```ruby
      when [100,200) parent = Info
      when [200,300) parent = Success
      when [300,400) parent = Redirect
      when [400,500) parent = ClientError
      when [500,600) parent = ServerError
```

助记：
```
12345
ISRCS

I Suck Red Cold Sausage

```

常用的
- 200 OK
- 301 永久重定向
- 302 临时重定向
- 304 未修改
- 404 请求的资源不存在   
- 500 服务器内部错误  
- 502 Bad Gateway
- 503 服务器暂时不可用

[HTTP状态码](http://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)


简述下cookie的操作，还有cookie的属性都知道哪些
==============================================

网站优化
========

- 减少HTTP请求次数：CSS Spirit，Data URI
- JavaScript,CSS,HTML压缩

同源策略
========
[Same-origin policy - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/Same-origin_policy)
[Same-origin policy - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Same_origin_policy_for_JavaScript)
[Same Origin Policy - Web Security](http://www.w3.org/Security/wiki/Same_Origin_Policy)

Quick Answer:
> An origin is defined by the scheme, host, and port of a URL. Generally speaking, documents retrieved from distinct origins are isolated from each other. For example, if a document retrieved from http://example.com/doc.html tries to access the DOM of a document retrieved from https://example.com/target.html, the user agent will disallow access because the origin of the first document, (http, example.com, 80), does not match the origin of the second document (https, example.com, 443).

一个origin通过scheme，host，port定义。从不同origins得到的documents之间是相互隔绝。比如，UA会禁止一个`http://example.com/doc.html`的document访问`https://example.com/target.html`的DOM。因为二者不同源。不同源是因为二者的shceme不同，一个是http另一个是https。

HTTP GET的最大长度
==================

多数服务器的限制是8字节，这个值是可以配置的。
MSIE和Safari的限制是2K左右，Opera是4K，Firefox是8K。
所以255字节以内是比较安全的

[web services - maximum length of HTTP GET request? - Stack Overflow](http://stackoverflow.com/questions/2659952/maximum-length-of-http-get-request)

不同浏览器的URL最大长度
=======================

HTTP1.1协议没有明确限制URL的长度。但是不同的浏览器和HTTP服务器有自己的限制。
比如IE的URL不能超过*2083个*字符。
最佳实践是不要让URL超过2000个字符。

[What is the maximum length of a URL in different browsers?](http://stackoverflow.com/questions/417142/what-is-the-maximum-length-of-a-url-in-different-browsers/417180#417180)


列举HTTP请求的头有哪些内容
==========================

HTTP头中的HOST作用是什么？
=========================
按说在浏览器得到远端server IP之后就可以直接用IP来发送数据了，为什么还需要HOST字段呢？
因为一个IP上可能有多个虚拟主机对应于不同的域名。根据域名来判断是要访问哪个虚拟主机。

描述一下HTTP服务器session机制
=============================

描述一下cookie机制
==================

高性能网站
==========

协议相关的优化方法
------------------

- Reduce DNS Lookups
- Make few HTTP Request
  - Image Map
  - CSS Sprites
  - Inline Images
  - Combined Scripts and Stylesheets
- Gzip
- CDN

- Add Expires Header
- Configure ETags
- Avoid Redirection


**助记：三减少，增避配**

- 3减少：减少HTTP请求、减少DNS查询、压缩以减少资源尺寸 
- 增避配：增加过期头、避免重定向，配置ETags

助记图
```
Browser->DNS->HTTP->CDN---\
                            Server 增避配
Browser<-----Gzip---------/
```


HTML、JavaScript、CSS先关的优化方法
-----------------------------------
- External JS/CSS
- Remove Duplicated JS/CSS
- Stylesheets at Top
- Scripts at Bottom

- Minify JavaScript
- Make Ajax Cachable

- Avoid CSS expressions

助记：

- JS/CSS:**外部化，别重复，样式头，脚本尾**
- JS: **Minify，缓存Ajax**
- CSS:**避免css表达式**


高性能JavaScript
================
