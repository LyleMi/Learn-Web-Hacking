ATT&CK
========================================

Introduction
----------------------------------------
MITER is a U.S. government-funded research institute that was spun off from MIT in 1958 and has been involved in many commercial and top secret projects. These include the development of the FAA air traffic control system and the AWACS airborne radar system. MITER engages in numerous cybersecurity practices with funding from the National Institute of Standards and Technology (NIST).

MITER launched the ATT&CK™ model in 2013. Its full name is Adversarial Tactics, Techniques, and Common Knowledge (ATT&CK). It is a model that describes the techniques used in each stage of the attack from the attacker's perspective. Convert known attacker behaviors into a structured list, summarize these known behaviors into tactics and techniques, and represent them through several matrices as well as Structured Threat Information Expressions (STIX) and Trusted Automated Exchange of Indicator Information (TAXII). Because this list is a fairly comprehensive representation of the behaviors used by attackers when attacking a network, it is useful for a variety of offensive and defensive metrics, representations, and other mechanisms. It is mostly used for simulating attacks, evaluating and improving defense capabilities, threat intelligence extraction and modeling, threat assessment and analysis.

The official description of ATT&CK is:

::

    MITRE’s Adversarial Tactics, Techniques, and Common Knowledge (ATT&CK) is a curated knowledge base and model for cyber adversary behavior, reflecting the various phases of an adversary’s attack lifecycle and the platforms they are known to target.


Compared with models such as Kill Chain, ATT&CK has a lower level of abstraction, but it is higher than ordinary exploit and vulnerability databases. MITER believes that Kill Chain is helpful in understanding the attack process in a high dimension, but it cannot effectively describe the opponent's behavior in a single vulnerability.

The current ATT&CK model is divided into three parts, namely PRE-ATT&CK, ATT&CK for Enterprise (including Linux, macOS, Windows) and ATT&CK for Mobile (including iOS, Android). PRE-ATT&CK covers the first two stages of the attack chain model (reconnaissance and tracking, weapon construction), ATT&CK for Enterprise covers the last five stages of the attack chain (payload delivery, vulnerability exploitation, installation implantation, command and control, target achievement), and ATT&CK Matrix for Mobile is mainly targeted at mobile platforms.

PRE-ATT&CK includes tactics such as priority definition, target selection, information collection, vulnerability discovery, offensive exploitation of development platforms, establishment and maintenance of infrastructure, personnel development, establishment of capabilities, testing capabilities, and segmentation capabilities.

The tactics included in ATT&CK for Enterprise include access initialization, execution, persistence, privilege escalation, defense evasion, access credentials, discovery, lateral movement, collection, data acquisition, and command and control.

TTP
----------------------------------------
When MITER defined ATT&CK, it defined some key objects: Groups, Software, Techniques, and Tactics.

Organizations use tactics and software, software implements technology, and technology implements tactics. For example, APT28 (organization) uses Mimikatz (software) to achieve the effect of obtaining login credentials (technical) and achieve the purpose of logging in with user rights (tactics). The entire attack behavior is also called TTP, which is a collection of tactics, techniques, and processes.

Reference link
----------------------------------------
- `Mitre ATT&CK <https://attack.mitre.org/>`_
- `Adversarial Threat Matrix <https://github.com/mitre/advmlthreatmatrix>`_
- `MITRE ATT&CK：Design and Philosophy <https://www.mitre.org/sites/default/files/publications/pr-18-0944-11-mitre-attack-design-and-philosophy.pdf>`_
- `ATT&CK General Study Notes <https://bbs.pediy.com/thread-254825.htm>`_
- `Cyber Threat Intelligence Repository expressed in STIX 2.0 <https://github.com/mitre/cti>`_
- `sigma <https://github.com/Neo23x0/sigma>`_ Generic Signature Format for SIEM Systems
- `caldera <https://github.com/mitre/caldera>`_  Automated Adversary Emulation
- `RTA <https://github.com/endgameinc/RTA>`_ Red Team Automation
