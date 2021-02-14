# WeAct Studio STM32F411CEU6 核心板

* [English Version](./README.md)

## Important note

If there is no `WeAct` and `version number` on the back of the board, the chip batch is `537` or old, the stitches and board are packaged in one bag, `the board screen printing is wrong`(`3V3` is going to be labeled `V3V`), it is definitely pirated.Please comment on issues or let us know by email (WeAct_TC@163.com).

## 如何编译micropython 需使用linux (ubuntu或Win10企业版linux子系统)

不建议自己编译固件，使用我们提供的固件即可，如确实需要编译，请自备linux基础使用知识，以下均为linux下的操作

``` sh
git clone https://github.com/micropython/micropython.git
cd micropython
git submodule update --init
cd mpy-cross
make -j4
cd ../ports/stm32/boards
git clone https://github.com/WeActTC/WeAct_F411CE-MicroPython.git WeAct_F411CE
cd ..
make BOARD=WeAct_F411CE CROSS_COMPILE=/mnt/e/MCU/tools/gcc-arm-none-eabi-8-2018-q4-major/bin/arm-none-eabi- -j
# 或者
make BOARD=WeAct_F411CE -j
```

> 注意：CROSS_COMPILE 修改为自己的编译器路径

## mpconfigboard.h 相应修改

``` c
/* 板子版本为 V2.0 设置为 1 ，其他设置为 0 例如.V1.3,V2.1 V3.0 */
#define VERSION_V20 (1)

/* 使用内置flash改1 使用外置flash改0 */
#define MICROPY_HW_ENABLE_INTERNAL_FLASH_STORAGE (1)

// Flash Size:
// 4MB Flash 32Mbit
// 8MB Flash 64Mbit
// 16MB Flash 128Mbit
#define MICROPY_HW_SPIFLASH_SIZE_BITS (32 * 1024 * 1024)
```

SPI FLASH:

``` c
#define MICROPY_HW_SPIFLASH_CS      (pin_A4)
#define MICROPY_HW_SPIFLASH_SCK     (pin_A5)
#if VERSION_V20
 #define MICROPY_HW_SPIFLASH_MISO    (pin_B4)
#else
 #define MICROPY_HW_SPIFLASH_MISO    (pin_A6)
#endif
#define MICROPY_HW_SPIFLASH_MOSI    (pin_A7)
```
