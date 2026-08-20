Virtualization technology and container technology
----------------------------------------

Traditional virtualization technology
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Traditional virtualization technology adds a hypervisor layer to virtualize virtual hardware such as network cards, memory, and CPUs, and then builds clients on top of them. Each client has its own system kernel. Traditional virtualization technology uses virtual machines as management units. Each virtual machine has an independent operating system kernel and does not share the host's software system resources. Therefore, it has good isolation and is suitable for multi-tenant scenarios in cloud computing environments.

Container technology
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Container technology can be regarded as a lightweight virtualization method. Container technology virtualizes at the operating system layer and can run multiple virtualization environments on the host kernel. Compared with traditional application testing and deployment, container deployment does not need to consider the compatibility of the application's operating environment in advance; compared with traditional virtual machines, containers can run on the host without an independent operating system kernel, achieving higher operating efficiency and resource utilization.
