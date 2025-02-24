XSS protection
===================================================

HTML Filtering
---------------------------------------------------
Use some whitelists or blacklists to filter the HTML entered by the user to achieve the filtering effect. For example, tools such as DOMPurify use this method to achieve XSS protection.

X-Frame
---------------------------------------------------
The X-Frame-Options response header has three optional values:

- DENY
- Pages cannot be embedded in any iframe or frame
- SAMEORIGIN
- Pages can only be embedded in iframe or frame by this website page
- ALLOW-FROM
- Page allows frame or frame to load

XSS protection header
---------------------------------------------------
A browser based on the Webkit kernel (such as Chrome) has a protection mechanism called XSS auditor within a specific version. If the browser detects that input containing malicious code is rendered in an HTML document, then the malicious code presented is either Delete or escaped, the malicious code will not be rendered normally.

Whether the browser wants to intercept this malicious code depends on the browser's XSS protection settings.

To set the browser's protection mechanism, you can use the X-XSS-Protection field
This field has three optional values

- ``0``: Indicates that the browser's XSS protection mechanism is closed
- ``1``: Delete the detected malicious code. If the X-XSS-Protection field is not seen in the response message, the browser considers that X-XSS-Protection is configured as 1, which is the default setting of the browser.
- ``1; mode=block``: If malicious code is detected, malicious code is not rendered

FireFox does not have a relevant protection mechanism. If protection is required, you can use NoScript and other related plug-ins.
