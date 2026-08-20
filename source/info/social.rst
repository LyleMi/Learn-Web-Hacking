social engineering
========================================

Corporate information collection
----------------------------------------
Some websites, such as Tianyancha, can provide information inquiries such as corporate relationship mining, industrial and commercial information, trademarks and patents, corporate annual reports, etc., and can provide more detailed information about the company.

The company's main website will contain information such as business directions and cooperative units.

Personnel information collection
----------------------------------------
When collecting information about people, consider the collection and analysis of important target personnel, organizational structures, and social relationships. Among them, important personnel mainly refer to the personal computers of senior executives, system administrators, development, operation and maintenance, finance, personnel, and business personnel.

The easier entry point for collecting personnel information is the website, which may contain information about the development, management and maintenance of the website. The names, email addresses and other contact information of all developers and maintainers may be obtained from the website contact function and the code comment information.

After obtaining this information, you can further search for all the information related to the target site published by these people on the Internet in social and recruitment websites such as Github/Linkedin, analyze and discover useful information.

In addition, password blasting can be performed on the obtained email address to obtain the corresponding password.

fishing
----------------------------------------
Based on the previously collected information, you can use Office/CHM/RAR/EXE/shortcut and other file formats to create phishing emails and send them to the target to further collect information.

Among them, Office can use Office vulnerabilities, macros, OLE objects, PPSX and other methods to construct exploit files.

Exe can use special Unicode control characters such as RLO (Right-to-Left Override) to construct confusing file names.

RAR mainly uses self-extracting methods to construct malicious files. Similarly, encrypted compressed packages can also evade detection by email gateways to a certain extent.

If the mailbox of the operation and maintenance personnel is obtained through the early stage of information collection, you can use the mailbox of the operation and maintenance personnel to send the email. If the relevant information is not collected, you can use the method of forging the sending source to send the email.

It should be noted that phishing tests also need to pay attention to compliance issues. You cannot pretend to be a regulatory agency or send illegal information. For details, please refer to laws and regulations such as the "Telecommunications Regulations of the People's Republic of China" and the "Measures of the People's Republic of China for the Administration of Internet Email Services".

Other information
----------------------------------------
The company's official account, enterprise account, website, employee network disk, Baidu library, etc. may contain some sensitive information, such as VPN/bastion account, TeamViewer account, network device default password, server default password, etc.
