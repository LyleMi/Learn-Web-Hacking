镜像
========================================

基本概念
----------------------------------------
Docker 镜像可以看作是一个特殊的文件系统，用于提供容器运行时所需的文件，同时镜像还包含了一些为运行时准备的一些信息（环境变量、用户等）。

在构建之后镜像不会被改变，即是说镜像中不会包含动态的数据。

Windows 镜像
----------------------------------------
由于 Windows 并不直接开放 syscall ，所有的 Windows 程序都必须通过 sys dll 与内核沟通，这就导致 Windows 镜像并不能直接通过 scratch 来构建，只能基于微软提供的几个基础镜像来构建。

镜像包括：

- `windows servercore <https://hub.docker.com/_/microsoft-windows-servercore>`_ 功能最完整，包含传统的 .net framework 环境
- `windows nanoserver <https://hub.docker.com/_/microsoft-windows-nanoserver>`_ 包含 .net core 运行环境
- `windows <https://hub.docker.com/_/microsoft-windows>`_ 提供完整的 windows server api，正在被 windows server 替代
- `windows server <https://hub.docker.com/_/microsoft-windows-server/>`_ 提供完整的 windows server api
