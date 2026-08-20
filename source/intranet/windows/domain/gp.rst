group policy
========================================

Introduction
----------------------------------------
Group Policy (GP) is used to manage users and devices in a network environment and defines various template components required by system administrators for management work.

Group Policy has the following functions:

- Manage registry
- Setup script
- Redirect folder
- Management application
- Specify security options

Common concepts
----------------------------------------
The Group Policy Container (GPC) is stored in Active Directory and contains GPO attributes, configuration information, versions, etc. GPT can be found through GPC.

Group Policy Template (GPT) is stored in the domain controller and contains all group policy information. Includes administrative templates, security, scripts, software installation, and more.

The amount of information and capacity in GPC is small, while the amount of messages and capacity in GPT is large, so the two parts are stored separately. Prevent performance from being affected by excessive data storage in Active Directory.

A Group Policy Object (GPO) is a collection of various Windows Group Policy settings, stored in GPC and GPT.


