httponly
================================

- When the cookie is httponly, the operation can be completed directly on the origin site through XSS without directly obtaining the cookie.
- When there is a login operation, some sites may send login requests directly with cookies.
- Some specific versions of browsers may have issues with httponly support/processing
- Lower version browsers support TRACE / TRACK, which can obtain sensitive header fields
- Pages such as phpinfo may echo information, which contains http headers.
- Phishing via xss hijacking page
- Forge authorization requests such as oauth through xss and log in remotely
