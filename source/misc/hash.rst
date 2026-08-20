Hash
========================================

Introduction
----------------------------------------
Hash is generally translated as hash, also known as hash, or transliterated as hash. It is a method of mapping data into an output value of a specific length.

Common hash functions are:

- CRC32
- MD4 / MD5
- SHA0 / SHA1 / SHA256 / SHA512
- SipHash
- MurMurHash
- CityHash
- xxHash

Features
----------------------------------------
- Consistency, the same data has the same value calculated by the same hash algorithm
- Avalanche effect, small modifications to the original data can lead to huge changes in the hash results
- One-way, the hash can only be calculated from the original data, not in reverse
- Avoid collisions, it is difficult to find two different data that can calculate the same hash

perfect hash
----------------------------------------
Perfect Hashing means that there will be no conflicts during the hash calculation process, which means that the hash function is a completely injective function.

Perfect hashing is actually static, requires the implementation to know what data needs to be hashed, takes a long time to build the index, and cannot be updated in real time.

The existing perfect hash functions include FCH, CHD, PTHash, etc.

security risk
----------------------------------------

Hash-Flooding Attack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Hash-Flooding Attack is an attack method for Web back-end processing languages. It frequently triggers hash collisions by constructing specific form values, causing exponential performance degradation of the original Hash Map.
This is because the time complexity of query/insertion in the hash table when no collisions occur is approximately O(1), but when there are a large number of collisions, the time complexity is O(n). When inserting n elements with the same hash, the time complexity corresponds to O(n^2).

This attack method was proposed as early as 2003 in a usenix paper called Denial of Service via Algorithmic Complexity Attacks. However, there are still a large number of programming languages ​​that do not protect against this attack method, or only later versions have added corresponding protection mechanisms.

Around this attack method, researchers have designed new hash functions such as SipHash, MurmurHash, and CityHash. The core idea is to add a key to the hash algorithm so that the attacker cannot construct a hash conflict function.
Python, Rust, Ruby and other languages ​​also use SipHash as the default hash algorithm in later implementations.

Reference link
----------------------------------------
- `Denial of Service via Algorithmic Complexity Attacks <https://www.usenix.org/conference/12th-usenix-security-symposium/denial-service-algorithmic-complexity-attacks>`_
- `Application vulnerability due to Non Random Hash Functions <https://stackoverflow.com/questions/8669946/application-vulnerability-due-to-non-random-hash-functions>`_
- `SipHash <https://github.com/veorq/SipHash>`_ High-speed secure pseudorandom function for short messages

perfect hash function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- FCH `A Faster Algorithm for Constructing Minimal Perfect Hash Functions <http://cmph.sourceforge.net/papers/fch92.pdf>`_
- CHD `Hash, displace, and compress <http://cmph.sourceforge.net/papers/esa09.pdf>`_
- `PTHash: Revisiting FCH Minimal Perfect Hashing <https://dl.acm.org/doi/pdf/10.1145/3404835.3462849>`_
