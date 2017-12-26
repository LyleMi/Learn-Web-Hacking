Web Cache欺骗攻击
================================

简介
--------------------------------
网站通常都会通过如CDN、负载均衡器、或者反向代理来实现Web缓存功能。通过缓存频繁访问的文件，降低服务器响应延迟。例如，网站"htttp://www.example.com"配置了反向代理。对于那些包含用户个人信息的页面，如"http://www.example.com/home.php"，由于每个用户返回的内容有所不同，因此这类页面通常是动态生成，并不会在缓存服务器中进行缓存。通常缓存的主要是可公开访问的静态文件，如css文件、js文件、txt文件、图片等等。此外，很多最佳实践类的文章也建议，对于那些能公开访问的静态文件进行缓存，并且忽略HTTP缓存头。
Web cache攻击类似于RPO相对路径重写攻击(link1,link2)，都依赖于浏览器与服务器对URL的解析方式。当访问不存在的URL时，如"http://www.example.com/home.php/non-existent.css",浏览器发送get请求，依赖于使用的技术与配置，服务器返回了页面"http://www.example.com/home.php"的内容，同时URL地址任然是"http://www.example.com/home.php/non-existent.css"，http头的内容也与直接访问"http://www.example.com/home.php"相同，cacheing header、content-type（此处为text/html）也相同。

漏洞成因
--------------------------------
当代理服务器设置为缓存静态文件并忽略这类文件的caching header时，访问"http://www.example.com/home.php/no-existent.css"时，会发生什么呢？整个响应流程如下：
1.浏览器请求http://www.example.com/home.php/no-existent.css ;
2.服务器返回http://www.example.com/home.php 的内容(通常来说不会缓存该页面);
3.响应经过代理服务器;
4.代理识别该文件有css后缀;
5.在缓存目录下，代理服务器创建目录home.php，将返回的内容作为non-existent.css保存。

漏洞利用
--------------------------------
攻击者欺骗用户访问"http://www.example.com/home.php/logo.png?www.myhack58.com ",导致含有用户个人信息的页面被缓存，从而能被公开访问到。更严重的情况下，如果返回的内容包含session标识、安全问题的答案，或者Csrf token。这样攻击者能接着获得这些信息，因为通常而言大部分网站静态资源都是公开可访问的

漏洞存在的条件
--------------------------------
漏洞要存在，至少需要满足下面两个条件：
①web cache功能根据扩展进行保存，并忽略caching header;
②当访问如"http://www.examplecom/home.php/non-existent.css"不存在的页面，会返回"home.php"的内容。

漏洞防御
--------------------------------
防御措施主要包括3点：
①设置缓存机制，仅仅缓存http caching header允许的文件，这能从根本上杜绝该问题;
②如果缓存组件提供选项，设置为根据content-type进行缓存;
③访问"http://www.example.com/home.php/non-existent.css"这类不存在页面，不返回"home.php"的内容，而返回404或者302。

Web Cache欺骗攻击实例
--------------------------------
Paypal
Paypal在未修复之前，通过该攻击，可以获取的信息包括：用户姓名、账户金额、信用卡的最后4位数、交易数据、emaill地址等信息。
受该攻击的部分页面包括："https://www.paypal.com/myaccount/home/attack.css "、"https://www.paypal.com/myaccount/settings/notifications/attack.css "、"https://history.paypal.com/cgi-bin/webscr/attack.css?cmd=_history-details "。
可以缓存页面的静态文件后缀如下：aif、aiff、au、avi、bin、bmp、cab、carb、cct、cdf、class、css、doc、dcr、dtd、gcf、gff、gif、grv、hdml、hqx、ico、ini、jpeg、jpg、js、mov、mp3、nc、pct、ppc、pws、swa、swf、txt、vbs、w32、wav、wbmp、wml、wmlc、wmls、wmlsc、xsd、zip。
缓存有效期：经过测试，一旦文件被访问，它就会被缓存大约5小时。如果这之间该文件又被访问，则有效期延长。
