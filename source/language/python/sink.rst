Sink
================================

command execution
--------------------------------
- asyncio.new_event_loop().subprocess_exec
- asyncio.subprocess
- bdb.os
- cgi.os.system
- cgi.sys
- code.InteractiveInterpreter
- commands
- ctypes.CDLL
- eval
- exec
- execfile
- input // python2 only
- os.exec
- os.exec*
- os.fork
- os.popen
- os.spawn
- os.system
- platform.os
- platform.popen
- platform.sys
- popen2
- pty.os
- pty.spawn
- subprocess
- timeit.sys
- timeit.timeit
- typing.get_type_hints() + ``__annotations__``
- ...

file reading
--------------------------------
- open
- os.open
- urllib.request.urlopen('file:///')
- codecs.open
- fileinput
- Python2 only
    - types.FileType

Dangerous third-party libraries
--------------------------------
- Template
- subprocess32 

Deserialization
--------------------------------
- marshal
- PyYAML
- pickle
- cPickle
- shelve
- PIL
