File reading
================================

Consider reading files that may have sensitive information

- Sensitive files in user directory
- .bash_history
- .zsh_history
- .profile
- .bashrc
- .gitconfig
- .viminfo
- passwd

- Application configuration file
- /etc/apache2/apache2.conf
- /etc/nginx/nginx.conf

- Application log file
- /var/log/apache2/access.log
- /var/log/nginx/access.log

- Sensitive files in the site directory
- .svn/entries
- .git/HEAD
- WEB-INF/web.xml
- .htaccess

- Special backup files
- .swp
- .Swo
- .bak
- index.php~
- ...

- Python's Cache
- ``__pycache__\__init__.cpython-35.pyc``
