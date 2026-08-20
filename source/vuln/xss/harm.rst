harm
================================
When XSS vulnerabilities exist, the following situations may occur:

1. The user's cookie is obtained, which may contain sensitive information such as Session ID. If there is no corresponding protection on the server side, the attacker can use the corresponding cookie to log in to the server.

2. The attacker can record the user's keyboard input within certain limits.

3. Attackers perform dangerous operations as users through CSRF and other methods.

4. XSS worm.

5. Obtain user browser information.

6. Use XSS vulnerabilities to scan users’ intranets.
