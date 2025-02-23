IIS
========================================

IIS 6.0
----------------------------------------
- Suffix parsing ``/xx.asp;.jpg``
- The server does not parse the ``;`` number and its subsequent contents by default, which is equivalent to truncation.
- Directory analysis ``/xx.asp/xx.jpg`` (Arbitrary analysis under the xx.asp directory)
- Default parsing ``xx.asa````xx.cer````xx.cdx``
- PROPFIND Stack Overflow Vulnerability
- RCE CVE-2017-7269

IIS 7.0-7.5 / Nginx <= 0.8.37
----------------------------------------
When Fast-CGI is enabled, adding ``/xx.php`` to the file path, that is, ``xx.jpg/xx.php`` will be parsed into a php file.

PUT vulnerability
----------------------------------------
- Turn on WebDAV
- Have a guest user, and the guest user has upload permissions
- Can upload any file

Windows characteristics
----------------------------------------
Windows does not allow spaces and dots and some special characters as the ending. Creating such a file will automatically be renamed, so you can use ``xx.php[space]`, ``xx.php.``, ``xx.php.`, ``xx.php /``, ``xx.php::$DATA`` Upload script file.

File name guess
----------------------------------------
When supporting the NTFS 8.3 file format, you can use the short file name to guess the directory file. The short file name features are as follows:

- The file name is the first 6 characters of the original file name plus ``~1``, where the number part is incremented. If a file with the same prefix exists, the following number is incremented.
- The suffix name does not exceed 3 digits, and the excess part will be truncated
- All lowercase letters are converted to uppercase letters
- Short file names will only be generated if the file name suffix length is greater than or equal to 4 or the total length is greater than or equal to 9. If spaces or other special characters are included, the length conditions will be ignored.

The HTTP methods that support short file name guessing mainly include: DEBUG, OPTIONS, GET, POST, HEAD, and TRACE, and ASP.NET is required to be installed. The version after IIS 8.0 can only be guessed successfully through OPTIONS and TRACE methods, but there is no limit to ASP.NET.

The limitations of this approach are:

- The first 6 characters of the folder name are dotted "." The scanner will consider it to be a file instead of a folder, and a false alarm will eventually occur
- Chinese file names are not supported

This method can be fixed by turning off support for NTFS 8.3 file format by ``fsutil behavior set disable8dot3 1`.

Reference link
----------------------------------------
- `Efficient guess directory using Windows features <https://xz.aliyun.com/t/2318>`_
- `Uploading web.config for Fun and Profit 2 <https://soroush.secproject.com/blog/2019/08/uploading-web-config-for-fun-and-profit-2/>`_
