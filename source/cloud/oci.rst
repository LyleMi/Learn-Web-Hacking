容器标准
========================================

OCI
----------------------------------------
开放容器标准 (Open Container Initiative, OCI) 是用于规范容器格式和运行时行业标准。目前OCI提出的规范有：

- `OCI Runtime Specification <https://github.com/opencontainers/runtime-spec>`_
- `OCI Image Format <https://github.com/opencontainers/image-spec>`_
- `OCI Distribution Specification <https://github.com/opencontainers/distribution-spec>`_

CRI
----------------------------------------
容器运行时 (Container Runtime Interface, CRI) 定义了容器和镜像的接口，目前官方支持的容器运行时包括Docker、Containerd、CRI-O和frakti。

参考链接
----------------------------------------

文档
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Introducing Container Runtime Interface (CRI) in Kubernetes <https://kubernetes.io/blog/2016/12/container-runtime-interface-cri-in-kubernetes/>`_
- `cri-o <https://cri-o.io/>`_

实现
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `runc <https://github.com/opencontainers/runc>`_ OCI Runtime 的参考实现
- `Kata Containers <https://github.com/kata-containers/kata-containers>`_ 提供高性能的硬件虚拟化容器运行时
- `gvisor <https://github.com/google/gvisor>`_ Go 实现的基于用户态内核的容器运行时
- `buildkit <https://github.com/moby/buildkit>`_ docker build 拆分出来的build项目
