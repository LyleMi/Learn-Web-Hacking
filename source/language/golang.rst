Golang
========================================

Golang Runtime
----------------------------------------
Threads in Go are called Goroutines or G, and kernel threads are called M. These Gs are scheduled onto M, the so-called G:M threading model, or more commonly known as the M:N threading model, user space threads or green threading model.

String processing
----------------------------------------
- Go source code is always UTF-8
- The sequence of bytes representing a Unicode code point is called a ``rune``
- Go does not guarantee that characters in strings are normalized
- Strings can contain arbitrary bytes
- Strings always contain valid UTF-8 sequences when they do not contain byte-level escapes

Reference link
----------------------------------------
- `Strings, bytes, runes and characters in Go <https://blog.golang.org/strings>`_
