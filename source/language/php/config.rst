Security-related configuration
=================================

Function and class restrictions
---------------------------------
You can restrict functions and classes that PHP can call by ``disable_functions`` / ``disable_classes`.

Directory access restrictions
---------------------------------
Directories that are accessible to PHP can be restricted through ``open_basedir``.

Remote reference restrictions
---------------------------------
Remote file inclusion can be restricted by ``all_url_include``, and is closed by default.
Remote files can be opened through ``allow_url_fopen``, which is enabled by default.

Session
---------------------------------

Session.Save
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The default handler of PHP's Session is a file, stored in ``session.save_path`` of php.ini. If you have any permission to read and write files, you can modify or read the session. The session position can be obtained from phpinfo.

Session.Upload
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
PHP has enabled ``session.upload_progress.enabled`` by default. This option will cause the upload progress file to be generated, and its storage path can be obtained in phpinfo.

Then special messages can be constructed to send to the server, and can be used in the case of LFI.
