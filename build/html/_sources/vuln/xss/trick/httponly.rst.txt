httponly
================================

- When the cookie is httponly, the operation can be completed directly on the source site through xss, and the cookie is not directly obtained.
- In the case of login operation, some sites may send login requests directly with cookies.
- Some specific versions of browsers may have problems with httponly support/processing
- Low-version browsers support TRACE/TRACK, which can obtain sensitive header fields
- Pages such as phpinfo may echo information, which contains http headers
-Phone jailing page phishing via xss
- Forged authorization requests such as oauth through xss, remote login
