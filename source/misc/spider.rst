reptile
========================================

Anti-crawler mechanism
----------------------------------------
- Detect User-Agent
- Data encryption
- Interface signature
- Cluster risk control
- Browser fingerprint detection
    - Hardware features
    - Plugin ``window.navigator.plugins``
    - screen ``window.screen``
    - ...
- canvas fingerprint detection

Front-end anti-debugging
----------------------------------------
- hook key events, disable F12 / right click
    - document.oncontextmenu
    - document.onkeydown
    - document.onkeyup
    - document.onkeypress
- Loop debugger
- Actively trigger OOM after the detection console is opened
