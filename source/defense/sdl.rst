Safe development
========================================

Introduction
----------------------------------------
Security Development Lifecycle (SDL) is a management model proposed by Microsoft to guide the software development process from a security perspective. Used to help developers build safer software, solve security compliance requirements, and reduce development costs.

step
----------------------------------------

Phase 1: Training
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
All members of the development team must receive appropriate security training and understand relevant security knowledge. The training targets include developers, testers, project managers, product managers, etc.

Phase 2: Identify security requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Before the project is established, it is necessary to determine the safety requirements in advance, determine the project's planning time, and avoid changes in demand caused by safety as much as possible.

Phase 3: Design
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The minimum acceptable level of safety is determined during the design phase. Consider what attack surfaces the project involves and whether it can reduce the attack surface.

Model the project threat, clarify what aspects of the attack that may come from, and consider which parts of the project need to be penetration testing.

Phase 4: Implementation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The implementation stage mainly involves tools, unsafe functions, static analysis and other aspects.

In terms of tools, the main consideration is that the editors, linkers and other related tools used by the development team may involve some security-related issues. Therefore, when using the tool version, you need to communicate with the security team in advance.

In terms of functions, the main consideration is that many commonly used functions may have security risks, and unsafe functions and APIs should be disabled and functions recommended by the security team should be used.

Code static analysis can be accomplished with relevant tools, and the results are combined with manual analysis.

Phase 5: Verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The verification phase involves dynamic program analysis and attack surface reaudification. Dynamic analysis supplements static analysis, and the commonly used methods are fuzzy testing and penetration testing. Fuzz testing finds possible problems for the program by introducing specific formats or random data to the application.

Considering that the project often causes the final product to be inconsistent with the initial goal due to changes in demand, it is necessary to analyze and consider the threat model and attack surface later in the project, and correct it if a problem occurs.

Phase 6: Release
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
After the program is released, it is necessary to respond to security incidents and preset how to deal with security problems.

In addition, if the product contains third-party code, you also need to consider how to respond to the problems introduced by third-party dependencies.

Reference link
----------------------------------------
- `SDL Practices <https://www.microsoft.com/en-us/securityengineering/sdl/practices>`_
- `Threat Modeling  <https://www.microsoft.com/en-us/securityengineering/sdl/threatmodeling>`_
