Security related configuration
=================================

Function and class restrictions
---------------------------------
The functions and classes that PHP can call can be restricted through ``disable_functions`` / ``disable_classes``.

Directory access restrictions
---------------------------------
Directories accessible to PHP can be restricted through ``open_basedir``.

Remote reference restrictions
---------------------------------
Remote file inclusion can be restricted through ``all_url_include``, which is turned off by default.
Remote file opening can be restricted through ``allow_url_fopen``, which is enabled by default.

Session
---------------------------------

Session.Save
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
PHP's Session default handler is a file, which is stored in ``session.save_path`` of php.ini. If you have any permission to read and write files, you can modify or read the session. The session location can be obtained from phpinfo.

Session.Upload
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
PHP turns on ``session.upload_progress.enabled`` by default. This option will cause the upload progress file to be generated, and its storage path can be obtained in phpinfo.

Then you can construct a special message and send it to the server, which can be used if LFI is available.
