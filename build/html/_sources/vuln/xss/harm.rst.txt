harm
================================
When an XSS vulnerability exists, the following situations may be caused:

1. The user's cookie is obtained, which may contain sensitive information such as Session ID. If the server does not provide corresponding protection, the attacker can log in to the server with the corresponding cookie.

2. The attacker can record the user's keyboard input within a certain limit.

3. The attacker performs dangerous operations as a user through CSRF and other means.

4. XSS worm.

5. Obtain user browser information.

6. Use XSS vulnerabilities to scan the user's intranet.
