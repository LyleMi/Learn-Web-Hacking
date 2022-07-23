Active Directory
========================================
活动目录 (Active Directory，AD) 是面向Windows Server的目录服务。Active Directory存储了有关网络对象的信息，并且让管理员和用户能够查找和使用这些信息。

ADDS
----------------------------------------
Active Directory提供目录服务的组件被称作Active Directory域服务 (Active Directory Domain Services, ADDS) ，负责目录数据库的存储、增删改查等工作，可以用在多种局域网、广域网的场景中。

从逻辑上看，ADDS的组件可以分为Partition、Schema、Domain、Domain tree、Forest、OU、Container。

Partition也被称为naming context，是AD DS数据库的一部分。Schema是存储在 ADDS 中数据的定义。Container是为ADDS提供组织框架的对象。

从实现上区分，ADDS可以分为Domain controller、Data store、Global catalog server、RODC (Read-only domain controller) 、Site、Subnet。

每个域控制器都有完整的ADDS数据，每个域控都可以处理数据的修改并同步至其他的域控。

域控会有一份数据拷贝 (Data store) ，默认存储在 ``C:\Windows\NTDS`` 目录下。

Global catalog server是存储全局catalog的域控，catlog以只读的方式存储了一个multiple-domain forest的所有对象，用于加速搜索。

名称空间
----------------------------------------
名称空间 (namespace) 是一块界定好的区域，在区域内可以用名称找到与之相关的信息。

对象与属性
----------------------------------------
ADDS内的资源都是以对象 (Object) 的形式存在的，对象通过属性 (Attrbute) 来描述其特征。
