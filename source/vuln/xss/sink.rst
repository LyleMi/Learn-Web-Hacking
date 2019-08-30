Sink
===================================================

执行JavaScript
---------------------------------------------------
- ``eval(payload)``
- ``setTimeout(payload, 100)``
- ``setInterval(payload, 100)``
- ``Function(payload)()``
- ``<script>payload</script>``
- ``<img src=x onerror=payload>``

加载URL
---------------------------------------------------
- ``location=javascript:alert(/xss/)``
- ``location.href=javascript:alert(/xss/)``
- ``location.assign(javascript:alert(/xss/))``
- ``location.replace(javascript:alert(/xss/))``

执行HTML
---------------------------------------------------
- ``xx.innerHTML=payload``
- ``xx.outerHTML=payload``
- ``document.write(payload)``
- ``document.writeln(payload)``
