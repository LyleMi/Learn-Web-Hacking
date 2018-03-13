phpinfo相关漏洞
=================================

Session.Save
---------------------------------
PHP的Session默认handler为文件，存储在 php.ini 的 ``session.save_path`` 中，若有任意读写文件的权限，则可修改或读取session。
从phpinfo中可获得session位置

Session.Upload
---------------------------------
php.ini默认开启了 ``session.upload_progress.enabled`` ， 该选项会导致生成上传进度文件，其存储路径可以在phpinfo中获取。

那么可以构造特别的报文向服务器发送，在有LFI的情况下即可利用。

/tmp临时文件竞争
---------------------------------
phpinfo中可以看到上传的临时文件的路径，从而实现LFI