Virtualization technology and container technology
----------------------------------------

Traditional virtualization technology
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Traditional virtualization technology adds hypervisor layer, virtual network card, memory, CPU and other virtual hardware, and then builds clients on it. Each client has its own system core. Traditional virtualization technology uses virtual machines as management units. Each virtual machine has independent operating system cores and does not share the host's software system resources. Therefore, it has good isolation and is suitable for multi-tenant scenarios in cloud computing environments.

Container technology
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Container technology can be regarded as a lightweight virtualization method. Container technology is virtualized at the operating system layer and can run multiple virtualization environments on the host kernel. Compared with traditional application testing and deployment, container deployment does not require pre-consideration of application operational environment compatibility issues; compared with traditional virtual machines, containers can run in the host without an independent operating system kernel, achieving higher operational efficiency and resource utilization rate.
