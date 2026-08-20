Attack surface analysis
----------------------------------------

supply chain security
----------------------------------------
In the process of building a Dockerfile, even if you use a top-ranked source, there may be issues such as CVE vulnerabilities, backdoors, contaminated images, and vulnerabilities in dependency libraries in the images.

container escape
----------------------------------------

Virtualization risks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Although Docker performs basic isolation of file system resources through namespaces, there are still important system file directories and namespace information such as ``/sys``, ``/proc/sys``, ``/proc/bus``, ``/dev``, ``time``, ``syslog``, etc. that are not isolated, but share related resources with the host.

Escape using kernel vulnerabilities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2022-0847 Dirty Pipe
- CVE-2021-4034 Polkit
- CVE-2018-18955
- CVE-2016-5195

Container escape vulnerability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- CVE-2021-41091
- CVE-2020-15257 Containerd escape
    - The network needs to be set to host mode
- CVE-2019-14271 Docker cp
- CVE-2019-13139 Docker build code execution
- CVE-2019-5736 runC
    - Docker Version < 18.09.2
    - Version <= 1.0-rc6

Improper configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Turn on privileged
- Mount sensitive directories on the host
- Improper cap configuration
    - Process injection: SYS_PTRACE
    - Load kernel module: SYS_MODULE
    - Read host shadow: DAC_READ_SEARCH
    - Change host shadow: DAC_READ_SEARCH + DAC_OVERRIDE
    - ``--cap-add=SYS_ADMIN``
- Bypass namespace
    - ``--net=host``
    - ``--pid=host``
    - ``--ipc=host``

Dangerous mount
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Mount ``/var/run/docker.sock``
- Mount dangerous directories such as host ``/dev`` ``/proc``

escape techniques
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Escape via ``binfmt_misc``
- Escape via eBPF
- If the host directory can be mounted, the host root directory can be mounted to the directory in the container.

Denial of service
----------------------------------------
- CPU exhaustion
- memory exhausted
- Storage exhausted
- Network resources exhausted

Attacking the Docker daemon
----------------------------------------
Although Docker containers have strong security protection measures, the Docker daemon itself is not fully protected. The Docker daemon process itself is run by the root user by default, and the process itself is not protected by security modules such as Seccomp or AppArmor. This allows an attacker to successfully find a vulnerability and control the Docker daemon to write arbitrary files or execute code, then he can successfully obtain the root permissions of the host without being hindered by various security mechanisms. It is worth mentioning that Docker does not enable User Namespace isolation by default, which also means that the root inside Docker and the host root have the same read and write permissions on files. This results in file permissions not becoming another issue once the root process inside the container gets a chance to read and write host files. This is demonstrated in the CVE-2019-5636 exploit.

Related CVEs
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
