Mirror
========================================

Basic concepts
----------------------------------------
The Docker image can be regarded as a special file system, which provides the files required for the container runtime. At the same time, the image also contains some information prepared for the runtime (environment variables, users, etc.).

The image will not be changed after construction, that is, the image will not contain dynamic data.

Windows Mirror
----------------------------------------
Since Windows does not directly open syscall, all Windows programs must communicate with the kernel through sys dll, which leads to Windows images that cannot be built directly through scratch, but can only be built based on several basic images provided by Microsoft.

Mirroring includes:

- `windows servercore <https://hub.docker.com/_/microsoft-windows-servercore>`_ has the most complete functions and includes the traditional .net framework environment
- `windowsnanoserver <https://hub.docker.com/_/microsoft-windows-nanoserver>`_ contains the .net core running environment
- `windows <https://hub.docker.com/_/microsoft-windows>`_ Provides the complete windows server api, which is being replaced by windows server
- `windows server <https://hub.docker.com/_/microsoft-windows-server//microsoft-windows-server//>`_ Provides the complete windows server api
