嗅探工具
================================

Nmap
--------------------------------
``nmap [<扫描类型>...] [<选项>] {<扫描目标说明>}``

指定目标
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CIDR风格 ``192.168.1.0/24``
- 逗号分割 ``www.baidu.com,www.zhihu.com``
- 分割线 ``10.22-25.43.32``
- 来自文件 ``-iL <inputfile>``
- 排除不需要的host ``--exclude <host1 [, host2] [, host3] ... >`` ``--excludefile <excludefile>``

主机发现
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-sL`` List Scan - simply list targets to scan
- ``-sn/-sP`` Ping Scan - disable port scan
- ``-Pn`` Treat all hosts as online -- skip host discovery
- ``-sS/sT/sA/sW/sM`` TCP SYN/Connect()/ACK/Window/Maimon scans
- ``-sU`` UDP Scan
- ``-sN/sF/sX`` TCP Null, FIN, and Xmas scans

.. list-table:: 扫描方式表
   :widths: 15 15 25 25 20
   :header-rows: 1

   * - 名称
     - 包标记
     - 端口OPEN
     - 端口CLOSE
     - 特点
   * - TCP SYN scan
     - SYN
     - 回复ACK+SYN
     - 回复RST
     - 应用程序无日志，但是容易被发现
   * - 全连接扫描
     - SYN
     - 回复ACK+SYN
     - 回复RST
     - 容易被发现
   * - ACK扫描
     - ACK
     - 回复RST
     - 包被丢弃
     - .
   * - FIN扫描
     - FIN
     - 包被丢弃
     - 回复RST
     - 需要等待超时，效率低
   * - TCP Xmas扫描
     - FIN+URG+PSH
     - 包被丢弃
     - 回复RST
     - 需要等待超时，效率低；不适用所有操作系统
   * - TCP NULL扫描
     - NULL
     - 包被丢弃
     - 回复RST
     - 需要等待超时，效率低；不适用所有操作系统

端口扫描
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``--scanflags``  定制的TCP扫描
- ``-P0`` 无ping
- ``PS [port list]`` (TCP SYN ping) // need root on Unix
- ``PA [port list]`` (TCP ACK ping)
- ``PU [port list]`` (UDP ping)
- ``PR (Arp ping)``
- ``p <port message>``
- ``F`` 快速扫描
- ``r`` 不使用随机顺序扫描

服务和版本探测
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-sV`` 版本探测
- ``--allports`` 不为版本探测排除任何端口
- ``--version-intensity <intensity>``  设置 版本扫描强度
- ``--version-light`` 打开轻量级模式 // 级别2
- ``--version-all`` 尝试每个探测 // 级别9
- ``--version-trace`` 跟踪版本扫描活动
- ``-sR RPC`` 扫描

操作系统扫描
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-O`` 启用操作系统检测 
- ``--osscan-limit`` 针对指定的目标进行操作系统检测
- ``--osscan-guess``
- ``--fuzzy`` 推测操作系统检测结果

时间和性能
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 调整并行扫描组的大小
    - ``--min-hostgroup<milliseconds>``
    - ``--max-hostgroup<milliseconds>``
- 调整探测报文的并行度
    - ``--min-parallelism<milliseconds>``
    - ``--max-parallelism<milliseconds>``
- 调整探测报文超时
    - ``--min_rtt_timeout <milliseconds>``
    - ``--max-rtt-timeout <milliseconds>``
    - ``--initial-rtt-timeout <milliseconds>``
- 放弃低速目标主机
    - ``--host-timeout<milliseconds>``
- 调整探测报文的时间间隔
    - ``--scan-delay<milliseconds>``
    - ``--max_scan-delay<milliseconds>``
- 设置时间模板
    - ``-T <Paranoid|Sneaky|Polite|Normal|Aggressive|Insane>``
    - ``-T<0-5>`` (越大越快)

逃避检测相关
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-f`` 报文分段
- ``--mtu`` 使用指定的MTU
- ``-D<decoy1[， decoy2][， ME]， ...>`` 使用诱饵隐蔽扫描
- ``-S<IP_Address>`` 源地址哄骗
- ``-e <interface>`` 使用指定的接口
- ``--source-port<portnumber>;-g<portnumber>`` 源端口哄骗
- ``--data-length<number>`` 发送报文时 附加随机数据
- ``--ttl <value>`` 设置ttl
- ``--randomize-hosts`` 对目标主机的顺序随机排列
- ``--spoof-mac<macaddress， prefix， orvendorname>`` MAC地址哄骗

输出
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-oN<filespec>`` 标准输出
- ``-oX<filespec>`` XML输出
- ``-oS<filespec>`` ScRipTKIdd|3oUTpuT
- ``-oG<filespec>`` Grep输出
- ``-oA<basename>`` 输出至所有格式
- ``--open`` 仅输出可能开放的端口信息

细节和调试
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``-v`` 信息详细程度
- ``-d [level]`` debug level
- ``--packet-trace`` 跟踪发送和接收的报文
- ``--iflist`` 列举接口和路由

Masscan
--------------------------------

编译
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: bash

    sudo apt-get install git gcc make libpcap-dev
    git clone https://github.com/robertdavidgraham/masscan
    cd masscan
    make -j

命令行选项
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``--ports`` 指定端口范围
- ``--rate`` 指定速率
- ``--source-ip`` 指定源IP
