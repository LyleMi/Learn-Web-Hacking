Download Tool
================================

wget
--------------------------------

Commonly used
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Normal download ``wget http://example.com/file.iso``
- Specify the save file name ``wget ‐‐output-document=myname.iso http://example.com/file.iso``
- Save to the specified directory ``wget ‐‐directory-prefix=folder/subfolder http://example.com/file.iso``
- Large file breakpoints continue to pass ``wget ‐‐continue http://example.com/big.file.iso``
- Download the url list in the specified file ``wget ‐‐input list-of-file-urls.txt``
- Download multiple files with a specified number list ``wget http://example.com/images/{1..20}.jpg``
- Download all resources of the web page ``wget ‐‐page-requisites ‐‐span-hosts ‐‐convert-links ‐‐adjust-extension http://example.com/dir/file``

Download the entire site
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Download all linked pages and files ``wget ‐‐execute robots=off ‐‐recursive ‐‐no-parent ‐continue ‐‐no-clobber http://example.com/``
- Download the file with the specified suffix ``wget ‐‐level=1 ‐‐recursive ‐no-parent ‐‐accept mp3,MP3 http://example.com/mp3/``
- Exclude the specified directory download ``wget ‐‐recursive ‐no-clobber ‐‐no-parent ‐exclude-directories /forums,/support http://example.com``

Specify parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- user agent ``‐‐user-agent="Mozilla/5.0 Firefox/4.0.1"``
- basic auth ``‐‐http-user=user ‐‐http-password=pwd``
- 保存cookie ``‐‐cookies=on ‐‐save-cookies cookies.txt ‐‐keep-session-cookies``
- 使用cookie ``‐‐cookies=on ‐‐load-cookies cookies.txt ‐‐keep-session-cookies``

curl
--------------------------------

Commonly used
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Show directly ``curl www.example.com``
- Save the specified name ``-o newname``
- No name specified ``-O``

Regular
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- File name ``curl ftp://example.com/file[1-100].txt``
- 域名 ``curl http://site.{one,two,three}.com``
