container standards
========================================

OCI
----------------------------------------
The Open Container Initiative (OCI) is an industry standard for standardizing container formats and runtimes. The current specifications proposed by OCI are:

- `OCI Runtime Specification <https://github.com/opencontainers/runtime-spec>`_
- `OCI Image Format <https://github.com/opencontainers/image-spec>`_
- `OCI Distribution Specification <https://github.com/opencontainers/distribution-spec>`_

CRI
----------------------------------------
Container Runtime Interface (CRI) defines the interface between containers and images. Currently officially supported container runtimes include Docker, Containerd, CRI-O and frakti.

Reference link
----------------------------------------

document
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Introducing Container Runtime Interface (CRI) in Kubernetes <https://kubernetes.io/blog/2016/12/container-runtime-interface-cri-in-kubernetes/>`_
- `cri-o <https://cri-o.io/>`_

accomplish
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `runc <https://github.com/opencontainers/runc>`_ Reference implementation of OCI Runtime
- `Kata Containers <https://github.com/kata-containers/kata-containers>`_ provides a high-performance hardware virtualization container runtime
- `gvisor <https://github.com/google/gvisor>`_ Container runtime based on user mode kernel implemented by Go
- `buildkit <https://github.com/moby/buildkit>`_ docker build split build project
