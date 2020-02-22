Unicode
========================================

等价性问题
----------------------------------------

简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Unicode（统一码）包含了许多特殊字符，为了使得许多现存的标准能够兼容，提出了Unicode等价性（Unicode equivalence）。在字符中，有些在功能上会和其它字符或字符序列等价。因此，Unicode将一些码位序列定义成相等的。

Unicode提供了两种等价概念：标准等价和兼容等价。前者是后者的一个子集。例如，字符n后接着组合字符 `~` 会（标准和兼容）等价于Unicode字符ñ。而合字ﬀ则只有兼容等价于两个f字符。

Unicode正规化是文字正规化的一种形式，是指将彼此等价的序列转成同一列序。此序列在Unicode标准中称作正规形式。

对于每种等价概念，Unicode又定义两种形式，一种是完全合成的，一种是完全分解的。因此，最后会有四种形式，其缩写分别为：NFC、NFD、NFKC、NFKD。对于Unicode的文字处理程序而言，正规化是很重要的。因为它影响了比较、搜索和排序的意义。 

标准等价
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
统一码中标准等价的基础概念为字符的组成和分解的交互使用。合成指的是将简单的字符合并成较少的预组字符的过程，如字符n和组合字符 `~` 可以组成统一码ñ。分解则是反向过程，即将预组字符变回部件。

标准等价是指保持视觉上和功能上的等价。例如，含附加符号字母被视为和分解后的字母及其附加符号是标准等价。换句话说，预组字符‘ü’和由‘u’及 ‘¨’所组成的序列是标准等价。相似地，统一码统合了一些希腊附加符号和外观与附加符号类似的标点符号。

兼容等价
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
兼容等价的范围较标准等价来得广。如果序列是标准等价的话就会是兼容等价，反之则未必对。兼容等价更关注在于纯文字的等价，并把一些语义上的不同形式归结在一起。

例如，上标数字和其所使用的数字是兼容等价，但非标准等价。其理由为下标和上标形式虽然在某些时侯属于不同意义，但若应用程序将他们视为一样也是合理的（虽然视觉上可区分）。如此，在统一码富文件中，上标和下标就可以以比较不累赘地方式出现（见下一节）。

全角和半角的片假名也是一种兼容等价但不是标准等价。如同合字和其部件序列。其只有视觉上但没有语义上的区别。换句话说，作者通常没有特别宣称使用合字是一种意思，而不使用是另一种意思。相对地，这尽限于印刷上的选择。 

文字处理软件在实现统一码字符串的搜索和排序时，须考虑到等价性的存在。如果没有此特性的话，用户在搜索时将无法找到在视觉上无法区分的字形。

统一码提供了一个标准的正规化算法，可将所有相同的序列产生一个唯一的序列。 其等价准绳可以为标准的（NF）或兼容的（NFK）。 既然可以任意选择等价类中的元素，对每一个等价标准有多个标准形式也是有可能的。 统一码为每一种等价准绳分别提供两种正规形式：合成用的NFC和NFKC以及分解用的NFD和NFKD。 而不论是组合的或分解的形式，都会使用标准顺序，以此限制正规形式只有唯一形式。

正规化
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
为了比较或搜索统一码字符串，软件可以使用合成或分解形式其中之一。 只要被比较或搜索的字符串使用的形式是相同的，哪种选择都没关系。 另一方面，等价概念的选择则会影响到搜索结果。 譬如，有些合字如ﬃ（U+FB03）、罗马数字如Ⅸ（U+2168），甚至是上标数字如⁵（U+2075）有其个别统一码码位。 标准正规形式并不会影响这些结果。 但兼容正规形式会分解ﬃ成f、f、i。所以搜索U+0066（f）时，在NFKC中会成功，但在NFC则会失败。 同样地有在预组罗马数字Ⅸ 中搜索拉丁字母I（U+0049）。类似地，“⁵”会转成“5”。

对于浏览器，将上标转换成到基下划线未必是好的，因为上标的信息会因而消失。为了允许这种不同，统一码字符数据库句含了兼容格式标签，其提供了兼容转换的细节。在合字的情况下，这个标签只是 ``<compat>`` ，而在上标的情况下则为 ``<super>`` 。丰富文件格式如超文本置标语言则会使用兼容标签。例如，HTML使用自定义标签来将“5”放到上标位置。

正规形式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- NFD Normalization Form Canonical Decomposition 以标准等价方式来分解
- NFC Normalization Form Canonical Composition 以标准等价方式来分解，然后以标准等价重组之。若是singleton的话，重组结果有可能和分解前不同。
- NFKD Normalization Form Compatibility Decomposition  以兼容等价方式来分解NFKC
- Normalization Form Compatibility Composition 以兼容等价方式来分解，然后以标准等价重组之

安全问题
----------------------------------------

Visual Spoofing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
例如bаidu.com(此处的a为\u0430)和baidu.com(此处的a为\x61)视觉上相同，但是实际上指向两个不同的域名。

bａidu.com(此处的a为\uff41)和baidu.com(此处的a为\x61)有一定的不同，但是指向两个相同的域名。

这种现象可以引起一些Spoofing或者WAF Bypass的问题。

Best Fit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
如果两个字符前后编码不同，之前的编码在之后的编码没有对应，程序会尝试找最佳字符进行自动转换。

当宽字符变成了单字节字符，字符编码会有一定的变化。

这种现象可能引起一些WAF Bypass。

Syntax Spoofing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
以下四个Url在语法上看来是没问题的域名，但是用来做分割的字符并不是真正的分割字符，而是U+2044( ⁄ )，可以导致一些UI欺骗的问题。

- http://macchiato.com/x.bad.com  macchiato.com/x     bad.com  
- http://macchiato.com?x.bad.com  macchiato.com?x     bad.com  
- http://macchiato.com.x.bad.com  macchiato.com.x     bad.com  
- http://macchiato.com#x.bad.com  macchiato.com#x     bad.com  

Punycode Spoofs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- http://䕮䕵䕶䕱.com        http://xn--google.com  
- http://䁾.com              http://xn--cnn.com  
- http://岍岊岊岅岉岎.com    http://xn--citibank.com  

有些浏览器会直接显示puncode，但是也可以借助这种机制实现UI Spooof。

Buffer Overflows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在编码转换的时候，有的字符会变成多个字符，如Fluß → FLUSS → fluss这样可能导致BOF。

常见载荷
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

SQL注入
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``＇`` (U+FF07)
- ``＂`` (U+FF02)
- ``﹣`` (U+FE63)

XSS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``＜`` (U+FF1C)
- ``＂`` (U+FF02)

命令注入
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``＆`` (U+FF06)
- ``｜`` (U+FF5C)

模板注入
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- ``﹛`` (U+FE5B)
- ``［`` (U+FF3B)

参考链接
----------------------------------------
- `Unicode equivalence <https://en.wikipedia.org/wiki/Unicode_equivalence>`_
- `Unicode Normalization Forms <http://unicode.org/reports/tr15/>`_
- `Unicode Security Considerations <http://unicode.org/reports/tr36/>`_
- `IDN homograph attack <https://en.wikipedia.org/wiki/IDN_homograph_attack>`_
- `Black Hat <https://www.blackhat.com/presentations/bh-usa-09/WEBER/BHUSA09-Weber-UnicodeSecurityPreview-PAPER.pdf>`_
- `Request encoding to bypass web application firewalls <https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2017/august/request-encoding-to-bypass-web-application-firewalls/>`_
- `domain hacks with unusual unicode characters <https://shkspr.mobi/blog/2018/11/domain-hacks-with-unusual-unicode-characters/>`_
