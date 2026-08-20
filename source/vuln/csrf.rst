CSRF
========================================

Introduction
----------------------------------------
Cross-Site Request Forgery (CSRF), also known as One Click Attack or Session Riding, often abbreviated as CSRF, is a malicious use of a website. Although it sounds like XSS, it is very different from XSS, which exploits trusted users within a site, while CSRF exploits trusted websites by disguising requests from trusted users.

Classification
----------------------------------------

Resources include
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Resource inclusion is of the type you might see in most presentations or basic courses that introduce CSRF concepts. This type boils down to an attacker taking control of resources contained in HTML tags such as <image>, <audio>, <video>, <object>, <script>, etc. Any tag containing a remote resource can complete the attack if the attacker can affect the URL being loaded.

Due to the lack of point-of-origin checking of cookies, as mentioned above, this attack does not require XSS and can be performed by any attacker-controlled site or the site itself. This type is limited to GET requests, as these are the only request types browsers make for resource URLs. The main limitation of this type is that it requires incorrectly using secure HTTP request methods.

form based
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Typically seen when secure request methods are used correctly. The attacker creates a form that the victim is expected to submit; it contains a JavaScript snippet that forces the victim's browser to submit.

The form can be composed entirely of hidden elements, making it difficult for the victim to discover it.

If cookies are not handled properly, an attacker can launch an attack on any site, and the attack will be successful as long as the victim logs in with a valid cookie. If the request is targeted, a successful attack will return the victim to their usual page. This method is particularly effective against phishing attacks where the attacker can point the victim to a specific page.

XMLHttpRequest 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
XMLHttpRequest is probably the least seen way, and since many modern web applications rely on XHR, many applications spend a lot of time building and implementing this specific workaround.

XHR-based CSRF often comes in the form of XSS payloads due to SOPs. Without Cross-Origin Resource Sharing (CORS), XHR is limited to origin requests where the attacker hosts their own payload.

The attack payload for this type of CSRF is basically a standard XHR that attackers have found some way to inject into the victim's browser DOM.

defense
----------------------------------------
- Detect user submissions through CSRF-token or verification code
- Verify Referer/Content-Type
- It is best to use POST operations for operations such as user modification and deletion.
- Avoid cookies that are common to the whole site and strictly set the domain of the cookie

Reference link
----------------------------------------
- `demo <https://www.github.com/jrozner/csrf-demo>`_
- `Wiping Out CSRF <https://medium.com/@jrozner/wiping-out-csrf-ded97ae7e83f>`_
- `Neat tricks to bypass CSRF protection <https://www.slideshare.net/0ang3el/neat-tricks-to-bypass-csrfprotection>`_
