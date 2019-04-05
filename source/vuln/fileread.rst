文件读取
================================

考虑读取可能有敏感信息的文件

- 用户目录下的敏感文件
    - .bash_history
    - .zsh_history
    - .profile
    - .bashrc
    - .gitconfig
    - .viminfo
    - passwd

- 应用的配置文件
    - /etc/apache2/apache2.conf
    - /etc/nginx/nginx.conf

- 应用的日志文件
    - /var/log/apache2/access.log
    - /var/log/nginx/access.log

- 站点目录下的敏感文件
    - .svn/entries
    - .git/HEAD
    - WEB-INF/web.xml
    - .htaccess

- 特殊的备份文件
    - .swp
    - .swo
    - .bak
    - index.php~
    - ...

- Python的Cache
    - ``__pycache__\__init__.cpython-35.pyc``