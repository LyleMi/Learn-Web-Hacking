file reading
================================

Consider reading files that may contain sensitive information

- Sensitive files in user directory
    - .bash_history
    - .zsh_history
    - .profile
    - .bashrc
    - .gitconfig
    - .viminfo
    - passwd

- Application configuration files
    - /etc/apache2/apache2.conf
    - /etc/nginx/nginx.conf

- Application log files
    - /var/log/apache2/access.log
    - /var/log/nginx/access.log

- Sensitive files in the site directory
    - .svn/entries
    - .git/HEAD
    - WEB-INF/web.xml
    - .htaccess

- Special backup files
    - .swp
    - .swo
    - .bak
    - index.php~
    - ...

- Python Cache
    - ``__pycache__\__init__.cpython-35.pyc``