Code Audit
========================================

Introduction
----------------------------------------
Code auditing is the process of finding application defects. It usually includes white box audit, black box audit, gray box audit and other methods. White box audit refers to finding application defects through analysis of source code. Black box audit usually does not involve source code and mostly uses fuzzy testing, while gray box audit is a combination of black and white. The three different testing methods have different advantages and disadvantages.

Common concepts
----------------------------------------

enter
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Input is usually also called Source. The input of a web application can be a user-controlled or indirectly controllable place such as requested parameters (GET, POST, etc.), uploaded files, cookies, database data.

For example, ``$_GET``/``$_POST``/``$_REQUEST``/``$_COOKIE``/``$_FILES``/``$_SERVER`` etc. in PHP can all be used as The input to the application.

Processing functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Processing functions are functions that filter or code data, usually called Clean/Filter/Sanitizer. These functions operate or filter the input securely, bringing uncertainty to exploits.

Take PHP as an example, such functions may be ``mysqli_real_escape_string`` / ``htmlspecialchars`` / ``base64_encode`` / ``str_rot13`` etc., or they may also be applied to custom filtering functions.

Danger function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Dangerous functions are often called Sink Calls and vulnerability points. They are functions that may trigger dangerous behaviors such as file operations, command execution, database operations, etc.

In PHP, it might be ``include``/``system``/`echo`` etc.

Automated audit
----------------------------------------
It is generally believed that the triggering process of a vulnerability is a process from filtering the input to a dangerous function (Source To Sink), and audit is the process of finding this chain. Common automated audit solutions include dangerous function matching, control flow analysis, etc.

Danger function matching
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The most common way of white box auditing is to locate vulnerabilities by searching for hazard functions and hazard parameters. The more representative tool is the audit tool developed by Seay. This method has a very high false positive rate because this method does not conduct in-depth analysis of the program's flow. On the other hand, this method usually analyzes each file in isolation, ignoring the complex calling relationship between files.

Specifically, this method can achieve almost no omissions in some environments. As long as the auditor is patient, most of the vulnerabilities can be discovered, but in highly framework code, the vulnerabilities can be found are relatively limited.

Control flow analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In later systems, taking into account the introduction of AST as a basis for analysis to a certain extent, false positives were reduced to a certain extent, but there are still many defects.

Then, Dahse J et al. designed RIPS, which performs data flow and control flow analysis, and combines the analysis within and between processes to obtain audit results. Compared with the method of matching hazardous functions, the false alarm rate is much lower, but the same It also increases overhead.

Graph-based analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Graph-based analysis is an improvement to control flow analysis. It uses the characteristics of CFG and graph calculation algorithms to simplify the calculation to a certain extent. The more representative ones are the articles published by Microsoft's Semmle QL and NDSS in 2017 Efficient and Flexible Discovery of PHP Application Vulnerabilities.

Code similarity comparison
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Some developers will copy the code of other frameworks, or use various frameworks. If a corresponding vulnerability map is established in advance, the similarity method can be used to find the vulnerability.

Grey box analysis
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The analysis cost based on control flow is relatively high, so someone proposed a runtime analysis method to hook the code, and automatically trace the input when it is executed to find the input and determine whether it is available.

This method solves the problem of complex implementation of control flow analysis and high overhead in computing paths, and also has certain breakthroughs in judging filter functions, but the gray box method does not necessarily trigger all vulnerabilities. The prvd developed by fate0 is based on this design idea.

Manual audit process
----------------------------------------
- Get the code, determine the version, try to analyze it in advance
- Find historical vulnerability information
- Find an example to apply this system
- Determine if there are vulnerabilities in the dependency library
- Preliminary analysis based on audit tools
- Understand the program running process
- File loading method
- Class library dependencies
- Whether to load waf
- Database connection method
- mysql/mysqli/pdo
- Whether to enable precompilation
- View Rendering
- XSS
- Template Injection
- SESSION processing mechanism
- document
- database
- Memory
- Cache processing mechanism
- File cache may write shell
- Database cache may be injected
- Memcache
- Account system
- Auth way
- Pages that can be accessed in the case of Pre-Auth
- Regular user's account
- Can you obtain ordinary user permissions
- Default password for administrator account
- Account system
- Encryption method
- Blasting password
- Reset vulnerability
- Password modification vulnerability
- Modify other account passwords
- Find Sink by vulnerability type
- SQVI
- Can global filtering be bypass
- Is there a place to directly execute SQL
- SQL driver, mysql/mysqli/pdo
- If using PDO, search for whether there is a direct execution part
- XSS
- Global bypass
- View Rendering
- FILE
- Find upload function points
- Upload download overwrite deletion
- Include
- life
- RFI
- Global search include, require
- RCE
- XXE
- CSRF
- SSRF
- Deserialization
- Variable overwrite
- LDAP
- XPath
- Cookie forgery
- Filter
- Find WAF filtering method to determine whether it can be bypassed

Reference link
----------------------------------------
- `rips <https://github.com/ripsscanner/rips>`_
- `prvd <https://github.com/fate0/prvd>` _
- `PHP runtime vulnerability detection <http://blog.fatezero.org/2018/11/11/prvd//2018`_
- Backes M , Rieck K , Skoruppa M , et al. Efficient and Flexible Discovery of PHP Application Vulnerabilities[C]// IEEE European Symposium on Security & Privacy. IEEE, 2017.
- Dahse J. RIPS-A static source code analyser for vulnerabilities in PHP scripts[J]. Retrieved: February, 2010, 28: 2012.
