That & ck
========================================

Introduction
----------------------------------------
MITRE is a U.S. government-funded research institution, which was separated from MIT in 1958 and has been involved in many commercial and top secret projects. This includes the development of the FAA air traffic control system and the AWACS airborne radar system. MITRE engages in a large number of cybersecurity practices under the support of the National Institute of Standards and Technology (NIST).

MITRE launched the ATT&CK™ model in 2013, its full name is Adversarial Tactics, Techniques, and Common Knowledge (ATT&CK), a model that describes the technologies used in each stage of an attack from the perspective of an attacker. Convert known attacker behaviors into structured lists, summarize these known behaviors into tactics and techniques, and trusted automated exchange of metric information through several matrices, structured threat information expressions (STIX), and metric information (TAXII) To express it. Since this list is quite comprehensive in presenting the behaviors that an attacker takes when attacking a network, it is very useful for a variety of offensive and defensive metrics, representations, and other mechanisms. It is mostly used to simulate attacks, evaluate and improve defense capabilities, threat intelligence extraction and modeling, threat assessment and analysis.

The official description of ATT&CK is:

::

MITRE’s Adversarial Tactics, Techniques, and Common Knowledge (ATT&CK) is a curated knowledge base and model for cyber adversary behavior, reflecting the various phases of an adversary’s attack lifecycle and the platforms they are known to target.


Compared with models such as Kill Chain, ATT&CK has a lower abstraction, but it is higher than ordinary exploitation and vulnerability databases. MITRE believes that Kill Chain is helpful in understanding the attack process in a high-dimensional manner, but cannot effectively describe the behavior of an adversary in a single vulnerability.

Currently, the ATT&CK model is divided into three parts, namely PRE-ATT&CK, ATT&CK for Enterprise (including Linux, macOS, Windows) and ATT&CK for Mobile (including iOS, Android). PRE-ATT&CK covers the first two stages of the attack chain model ( Reconnaissance and tracking, weapon construction), ATT&CK for Enterprise covers the last five stages of the attack chain (payment, vulnerability utilization, installation and implantation, command and control, and target achievement). ATT&CK Matrix for Mobile is mainly aimed at mobile platforms.

The tactics included in PRE-ATT&CK include priority definition, target selection, information collection, discovery of vulnerabilities, aggressive utilization of development platforms, establishment and maintenance of infrastructure, personnel development, establishment capabilities, testing capabilities, and segmentation capabilities.

ATT&CK for Enterprise includes tactics such as access initialization, execution, resident, escalation, defense evasion, access credentials, discovery, horizontal movement, collection, data acquisition, command and control.

TTP
----------------------------------------
When defining ATT&CK, MITRE defines some key objects: organizations (Groups), software (Software), technology (Techniques), and tactics (Tactics).

Among them, the organization uses tactics and software, software to realize technology, and technology to realize tactics. For example, APT28 (organization) uses Mimikatz (software) to achieve the effect of obtaining login credentials (technology) and realizes the purpose of logging in with user permissions (tactics). The entire attack behavior is also called TTP, which is a collection of tactics, techniques and processes.

Reference link
----------------------------------------
- `Mitre that & ck <https://attack.mitre.org/>` _
- `Adversarial Threat Matrix <https://github.com/mitre/advmlthreatmatrix>`_
- `MITRE ATT&CK：Design and Philosophy <https://www.mitre.org/sites/default/files/publications/pr-18-0944-11-mitre-attack-design-and-philosophy.pdf>`_
- `ATT&CK General Study Notes <https://bbs.pediy.com/thread-254825.htm>`_
- `Cyber Threat Intelligence Repository expressed in STIX 2.0 <https://github.com/mitre/cti>`_
- `sigma <https://github.com/Neo23x0/sigma>`_ Generic Signature Format for SIEM Systems
- `caldera <https://github.com/mitre/caldera>`_  Automated Adversary Emulation
- `RTA <https://github.com/endgameinc/RTA>`_ Red Team Automation
