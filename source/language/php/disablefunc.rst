Disable Functions
================================

机制实现
---------------------------------
PHP中Disable Function的实现是在php-src/Zend/Zend-API.c中。PHP在启动时，读取配置文件中禁止的函数，逐一根据禁止的函数名调用 ``zend_disable_function`` 来实现禁止的效果。

这个函数根据函数名在内置函数列表中找到对应的位置并修改掉，当前版本的代码如下：

.. code-block:: cpp

    ZEND_API int zend_disable_function(char *function_name, size_t function_name_length) /* {{{ */
    {
        zend_internal_function *func;
        if ((func = zend_hash_str_find_ptr(CG(function_table), function_name, function_name_length))) {
            zend_free_internal_arg_info(func);
            func->fn_flags &= ~(ZEND_ACC_VARIADIC | ZEND_ACC_HAS_TYPE_HINTS | ZEND_ACC_HAS_RETURN_TYPE);
            func->num_args = 0;
            func->arg_info = NULL;
            func->handler = ZEND_FN(display_disabled_function);
            return SUCCESS;
        }
        return FAILURE;
    }

和函数的实现方式类似，disable classes也是这样实现的

.. code-block:: cpp

    ZEND_API int zend_disable_class(char *class_name, size_t class_name_length) /* {{{ */
    {
        zend_class_entry *disabled_class;
        zend_string *key;

        key = zend_string_alloc(class_name_length, 0);
        zend_str_tolower_copy(ZSTR_VAL(key), class_name, class_name_length);
        disabled_class = zend_hash_find_ptr(CG(class_table), key);
        zend_string_release_ex(key, 0);
        if (!disabled_class) {
            return FAILURE;
        }
        INIT_CLASS_ENTRY_INIT_METHODS((*disabled_class), disabled_class_new);
        disabled_class->create_object = display_disabled_class;
        zend_hash_clean(&disabled_class->function_table);
        return SUCCESS;
    }

因为这个实现机制的原因，在PHP启动后通过 ``ini_set`` 来修改 ``disable_functions`` 或 ``disable_classes`` 是无效的。

Bypass
---------------------------------
- LD_PRELOAD绕过
    - https://github.com/yangyangwithgnu/bypass_disablefunc_via_LD_PRELOAD
    - ``mail()`` + ``putenv``
- PHP OPcache
- Mail函数
- imap_open
    - https://www.cvedetails.com/cve/cve-2018-19518
