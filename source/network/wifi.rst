In
========================================

Introduction
----------------------------------------
Wi-Fi, also known as "wireless hotspot" or "wireless network", is a trademark of the Wi-Fi alliance, a wireless LAN technology based on the IEEE 802.11 standard.

attack
----------------------------------------

Brute force cracking
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
WiFi passwords are based on preset keys, and password blasting can be attempted locally in batches by crawling packets.

Fake hot spots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
AP can broadcast itself dynamically, and customers can also actively send probe requests. It can be forged that the AP sends a response packet to the probe request to allow the client to identify the error.

Key Reinstall Attack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The vulnerability was discovered by Vanhoef. Wi-Fi will update the key when shaking hands. This attack replays the handshake information and causes the client to reinstall the same key.

Dragonblood
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The latest version of WPA3 standard has some problems in implementation, which was also discovered by Vanhoef. Including denial of service attacks, downgrade attacks, side channel leakage, etc.

Reference link
----------------------------------------
- `Wi-Fi Alliance <https://www.wi-fi.org/>`_
- `Dragonblood <https://papers.mathyvanhoef.com/dragonblood.pdf>`_ : Analyzing the Dragonfly Handshake of WPA3 and EAP-pwd
- `Improving Privacy through Fast Passive Wi-Fi Scanning <https://papers.mathyvanhoef.com/nordsec2019.pdf>`_
- `Practical Side-Channel Attacks against WPA-TKIP <https://papers.mathyvanhoef.com/asiaccs2019.pdf>`_
- `Key Reinstallation Attacks: Breaking the WPA2 Protocol <https://papers.mathyvanhoef.com/blackhat-eu2017.pdf>`_
- `RFC 7664 Dragonfly Key Exchange <https://tools.ietf.org/html/rfc7664>`_
