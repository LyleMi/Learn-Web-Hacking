​​ATT&CK
========================================

简介
----------------------------------------
MITRE是美国政府资助的一家研究机构，该公司于1958年从MIT分离出来，并参与了许多商业和最高机密项目。其中包括开发FAA空中交通管制系统和AWACS机载雷达系统。MITRE在美国国家标准技术研究所（NIST）的资助下从事了大量的网络安全实践。

MITRE在2013年推出了ATT&CK™ 模型，它的全称是 Adversarial Tactics, Techniques, and Common Knowledge (ATT&CK)，它是一个站在攻击者的视角来描述攻击中各阶段用到的技术的模型。将已知攻击者行为转换为结构化列表，将这些已知的行为汇总成战术和技术，并通过几个矩阵以及结构化威胁信息表达式（STIX）、指标信息的可信自动化交换（TAXII）来表示。由于此列表相当全面地呈现了攻击者在攻击网络时所采用的行为，因此对于各种进攻性和防御性度量、表示和其他机制都非常有用。多用于模拟攻击、评估和提高防御能力、威胁情报提取和建模、威胁评估和分析。

官方对 ATT&CK的描述是：

::

    MITRE’s Adversarial Tactics, Techniques, and Common Knowledge (ATT&CK) is a curated knowledge base and model for cyber adversary behavior, reflecting the various phases of an adversary’s attack lifecycle and the platforms they are known to target.


和Kill Chain等模型相比，ATT&CK的抽象程度会低一些，但是又比普通的利用和漏洞数据库更高。MITRE公司认为，Kill Chain在高维度理解攻击过程有帮助，但是无法有效描述对手在单个漏洞的行为。

目前ATT&CK模型分为三部分，分别是PRE-ATT&CK，ATT&CK for Enterprise（包括Linux、macOS、Windows）和ATT&CK for Mobile（包括iOS、Android），其中PRE-ATT&CK覆盖攻击链模型的前两个阶段（侦察跟踪、武器构建），ATT&CK for Enterprise覆盖攻击链的后五个阶段（载荷传递、漏洞利用、安装植入、命令与控制、目标达成），ATT&CK Matrix for Mobile主要针对移动平台。

PRE-ATT&CK包括的战术有优先级定义、选择目标、信息收集、发现脆弱点、攻击性利用开发平台、建立和维护基础设施、人员的开发、建立能力、测试能力、分段能力。

ATT&CK for Enterprise包括的战术有访问初始化、执行、常驻、提权、防御规避、访问凭证、发现、横向移动、收集、数据获取、命令和控制。

TTP
----------------------------------------
MITRE在定义ATT&CK时，定义了一些关键对象：组织 (Groups)、软件 (Software)、技术 (Techniques)、战术 (Tactics)。

其中组织使用战术和软件，软件实现技术，技术实现战术。例如APT28（组织）使用Mimikatz（软件）达到了获得登录凭证的效果（技术）实现了以用户权限登录的目的（战术）。整个攻击行为又被称为TTP，是战术、技术、过程的集合。


参考链接
----------------------------------------
- `Mitre ATT&CK <https://attack.mitre.org/>`_
- `MITRE ATT&CK：Design and Philosophy <https://www.mitre.org/sites/default/files/publications/pr-18-0944-11-mitre-attack-design-and-philosophy.pdf>`_
- `ATT&CK一般性学习笔记 <https://bbs.pediy.com/thread-254825.htm>`_
- `Cyber Threat Intelligence Repository expressed in STIX 2.0 <https://github.com/mitre/cti>`_
- `sigma <https://github.com/Neo23x0/sigma>`_ Generic Signature Format for SIEM Systems
- `caldera <https://github.com/mitre/caldera>`_  Automated Adversary Emulation
- `RTA <https://github.com/endgameinc/RTA>`_ Red Team Automation
