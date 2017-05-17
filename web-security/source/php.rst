PHP漏洞
================================

弱类型
    magic hash

截断
    ereg
    %00 截断
    iconv

变量覆盖
    global变量
    extract()
    parse_str

命令执行
    preg_replace 
    preg_replace 第一个参数是//e的时候  第二个参数会被当作命令执行