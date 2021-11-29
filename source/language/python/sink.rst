Sink
================================

命令执行
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

文件读取
--------------------------------
- open
- os.open
- urllib.request.urlopen('file:///')
- codecs.open
- fileinput
- 仅Python2
    - types.FileType

危险第三方库
--------------------------------
- Template
- subprocess32 

反序列化
--------------------------------
- marshal
- PyYAML
- pickle
- cPickle
- shelve
- PIL
