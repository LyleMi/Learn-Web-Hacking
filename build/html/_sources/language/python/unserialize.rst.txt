Deserialization
========================================

pickle demo
----------------------------------------
Python Pickle will call ``__reduce__`` when deserialized, and the attack can be implemented using the custom ``__reduce__` function.

.. code-block:: python

import pickle
import pickletools
import subprocess

class A(object):
a = 1
b = 2
def __reduce__(self):
return (subprocess.Popen, (('cmd.exe',),))

data = pickle.dumps(A())
pickletools.dis(data)

For this kind of attack, the scope can be defined by overloading find_class, `reference <https://docs.python.org/3/library/pickle.html#restricting-globals>`_

.. code-block:: python

import builtins
import io
import pickle

safe_builtins = {
'range',
'complex',
'set',
'frozenset',
'slice',
}

class RestrictedUnpickler(pickle.Unpickler):

def find_class(self, module, name):
# Only allow safe classes from builtins.
if module == "builtins" and name in safe_builtins:
return getattr(builtins, name)
# Forbid everything else.
raise pickle.UnpicklingError("global '%s.%s' is forbidden" %
(module, name))

def restricted_loads(s):
"""Helper function analogous to pickle.loads()."""
return RestrictedUnpickler(io.BytesIO(s)).load()

Other serialization libraries
----------------------------------------
- PyYAML
- Marshal
- shelve
