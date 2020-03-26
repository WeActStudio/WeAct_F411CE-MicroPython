# WeAct STM32F411 Core Board

## How to build 如何编译 ubuntu/Win10内置linux

```
git clone https://github.com/micropython/micropython.git
cd micropython
git submodule update --init
cd mpy-cross
make -j4
cd ../ports/stm32/boards
git clone https://github.com/WeActTC/WeAct_F411CE.git
cd ..
# CROSS_COMPILE 修改为自己的编译器路径
# CROSS_COMPILE Change to your own compiler path
make BOARD=WeAct_F411CE CROSS_COMPILE=/mnt/e/MCU/tools/gcc-arm-none-eabi-8-2018-q4-major/bin/arm-none-eabi- -j4
# or 或者
make BOARD=WeAct_F411CE -j4
```
## mpconfigboard.h
```
/* BOARD Ver 2.0 set 1 ，other set 0 ex.V1.3,V2.1 */
#define VERSION_V20 (1)

/* 使用内置flash改1 使用外置flash改0 */
/* Use the built-in flash to change to 1 
   use the external flash to change to 0 */
#define MICROPY_HW_ENABLE_INTERNAL_FLASH_STORAGE (1)
```

![STM32F4X1 V2.0+](https://github.com/WeActTC/MiniF4-STM32F4x1/raw/master/images/STM32F4x1-V22-3D.jpg "STM32F4X1 V2.0+")