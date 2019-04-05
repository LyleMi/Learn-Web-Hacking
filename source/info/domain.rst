域名信息
========================================

- `Whois <https://www.whois.com/>`_
- 子域名收集
    - 利用第三方查询
        - `DNSDumpster <https://dnsdumpster.com/>`_
        - `Virustotal <https://www.virustotal.com/>`_
        - CrtSearch
        - threatminer
    - ASN
        - ``whois -h whois.radb.net -- '-i origin AS111111' | grep -Eo "([0-9.]+){4}/[0-9]+" | uniq``
        - ``nmap --script targets-asn --script-args targets-asn.asn=15169``
    - CSP规则中获取
    - 子域爆破
    - PassiveDNS
    - 利用兄弟域名查询流程
        - 查询域名注册邮箱
        - 通过域名查询备案号
        - 通过备案号查询域名
        - 反查注册邮箱
        - 反查注册人
        - 通过注册人查询到的域名在查询邮箱
        - 通过上一步邮箱去查询域名
        - 查询以上获取出的域名的子域名
    - 利用域传送漏洞
    - SSL/TLS证书中可能会有多个域名的信息
    - DNS记录中的SPF记录
- 若目标使用cdn，绕过cdn找到ip
