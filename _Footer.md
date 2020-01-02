If you need to install STM32CubeProgrammer in another directory under Linux, the above mentioned procedure did not work for me.

I had to enable compilation and upload verbose under File->Preferences. Then compile+ upload to see the this script was been called
`/home/username/.arduino15/packages/STM32/tools/STM32Tools/1.3.2/tools/linux/stm32CubeProg.sh`.

Then I had to replace line 44 (commented) by my actual path. 
```
  command -v $STM32CP_CLI >/dev/null 2>&1
  if [ $? != 0 ]; then
    #export PATH="$HOME/STMicroelectronics/STM32Cube/STM32CubeProgrammer/bin":$PATH    
    export PATH="/opt/STM32Cube/STM32CubeProgrammer/bin":$PATH
  fi
```

for some reason, this script ignores the PATH variable I set pointing to `/opt/STM32Cube/STM32CubeProgrammer/bin`. For these reason this hack was necessary.

Alexandre 
