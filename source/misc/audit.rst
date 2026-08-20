Code audit
========================================

Introduction
----------------------------------------
Code auditing is the process of finding application flaws. It usually includes white box audit, black box audit, gray box audit and other methods. White-box auditing refers to finding application defects through source code analysis. Black-box auditing usually does not involve source code and mostly uses fuzz testing, while gray-box auditing is a combination of black and white. The three different testing methods have different advantages and disadvantages.

Common concepts
----------------------------------------

enter
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Input is usually also called Source. The input of a web application can be request parameters (GET, POST, etc.), uploaded files, cookies, database data and other places that are controllable or indirectly controllable by the user.

For example, ``$_GET`` / ``$_POST`` / ``$_REQUEST`` / ``$_COOKIE`` / ``$_FILES`` / ``$_SERVER`` in PHP can all be used as input to the application.

Handling function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The processing function is a function that filters or encodes and decodes data, usually called Clean/Filter/Sanitizer. These functions perform security operations or filtering on the input, creating uncertainty for vulnerability exploitation.

Taking PHP as an example, such functions may be ``mysqli_real_escape_string`` / ``htmlspecialchars`` / ``base64_encode`` / ``str_rot13``, etc., or they may apply a custom filter function.

hazard function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Dangerous functions are often called sink calls and vulnerability points. They are functions that may trigger dangerous behaviors such as file operations, command execution, database operations, etc.

In PHP, it may be ``include`` / ``system`` / ``echo`` etc.

Automated auditing
----------------------------------------
It is generally believed that the triggering process of a vulnerability is the process from input filtering to dangerous functions (Source To Sink), and auditing is the process of finding this chain. Common automated audit solutions include dangerous function matching, control flow analysis, etc.

Dangerous function matching
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The most common way of white-box auditing is to locate vulnerabilities by searching for dangerous functions and dangerous parameters. A more representative tool is the audit tool developed by Seay. The false positive rate of this method is quite high. This is because this method does not conduct an in-depth analysis of the program flow. On the other hand, this method usually analyzes each file in isolation, ignoring the complex calling relationships between files.

Specifically, this method can achieve almost no omissions in some environments. As long as the auditor is patient, most vulnerabilities can be found. However, in highly framed code, the number of vulnerabilities that can be found is relatively limited.

control flow analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In later systems, considering the introduction of AST as the basis for analysis to a certain extent, false alarms were reduced to a certain extent, but there are still many flaws.

Then, Dahse J and others designed RIPS. This tool performs data flow and control flow analysis, and combines intra-process and inter-process analysis to obtain audit results. Compared with the dangerous function matching method, the false positive rate is much lower, but it also increases the overhead.

Graph-based analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Graph-based analysis is an improvement on control flow analysis. It uses the characteristics of CFG and graph calculation algorithms to simplify calculations to a certain extent. The more representative ones are the article Efficient and Flexible Discovery of PHP Application Vulnerabilities published by Microsoft's Semmle QL and NDSS in 2017.

Code similarity comparison
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some developers copy code from other frameworks, or use various frameworks. If a corresponding vulnerability map has been established in advance, the similarity method can be used to find the vulnerability.

Gray box analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Analysis based on control flow is relatively expensive, so some people have proposed a runtime-based analysis method, hooking the code, automatically tracing back the input when executing the dangerous function, finding the input and determining whether it is available.

This method solves the problems of complex implementation of control flow analysis and high computational path overhead. It also makes certain breakthroughs in judging filter functions, but the gray box method does not necessarily trigger all vulnerabilities. prvd developed by fate0 is based on this design idea.

Manual audit process
----------------------------------------
- Get the code, determine the version, and try preliminary analysis
    - Find historical vulnerability information
    - Find examples of applications of the system
    - Determine whether there are vulnerabilities in dependent libraries
- Preliminary analysis based on audit tools
- Understand the program running process
    - File loading method
        - Class library dependencies
        - Whether to load waf
    - Database connection method
        - mysql/mysqli/pdo
        - Whether to enable precompilation
    - View rendering
        - XSS
        - Template injection
    - SESSION processing mechanism
        - document
        - database
        - Memory
    - Cache processing mechanism
        - File cache may write shell
        - Database cache may be injected
        - memcache
- Account system
    - Auth method
    - Pages that can be accessed under Pre-Auth
    - Ordinary user account
        - Is it possible to obtain ordinary user rights?
    - Default password for administrator account
    - Account system
        - Encryption method
        - Blast passwords
        - Reset vulnerability
        - Change password vulnerability
            - Change other account passwords
- Find sinks based on vulnerability type
    - SQLi
        - Can global filtering be bypassed?
        - Is there a place to directly execute SQL?
        -SQL driver, mysql/mysqli/pdo
            - If using PDO, search if there is a direct execution part
    - XSS
        - Global bypass
        - View rendering
    - FILE
        - Find upload function points
        - Upload and download overwrite and delete
        - Include
            - LFI
            - RFI
            - Find include and require globally
    - RCE
    - XXE
    - CSRF
    - SSRF
    - Deserialization
    - Variable override
    - LDAP
    - XPath
    - Cookie forgery
- filter
    - Find the WAF filtering method to determine whether it can be bypassed

Reference link
----------------------------------------
- `rips <https://github.com/ripsscanner/rips>`_
- `prvd <https://github.com/fate0/prvd>`_
- `PHP runtime vulnerability detection <http://blog.fatezero.org/2018/11/11/prvd/>`_
- Backes M , Rieck K , Skoruppa M , et al. Efficient and Flexible Discovery of PHP Application Vulnerabilities[C]// IEEE European Symposium on Security & Privacy. IEEE, 2017.
- Dahse J. RIPS-A static source code analyser for vulnerabilities in PHP scripts[J]. Retrieved: February, 2010, 28: 2012.
