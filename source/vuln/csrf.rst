CSRF
========================================

简介
----------------------------------------
跨站请求伪造 (Cross-Site Request Forgery, CSRF)，也被称为 One Click Attack 或者 Session Riding ，通常缩写为CSRF，是一种对网站的恶意利用。尽管听起来像XSS，但它与XSS非常不同，XSS利用站点内的信任用户，而CSRF则通过伪装来自受信任用户的请求来利用受信任的网站。

分类
----------------------------------------

资源包含
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
资源包含是在大多数介绍CSRF概念的演示或基础课程中可能看到的类型。这种类型归结为控制HTML标签（例如<image>、<audio>、<video>、<object>、<script>等）所包含的资源的攻击者。如果攻击者能够影响URL被加载的话，包含远程资源的任何标签都可以完成攻击。

由于缺少对Cookie的源点检查，如上所述，此攻击不需要XSS，可以由任何攻击者控制的站点或站点本身执行。此类型仅限于GET请求，因为这些是浏览器对资源URL唯一的请求类型。这种类型的主要限制是它需要错误地使用安全的HTTP请求方式。 

基于表单
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
通常在正确使用安全的请求方式时看到。攻击者创建一个想要受害者提交的表单; 其包含一个JavaScript片段，强制受害者的浏览器提交。

该表单可以完全由隐藏的元素组成，以致受害者很难发现它。

如果处理cookies不当，攻击者可以在任何站点上发动攻击，只要受害者使用有效的cookie登录，攻击就会成功。如果请求是有目的性的，成功的攻击将使受害者回到他们平时正常的页面。该方法对于攻击者可以将受害者指向特定页面的网络钓鱼攻击特别有效。

XMLHttpRequest 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
XMLHttpRequest可能是最少看到的方式，由于许多现代Web应用程序依赖XHR，许多应用花费大量的时间来构建和实现这一特定的对策。

基于XHR的CSRF通常由于SOP而以XSS有效载荷的形式出现。没有跨域资源共享策略 (Cross-Origin Resource Sharing, CORS)，XHR仅限于攻击者托管自己的有效载荷的原始请求。

这种类型的CSRF的攻击有效载荷基本上是一个标准的XHR，攻击者已经找到了一些注入受害者浏览器DOM的方式。 

防御
----------------------------------------
- 通过CSRF-token或者验证码来检测用户提交
- 验证 Referer/Content-Type
- 对于用户修改删除等操作最好都使用POST操作
- 避免全站通用的Cookie，严格设置Cookie的域

参考链接
----------------------------------------
- `demo <https://www.github.com/jrozner/csrf-demo>`_
- `Wiping Out CSRF <https://medium.com/@jrozner/wiping-out-csrf-ded97ae7e83f>`_
- `Neat tricks to bypass CSRF protection <https://www.slideshare.net/0ang3el/neat-tricks-to-bypass-csrfprotection>`_
