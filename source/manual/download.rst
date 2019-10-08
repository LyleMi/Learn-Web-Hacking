下载工具
================================

wget
--------------------------------

常用
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 普通下载 ``wget http://example.com/file.iso``
- 指定保存文件名 ``wget ‐‐output-document=myname.iso http://example.com/file.iso``
- 保存到指定目录 ``wget ‐‐directory-prefix=folder/subfolder http://example.com/file.iso``
- 大文件断点续传 ``wget ‐‐continue http://example.com/big.file.iso``
- 下载指定文件中的url列表 ``wget ‐‐input list-of-file-urls.txt``
- 下载指定数字列表的多个文件 ``wget http://example.com/images/{1..20}.jpg``
- 下载web页面的所有资源 ``wget ‐‐page-requisites ‐‐span-hosts ‐‐convert-links ‐‐adjust-extension http://example.com/dir/file``

整站下载
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 下载所有链接的页面和文件 ``wget ‐‐execute robots=off ‐‐recursive ‐‐no-parent ‐‐continue ‐‐no-clobber http://example.com/``
- 下载指定后缀的文件 ``wget ‐‐level=1 ‐‐recursive ‐‐no-parent ‐‐accept mp3,MP3 http://example.com/mp3/``
- 排除指定目录下载 ``wget ‐‐recursive ‐‐no-clobber ‐‐no-parent ‐‐exclude-directories /forums,/support http://example.com``

指定参数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- user agent ``‐‐user-agent="Mozilla/5.0 Firefox/4.0.1"``
- basic auth ``‐‐http-user=user ‐‐http-password=pwd``
- 保存cookie ``‐‐cookies=on ‐‐save-cookies cookies.txt ‐‐keep-session-cookies``
- 使用cookie ``‐‐cookies=on ‐‐load-cookies cookies.txt ‐‐keep-session-cookies``

curl
--------------------------------

常用
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 直接显示 ``curl www.example.com``
- 保存指定的名字 ``-o newname``
- 不指定名字 ``-O``

正则
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 文件名 ``curl ftp://example.com/file[1-100].txt``
- 域名 ``curl http://site.{one,two,three}.com``
