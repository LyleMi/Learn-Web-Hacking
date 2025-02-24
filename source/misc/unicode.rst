Unicode
========================================

Basic concepts
----------------------------------------

BMP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
BMP (Basic Multilingual Plane), translated as a basic multilingual plane, is an encoded block in Unicode.

Code plane
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Unicode encoding points are divided into 17 planes, each plane contains 2^16 (i.e. 65536) code bits. The code bits of the 17 planes can be represented from U+xx0000 to U+xxFFFF, where xx represents the hexadecimal value from 0016 to 1016, with a total of 17 planes.

Code Point
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Code Point is also called Code Position, which is translated as code bits or encoded positions, and refers to the numerical value that makes up the code space.

Code Unit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Refers to the minimum number of bytes required to encode a Code Point in a certain Unicode encoding method. For example, UTF-8 requires at least one byte, UTF-16 requires at least two bytes, UCS-2 requires at least two bytes, UCS-4 and UTF -32 Four bytes.

Surrogate Pair
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Surrogate Pair is used for UTF-16 to be backward compatible with UCS-2. The method is to take the code bits of 0xD800~0xDBFF (called high surrogates) and 0xDC00~0xDFF (called low surrogates) in the UCS-2 range. A high surrogate followed by a low surrogate is spelled into four bytes to represent characters exceeding BMP. Both surrogate ranges are 1024 code bits, so surrogate pair can express 1024 x 1024 = 1048576 = 0x100000 characters.

Combining Character
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For example, ``He̊llö`` contains characters such as accents, and combining them will use a large number of code points. Therefore, this kind of character is achieved by combining it.

BOM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Byte-order mark (BOM) is a unified code character with special meaning, with a code point of ``U+FEFF``. When encoding a string composed of UCS characters with UTF-16 or UTF-32, this character is used to indicate its byte order. Often used to distinguish whether it is UTF encoding.

Coding method
----------------------------------------

UCS-2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
UCS-2 (2-byte Universal Character Set) is a fixed-length encoding method. UCS-2 simply uses a 16-bit symbol to represent the code bits, which means that the code range is between 0 and 0xFFFF. Inside.

UTF-8
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
UTF-8 (8-bit Unicode Transformation Format) is a variable-length character encoding for Unicode and is also a prefix code. It can encode all valid encoding points in the Unicode character set in one to four bytes and is part of the Unicode standard. The encoding method is as follows

+------------+-----------+------------+----------+----------+----------+----------+----------+----------+----------+
| Number of digits of code points | Starting value of code points | End value of code points | Byte sequence | Byte 1 | Byte 2 | Byte 3 | Byte 4 | Byte 5 | Byte 6 |
+============+===========+============+==========+==========+==========+==========+==========+==========+==========+
| 7          | U+0000    | U+007F     | 1        | 0xxxxxxx |          |          |          |          |          |
+------------+-----------+------------+----------+----------+----------+----------+----------+----------+----------+
| 11         | U+0080    | U+07FF     | 2        | 110xxxxx | 10xxxxxx |          |          |          |          |
+------------+-----------+------------+----------+----------+----------+----------+----------+----------+----------+
| 16         | U+0800    | U+FFFF     | 3        | 1110xxxx | 10xxxxxx | 10xxxxxx |          |          |          |
+------------+-----------+------------+----------+----------+----------+----------+----------+----------+----------+
| 21         | U+10000   | U+1FFFFF   | 4        | 11110xxx | 10xxxxxx | 10xxxxxx | 10xxxxxx |          |          |
+------------+-----------+------------+----------+----------+----------+----------+----------+----------+----------+
| 26         | U+200000  | U+3FFFFFF  | 5        | 111110xx | 10xxxxxx | 10xxxxxx | 10xxxxxx | 10xxxxxx |          |
+------------+-----------+------------+----------+----------+----------+----------+----------+----------+----------+
| 31         | U+4000000 | U+7FFFFFFF | 6        | 1111110x | 10xxxxxx | 10xxxxxx | 10xxxxxx | 10xxxxxx | 10xxxxxx |
+------------+-----------+------------+----------+----------+----------+----------+----------+----------+----------+

UTF-16
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
UTF-16 (16-bit Unicode Transformation Format) is an extension of UCS-2. It uses one or two 16-bit symbols to represent code bits, and code bits from 0 to 0x10FFFF can be encoded.

Equivalence issues
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Unicode contains many special characters. In order to make many existing standards compatible, Unicode equivalence is proposed. Among characters, some are functionally equivalent to other characters or sequences of characters. Therefore, Unicode defines some sequences of code bits as equal.

Unicode provides two equivalent concepts: standard equivalent and compatible equivalent. The former is a subset of the latter. For example, the character n followed by the combination of the character `~` will (standard and compatible) be equivalent to the Unicode character N. The combined character ﬀ is only compatible with two f characters.

Unicode regularization is a form of text regularization, which refers to converting sequences of equivalents to the same sequence. This sequence is called the regular form in the Unicode standard.

For each equivalent concept, Unicode defines two forms, one is completely synthesized and the other is completely decomposed. Therefore, there will be four forms at the end, and their abbreviations are: NFC, NFD, NFKC, and NFKD. For Unicode word processing programs, regularization is very important. Because it affects the meaning of comparison, search and sorting.

Standard equivalent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The basic concept of standard equivalent in unified code is the interactive use of characters composition and decomposition. Synthesis refers to the process of complying simple characters into fewer pregroup characters, such as character n and combination characters `~` can form a unified code n. Decomposition is a reverse process, that is, converting pregroup characters back to components.

Standard equivalence means maintaining visual and functional equivalence. For example, letters containing additional symbols are considered and decomposed letters and their additional symbols are standard equivalents. In other words, the pregroup character ‘ü’ and the sequence composed of ‘u’ and ‘¨’ are standard equivalents. Similarly, the Uniform Code integrates some Greek additional symbols and punctuation marks that look similar to the additional symbols.

Compatible equivalent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The range of compatible equivalents is wider than that of standard equivalents. If the sequence is standard equivalent, it will be compatible equivalent, otherwise it may not be correct. Compatibility equivalence focuses more on the equivalence of pure text and attributes some semantic different forms together.

For example, the superscript number and the number it uses are compatible equivalents, but not standard equivalents. The reason is that although subscripts and superscript forms have different meanings at some point, it is reasonable if the application considers them the same (although visually distinguishable). In this way, in a unified code-rich file, the superscript and the subscript can appear in a relatively less cumbersome way (see next section).

The full and half-width Katakana is also a compatible equivalent but not a standard equivalent. Like a combination and its component sequence. It only has visual but no semantic differences. In other words, the author usually does not specifically claim that using the word combo means one meaning, and not using it means another. Relatively, this is limited to selection on printing.

When word processing software realizes the search and sorting of unified coded strings, it must take into account the existence of equivalence. Without this feature, users will not be able to find visually indistinguishable glyphs when searching.

Unified code provides a standard regularization algorithm that produces a unique sequence for all the same sequences. Its equivalent standard can be standard (NF) or compatible (NFK). Since elements in the equivalent class can be selected arbitrarily, it is also possible to have multiple standard forms for each equivalent standard. The unified code provides two formal forms for each equivalent standard: NFC and NFKC for synthesis and NFD and NFKD for decomposition. Whether combined or decomposed forms, standard order will be used, so as to limit the regular form to only have unique forms.

normalization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To compare or search for unified code strings, the software can use one of them in synthesis or decomposition. As long as the strings that are compared or searched are used in the same form, it doesn't matter which choice. On the other hand, the choice of the concept of equivalents will affect the search results. For example, some combined characters such as ﬃ (U+FB03), Roman numerals such as Ⅸ (U+2168), and even superscript numerals such as ⁵ (U+2075) have their own individual unified code points. Standard formal forms do not affect these results. But compatible formal forms will be decomposed into f, f, i. So when searching for U+0066(f), it will succeed in NFKC, but it will fail in NFC. Similarly, search for the Latin letter I (U+0049) in the pre-group of Roman numerals IX. Similarly, "⁵" will turn into "5".

For browsers, converting the superscript to a base underscore is not necessarily good, because the information on the superscript will disappear. To allow for this difference, the unified code character database sentence contains compatible format tags, which provide details of compatible conversions. In the case of combinatorial characters, this tag is just ``<compat>``, and in the case of superscript it is ``<super>``. Rich file formats such as hypertext labeling languages will use compatible tags. For example, HTML uses custom tags to place "5" in the superscript position.

Formal form
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- NFD Normalization Form Canonical Decomposition Decomposition in standard equivalent
- NFC Normalization Form Canonical Composition is broken down in a standard equivalent manner and then reorganized in a standard equivalent. If it is a singleton, the restructuring result may be different from before decomposition.
- NFKD Normalization Form Compatibility Decomposition Decomposition NFKC in a compatible equivalent way
- Normalization Form Compatibility Composition is broken down in a compatible equivalent manner and then reorganizes it in a standard equivalent manner.

Tricks
----------------------------------------
- The length of some languages is not the length of the character, a UTF-16 may be two digits.
- Some languages will handle errors when flipping UTF-16 and other multi-byte encodings.

Security Question
----------------------------------------

Visual Spoofing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For example, bаidu.com (a here is \u0430) and baidu.com (a here is \x61) are visually the same, but actually point to two different domain names.

baidu.com (a here is \uff41) and baidu.com (a here is \x61), but point to two identical domain names.

This phenomenon can cause some problems with Spoofing or WAF Bypass.

Best Fit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the two characters have different encodings before and after encoding, and the previous encoding does not correspond to the subsequent encoding, the program will try to find the best character for automatic conversion.

When a wide character becomes a single-byte character, the character encoding will change to a certain extent.

This phenomenon may cause some WAF Bypass.

Syntax Spoofing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The following four Urls seem to be a good domain name syntactically, but the characters used for segmentation are not really split characters, but U+2044( ⁄ ), which can lead to some UI spoofing problems.

- http://macchiato.com/x.bad.com  macchiato.com/x     bad.com
- http://macchiato.com?x.bad.com  macchiato.com?x     bad.com
- http://macchiato.com.x.bad.com Macchiato.com.x Bad.com
- http://macchiato.com#x.bad.com  macchiato.com#x     bad.com

Punycode Spoofs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- http://�定定定定.com http://xn--google.com
- http://䁾.com              http://xn--cnn.com
- http://田少田少田.com http://xn--citibank.com

Some browsers will directly display puncode, but this mechanism can also be used to implement UI Spooof.

Buffer Overflows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
During encoding conversion, some characters will become multiple characters, such as Fluß → FLUSS → fluss, which may lead to BOF.

Common loads
----------------------------------------

URL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``‥`` (U+2025)
- ``︰`` (U+FE30)
- ``。`` (U+3002)
- `⓪ ⓪``` (U + 24EA)
- ``／`` (U+FF0F)
- ``ｐ`` (U+FF50)
- ``ʰ`` (U+02B0)
- `` ª``` (the + 00aa)

SQL Injection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``＇`` (U+FF07)
- ``＂`` (U+FF02)
- ``﹣`` (U+FE63)

XSS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `` ＜ `` (u+ff1c)
- ``＂`` (U+FF02)

Command Injection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``＆`` (U+FF06)
- `` ｜ `` (U+FF5C)

Template injection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `﹛` `(U+Fe5b)
- ``［`` (U+FF3B)

Reference link
----------------------------------------

Official Documentation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `Unicode equivalence <https://en.wikipedia.org/wiki/Unicode_equivalence>`_
- `Unicode Normalization Forms <http://unicode.org/reports/tr15/>`_
- `Unicode Security Considerations <http://unicode.org/reports/tr36/>`_

RFC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `RFC 3629 <https://tools.ietf.org/html/rfc3629>`_ UTF-8, a transformation format of ISO 10646
- `RFC 2044 <https://tools.ietf.org/html/rfc2044>`_ UTF-8, a transformation format of ISO 10646
- `RFC 2279 <https://tools.ietf.org/html/rfc2279>`_ UTF-8, a transformation format of ISO 10646

Tricks / Blogs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- `IDN homograph attack <https://en.wikipedia.org/wiki/IDN_homograph_attack>`_
- `Black Hat Unicode Security <https://www.blackhat.com/presentations/bh-usa-09/WEBER/BHUSA09-Weber-UnicodeSecurityPreview-PAPER.pdf>`_
- `Request encoding to bypass web application firewalls <https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2017/august/request-encoding-to-bypass-web-application-firewalls/>`_
- `domain hacks with unusual unicode characters <https://shkspr.mobi/blog/2018/11/domain-hacks-with-unusual-unicode-characters/>`_
- `You don't actually understand Unicode <https://zhuanlan.zhihu.com/p/53714077>`_
