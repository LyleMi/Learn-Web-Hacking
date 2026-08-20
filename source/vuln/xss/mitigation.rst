XSS protection
===================================================

HTML filtering
---------------------------------------------------
Use some whitelists or blacklists to filter the HTML input by users to achieve filtering effects. For example, tools such as DOMPurify use this method to protect XSS.

X-Frame
---------------------------------------------------
The X-Frame-Options response header has three optional values:

- DENY
    - The page cannot be embedded in any iframe or frame
- SAMEORIGIN
    - The page can only be embedded into an iframe or frame by this site's page
- ALLOW-FROM
    - The page allows frame or frame loading

XSS protection header
---------------------------------------------------
Browsers based on the Webkit kernel (such as Chrome) have a protection mechanism called XSS auditor within a specific version range. If the browser detects that input containing malicious code is rendered in an HTML document, the malicious code presented will either be deleted or escaped, and the malicious code will not be rendered normally.

Whether the browser should intercept this malicious code depends on the browser's XSS protection settings.

To set the browser's protection mechanism, you can use the X-XSS-Protection field
This field has three optional values

- ``0`` : indicates turning off the browser's XSS protection mechanism
- ``1``: Delete the detected malicious code. If the X-XSS-Protection field is not seen in the response message, the browser assumes that X-XSS-Protection is configured as 1, which is the browser's default setting.
- ``1; mode=block`` : If malicious code is detected, do not render the malicious code

FireFox has no relevant protection mechanism. If you need protection, you can use related plug-ins such as NoScript.
