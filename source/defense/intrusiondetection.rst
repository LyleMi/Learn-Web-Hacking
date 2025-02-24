
========================================

IDS and IPS
----------------------------------------
IDS and IPS are common protective devices. The difference between IPS and IDS is that IPS usually has blocking capabilities.

Common intrusion points
----------------------------------------

- High-risk service intrusion

Monitoring implementation
----------------------------------------

Client monitoring
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Monitor sensitive configuration files
- Commonly used command ELF file integrity monitoring
- ``ps``
- ``lsof``
- ...
- rootkit monitoring

- Memory usage
- CPU usage rate
- IO usage rate
- Network usage rate
- New process monitoring
- File monitoring based on inotify

Network detection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Detection based on attack vectors at the network level, such as Snort, etc.

Log Analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The host system security log/operation log, network device traffic log, web application access log, SQL application access log and other logs are concentrated in a unified background to conduct a comprehensive analysis of various logs in the background.

Reference link
----------------------------------------
- `HIDS for enterprise security construction <https://www.freebuf.com/articles/es/194510.html>`_
- `Summary of practical intrusion detection of large Internet companies <https://xz.aliyun.com/t/1626/>`_
- `Tongchain intrusion detection system <https://mp.weixin.qq.com/s/kzeAEvz-ejLD71fgb5t8tA>`_
- `Web log security analysis system practice <https://xz.aliyun.com/t/2136>`_
- `A brief discussion on Web log security analysis <https://xz.aliyun.com/t/1121>`_
- `Some explorations of network layer bypassing IDS/IPS <https://mp.weixin.qq.com/s/QJeW7K-KThYHggWtJ-Fh3w>`_
