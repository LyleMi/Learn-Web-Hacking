持久化
========================================

基于存储
----------------------------------------
有时候网站会将信息存储在Cookie或localStorage，而因为这些数据一般是网站主动存储的，很多时候没有对Cookie或localStorage中取出的数据做过滤，会直接将其取出并展示在页面中，甚至存了JSON格式的数据时，部分站点存在 ``eval(data)`` 之类的调用。因此当有一个XSS时，可以把payload写入其中，在对应条件下触发。

在一些条件下，这种利用方式可能因为一些特殊字符造成问题，可以使用 ``String.fromCharCode`` 来绕过。

Service Worker
----------------------------------------
Service Worker可以拦截http请求，起到类似本地代理的作用，故可以使用Service Worker Hook一些请求，在请求中返回攻击代码，以实现持久化攻击的目的。

在Chrome中，可通过 ``chrome://inspect/#service-workers`` 来查看Service Worker的状态，并进行停止。

AppCache
----------------------------------------
在可控的网络环境下（公共wifi），可以使用AppCache机制，来强制存储一些Payload，未清除的情况下，用户访问站点时对应的payload会一直存在。
