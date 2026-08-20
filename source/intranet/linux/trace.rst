trace cleaning
========================================

historical command
----------------------------------------
- ``unset HISTORY HISTFILE HISTSAVE HISTZONE HISTORY HISTLOG; export HISTFILE=/dev/null;``
- ``kill -9 $$`` kill history
- ``history -c``
- Set ``HISTSIZE=0`` in ``HISTSIZE=0``

Clear/modify log files
----------------------------------------
- ``/var/log/btmp``
- ``/var/log/lastlog``
- ``/var/log/wtmp``
- ``/var/log/utmp``
- ``/var/log/secure``
- ``/var/log/message``

Login traces
----------------------------------------
- Delete records in ``~/.ssh/known_hosts``
- Modify file timestamp
    - ``touch –r``
- Delete temporary files in tmp directory

Operation traces
----------------------------------------
- vim does not record historical commands ``:set history=0``
- ssh login traces
    - Incognito login ``ssh -T user@host /bin/bash -i``

overwrite file
----------------------------------------
- shred
- dd
- wipe

difficulty
----------------------------------------
- It is difficult to completely remove traces of attacks and intrusions, and the lack of logging is also a characteristic
- Even if local logs are deleted, there are still records in network devices, security devices, and centralized log systems
- The retained backdoor contains the attacker’s information
- The proxy or springboard used may be reverse invaded

Notice
----------------------------------------
- Check if there is a user online before operating
- Delete files using disk overwrite function
- Try to remain as consistent as you were before the attack

Reference link
----------------------------------------
- `Linux intrusion trace cleaning techniques <https://mp.weixin.qq.com/s/i2WvFmF1qQjbx-BaStXb1Q>`_
