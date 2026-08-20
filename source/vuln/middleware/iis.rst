IIS
========================================

IIS 6.0
----------------------------------------
- Suffix analysis ``/xx.asp;.jpg``
    - The server does not parse the ``;`` number and the content after it by default, which is equivalent to truncation.
- Directory analysis ``/xx.asp/xx.jpg`` (any analysis under the xx.asp directory)
- Default parsing ``xx.asa`` ``xx.cer`` ``xx.cdx``
- PROPFIND stack overflow vulnerability
- RCE CVE-2017-7269

IIS 7.0-7.5 / Nginx <= 0.8.37
----------------------------------------
When Fast-CGI is turned on, add ``/xx.php`` after the file path, that is, ``xx.jpg/xx.php`` will be parsed as a php file.

PUT vulnerability
----------------------------------------
- Enable WebDAV
- Have a guest user, and the guest user has upload permissions
- Any file can be uploaded

Windows features
----------------------------------------
Windows does not allow spaces, dots, and some special characters as endings. Creating such a file will automatically rename it, so you can use ``xx.php[space]``, ``xx.php.``, ``xx.php/``, ``xx.php::$DATA`` to upload script files.

File name guessing
----------------------------------------
When supporting the NTFS 8.3 file format, short file names can be used to guess directory files. The characteristics of short file names are as follows:

- The file name is the first 6 characters of the original file name plus ``~1``. The number part is incremented. If there is a file with the same prefix, the following number is incremented.
- The suffix name must not exceed 3 characters, and the excess part will be truncated.
- All lowercase letters are converted to uppercase letters
- A short file name will be generated only when the file name suffix length is greater than or equal to 4 or the total length is greater than or equal to 9. If it contains spaces or other special characters, the length condition will be ignored.

Versions before IIS 8.0 support six HTTP methods for short file name guessing: DEBUG, OPTIONS, GET, POST, HEAD, and TRACE, which require ASP.NET to be installed. Versions after IIS 8.0 can only guess successfully through the OPTIONS and TRACE methods, but there are no restrictions on ASP.NET.

The limitations of this approach are:

- If the first 6 characters of the folder name are dotted with ".", the scanner will think it is a file instead of a folder, resulting in false positives.
- Does not support Chinese file names

This method can be fixed by turning off support for the NTFS 8.3 file format with the command ``fsutil behavior set disable8dot3 1``.

Reference link
----------------------------------------
- `Use Windows features to efficiently guess directories <https://xz.aliyun.com/t/2318>`_
- `Uploading web.config for Fun and Profit 2 <https://soroush.secproject.com/blog/2019/08/uploading-web-config-for-fun-and-profit-2/>`_
