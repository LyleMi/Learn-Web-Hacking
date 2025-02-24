Hash
========================================

Introduction
----------------------------------------
Hash is generally translated as hash, also known as hash, or transliterated as hash, which is a method of mapping data into output values of a specific length.

Common hash functions are:

- CRC32
- MD4 / MD5
- Sha1 / sha1 / sha256
- Sifash
- MurMurHash
- CityHash
- xxHash

Features
----------------------------------------
- Consistency, the value calculated by the same data through the same hashing algorithm is the same
- Avalanche effect, small modifications to the original data will also lead to huge changes in the hash result
- One-way, hash can only be calculated from the original data, not in reverse
- Avoid conflicts, it's hard to find two different data that can compute the same hash

Perfect hash
----------------------------------------
Perfect hashing means that there will be no conflict during hash calculation, which means that the hash function is a completely single-injection function.

Perfect hash is actually static, requiring the implementation to know which data needs to be hashed and to use it for a long time to index it, and it cannot be updated in real time.

The perfect hash functions currently available include FCH, CHD, PTHash, etc.

Security risks
----------------------------------------

Hash-Flooding Attack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Hash-Flooding Attack is an attack method for web backend processing languages. By constructing specific form values, it frequently triggers hash collisions, causing the original Hash Map to achieve exponential performance degradation.
This is because the time complexity of the hash table when there is no collision is approximately O(1), but in a large number of collisions, the time complexity is O(n), and n elements with the same hash are inserted. , the time complexity corresponds to O(n^2).

As early as 2003, a paper by useenix called Denial of Service via Algorithmic Complexity Attacks proposed this attack method, but there are still a large number of programming languages that do not protect this attack method, or later versions. The corresponding protection mechanism has been added.

Based on this attack method, the researchers designed new hash functions such as SipHash, MurmurHash, and CityHash. The core idea is to add a key to the hash algorithm, so that the attacker cannot construct a hash conflict function.
Python, Rust, Ruby and other languages also use SipHash as the default hashing algorithm in later implementations.

Reference link
----------------------------------------
- `Denial of Service via Algorithmic Complexity Attacks <https://www.usenix.org/conference/12th-usenix-security-symposium/denial-service-algorithmic-complexity-attacks>`_
- `Application vulnerability due to Non Random Hash Functions <https://stackoverflow.com/questions/8669946/application-vulnerability-due-to-non-random-hash-functions>`_
- `SipHash <https://github.com/veorq/SipHash>`_ High-speed secure pseudorandom function for short messages

Perfect hash function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- FCH `A Faster Algorithm for Constructing Minimal Perfect Hash Functions <http://cmph.sourceforge.net/papers/fch92.pdf>`_
- CHD `Hash, displace, and compress <http://cmph.sourceforge.net/papers/esa09.pdf>`_
- `PTHash: Revisiting FCH Minimal Perfect Hashing <https://dl.acm.org/doi/pdf/10.1145/3404835.3462849>`_
