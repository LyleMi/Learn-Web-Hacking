# Web安全学习笔记

![](https://img.shields.io/github/stars/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/forks/lylemi/learn-web-hacking.svg)
![](https://img.shields.io/github/issues/lylemi/learn-web-hacking.svg)

在学习Web安全的过程中，深感相关知识浩如烟海，而且很多知识点是零散的，于是尝试把一些知识和想法总结下来。

所学浅薄、精力有限，因此这份笔记有一些缺漏或是未完成的部分，在持续更新中，如果有错误恳请广大读者批评指正。在线版本可点击[这里](https://websec.readthedocs.io)查看。

在完成的过程中参考了很多资料，都在文末记录了相应的链接，感谢作者的分享。

### 笔记大纲

1. 基础知识
    - Web发展简史
    - 计算机网络
    - 域名系统
    - HTTP标准
    - 代码审计
    - WAF
2. 信息收集
    - 域名信息收集
    - 站点信息收集
    - 端口信息
3. 内网渗透
    - Windows信息收集
    - Windows持久化
    - Linux信息收集
    - 痕迹清理
4. 常见漏洞
    - SQL注入
    - XSS
    - 文件相关漏洞
    - XXE
    - CSRF
    - SSRF
    - 模版注入
    - Xpath注入
    - 命令注入
    - 逻辑漏洞 / 业务漏洞
    - 配置安全
    - 引擎解析漏洞
    - Web Cache欺骗攻击
5. 语言及其框架相关漏洞
    - PHP相关
    - Python相关
    - Java相关
    - JavaScript相关
    - Ruby
6. 防御
    - 防御思路
    - 加固检查
    - 应急响应
    - 溯源分析
    - 威胁情报
    - 蜜罐技术
7. 工具与资源
    - 爆破工具
    - 下载工具
    - 流量相关
    - 嗅探工具
    - SQLMap使用
    - 工具列表
    - 推荐资源
8. 其他
    - 认证方式
    - 拒绝服务攻击
    - Docker

### 本地生成 HTML 格式的文档

```shell
$ sudo pip install sphinx sphinx-rtd-theme
$ make html
```

### 注

该仓库仅供学习和交流使用，请勿使用相关内容进行非法行为。

本笔记内容可以任意转载，但请注明来源并提供链接。
