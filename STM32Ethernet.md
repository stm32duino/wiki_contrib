# STM32Ethernet library

The STM32Ethernet library allows an STM32 board to connect to the internet.  
It is based on the Ethernet library provides by Arduino.  
This library is fully compatible with Arduino Ethernet library (https://www.arduino.cc/en/Reference/Ethernet).  
Examples allow a quickstart.  

## Requirement

This library could only be used with STM32 board with Ethernet compatibility.  
Ex: 
- NUCLEO-F429ZI
- STM32F746G-DISCOVERY

The LwIP library must be installed to use the STM32Ethernet library.

## Installation
Both libraries are available through the Arduino Libraries manager.<br>
Click on "**Sketch**" menu and then "**Include Library > Manage Libraries...**"<br>
Search "_LwIP_" then install "**_LwIP_**" and "**_STM32Ethernet_**"

## Note

* The library is based on LwIP, a Lightweight TCP/IP stack.  
<http://git.savannah.gnu.org/cgit/lwip.git>  
<http://lwip.wikia.com/wiki/LwIP_Wiki>  

* EthernetClass::maintain() in no more required to renew IP address from DHCP.  
It is done automatically by the LwIP stack in a background task.  

* An Idle task is required by the LwIP stack to handle timer and data reception.  
This idle task is called inside the main loop in background by the function stm32_eth_scheduler().  
Be careful to not lock the system inside the function loop() where LwIP could never be updated.  
Call EthernetUDP::parsePacket() or EthernetClient::available() performs an update of the LwIP stack.  

## Source

STM32Ethernet  
https://github.com/stm32duino/STM32Ethernet  

LwIP  
https://github.com/stm32duino/LwIP  
