Intrusion detection
========================================

IDS and IPS
----------------------------------------
IDS and IPS are common protection devices. The difference between IPS and IDS is that IPS usually has blocking capabilities.

Common entry points
----------------------------------------
- Web intrusion
- High-risk service intrusion

Monitoring implementation
----------------------------------------

Client monitoring
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Monitor sensitive configuration files
- Commonly used commands for ELF file integrity monitoring
    - ``ps``
    - ``lsof``
    - ...
- rootkit monitoring
- Resource usage alarm
    - Memory usage
    -CPU usage
    - IO usage
    - Network usage
- New process monitoring
- File monitoring based on inotify

Network detection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Detection based on network-level attack vectors, such as Snort, etc.

Log analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Concentrate host system security logs/operation logs, network device traffic logs, Web application access logs, SQL application access logs and other logs into a unified backend, and conduct comprehensive analysis of various logs in the backend.

Reference link
----------------------------------------
- `HIDS for enterprise security construction <https://www.freebuf.com/articles/es/194510.html>`_
- `A practical summary of intrusion detection for large Internet companies <https://xz.aliyun.com/t/1626/>`_
- `Tongcheng Intrusion Detection System <https://mp.weixin.qq.com/s/kzeAEvz-ejLD71fgb5t8tA>`_
- `Web log security analysis system practice <https://xz.aliyun.com/t/2136>`_
- `A brief discussion on Web log security analysis <https://xz.aliyun.com/t/1121>`_
- `Some exploration of network layer bypassing IDS/IPS <https://mp.weixin.qq.com/s/QJeW7K-KThYHggWtJ-Fh3w>`_
