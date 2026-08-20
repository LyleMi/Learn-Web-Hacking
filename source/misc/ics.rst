Industrial control safety
========================================

Introduction
----------------------------------------
Industrial control security, that is, industrial control system security, is an important branch of network security. It mainly focuses on the security of industrial control systems and their data to ensure that normal industrial production is not affected.

Industrial Control System (ICS) includes Fieldbus Control System (FCS), Supervisory Control and Data Acquisition (SCADA), etc., which are widely used in energy supply, manufacturing, scientific research, navigation, and autonomous vehicle driving.

Communication protocol
----------------------------------------
In addition to commonly used network protocols, industrial control systems also use MODBUS, CAN and other protocols for communication.

MODBUS is a serial communication protocol suitable for connecting different types of devices. It adopts a master-slave structure. Each slave device has an independent address. The master station can communicate with the slave station by reading and writing registers. The MODBUS protocol has the characteristics of simplicity, ease of use, high reliability, and strong flexibility, and is widely used in various automation control systems.

CAN (Controller Area Network) bus is a widely used control network, often used in the automotive and industrial control fields. It adopts a multi-master structure, and all devices are located on the same bus. CAN bus communication speed is high and has good real-time performance. The CAN bus was originally designed as a microcontroller communication in the automotive environment to exchange information between various electronic control devices ECU in the vehicle to form an automotive electronic control network.

Reference link
----------------------------------------
- `awesome industrial control system security <https://github.com/hslatman/awesome-industrial-control-system-security>`_
