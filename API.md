# Core

This part describes the STM32 core functions.

## core_callback.c

CoreCallback functions allows to register a callback function called in the loop of the main() function.  
If you need to call as often as possible a function to update your system and you want to be sure this function to be called, you can add it to the callback list. Otherwise, your function should be called inside the loop() function of
the sketch.

* **void registerCoreCallback(void (*func)(void))**: register a callback function  
_Params_ func pointer to the callback function  

* **void unregisterCoreCallback(void (*func)(void))**: unregister a callback function  
_Params_ func pointer to the callback function  