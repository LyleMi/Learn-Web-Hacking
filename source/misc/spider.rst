爬虫
========================================

反爬虫机制
----------------------------------------
- 检测 User-Agent
- 数据加密
- 接口签名
- 聚类风控
- 浏览器指纹检测
    - 硬件特性
    - 插件 ``window.navigator.plugins``
    - 屏幕 ``window.screen``
    - ...
- canvas 指纹检测

前端反调试
----------------------------------------
- hook 按键事件，禁止 F12 / 右键
    - document.oncontextmenu
    - document.onkeydown
    - document.onkeyup
    - document.onkeypress
- 循环 debugger
- 检测控制台打开后主动触发 OOM
