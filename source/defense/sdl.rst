Safe development
========================================

Introduction
----------------------------------------
Security Development Lifecycle (SDL) is a management model proposed by Microsoft to guide the software development process from a security perspective. Designed to help developers build more secure software, address security compliance requirements, and reduce development costs.

step
----------------------------------------

Phase 1: Training
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
All members of the development team must receive appropriate security training and understand relevant security knowledge. Training targets include developers, testers, project managers, product managers, etc.

Phase 2: Determine security needs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Before the project is established, it is necessary to determine the security requirements in advance, determine the project planning time, and avoid changes in requirements caused by security as much as possible.

Stage 3: Design
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Determine the minimum acceptable level of safety during the design phase. Consider what attack surfaces the project involves and whether the attack surfaces can be reduced.

Conduct threat modeling on the project to identify possible attack vectors and consider which parts of the project require penetration testing.

Stage 4: Implementation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The implementation phase mainly involves tools, unsafe functions, static analysis, etc.

In terms of tools, the main consideration is that the editors, linkers and other related tools used by the development team may involve some security-related issues. Therefore, it is necessary to communicate with the security team in advance on the version of the tools to be used.

In terms of functions, we mainly consider that many commonly used functions may have security risks. Unsafe functions and APIs should be disabled and functions recommended by the security team should be used.

Code static analysis can be completed with the assistance of relevant tools, and the results are combined with manual analysis.

Stage 5: Verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The verification phase involves dynamic program analysis and attack surface re-auditing. Dynamic analysis supplements static analysis, and the commonly used methods are fuzz testing and penetration testing. Fuzz testing works by introducing possible problems with format-specific or random data finders into your application.

Considering that projects often cause the final product to be inconsistent with the initial goals due to changes in requirements, etc., the threat model and attack surface need to be analyzed and considered again in the later stages of the project, and if problems arise, they must be corrected.

Stage 6: Release
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
After the program is released, it needs to respond to security incidents, and it is necessary to preset how to deal with security problems.

In addition, if the product contains third-party code, you also need to consider how to respond to problems introduced by third-party dependencies.

Reference link
----------------------------------------
- `SDL Practices <https://www.microsoft.com/en-us/securityengineering/sdl/practices>`_
- `Threat Modeling  <https://www.microsoft.com/en-us/securityengineering/sdl/threatmodeling>`_
