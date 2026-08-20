defensive framework
========================================

defense depth
----------------------------------------
According to the depth, defense can be divided into physical layer, data layer, terminal layer, system layer, network layer and application layer. There is a progressive interdependence between these layers.

physical layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The physical layer has less contact in actual applications, but it is still a very important position. If the physical layer is not designed properly, it is easy for attackers to bypass the upper layer of defense through physical means.

data layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Data is at the lower level of the defense depth, and the target of attacks is often to obtain data. Many defenses also focus on preventing data from being destroyed or stolen.

terminal layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Terminals include PCs, mobile phones, IoT and other smart devices. Whether the terminals connected to the network are trustworthy is a problem that needs to be solved.

System layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The operating system runs on the terminal, and there may be problems such as privilege escalation and unauthorized access.

network layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The network layer uses communication lines to connect multiple computers to each other and communicate according to agreed-upon protocols. There are attacks such as MITM and DDoS at the network layer.

Application layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The application layer is the top layer and mainly involves various attacks on Web applications.

access control
----------------------------------------
Web applications need to restrict user access to the application's data and functionality to prevent unauthorized access by users. The access control process can be divided into three parts: authentication, session management and access control.

Verification mechanism
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Authentication mechanism is the most basic part in user access processing of an application. Authentication is to determine the validity of the user. Most web applications use an authentication model where the user submits a username and password and the application checks their validity. In security-critical applications such as banking, the basic authentication model often requires the addition of additional certificates and multi-level login processes, such as client certificates, hardware, etc.

Session management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to implement effective access control, the application needs a way to identify and handle this series of requests from each different user. Most programs create a unique token for each session to identify it.

For attackers, the session management mechanism is highly dependent on the security of the token. In some cases, an attacker can pretend to be a victim's authorized user and use the web application. There may be several reasons for this situation. One is a flaw in the token generation algorithm, which allows the attacker to guess the tokens of other users; the other is a flaw in the subsequent token processing method, which allows the attacker to obtain the tokens of other users.

access control
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The final step in handling user access is to correctly decide whether to allow or deny each individual request. If the previous mechanisms are working properly, then the application will know the user ID of each received request and decide based on this whether the user is authorized to perform the requested action or access the data.

Due to the complexity of access control itself, this makes it a common target for attackers. Developers often make flawed assumptions about how users will interact with applications and often omit access control checks for certain application features.

Input processing
----------------------------------------
Many attacks on web applications involve submitting unexpected input, which results in behavior that was not intended by the application designers. Therefore, a key requirement for application security is that it handles user input in a secure manner.

Input-based vulnerabilities can appear anywhere in an application's functionality and are related to the type of technology it uses. Input validation is a common and necessary defense against this attack. Commonly used protection mechanisms include the following: blacklist, whitelist, filtering, and processing.

blacklist
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A blacklist contains a literal set of strings or patterns known to be used in attacks, and validation mechanisms block any data that matches the blacklist.

Generally speaking, this method is considered to have poor input effect. There are two main reasons. First, a typical vulnerability in a web application can be exploited using many different inputs. The input can be encrypted or represented in various different ways.

Second, vulnerability exploitation technology is constantly improving, and new methods of exploiting existing vulnerability types cannot be blocked by the current blacklist.

whitelist
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A whitelist consists of a series of strings, patterns, or a set of criteria that match input that meets the requirements. This checking mechanism allows data that matches a whitelist and blocks any data outside of it. This method is relatively effective, but requires better design.

filter
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Filtering removes potentially malicious characters and leaves behind safe characters. Data-based filtering is often effective and, in many cases, serves as a general solution for handling malicious input.

Process data securely
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Many web application vulnerabilities occur because user-supplied data is processed in insecure ways. In some cases, safe programming methods exist that avoid common problems. For example, SQL injection attacks can be organized through precompilation, and XSS can be defended by escaping in most cases.
