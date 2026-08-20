mirror
========================================

Basic concepts
----------------------------------------
The Docker image can be regarded as a special file system that provides the files required for the container to run. The image also contains some information (environment variables, users, etc.) prepared for runtime.

The image will not be changed after it is built, which means that the image will not contain dynamic data.

Windows mirroring
----------------------------------------
Since Windows does not directly open syscall, all Windows programs must communicate with the kernel through sys dll. This means that Windows images cannot be built directly through scratch and can only be built based on several basic images provided by Microsoft.

Mirrors include:

- `windows servercore <https://hub.docker.com/_/microsoft-windows-servercore>`_ has the most complete functions and includes the traditional .net framework environment
- `windows nanoserver <https://hub.docker.com/_/microsoft-windows-nanoserver>`_ contains .net core running environment
- `windows <https://hub.docker.com/_/microsoft-windows>`_ provides a complete windows server api and is being replaced by windows server
- `windows server <https://hub.docker.com/_/microsoft-windows-server/>`_ provides complete windows server api
