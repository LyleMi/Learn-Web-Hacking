Open Basedir
================================

机制实现
---------------------------------
PHP中Disable Function的实现是在php-src/main/fopen-wrappers.c中，实现方式是在调用文件等相关操作时调用函数根据路径来检查是否在basedir内，其中一部分实现代码如下：

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
