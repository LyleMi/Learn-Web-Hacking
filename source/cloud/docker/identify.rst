Docker environment identification
----------------------------------------

In Docker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The MAC address is ``02:42:ac:11:00:00`` - ``02:42:ac:11:ff:ff``
- ``ps aux`` Most of the running programs have very small pids
- ``cat /proc/1/cgroup`` docker process
- There is ``.dockerenv`` in the docker environment
- Some containers lack many commonly used commands such as ``ping``, etc.

Outside Docker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``/var/run/docker.sock`` file exists
- ``2375`` / ``2376`` port is opened

Information collection in container
----------------------------------------
- User information (current user, user list)
- Operating system and kernel versions
- Running process information (process name, permissions, etc.)
- Is the container a privileged container?
- Environment variables
- Determine the container mount information and try to mount Docker Socket
- Network environment, judge the network segment that can be reached
- In a cloud environment, try to obtain metadata information
