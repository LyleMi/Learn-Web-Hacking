文件
================================

总体思路
--------------------------------
1. 上传下载覆盖删除
    1. move_uploaded_file
    2. file_put_contents/file_get_contents
    3. unlink
    4. fopen/fgets
2. 包含
    1. LFI
    2. RFI
    3. 全局找include, require
3. 正常上传
    1. 看上传是如何确定能否上传文件的


绕过
--------------------------------
一般在文件包含之前，可能会调用file_exists，那么，如何对其进行绕过呢

1. 截断

1.1 %00截断

    几乎是最常用的方法，条件是magic_quotes_gpc打开，而且php版本小于5.3.4。

1.2 长度截断

    Windows上的文件名长度和文件路径有关。具体关系为：从根目录计算，文件路径长度最长为259个bytes。

    msdn定义```#define MAX_PATH 260```，第260个字符为字符串结尾的```\0```

    linux可以用getconf来判断文件名长度限制和文件路径长度限制

    获取最长文件路径长度：getconf PATH_MAX /root 得到4096
    获取最长文件名：getconf NAME_MAX /root 得到255

    那么在长度有限的时候，```././././``` (n个) 的形式就可以通过这个把路径爆掉

2. 伪协议绕过
3. url绕过
4. 特殊字符绕过