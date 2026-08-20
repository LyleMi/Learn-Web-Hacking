Unicode
========================================

Basic concepts
----------------------------------------

BMP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
BMP (Basic Multilingual Plane), translated as Basic Multilingual Plane, is a coding block in Unicode.

code plane
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Unicode code points are divided into 17 planes, each plane contains 2^16 (ie 65536) code points. The code bits of the 17 planes can be expressed as from U+xx0000 to U+xxFFFF, where xx represents the hexadecimal value from 0016 to 1016, a total of 17 planes.

Code Point
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Code Point is also called Code Position, translated as code point or coding position, which refers to the numerical value that makes up the code space.

Code Unit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Refers to the minimum number of bytes required to encode a Code Point in a certain Unicode encoding method. For example, UTF-8 requires at least one byte, UTF-16 requires at least two bytes, UCS-2 requires two bytes, and UCS-4 and UTF-32 require four bytes.

Surrogate Pair
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Surrogate Pair is used for UTF-16 to be backward compatible with UCS-2. The method is to take the code points of 0xD800~0xDBFF (called high surrogates) and 0xDC00~0xDFFF (called low surrogates) in the UCS-2 range. A high surrogate is followed by a low surrogate to form four bytes to represent characters beyond BMP. Both surrogate ranges are 1024 code points, so the surrogate pair can express 1024 x 1024 = 1048576 = 0x100000 characters.

Combining Character
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For example, ``He̊llö`` contains characters such as accents, which would use a large number of code points to combine. Therefore, this kind of characters are often implemented in a combination of ways.

BOM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The byte-order mark (BOM) is a Unicode character with special meaning, and the code point is ``U+FEFF``. This character is used to indicate the byte order when encoding a string of UCS characters in UTF-16 or UTF-32. Often used to distinguish whether it is UTF encoded.

encoding method
----------------------------------------

UCS-2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
UCS-2 (2-byte Universal Character Set) is a fixed-length encoding method. UCS-2 simply uses a 16-bit code element to represent the code point, which means that the encoding range is in the code point range from 0 to 0xFFFF.

UTF-8
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
UTF-8 (8-bit Unicode Transformation Format) is a variable-length character encoding for Unicode and a prefix code. It can encode all valid code points in the Unicode character set with one to four bytes and is part of the Unicode standard. The encoding method is as follows

+------------+-----------+------------+----------+----------+----------+----------+----------+----------+----------+
| Number of digits in the code point | Starting value of the code point | Ending value of the code point | Byte sequence | Byte 1 | Byte 2 | Byte 3 | Byte 4 | Byte 5 | Byte 6 |
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
UTF-16 (16-bit Unicode Transformation Format) is an extension of UCS-2. It uses one or two 16-bit code elements to represent code points, and can encode code points from 0 to 0x10FFFF.

equivalence problem
----------------------------------------

Introduction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Unicode (Unicode) contains many special characters. In order to make many existing standards compatible, Unicode equivalence (Unicode equivalence) was proposed. Among characters, some are functionally equivalent to other characters or sequences of characters. Therefore, Unicode defines some code point sequences as equal.

Unicode provides two concepts of equivalence: standard equivalence and compatible equivalence. The former is a subset of the latter. For example, the character n followed by the combining character `~` is (standards and compatible) equivalent to the Unicode character ñ. The ligature ff is only compatible with two f characters.

Unicode normalization is a form of text normalization, which refers to converting sequences that are equivalent to each other into the same column sequence. This sequence is called the canonical form in the Unicode standard.

For each equivalent concept, Unicode defines two forms, one is completely synthetic and the other is completely decomposed. Therefore, in the end there will be four forms, whose abbreviations are: NFC, NFD, NFKC, NFKD. For Unicode word processing programs, normalization is very important. Because it affects the meaning of comparison, search, and sorting.

standard equivalent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The basic concept of standard equivalence in Unicode is the interactive use of character composition and decomposition. Composition refers to the process of combining simple characters into fewer pre-combined characters, such as the character n and the combining character `~` to form Unicode ñ. Decomposition is the reverse process, converting preassembled characters back into components.

Standard equivalence means maintaining visual and functional equivalence. For example, letters with diacritics are considered standard equivalents to the decomposed letters and their diacritics. In other words, the precomposed character 'ü' is canonically equivalent to the sequence consisting of 'u' and '¨'. Similarly, Unicode incorporates some Greek diacritics and punctuation marks that look similar to the diacritics.

Compatible equivalent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The scope of compatible equivalence is wider than that of standard equivalence. If the sequences are standard equivalents, they will be compatible equivalents, but not vice versa. Compatible equivalence focuses more on pure literal equivalence and brings together some semantically different forms.

For example, superscript numbers are compatible but not standard equivalents to the numbers they are used in. The reason is that although subscript and superscript forms have different meanings at some times, it is reasonable for applications to treat them as the same (although visually distinguishable). In this way, superscripts and subscripts can appear in a less cumbersome manner in Unicode-rich files (see next section).

Full-width and half-width katakana are also compatible equivalences but not standard equivalences. Like ligatures and their component sequences. There is only a visual but no semantic difference. In other words, the author usually does not specifically claim that using a ligature means one thing and not using it means another. In contrast, this is limited to printing choices.

Word processing software must take into account the existence of equivalence when implementing the search and sorting of Unicode strings. Without this feature, users would not be able to find visually indistinguishable glyphs when searching.

Unicode provides a standard normalization algorithm that produces a unique sequence from all identical sequences. Its equivalent standard can be standard (NF) or compatible (NFK). Since the elements of an equivalence class can be chosen arbitrarily, it is possible to have multiple standard forms for each equivalence criterion. Unicode provides two formal forms for each equivalence criterion: NFC and NFKC for synthesis and NFD and NFKD for decomposition. Regardless of whether it is a combined or decomposed form, the standard order will be used to limit the regular form to only a unique form.

normalization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To compare or search Unicode strings, software can use one of the composite or decomposed forms. It doesn't matter which option you choose as long as the strings being compared or searched use the same form. On the other hand, the choice of equivalent concepts will affect the search results. For example, some ligatures such as ﬃ (U+FB03), Roman numerals such as Ⅸ (U+2168), and even superscript numbers such as ⁵ (U+2075) have their own Unicode code points. The standard formal form does not affect these results. But the compatible normal form will decompose ﬃ into f, f, i. So when searching for U+0066(f), it will succeed in NFKC, but it will fail in NFC. Likewise there is a search for the Latin letter I (U+0049) in the pre-assembled Roman numeral IX. Similarly, "⁵" will turn into "5".

For browsers, it is not necessarily a good idea to convert superscripts to base underscores because the superscript information will be lost. To allow for this difference, Unicode character database statements contain compatible format tags, which provide details of compatible conversions. In the case of ligatures, this tag is simply ``<compat>``, and in the case of superscripts it is ``<super>``. Rich file formats such as Hypertext Markup Language use compatible tags. For example, HTML uses a custom tag to put "5" in a superscript position.

formal form
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- NFD Normalization Form Canonical Decomposition is decomposed in a standard equivalent way
- NFC Normalization Form Canonical Composition decomposes it in a standard equivalent way, and then reassembles it in a standard equivalent way. If it is a singleton, the reorganization result may be different from before decomposition.
- NFKD Normalization Form Compatibility Decomposition decomposes NFKC in a compatible and equivalent manner
- Normalization Form Compatibility Composition decomposes it in a compatible and equivalent way, and then reorganizes it in a standard equivalent way.

Tricks
----------------------------------------
- The length of some languages ​​is not the length of characters. A UTF-16 may be two bits.
- Some languages ​​will handle errors when flipping multi-byte encodings such as UTF-16.

Security Question
----------------------------------------

Visual Spoofing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
For example, bаidu.com (where a is \u0430) and baidu.com (where a is \x61) are visually identical, but actually point to two different domain names.

There are some differences between baidu.com (a here is \uff41) and baidu.com (a here is \x61), but they point to the same two domain names.

This phenomenon can cause some Spoofing or WAF Bypass problems.

Best Fit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If two characters have different encodings before and after, and the previous encoding does not correspond to the subsequent encoding, the program will try to find the best character for automatic conversion.

When wide characters become single-byte characters, the character encoding will change.

This phenomenon may cause some WAF Bypass.

Syntax Spoofing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The following four URLs appear to be grammatically correct domain names, but the characters used for separation are not real separation characters, but U+2044 ( ⁄ ), which can cause some UI deception problems.

- http://macchiato.com/x.bad.com  macchiato.com/x     bad.com  
- http://macchiato.com?x.bad.com  macchiato.com?x     bad.com  
- http://macchiato.com.x.bad.com  macchiato.com.x     bad.com  
- http://macchiato.com#x.bad.com  macchiato.com#x     bad.com  

Punycode Spoofs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- http://䕮䕵䕶䱱.com http://xn--google.com
- http://䁾.com http://xn--cnn.com
- http://卍岲岲岅岉厎.com http://xn--citibank.com

Some browsers will display puncode directly, but you can also use this mechanism to implement UI Spooof.

Buffer Overflows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
During encoding conversion, some characters will become multiple characters, such as Fluß → FLUSS → fluss, which may cause BOF.

Common loads
----------------------------------------

URL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``‥`` (U+2025)
- ``︰`` (U+FE30)
- ``。`` (U+3002)
- ``⓪``  (U+24EA)
- ``／`` (U+FF0F)
- ``ｐ`` (U+FF50)
- ``ʰ`` (U+02B0)
- ``ª`` (U+00AA)

SQL injection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``＇`` (U+FF07)
- ``＂`` (U+FF02)
- ``﹣`` (U+FE63)

XSS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``＜`` (U+FF1C)
- ``＂`` (U+FF02)

command injection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``＆`` (U+FF06)
- ``｜`` (U+FF5C)

template injection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``﹛`` (U+FE5B)
- ``［`` (U+FF3B)

Reference link
----------------------------------------

Official documentation
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
- `Actually you don’t understand Unicode <https://zhuanlan.zhihu.com/p/53714077>`_
