审计流程大纲
================================


- 拿到代码，确定版本，确定能否正常运行
    - 找历史漏洞
    - 找应用该系统的实例

- 简单审计，运行审计工具看是否有漏洞

- 大概看懂整个程序是如何运行的
    - 文件如何加载
        - 类库依赖
        - 有没有加载waf

    - 数据库如何连接
        - mysql/mysqli/pdo
        - 有没有用预编译

    - 视图如何形成
        - 能不能xss
        - 能不能模版注入

    - SESSION如何处理
        - 文件
        - 数据库
        - 内存

    - Cache如何处理
        - 文件cache可能写shell
        - 数据库cache可能注入
        - memcache

- 看账户体系
    - 管理员账户的密码
        - 加密方式
        - 泄漏数据后能不能爆破密码
        - 重置漏洞
        - 修改密码漏洞
            - 修改其他人密码 

    - 普通用户的帐号
        - 能否拿到普通用户权限
        - 普通用户帐号能否盗号

    - 重点找没有帐号的情况下可以访问的页面
    - 是不是OAuth

- 攻击
    - SQLi
        - 看全局过滤能否bypass
        - 看是否有直接执行sql的地方
        - 看是用的什么驱动，mysql/mysqli/pdo
            - 如果使用PDO，看是否是直接执行的地方

    - XSS
        - 全局bypass
        - 直接echo
        - 看视图是怎么加载的

    - FILE
        - 上传下载覆盖删除
        - 包含
            - LFI
            - RFI
            - 全局找include, require
        - 正常上传
            - 看上传是如何确定能否上传文件的

    - RCE
        - call_user_func
        - eval
        - assert
        - preg_replace /e

    - XXE
    - CSRF
    - SSRF
    - 反序列化
    - 变量覆盖
        - extract
        - parse_str
        - array_map

    - LDAP
    - XPath
    - Cookie伪造

- 过滤
    - 找WAF
        - 看waf怎么过滤的，相应的如何绕过







