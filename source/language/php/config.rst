安全相关配置
=================================

函数与类限制
---------------------------------
可通过 ``disable_functions`` / ``disable_classes`` 限制PHP可调用的函数和类。

目录访问限制
---------------------------------
可通过 ``open_basedir`` 限制PHP可访问的目录。

远程引用限制
---------------------------------
可通过 ``all_url_include`` 限制远程文件包含，默认关闭。
可通过 ``allow_url_fopen`` 限制打开远程文件，默认开启。

Session
---------------------------------

Session.Save
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
PHP的Session默认handler为文件，存储在 php.ini 的 ``session.save_path`` 中，若有任意读写文件的权限，则可修改或读取session。从phpinfo中可获得session位置。

Session.Upload
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
PHP默认开启了 ``session.upload_progress.enabled`` ， 该选项会导致生成上传进度文件，其存储路径可以在phpinfo中获取。

那么可以构造特别的报文向服务器发送，在有LFI的情况下即可利用。
