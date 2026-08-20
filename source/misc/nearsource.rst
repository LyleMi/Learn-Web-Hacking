near source penetration
========================================

USB attack
----------------------------------------

BadUSB
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
By reprogramming the USB device's internal microcontroller, it can perform malicious operations, such as registering as a keyboard device and sending specific keystrokes to perform malicious operations.

AutoRUN
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Depending on how the host is configured, some operating systems will automatically execute scheduled files located on the USB device's memory. Malware can be executed in this way.

USB Killer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Permanently destroy the device electrically via a special USB device.

side channel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Add some monitoring/testing channel transmission equipment by modifying USB.

HID attack
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
HID (human interface device) refers to human-computer interaction devices such as keyboards and mice used to provide data input for computers. HID attacks refer to attackers simulating a special USB device as a keyboard and performing predetermined malicious operations once connected to the computer. HID attacks can be implemented based on Android devices, data line devices, etc.

Wi-Fi
----------------------------------------

Password blasting
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Based on the WPA2 authentication method, Wi-Fi can conduct offline password blasting by grabbing handbags.

signal suppression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Man-in-the-middle attacks can be achieved by using powerful devices to capture handshake packets and impersonate the target AP.

access control
----------------------------------------

electromagnetic pulse
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The integrated circuits in the electronic systems of some electronic access control and electronic code locks are sensitive to electromagnetic pulses, and the device can be destroyed by applying electromagnetic pulse (EMP) to achieve the opening effect.

IC card
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Devices such as Chameleon can use simulated, cracked, and copied IC cards to crack access control.

Reference link
----------------------------------------
- `Near Source Penetration Hardware Guide <https://www.secpulse.com/archives/123723.html>`_
- `Red and Blue Confrontation: Near Source Penetration <https://mp.weixin.qq.com/s/dmh3dDt0BaZYIcWdSTsQcg>`_
