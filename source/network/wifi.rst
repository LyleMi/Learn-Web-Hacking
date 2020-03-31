Wi-Fi
========================================

简介
----------------------------------------
Wi-Fi又称“无线热点”或“无线网络”，是Wi-Fi联盟的商标，一个基于IEEE 802.11标准的无线局域网技术。

攻击
----------------------------------------

暴力破解
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
WiFi密码是基于预置的秘钥，可以通过抓取报文的方式在本地快速的批量进行密码爆破尝试。

伪造热点
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
AP可以动态的广播自己，客户也可以主动发送探针请求。可以伪造AP发送对探针请求的响应包，来让客户端错误的识别。

秘钥重装攻击
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
该漏洞由Vanhoef发现。Wi-Fi在握手时双方会更新秘钥，该攻击通过重放握手信息，令客户端重新安装相同的秘钥。

Dragonblood
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
最新版的WPA3标准在实现上存在一些问题，同样由Vanhoef发现。包含拒绝服务攻击、降级攻击、侧信道泄露等。

参考链接
----------------------------------------
- `Wi-Fi Alliance <https://www.wi-fi.org/>`_
- `Dragonblood <https://papers.mathyvanhoef.com/dragonblood.pdf>`_ : Analyzing the Dragonfly Handshake of WPA3 and EAP-pwd
- `Improving Privacy through Fast Passive Wi-Fi Scanning <https://papers.mathyvanhoef.com/nordsec2019.pdf>`_
- `Practical Side-Channel Attacks against WPA-TKIP <https://papers.mathyvanhoef.com/asiaccs2019.pdf>`_
- `Key Reinstallation Attacks: Breaking the WPA2 Protocol <https://papers.mathyvanhoef.com/blackhat-eu2017.pdf>`_
- `RFC 7664 Dragonfly Key Exchange <https://tools.ietf.org/html/rfc7664>`_
