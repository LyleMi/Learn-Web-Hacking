Trace cleaning
========================================

Historical Commands
----------------------------------------
- ``unset HISTORY HISTFILE HISTSAVE HISTZONE HISTORY HISTLOG; export HISTFILE=/dev/null;``
- ``kill -9 $$`` kill history
- ``history -c``
- Set ``HISTSIZE=0`` in ``HISTSIZE=0``

Clear/modify log files
----------------------------------------
- `/was/log/btmp```s
- ``/was/log/load log``
- ``/VAR/LOG/WTMP``
- ``/was/log/ump```s
- ``/var/log/secure``
- ``/VAR/LOG/MESSAGE`

Login traces
----------------------------------------
- Delete the records in ``~/.ssh/known_hosts``
- Modify file timestamp
- ``touch –r``
- Delete Temporary Files of the TMP Directory

Operation traces
----------------------------------------
- vim does not record historical commands ``:set history=0``
- ssh login traces
- Wuhen Login ``ssh -T user@host /bin/bash -i``

Overwrite the file
----------------------------------------
- shred
- dd
- wipe

difficulty
----------------------------------------
- It is difficult to completely delete traces when attacking and intrusion, and no logging is also a feature
- Even if the local log is deleted, there are still records in network equipment, security equipment, and centralized log systems
- The retained backdoor contains the attacker's information
- The agent or springboard used may be reverse-invaded

Notice
----------------------------------------
- Check if there are users online before operation
- Delete files using disk override function
- Try to keep the same state as before the attack

Reference link
----------------------------------------
- `Linux intrusion trace cleaning skills <https://mp.weixin.qq.com/s/i2WvFmF1qQjbx-BaStXb1Q>`_
