Group Policy
========================================

Introduction
----------------------------------------
Group Policy (GP) is used to manage users and devices in a network environment, and defines various template components required by system administrators to manage their work.

Group Policy has the following functions:

- Manage registry
- Setting up scripts
- Redirect folders
- Manage applications
- Specify security options

Common concepts
----------------------------------------
Group Policy Container (GPC) is stored in the active directory and contains GPO properties, configuration information, and versions. GPT can be found through GPC.

Group Policy Template (GPT) is stored in domain control and contains all Group Policy information. Including management templates, security, scripts, software installation, etc.

Among them, there is a small amount of information in GPC and a small capacity, while in GPT, there is a large amount of messages and a large capacity, so the two parts are stored separately. Prevent performance from being affected by excessive data stored in the active directory.

Group Policy Object (GPO) is a collection of multiple Windows Group Policy settings stored in GPC and GPT.


