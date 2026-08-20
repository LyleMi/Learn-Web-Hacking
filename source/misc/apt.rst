APT
========================================

Introduction
----------------------------------------
APT (Advanced Persistent Threat), translated as Advanced Persistent Threat. In 2006, the concept of APT attacks was formally proposed to describe covert and persistent cyber attacks discovered in U.S. military and government networks from the late 1990s to the early 2000s.

APT attacks are mostly used to use the Internet to carry out cyber espionage activities. Most of their goals are to obtain high-value sensitive intelligence or control the target system, which poses a very serious threat to the target system.

An APT attack is usually initiated by an organization, and its group is an entity that has the ability and intention to carry out attacks continuously and effectively. Attacks launched by individuals or small groups are generally not called APTs because even if their groups intend to attack specific targets, they rarely have the advanced and persistent resources to complete the corresponding attacks.

APT's attack methods usually include supply chain attacks, social engineering attacks, zero-day attacks and botnets. Based on these attack methods, customized malicious code will be placed on one or more computers to perform specific tasks and remain undetected for a long period of time.

Different from traditional large-area scanning attack methods, APT attacks usually only target a single specific target, and most attacks will combine a series of means to complete an APT attack, making them highly concealed and complex, making the detection of APT attacks very difficult. As the name suggests, the characteristics of APT are mainly reflected in the following three aspects.

Advanced
----------------------------------------
APT attacks will combine all currently available attack methods and technologies, making the attack highly concealable and penetrable.

Phishing is one such attack method. Attackers usually combine social engineering and other means to forge emails with high credibility, pretending to be a company or organization trusted by the target, and send malicious emails that are difficult to distinguish between true and false and are highly tempting to the target. These emails are used to trick victims into visiting attacker-controlled websites or downloading malicious code.

APT attacks usually use other methods to disguise their attack behaviors to avoid detection by security systems. For example, some malicious code will evade detection by anti-virus software by forging legitimate signatures. Take the Stuxnet virus as an example. It used a white-and-black pattern when attacking, and used legal certificates to sign its code. This attack method will cause most malicious code detection engines to directly consider the malicious code to be legitimate without any detection.

In addition to using legitimate signatures to bypass detection, APT attackers often use third-party sites as a medium to attack targets during the attack process, instead of using the traditional point-to-point attack mode. This pattern is often called a watering hole attack.

A watering hole attack is an intrusion technique. Generally speaking, after the attacker has a certain understanding of the target, he determines the websites that the target frequently visits, then invades one or several of these websites, and implants malicious code into these websites, and finally achieves the ability to use the website to infect the target. Because this kind of attack relies on a third-party website trusted by the target, the success rate of the attack is much higher than that of phishing attacks.

Another feature that reflects the advanced nature of APT attacks is zero-day vulnerabilities. Currently, the price of a zero-day vulnerability on the international black market ranges from hundreds of thousands to millions. The stable utilization of each zero-day vulnerability requires a large amount of resource investment. In APT attacks, zero-day vulnerabilities are widely used. Take APT28 as an example. According to statistics, in 2015 alone, APT28 used at least six zero-day vulnerabilities in attacks.

Persistent
----------------------------------------
It is very different from traditional network attacks based on short-term interests. The process of APT attacks usually includes multiple implementation stages. In many cases, attackers use layer-by-layer penetration to break through advanced defense systems. The entire attack process usually lasts for months or even years. Generally speaking, APT attacks can be divided into the following stages.

investigative stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to be able to find the target's vulnerabilities, attackers usually make a lot of preparations. At this stage, attackers will often use privacy collection based on big data analysis or attacks based on social engineering to collect target information and make full preparations for subsequent attacks.

initial invasion stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Based on the initial reconnaissance information, attackers can usually collect information such as the software used by the target and the version of the operating system. After obtaining this information, attackers can mine zero-day vulnerabilities in the corresponding version of the software or use known vulnerabilities to make initial intrusions into the system and gain certain control rights over the target.

Privilege escalation phase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In a complex network, the attacker usually obtains lower permissions for the initial intrusion. In order to carry out further attacks, the attacker needs to obtain higher permissions to complete the required attack behavior. At this stage, attackers usually use privilege escalation vulnerabilities or password blasting to achieve the purpose of elevating privileges, and finally gain administrator privileges on the system or even the domain.

maintain access phase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
After successfully invading the target computer and gaining certain permissions, attackers generally use various methods to maintain access to the system. One of the more common methods is to steal the login credentials of legitimate users. After obtaining the user's access credentials, you can use remote control tools (RAT, Remote Access Tools) to establish a connection, and after the connection is established, a specific backdoor is implanted to achieve continuous control.

Horizontal expansion stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Once the attacker has a certain target, he will gradually spread it on the intranet in a slower and more covert manner. The main method is to conduct certain investigations on the intranet first. Based on these investigations, relevant information about intranet computers is obtained, and combined with this information, software vulnerabilities or weak password blasting are used to further penetrate horizontally and obtain more permissions and information.

Attack gain stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The main purpose of APT attacks is to steal information from the target system or cause certain damage to it. After completing horizontal expansion and controlling certain intranet machines. Attackers aiming to collect information will use encrypted channels to gradually transmit the obtained information back and eliminate traces of intrusion. Attacks aimed at causing damage will carry out corresponding attacks and damage at this stage.

Threat
----------------------------------------
Different from traditional attacks, most of the attack methods and plans of APT attacks are designed for specific attack objects and purposes. Compared with other attacks, attackers have very clear goals and objectives. They rarely use automated attack methods, but precise attacks.

In addition, APT targets mostly sensitive enterprises and departments such as government agencies, finance, and energy. Once these targets are successfully attacked, the impact is often huge. According to currently known information, APT attacks have appeared in general elections in the United States, Russia and other countries, as well as in some political events in Europe. APT attacks have become an important means in the country's previous struggle.

Related events
----------------------------------------
- 2010 Iranian Stuxnet virus
- 2013 US Prism scandal
- ...

IoC
----------------------------------------
IoC (Indicators of Compromise) is defined in the forensic field as evidence that computer security has been breached.

Common IoCs include the following:

- hash
- IP
- Domain name
- network
- Host features
- tool
- TTPs

Reference link
----------------------------------------
- `APT analysis and TTPs extraction <https://projectsharp.org/2020/02/23/APT analysis and TTPs extraction>`_
