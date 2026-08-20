Wi-Fi
========================================

Introduction
----------------------------------------
Wi-Fi, also known as "wireless hotspot" or "wireless network", is a trademark of the Wi-Fi Alliance, a wireless LAN technology based on the IEEE 802.11 standard.

attack
----------------------------------------

Brute force cracking
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
WiFi passwords are based on preset secret keys, and password blasting attempts can be quickly performed locally and in batches by capturing messages.

fake hotspot
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
APs can dynamically broadcast themselves, and clients can also proactively send probe requests. The AP can be forged to send a response packet to the probe request to allow the client to misidentify it.

Key reinstallation attack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The vulnerability was discovered by Vanhoef. Wi-Fi will update the secret key during the handshake. This attack replays the handshake information to cause the client to reinstall the same secret key.

Dragonblood
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The latest version of the WPA3 standard has some implementation problems, which were also discovered by Vanhoef. Including denial of service attacks, downgrade attacks, side channel leaks, etc.

Reference link
----------------------------------------
- `Wi-Fi Alliance <https://www.wi-fi.org/>`_
- `Dragonblood <https://papers.mathyvanhoef.com/dragonblood.pdf>`_ : Analyzing the Dragonfly Handshake of WPA3 and EAP-pwd
- `Improving Privacy through Fast Passive Wi-Fi Scanning <https://papers.mathyvanhoef.com/nordsec2019.pdf>`_
- `Practical Side-Channel Attacks against WPA-TKIP <https://papers.mathyvanhoef.com/asiaccs2019.pdf>`_
- `Key Reinstallation Attacks: Breaking the WPA2 Protocol <https://papers.mathyvanhoef.com/blackhat-eu2017.pdf>`_
- `RFC 7664 Dragonfly Key Exchange <https://tools.ietf.org/html/rfc7664>`_
