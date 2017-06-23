# NativeEthernet library

The NativeEthernet library allows an STM32 board to connect to the internet.  
It is based on the Ethernet library provides by Arduino.  
This library is fully compatible with Arduino Ethernet library.  
Examples allow a quickstart.  

## Requirement

This library could only be used with STM32 board with Ethernet compatibility.  
Ex: NUCLEO-F429ZI

## Note

* The library is based on LwIP, a Lightweight TCP/IP stack.  
<http://git.savannah.gnu.org/cgit/lwip.git>  
<http://lwip.wikia.com/wiki/LwIP_Wiki>  

* EthernetClass::maintain() in no more required to renew IP address from DHCP.  
It is done automatically by the LwIP stack in a background task.  

* An Idle task is required to handle the LwIP timers and data reception. 
Be careful to not lock the system in a loop where LwIP could never be updated.  
Call EthernetUDP::parsePacket() or EthernetClient::available() performs an update of the LwIP stack.
