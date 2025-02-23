CSRF
========================================

Introduction
----------------------------------------
Cross-Site Request Forgery (CSRF), also known as One Click Attack or Session Riding, usually abbreviated as CSRF, is a malicious exploitation of the website. Although it sounds like XSS, it is very different from XSS, which exploits trusted users within the site, while CSRF exploits trusted websites by masquerading requests from trusted users.

Classification
----------------------------------------

Resources include
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Resources include types that may be seen in most demonstrations or basic courses introducing CSRF concepts. This type boils down to an attacker who controls the resources contained in HTML tags (e.g. <image>, <audio>, <video>, <object>, <script>, etc.). If an attacker can affect the URL being loaded, any tag containing remote resources can complete the attack.

Due to the lack of source point checking for cookies, as mentioned above, this attack does not require XSS and can be performed by any attacker-controlled site or the site itself. This type is limited to GET requests only, because these are the browser's unique request types for the resource URL. The main limitation of this type is that it requires incorrectly using a secure HTTP request method.

Based on form
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
It is usually seen when using the secure request method correctly. The attacker creates a form that wants the victim to submit; it contains a JavaScript snippet that forces the victim's browser to submit.

The form can be made up of hidden elements so completely that it is difficult for victims to spot it.

If cookies are handled improperly, an attacker can launch an attack on any site and the attack will succeed as long as the victim logs in with a valid cookie. If the request is purposeful, a successful attack will bring the victim back to their usual page. This method is particularly effective for phishing attacks where an attacker can point a victim to a specific page.

XMLHttpRequest
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
XMLHttpRequest is probably the least seen way, and since many modern web applications rely on XHR, many applications spend a lot of time building and implementing this specific countermeasure.

XHR-based CSRFs usually appear as XSS payloads due to SOP. Without Cross-Origin Resource Sharing (CORS), XHR is limited to the original requests that attackers host their own payloads.

This type of CSRF attack payload is basically a standard XHR, and attackers have found some ways to inject victim browser DOM.

defense
----------------------------------------
- Detect user submissions through CSRF-token or verification code
- Verify Referer/Content-Type
- It is best to use POST operations for user modification and deletion operations, etc.
- Avoid cookies that are common across the site and strictly set the cookie domain

Reference link
----------------------------------------
- `demo <https://www.github.com/jrozner/csrf-demo>`_
- `Wiping Out CSRF <https://medium.com/@jrozner/wiping-out-csrf-ded97ae7e83f>`_
- `Neat tricks to bypass CSRF protection <https://www.slideshare.net/0ang3el/neat-tricks-to-bypass-csrfprotection>`_
