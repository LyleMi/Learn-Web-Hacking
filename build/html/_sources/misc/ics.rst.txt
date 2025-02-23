Industrial control safety
========================================

Introduction
----------------------------------------
Industrial control security, that is, industrial control system security, is an important branch of network security. It mainly focuses on the security of industrial control systems and their data to ensure that normal industrial production is not affected.

Industrial Control System (ICS) includes fieldbus control system (FCS, Fieldbus Control System), monitoring and data acquisition system (SCADA, Supervisory Control and Data Acquisition), etc., which are widely used in energy supply, manufacturing, and scientific research. , navigation industry and autonomous driving in automobiles.

Communication Protocol
----------------------------------------
In addition to commonly used network protocols, the industrial control system also uses MODBUS, CAN and other protocols to communicate.

MODBUS is a serial communication protocol suitable for connecting different types of devices. It adopts a master-slave structure, each slave device has an independent address, and the master station can communicate with the slave station through reading and writing registers. The MODBUS protocol is simple and easy to use, high reliability and strong flexibility, and is widely used in various automated control systems.

The CAN (Controller Area Network) bus is a widely used control network, which is commonly used in automotive and industrial control fields. It adopts a multi-main structure, and all devices are located on the same bus. The CAN bus communication speed is high and has good real-time performance. The CAN bus was originally designed as a microcontroller communication in the automotive environment, exchanging information between the electronic control devices ECUs on the vehicle, forming an automotive electronic control network.

Reference link
----------------------------------------
- `awesome industrial control system security <https://github.com/hslatman/awesome-industrial-control-system-security>`_
