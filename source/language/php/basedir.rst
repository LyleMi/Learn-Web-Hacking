Open Basedir
================================

Mechanism implementation
---------------------------------
The implementation of Disable Function in PHP is in php-src/main/fopen-wrappers.c. The implementation method is to call the function to check whether it is within the basedir based on the path when calling files and other related operations. Part of the implementation code is as follows:

.. code:: c

    PHPAPI int php_check_open_basedir_ex(const char *path, int warn)
    {
        /* Only check when open_basedir is available */
        if (PG(open_basedir) && *PG(open_basedir)) {
            char *pathbuf;
            char *ptr;
            char *end;

            /* Check if the path is too long so we can give a more useful error
            * message. */
            if (strlen(path) > (MAXPATHLEN - 1)) {
                php_error_docref(NULL, E_WARNING, "File name is longer than the maximum allowed path length on this platform (%d): %s", MAXPATHLEN, path);
                errno = EINVAL;
                return -1;
            }

            pathbuf = estrdup(PG(open_basedir));

            ptr = pathbuf;

            while (ptr && *ptr) {
                end = strchr(ptr, DEFAULT_DIR_SEPARATOR);
                if (end != NULL) {
                    *end = '\0';
                    end++;
                }

                if (php_check_specific_open_basedir(ptr, path) == 0) {
                    efree(pathbuf);
                    return 0;
                }

                ptr = end;
            }
            if (warn) {
                php_error_docref(NULL, E_WARNING, "open_basedir restriction in effect. File(%s) is not within the allowed path(s): (%s)", path, PG(open_basedir));
            }
            efree(pathbuf);
            errno = EPERM; /* we deny permission to open it */
            return -1;
        }

        /* Nothing to check... */
        return 0;
    }
