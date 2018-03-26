# Web安全学习笔记

该仓库旨在完成Web安全相关知识的整理，尚有缺漏或未完成的部分，持续更新中。在线版本可点击[此处](http://websec.readthedocs.io)查看。

在完成的过程中参考了一些blog，皆在文末给出相应链接，感谢blog作者的分享。

该仓库仅供学习和交流使用，请勿使用相关内容进行非法行为。

### 目录结构

- 基础知识
    - 基础概念
    - 信息收集
    - 审计相关
    - 内网渗透
    - 相关工具
- 常见漏洞
    - SQL注入
    - XSS
    - 文件读取/上传/包含
    - XXE
    - CSRF
    - SSRF
    - XPath注入
    - 命令注入
    - 逻辑漏洞
    - 配置漏洞
- 语言及其框架相关漏洞
    - PHP
    - Python
    - Java
    - JavaScript
- 其他
    - 认证方式
	- Docker安全
	- 引擎解析漏洞
    - 缓存欺骗攻击
    - Web安全相关CTF题目

### 生成 HTML 格式的文档

```shell
$ sudo pip install sphinx
$ sudo pip install sphinx-rtd-theme
$ make html
```

### 反馈

欢迎大家提出各种意见和建议，不胜感激。

反馈邮箱 ``lylemi@126.com``