Disable Functions
================================

Mechanism implementation
---------------------------------
The implementation of Disable Function in PHP is in php-src/Zend/Zend-API.c. When PHP starts, it reads the prohibited functions in the configuration file and calls ``zend_disable_function`` one by one according to the prohibited function name to achieve the prohibited effect.

This function finds the corresponding position in the built-in function list based on the function name and modifys it. The code of the current version is as follows:

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

Similar to the implementation method of functions, disable classes are also implemented in this way.

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

Because of this implementation mechanism, modifying ``disable_functions`` or ``disable_classes`` after PHP is started is invalid.

Bypass
---------------------------------
- LD_PRELOAD Bypass
- https://github.com/yangyangwithgnu/bypass_disablefunc_via_LD_PRELOAD
- ``mail()`` + ``putenv``
- PHP OPCACHE
- Mail function
- imap_open
- https://www.cvedetails.com/cve/cve-2018-19518
