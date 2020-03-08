httponly
================================

- 在cookie为httponly的情况下，可以通过xss直接在源站完成操作，不直接获取cookie。
- 在有登录操作的情况下，部分站点直接发送登录请求可能会带有cookie
- 部分特定版本的浏览器可能会在httponly支持/处理上存在问题
- 低版本浏览器支持 TRACE / TRACK，可获取敏感的header字段
- phpinfo 等页面可能会回显信息，这些信息中包含http头
- 通过xss劫持页面钓鱼
- 通过xss伪造oauth等授权请求，远程登录
