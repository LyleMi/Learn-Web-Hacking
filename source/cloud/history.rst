云发展史
========================================

在2000年到2010年间，云计算主要在 IaaS 的方向发展。
在这个阶段以前，硬件、机房独立维护，运维成本高。应用部署、迁移困难，隔离性差。因此出现了 IaaS ，以基础设施做为服务，通过规模化部署来降低边际成本。
IaaS 的核心是各种虚拟化技术。
在这个时间段，出现了许多相关的虚拟化工具、商业化产品。

2000年，FreeBSD Jail 实现了第一个功能完整的操作系统虚拟化技术。
2001年，VMWare 发布 ESX 和 GSX ，推出虚拟化技术。同年，基于动态二进制翻译的 QEMU 发布。
2002年，亚马逊上线了Amazon Web Services。
2005年，Intel 推出了 VT-x 硬件辅助虚拟化技术。
2006年，KVM 诞生。同年，亚马逊发布了EC2 (Elastic Compute Cloud) 和 S3 (Simple Storage Service) 产品。
2008年，谷歌发布了第一版Google App Engine。
2010年，微软发布了Microsoft Azure。
2010年，开源软件 OpenStack 发布并成立社区。OpenStack 本质上是一组分配、管理虚拟机的自动化工具脚本。在 OpenStack 发布以后，许多做 IaaS 的厂商都使用了 OpenStack 。

IaaS 平台一定程度上提高了物理资源的利用效率，但是虚拟机在资源利用上仍然存在局限性。随后2011年到2013年期间，PaaS 开始逐渐成型，用于支持应用程序的完整生命周期，提供应用托管的能力。

2011年，由 VMWare 开发的 CloudFoundry 做为第一款 PaaS 平台开源。支持应用打包、部署、以容器的方式运行、负载均衡等功能。
2011年11月，Google Compute Engine发布。
2012年，OpenShift 开源。
2013年，Docker开源并发布，通过镜像的方式解决了应用开发、测试、生成环境不一致的问题。

2013年以后，云计算越来越成熟。规模也越来越大，容器的规模部署与管理成为了问题。Docker 发布了 Swarm ，而 Google 则发布了 Kubernetes 。

2013年，云原生概念被提出。
2014年，Google 发布 Kubernetes。
2015年，Google宣布成立CNCF基金会（云原生计算）。
