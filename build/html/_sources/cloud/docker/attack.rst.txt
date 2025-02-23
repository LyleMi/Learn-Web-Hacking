Attack surface analysis
----------------------------------------

Supply Chain Security
----------------------------------------
In the process of building Dockerfile, even if you use the top-ranked sources, there may be problems such as CVE vulnerabilities, backdoors, mirror contamination, and dependency libraries in the mirror.

Container escape
----------------------------------------

Virtualization risks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Although Docker performs basic isolation of file system resources through namespace, there are still ``/sys``, ``/proc/sys``, ``/proc/bus``, ``/dev``, `` Important system file directories and namespace information such as `time`, ``syslog`` are not isolated, but share relevant resources with the host.

Escape with kernel vulnerabilities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2022-0847 Dirty Pipe
- CVE-2021-4034 Polkit
- CVE-2018-18955
- CVE-2016-5195

Container escape vulnerability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2021-41091
- CVE-2020-15257 Containerd Escape
- Requires network setting to host mode
- CVE-2019-14271 Docker cp
- CVE-2019-13139 Docker build code execution
- CVE-2019-5736 Runc
- Docker Version < 18.09.2
- Version <= 1.0-rc6

Improper configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Turn on privileged
- Mount the host sensitive directory
- Improper cap configuration
- Process Injection: SYS_PTRACE
- Loading kernel module: SYS_MODULE
- Read host shadow: DAC_READ_SEARCH
- Change the host shadow: DAC_READ_SEARCH + DAC_OVERRIDE
- ``--cap-add=SYS_ADMIN``
- Bypass namespace
- ``--net=host``
- ``--pid=host``
- ``--ipc=host``

Dangerous mount
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Mount ``/var/run/docker.sock``
- Mount the host ``/dev````/proc`` and other dangerous directories

Escape skills
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Escape via ``binfmt_misc``
- Escape through eBPF
- When the host directory can be mounted, the host root directory can be mounted to the directory in the container

Denial of service
----------------------------------------
- CPU exhausted
- Memory exhausted
- Storage exhausted
- Network resources exhausted

Attacking Docker Daemon
----------------------------------------
Although Docker containers have strong security protection measures, the Docker daemon itself is not well protected. The Docker daemon itself is run by the root user by default, and the process itself is not protected by security modules such as Seccomp or AppArmor. This allows the attacker to successfully find the vulnerability to control the Docker daemon to write or execute any file or code, and can successfully obtain the host's root permissions without being hindered by various security mechanisms. It is worth mentioning that by default Docker will not enable User Namespace isolation, which also means that the root inside Docker has the same read and write permissions to files as the root of the host machine. This results in another issue that once the internal root process of the container gets the opportunity to read and write the host file. This is reflected in the use of CVE-2019-5636.

Related CVE
----------------------------------------
- CVE-2014-5277
- CVE-2014-6408
- CVE-2014-9357
- CVE-2014-9358
- CVE-2015-3627
- CVE-2015-3630
- CVE-2019-14271
- CVE-2019-5736
- CVE-2020-15257
- CVE-2022-0847
- CVE-2024-21626
- CVE-2024-23651
- CVE-2024-23652
- CVE-2024-23653
