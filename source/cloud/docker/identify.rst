Docker environment identification
----------------------------------------

Within Docker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- The MAC address is ``02:42:ac:11:00:00`` - ``02:42:ac:11:ff:ff``
- ``ps aux`` The pid of most running programs is very small
- ``cat /proc/1/cgroup`` docker process
- ``.dockerenv`` exists in the docker environment
- Some containers are missing many commonly used commands such as ``ping``, etc.

Outside Docker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``/var/run/docker.sock`` file exists
- ``2375`` / ``2376`` port open

Collection of information within the container
----------------------------------------
- User information (current user, user list)
- Operating system and kernel version
- Running process information (process name, permissions, etc.)
- Whether the container is a privileged container
- environment variables
- Determine the container mounting information and try to mount Docker Socket
- Network environment, determine the reachable network segments
- In a cloud environment, try to obtain metadata information
