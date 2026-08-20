Red and blue confrontation
========================================

concept
----------------------------------------
The concept of red-blue confrontation first originated from American exercises in the 1960s. Exercises refer specifically to large-scale real-force exercises conducted by the military. Exercises are usually divided into Red Army and Blue Army. The Blue Army usually refers to the troops that play the role of imaginary enemies in simulated confrontation exercises and conduct targeted training with the Red Army (representing our frontal forces). This method is also called Red Teaming.

The concept of red-blue confrontation in network security originated from this. As the corporate defender, the Red Army ensures corporate security through security reinforcement, attack monitoring, emergency response and other means. As the attacker, the blue army aims to discover security vulnerabilities and obtain business permissions or data. It uses various attack methods to try to bypass the layers of protection of the red army and achieve the set goals. What may cause confusion is that in Europe and the United States, the red team represents the attacking side and the blue team represents the defending side. The colors represent the opposite.

Network attack and defense drills
----------------------------------------
Some of the more influential exercises include "Locked Shields" and "Cyber ​​Storm". Among them, "Lock Shield" is held annually by the NATO Cooperative Cyber ​​Defense Center of Excellence (CCDCOE). "Cyberstorm" is led by the U.S. Department of Homeland Security (DHS). It began in 2006 and is held every two years.

Compared with APT attacks, offensive and defensive exercises are relatively short, only 1 to 4 weeks, and have a defensive goal. APT attacks have a unique target, can last from months to years, and are more covert.

Focus on
----------------------------------------
The work content of the enterprise network blue team mainly includes penetration testing and red-blue confrontation. The technologies used in these two methods are basically the same, but the focus is different.

Penetration testing focuses on discovering more security vulnerabilities in a shorter period of time, and generally does not pay much attention to whether attack behaviors are detected and discovered. The purpose is to help business systems expose and contain more risks.

Red-blue confrontation is closer to real scenes and is biased towards actual combat. It faces complex scenes and various technologies. Focus on bypassing the defense system and achieving the goal of obtaining business permissions or data without any noise. It is not necessary to discover all risk points, because the more attacks there are, the greater the probability of being discovered. Once discovered, the Red Army will kick the Blue Army off the battlefield. The purpose of the red-blue confrontation is to test the defense-in-depth capabilities, alarm operation quality, and emergency response capabilities in real attacks.

Target
----------------------------------------
- Assess the effectiveness of existing defense capabilities, identify weaknesses in the defense system and propose specific countermeasures
- Use real and effective simulated attacks to evaluate the potential business impact caused by security issues, and provide effective data for security management to quantify the ROI of security investment.
- Improve a company's security maturity and its ability to detect and respond to attacks

Preliminary preparation
----------------------------------------
-Organizational chart
- Whole network topology map
- Logical structure diagram of each system
- Calling relationships between systems
- Data flow relationships
- Asset sorting
    - Core asset list
    - Business system assets
    - Equipment assets
    - Outsourcing/third-party service assets
    - Historical legacy assets
- Business asset information
    - Business system name
    - Business system type
    - Server type
    - Domain name/IP address
    - Service port
    - Version
    - System deployment location
    - Development framework
    - middleware
    - database
    - Responsible person
    - Maintenance staff
- Equipment asset information
    -Device name
    - Device version number
    - Firmware version number
    - IP address
    - Deployment location
    - Responsible person
    - Maintenance staff
- Outsourcing/third-party service asset information
    - Manufacturer contact information
    - System name
    - System type
    - IP/URL address
    - Deployment location
    - Responsible person
    - Maintenance staff
    - Manufacturer contact information
    - Third party duty personnel
- Risk sorting
    - Infrastructure risks
    - Account permission sorting
    - Internet risk investigation
    - Convergence of attack surface
- Emergency response plan
- Business continuity plan
- Disaster recovery plan

Action process
----------------------------------------
- Preparation for attack
    - Clarify the scope of authorization, test objectives, restrictions, etc.
    -Reporting and authorization process
    - Action costs and budgets
- Attack execution
    - Within the filing time range
    - Within the target range of registration
    - The registered attack IP and network environment
- attack completed
    - Revert all changes
    - Remove all persistence controls
    - Submit attack reports and improvement suggestions

Things to note
----------------------------------------
- Report before testing
- Communicate in advance if it may affect business operations
- Vulnerabilities and business communication will be confirmed before issuing work orders for repair.
- Vulnerability closed loop

Reference link
----------------------------------------
- `Use offense to promote defense, thoughts on building a blue army in enterprises <https://mp.weixin.qq.com/s/8iJs2ON66NY1Jdbt7c-BTA>`_
- `Offense and defense on the cloud: Red Teaming for Cloud <http://avfisher.win/archives/1175>`_
- `Guidelines for building an enterprise blue team for network attack and defense drills <https://www.freebuf.com/articles/neopoints/252229.html>`_
