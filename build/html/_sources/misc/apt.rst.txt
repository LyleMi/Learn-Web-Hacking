APT
========================================

Introduction
----------------------------------------
APT (Advanced Persistent Threat), translates as advanced persistent threat. In 2006, the concept of APT attacks was formally proposed to describe hidden and ongoing cyberattacks discovered in U.S. military and government networks from the late 1990s to the early 2000s.

APT attacks are mostly used to use the Internet to conduct cyber espionage activities. Most of their targets are to obtain high-value sensitive intelligence or control target systems, which poses a very serious threat to target systems.

The APT attack is usually an organization whose group is an entity that has both the ability and intention to conduct an attack continuously and effectively. Attacks initiated by individuals or small groups are generally not called APTs, because even if their groups intend to attack specific targets, they rarely have advanced and lasting resources to complete the corresponding attack behavior.

APT attack methods usually include supply chain attacks, social engineering attacks, zero-day attacks, and botnets. Based on these attacks, it will place custom malicious code on one or more computers to perform specific tasks and keep it undiscovered for a long time.

Unlike the traditional large-area scanning attack method, APT attacks usually only target a single specific target, and most attacks will combine a series of means to complete an APT attack, making it very concealed and complex, making it very concealed and complex, Detection of APT attacks becomes quite difficult. As the name suggests, the characteristics of APT are mainly reflected in the following three aspects.

Advanced
----------------------------------------
APT attacks will combine all currently available attack methods and technologies, making the attack extremely concealed and permeable.

Phishing is one of the ways to attack. Attackers usually use social engineering and other means to forge highly credible emails, impersonate companies or organizations trusted by the target to send malicious emails that are difficult to distinguish between true and false. These emails are used to induce victims to visit websites controlled by the attacker or download malicious code.

APT attacks usually use other methods to disguise their own attack behavior, thereby achieving the purpose of avoiding security system detection. For example, some malicious codes will evade antivirus software detection by forging legal signatures. Take the Shibu virus as an example. It uses a white and black mode when attacking, and uses a legal certificate to sign its code. This attack method will make most malicious code search engines directly think that the malicious code is Legal, without any testing.

In addition to using legitimate signatures to bypass detection, APT attackers often use third-party sites as media to attack targets during the attack process, rather than using the traditional point-to-point attack mode. This pattern is often called a puddle attack.

Pud attack is a method of invasion. Generally speaking, after the attacker has a certain understanding of the target, he determines the websites frequently visited by the target, and then invades one or several of them, and implants maliciously on these websites. code, and finally achieve the ability to infect the target with the help of this website. Because this kind of attack uses the target's trusted third-party website, the success rate of the attack is much higher than that of phishing attacks.

Another feature that can reflect the advanced nature of APT attacks is the zero-day vulnerability. Currently, the price of a zero-day vulnerability in the black market in the international market ranges from hundreds of thousands to millions. The stable utilization of each zero-day vulnerability requires a large amount of resource investment. . In APT attacks, the zero-day vulnerability is widely used. Taking APT28 as an example, according to statistics, APT28 used at least six zero-day vulnerabilities in the attack in 2015 alone.

Persistent
----------------------------------------
It is very different from traditional cyber attacks based on short-term interests. The process of an APT attack usually involves multiple implementation phases. In many cases, attackers use layer by layer penetration to break through advanced defense systems. The entire attack process generally lasts for several months or even years. Generally speaking, APT attacks can be divided into the following stages.

Investigation phase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In order to be able to find the vulnerability of the target, the attacker usually does a lot of preparation. At this stage, attackers will mostly use privacy collection based on big data analysis or social engineering-based attacks to collect target information, and make full preparations for subsequent attacks.

The first invasion phase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Based on the information of the initial reconnaissance, the attacker can usually collect information such as the software, operating system version, and other information used by the target. After obtaining this information, the attacker can mine zero-day vulnerabilities in the corresponding version of the software or use known vulnerabilities to conduct initial intrusions on the system and obtain certain control rights for the target.

Permission enhancement phase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In complex networks, the permissions obtained by an attacker for the first intrusion are usually lower permissions, and for further attacks, the attacker needs to obtain higher permissions to complete the attack behavior they need. At this stage, attackers usually use permission escalation vulnerabilities or blasting passwords to achieve the purpose of permission escalation, and finally obtain the administrator rights of the system or even the domain.

Stay on the visit phase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
After successfully invading the target computer and having certain permissions, attackers generally use various methods to maintain access to the system. One of the more commonly used methods is to steal the login credentials of legitimate users. After obtaining the user's access credentials, you can use the remote control tool (RAT) to establish the connection, and after the connection is established, a specific backdoor is implanted to achieve the effect of continuous control.

Extended stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When an attacker grasps a certain target, it will gradually spread across the intranet in a slower and more concealed way. The main method is to conduct a certain investigation on the intranet first. Based on these investigations, relevant information about intranet computers are obtained, and combined with this information, software vulnerabilities or weak password blasting are used to conduct horizontal further penetration to obtain more permissions and information.

Attack Revenue Stage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The main purpose of APT attacks is to steal information from the target system or cause some damage to it. After completing the horizontal expansion control of certain intranet machines. Attackers targeting collecting information will use encrypted channels to gradually pass back the acquired information and eliminate traces of intrusion. Attacks targeting the damage will be carried out accordingly at this stage.

Threat
----------------------------------------
Unlike traditional attacks, the attack methods and solutions of APT attacks are mostly designed for specific attack objects and purposes. Compared with other attacks, attackers have very clear goals and goals, and rarely use automated attack methods, but precise attacks.

In addition, the targets of APT are mostly sensitive enterprises and departments such as government agencies, finance, and energy. Once these targets are successfully attacked, their impact is often very huge. According to currently known information, APT attacks have occurred in general elections in the United States, Russia and other countries, as well as in some political events in Europe. APT attacks have become an important means of the country's previous struggle.

Related events
----------------------------------------
- Iran earthquake virus in 2010
- 2013 American Prism Gate Incident
- ...

IoC
----------------------------------------
IoC (Indicators of Compromise) is defined in the field of forensics as evidence that computer security is compromised.

There are several common IoCs:

- hash
- IP
- Domain Name
- network
- Host Features
- tool
- TTPS

Reference link
----------------------------------------
- `APT analysis and TTPs extraction <https://projectsharp.org/2020/02/23/APT analysis and TTPs extraction>`_
