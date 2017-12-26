审计流程大纲
================================


- 拿到代码，确定版本，确定能否正常运行
    - 找历史漏洞
    - 找应用该系统的实例

- 大概阅读，跑跑审计工具看能不能捡漏
- 若需要安装
    - 安装之
    - 查看能否绕过判定重新安装
    - 查看能否利用安装文件获取信息
    - 看能否利用更新功能获取信息

- 大概看懂整个程序是如何运行的
    - 文件如何加载
        - 类库依赖
        - 有没有加载waf

    - 数据库怎么连接
        - mysql/mysqli/pdo
        - 有没有用预编译

    - 视图怎么形成
        - 能不能xss
        - 能不能模版注入

    - SESSION怎么处理
        - 文件
        - 数据库
        - 内存

    - Cache怎么处理
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
            - move_uploaded_file
            - file_put_contents/file_get_contents
            - unlink
            - fopen/fgets

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

- 逻辑
    - 支付逻辑
        - 直接发含金额的数据包
        - 没有限制数量
        - 异常处理
        - 负数

    - 账户确认逻辑
        - 改密码
        - 密码重置

    - ID生成有规律
    - 接口无限制
    - 加密算法
    - 越权
        - 水平越权
        - 垂直越权

    - 执行顺序
    - 敏感信息

- 过滤
    - 找WAF
        - 看waf怎么过滤的，相应的如何绕过







