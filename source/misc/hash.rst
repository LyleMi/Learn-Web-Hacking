哈希
========================================

简介
----------------------------------------
Hash 一般译作散列，又称杂凑，或音译为哈希，是一种把数据映射为特定长度输出值的方法。

常见的哈希函数有：

- CRC32
- MD4 / MD5
- SHA0 / SHA1 / SHA256 / SHA512
- SipHash
- MurMurHash
- CityHash
- xxHash

特点
----------------------------------------
- 一致性，同一个数据通过同种哈希算法计算出的值是一样的
- 雪崩效应，原始数据小的修改也会导致哈希结果的巨大变化
- 单向，只能从原始数据计算哈希，而不可以反向计算
- 避免冲突，很难找到两个不同的数据可以计算出相同的哈希

完美哈希
----------------------------------------
完美哈希 (Perfect Hashing) 是指在哈希计算过程中，不会出现冲突，也就是说哈希函数是一个完全单射函数。

完美哈希实际是静态的，要求实现知道需要哈希哪些数据，并使用较长时间来建立索引，也无法实时更新。

目前已有的完美哈希函数有 FCH、CHD、PTHash 等。

安全风险
----------------------------------------

Hash-Flooding Attack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Hash-Flooding Attack 是面向Web后端处理语言的一种攻击方式，通过构造特定的表单值频繁触发哈希碰撞，使得原本的Hash Map 获得指数级的性能下降。
这是因为哈希表在不产生碰撞时的查询/插入的时间复杂度近似为 O(1) ，但是大量碰撞时，时间复杂度则为 O(n) ，而插入n个哈希相同的元素，时间复杂度则对应为 O(n^2) 。

早在2003年usenix的一篇名为 Denial of Service via Algorithmic Complexity Attacks 的论文中提出了这种攻击的方式，但是仍有大量的编程语言并没有对这种攻击方式进行防护，或较晚的版本才加入了对应的防护机制。

围绕着这种攻击方式，研究员设计了SipHash、MurmurHash、CityHash等新的哈希函数，核心思路是为哈希算法加入了一个密钥，使得攻击者无法构造哈希冲突的函数。
Python、Rust、Ruby等等语言在后期实现中也将SipHash做为默认的哈希算法。

参考链接
----------------------------------------
- `Denial of Service via Algorithmic Complexity Attacks <https://www.usenix.org/conference/12th-usenix-security-symposium/denial-service-algorithmic-complexity-attacks>`_
- `Application vulnerability due to Non Random Hash Functions <https://stackoverflow.com/questions/8669946/application-vulnerability-due-to-non-random-hash-functions>`_
- `SipHash <https://github.com/veorq/SipHash>`_ High-speed secure pseudorandom function for short messages

完美哈希函数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- FCH `A Faster Algorithm for Constructing Minimal Perfect Hash Functions <http://cmph.sourceforge.net/papers/fch92.pdf>`_
- CHD `Hash, displace, and compress <http://cmph.sourceforge.net/papers/esa09.pdf>`_
- `PTHash: Revisiting FCH Minimal Perfect Hashing <https://dl.acm.org/doi/pdf/10.1145/3404835.3462849>`_
