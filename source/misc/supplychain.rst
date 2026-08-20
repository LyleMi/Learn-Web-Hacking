supply chain security
========================================

Introduction
----------------------------------------
Supply chain security refers to ensuring that all links in the software development and delivery process are secure to prevent malicious attackers from implanting malicious code or vulnerabilities in the software development and delivery process, thereby protecting the security and privacy of end users.

Supply chain security includes security assurance throughout the entire life cycle from software development, testing, deployment, maintenance to updates, etc., to ensure the integrity, reliability and security of the software. In the current digital age, supply chain security has become a very important topic, because malicious attackers can invade corporate and personal computer systems through supply chain attacks, steal sensitive information, or damage the system. Therefore, supply chain security has become one of the security issues that enterprises and organizations must pay attention to.

Can bypass traditional security defenses such as firewalls, intrusion detection systems, etc. In addition, because the links in the supply chain are so complex, attackers can choose to attack any one of them, making defense more difficult.

Supply chain security issues
----------------------------------------

supply chain failure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Supply chain compromise refers to malicious attackers attacking suppliers and entering users' computer systems or networks through the supplier's links.

Supply chain back door
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Supply chain backdoors refer to systems provided by suppliers that have preset backdoors, default passwords or reserved debugging interfaces.

supply chain vulnerabilities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Supply chain vulnerabilities refer to security holes in supply chain software that can be exploited by attackers to compromise end-user computer systems.

Supply chain vulnerabilities are usually caused by defects or errors in software development, testing, deployment, maintenance, etc.

supply chain contamination
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Supply chain contamination means that malicious attackers implant malicious code or vulnerabilities into the software by attacking one or more links in the software supply chain, thereby exposing the end user's computer system or network to attack.

Unlike supply chain backdoors, supply chain contamination usually refers to malicious code or vulnerabilities implanted by attackers in the software supply chain, and is not necessarily a special backdoor.

Supply chain data security
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Supply chain data security refers to the leakage of private and sensitive data in the supply chain.

Common attack methods
----------------------------------------
- Create packages with similar names
    - Combosquatting
    - Typosquatting
    - Modify word order
    - Modify separator
- Inject dependencies
    - named internal package
- Impact build
    - Exploiting CI/CD vulnerabilities
- Submit backdoor code
    - Hijack developer account
    - Submit logically hidden backdoors
    - Use rendering issues to hide submission logic
        - Homoglyph
        - Unicode Bidirectional
        - Other control characters
        - obfuscated / minified

Reference link
----------------------------------------
- `Introducing SLSA, an End-to-End Framework for Supply Chain Integrity <https://security.googleblog.com/2021/06/introducing-slsa-end-to-end-framework.html>`_
