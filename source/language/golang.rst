Golang
========================================

Golang Runtime
----------------------------------------
Threads in Go are called Goroutine or G, and kernel threads are called M. These Gs are scheduled to M, the so-called G:M thread model, or more commonly used M:N thread model, user space thread or green thread model.

String processing
----------------------------------------
- Go source code is always UTF-8
- The byte sequence representing Unicode code points is called ``rune``
- Go does not guarantee that characters in strings are normalized
- String can contain any byte
- When the string does not contain byte-level escape characters, the string always contains a valid UTF-8 sequence

Reference link
----------------------------------------
- `Strings, bytes, runes and characters in Go <https://blog.golang.org/strings>`_
