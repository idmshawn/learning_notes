
# BIOS
### 简介
BIOS (**B**asic **I**nput/**O**utput **S**ystem) is the program a computer's microprocessor uses to start the computer system after it is powered on. It also manages data flow between the computer's operating system (OS) and attached devices, such as the hard disk, video adapter, keyboard, mouse and printer.

BIOS是电脑主板上的固件(firmware)，烧在EPROM(erasable programmable read-only memory)中(其它嵌入式系统中，也可能在FLASH或ROM中)。电脑上电后，CPU会从EPROM同一地址读取BIOS。
BIOS做完硬件启动及自检后，BIOS将操作系统从硬盘加载到RAM中。

### 功能
BIOS完成以下功能
- Power-on self-test (POST). This tests the hardware of the computer before loading the OS.
- Bootstrap loader. This locates the OS.
- Software/drivers. This locates the software and drivers that interface with the OS once running.
- Complementary metal-oxide semiconductor (CMOS) setup. This is a configuration program that enable users to alter hardware and system settings. CMOS is the name of BIOS' non-volatile memory.

### 参考文档
1. [BIOS (basic input/output system)](https://whatis.techtarget.com/definition/BIOS-basic-input-output-system)

# UEFI
### 简介
UEFI(**U**nified **E**xtensible **F**irmware **I**nterface)用来定义操作系统与系统固件之间的软件界面，作为BIOS的替代方案(Intel 2017年宣称，将从2020年起，使用UEFI替代传统电脑的BIOS)。

### 参考文档
1. [What Is UEFI, and How Is It Different from BIOS?](https://www.howtogeek.com/56958/htg-explains-how-uefi-will-replace-the-bios/)

# BootLoader
### 简介
The term “bootloader” is a shortened form of the words “bootstrap loader”.
BootLoader是在操作系统内核运行之前运行的一段小程序，是一种特殊的操作系统软件。
电脑上电启动后，BIOS先从外接存储(removable media: CD/DVD, USB stick, external hard drive, etc.)中找bootloader，一般会从[MBR(master boot record)](https://www.ionos.com/digitalguide/server/configuration/what-is-mbr/)中找到，并拉起bootLoader，随后启动操作系统。
[uBoot](https://www.denx.de/wiki/U-Boot/WebHome)便是一种可支持多种CPU架构的通用BootLoader。

### 功能
BootLoader作为硬件和操作系统的桥梁，完成以下功能：
1. Load the main memory;
2. Loads the kernel of the operating system;
3. Processes different routine tasks and commands, e.g. integrating data storage;


### 参考文档
1. [Bootloader: What you need to know about the system boot manager](https://www.ionos.com/digitalguide/server/configuration/what-is-a-bootloader/)
2. [uboot官网](https://www.denx.de/wiki/U-Boot/WebHome)
3. [uboot开源代码(github)](https://github.com/u-boot/u-boot)

