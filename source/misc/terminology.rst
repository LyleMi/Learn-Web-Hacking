常见术语
========================================

Windows
----------------------------------------
- WMI (Windows Management Instrumentation)
- ETW (Event Tracing for Windows)
- WFP (Windows Filtering Platform)
- MS-RPC (Microsoft Remote Procedure Call)
- MS-SAMR (Security Account Manager Remote Protocol)
- MS-SCMR (Service Control Manager Remote Protocol)
- MS-DRSR (Directory Replication Service Remote Protocol)
- MS-TSCH (Task Scheduler Service Remoting Protocol)
- DCOM (Distributed Component Object Model)

网络相关
----------------------------------------

网络协议
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 轻型目录访问协议 (Lightweight Directory Access Protocol, LDAP)
- 标识名 (Distinguished Name, DN)
- 相对标识名 (Relative Distinguished Name, RDN)
- 服务器消息块 (Server Message Block, SMB)
- 网络文件共享系统 (Common Internet File System, CIFS)
- SMTP (Simple Mail Transfer Protocol)
- 简单网络管理协议 (Simple Network Management Protocol, SNMP)
- POP3 (Post Office Protocol 3)
- IMAP (Internet Mail Access Protocol)
- HTTP (HyperText Transfer Protocol)
- HTTPS (HyperText Transfer Protocol over Secure Socket Layer)
- 动态主机配置协议 (Dynamic Host Configuration Protocol, DHCP)
- 远程过程调用 (Remote Procedure Call, RPC)
- Java调试线协议 (Java Debug Wire Protocol, JDWP)
- 网络文件系统 (Network File System, NFS)
- 服务主体名称 (Service Principal Names, SPN)
- 简单身份验证 (Simple Authentication and Security Layer, SASL)
- 链路本地多播名称解析 (Link-Local Multicast Name Resolution, LLMNR)
- 分布式运行环境 / RPC (Distributed Computing Environment / Remote Procedure Calls, DCE/RPC)

路由系统
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 自治系统 (Autonomous System, AS)
- 内部网关协议 (Interior Gateway Protocol, IGP)
- 外部网关协议 (External Gateway Protocol, EGP)
- 域内路由选择 (interdomain routing)
- 域间路由选择 (intradomain routing)
- 路由信息协议 (Routing Information Protocol, RIP)
- 开放最短路径优先 (Open Shortest Path First, OSPF)
- 动态路由协议 (Dynamic Routing Protocols, DRP)
- 首跳冗余性协议 (First Hop Redundancy Protocols, FHRP)
- 热备份路由器协议 (Hot Standby Router Protocol, HSRP)
- 虚拟路由冗余协议 (Virtual Router Redundancy Protocol, VRRP)
- 网关负载均衡协议 (Gateway Load Balancing Protocol, GLBP)
- 网络地址转换 (Network Address Translation, NAT)
- 点对点协议 (Point-to-Point Protocol, PPP)
- 生成树协议 (Spanning Tree Protocol, STP)
- QUIC (Quick UDP Internet Connections)

网络应用
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 证书透明度 (Certificate Transparency, CT)
- DNS证书颁发机构授权 (DNS Certification Authority Authorization, CAA)
- 应用级网关 (Application Level Gateway, ALG)

Kerberos
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 密钥分发中心 (Key Distribution Center, KDC)
- 认证服务器 (Authentication Server, AS)
- 票据授权服务器 (Ticket Granting Server, TGS)

开发相关
----------------------------------------
- REST (Representation State Transformation)

安全相关
----------------------------------------
- 缺点 (defect / mistake)
    - 软件在实现上和设计上的弱点
    - 缺点是缺陷和瑕疵的统称
- 缺陷 (bug)
    - 实现层面的软件缺点
    - 容易被发现和修复
    - 例如：缓冲区溢出
- 瑕疵 (flaw)
    - 一种设计上的缺点，难以察觉
    - 瑕疵往往需要人工分析才能发现
    - 软件系统中错误处理或恢复模块，导致程序不安全或失效
- 漏洞 (vulnerability)
    - 可以用于违反安全策略的缺陷或瑕疵
- 交互式应用程序安全测试 (Interactive Application Security Testing, IAST)
- 动态应用程序安全测试 (Dynamic Application Security Testing, DAST)
- 静态应用程序安全测试 (Static Application Security Testing, SAST)
- ATT&CK™ (Adversarial Tactics, Techniques, and Common Knowledge, ATT&CK)
- 横向移动 (Lateral Movement)
- 入侵和攻击模拟 (Breach and Attack Simulation, BAS)

安全开发
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 安全信息和事件管理 (Security Information Event Management, SIEM)
- 自动化响应SOAR模型 (Security Orchestration, Automation and Response, SOAR)
- SDL (Security Development Lifecycle)

安全策略
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 跨域资源共享策略 (Cross-Origin Resource Sharing, CORS)
- 发件人策略框架 (Sender Policy Framework, SPF)
- 域名密钥识别邮件 (DomainKeys Identified Mail, DKIM)
- 基于域名的消息认证报告与一致性协议 (Domain-based Message Authentication, Reporting and Conformance, DMARC)
- DNSSEC (The Domain Name System Security Extensions)
- 基于DNS的命名实体身份验证 (DNS-based Authentication of Named Entities, DANE)

安全模型
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 构建安全成熟度模型 (Building Security In Maturity Model, BSIMM)

攻击相关
----------------------------------------

漏洞类型
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 跨站脚本攻击 (Cross Site Scripting, XSS)
- 跨站请求伪造 (Cross-Site Request Forgery, CSRF)
- 中间人攻击 (Man-in-the-middle, MITM)
- 服务端请求伪造 (Server Side Request Forgery, SSRF)
- 高级持续威胁 (Advanced Persistent Threat, APT)
- 远程命令执行 (Remote Command Execute, RCE)
- 远程代码执行 (Remote Code Execute, RCE)
- 带外数据 (Out-Of-Band, OOB)

攻击方式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 鱼叉攻击 (Spear Phishing)
- 水坑攻击 (Water Holing)
- 分布式拒绝服务 (Distributed Denial of Service, DDoS)

防御相关
----------------------------------------
- IoC (Indicators of Compromise)
- IoA (Indicators of Activity)

防御技术
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 网络检测响应 (Network-based Detection and Response, NDR)
- 终端检测响应 (Endpoint Detection and Response, EDR)
- 托管检测响应 (Managed Detection and Response, MDR)
- 扩展检测响应 (Extended Detection and Response, XDR)
- 自适应安全架构 (Adaptive Security Architecture, ASA)
- 零信任网络访问 (Zero Trust Network Access, ZTNA)
- 云安全配置管理 (Cloud Security Posture Management, CSPM)

防护设施
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 入侵检测系统 (Intrusion Detection System, IDS)
- 主机型入侵检测系统 (Host-based Intrusion Detection System, HIDS)
- 主机入侵防御系统 (Host Intrusion Prevent System, HIPS)
- RASP (Runtime Application Self-protection)
- 统一端点管理 (Unified Endpoint Management, UEM)

运维
----------------------------------------
- 智能运维 (Artificial Intelligence for IT Operations, AIOps)
- 风险和脆弱性评估 (Risk and Vulnerability Assessments, RVA)
- 计算机安全应急响应组 (Computer Emergency Response Team, CERT)

认证
----------------------------------------
- 单点登录 (Single Sign-On, SSO)
- 双因素认证 (Two-Factor Authentication, 2FA)
- 多因素认证 (Multi-Factor Authentication, MFA)
- 一次性密码 (One-Time Password, OTP)

Kerbose
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 认证服务器 (Authentication Server, AS)
- 密钥分发中心 (Key Distribution Center, KDC)
- 票据授权票据，票据的票据 (Ticket Granting Ticket, TGT)
- 票据授权服务器 (Ticket Granting Server, TGS)
- 特定服务提供端 (Service Server, SS)

可信计算
----------------------------------------
- 可信平台模块 (Trusted Platform Module, TPM)

云
----------------------------------------

容器
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 容器运行时 (Container Runtime Interface, CRI)
- 开放容器标准 (Open Container Initiative, OCI)
- 开放容器格式标准 (Open Container Format, OCF)

计算
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 弹性云计算 (Elastic Compute Cloud, EC2)
- 阿里云弹性云计算 (Elastic Compute Service, ECS)
- 云服务器 (Cloud Virtual Machine, CVM)

存储
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 简单存储服务 (Simple Storage Service, S3)
- 对象存储 (Cloud Object Storage, COS) 

XaaS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 函数即服务 (Function as a Service, FaaS)
- 容器即服务 (Container as a Service, CaaS)
- 软件即服务 (Software as a Service, SaaS)
- 平台即服务 (Platform as a Service, PaaS)
- 基础设施即服务 (Insfrastructure as a Service, IaaS)

特定平台
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- OCI (Oracle Cloud Infrastructure)

其他服务
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 元数据服务 (Instance Metadata Service, IMDS)
- 持续集成 (Continuous Integration, CI)
- 持续交付 (Continuous Deployment, CD)
- 边缘计算机器 (Edge Computing Machine, ECM)
