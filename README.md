# MR200v4 support for OpenWrt notes

## HW
Soc: MT7628
CPU freq: 580 MHZ
RAM: 64 MB
Flash: 8 MB W25Q64BV


## MTD
```
Creating 6 MTD partitions on "raspi":
0x000000000000-0x000000020000 : "boot"
0x000000020000-0x000000160000 : "kernel"
0x000000160000-0x0000007d0000 : "rootfs"
mtd: partition "rootfs" set to be root filesystem
0x0000007d0000-0x0000007e0000 : "config"
0x0000007e0000-0x0000007f0000 : "romfile"
0x0000007f0000-0x000000800000 : "radio"
```

## GPIO
```
gpiomode1 55154404.
gpiomode2 05550555.
######GPIO CTRL 0 for GPIO 0~31 OUTPUT tmp(0x00000030)#####
######GPIO CTRL 1 for GPIO 32~64 OUTPUT tmp(0x00000f80)#####
######GPIO CTRL 1 for GPIO 32~64 INPUT tmp(0x00000f80)#####
```

## Available U-Boot commands
```
MT7628 # help
?       - alias for 'help'
base    - print or set address offset
bdinfo  - print Board Info structure
bootm   - boot application image from memory
bootp	- boot image via network using BootP/TFTP protocol
coninfo - print console devices and information
cp      - memory copy
crc32   - checksum calculation
erase   - erase SPI FLASH memory
go      - start application at address 'addr'
help    - print online help
loadb   - load binary file over serial line (kermit mode)
loop    - infinite loop on address range
md      - memory display
mdio   - Ralink PHY register R/W command !!
mm      - memory modify (auto-incrementing)
mtest   - simple RAM test
nm      - memory modify (constant address)
printenv- print environment variables
rarpboot- boot image via network using RARP/TFTP protocol
reset   - Perform RESET of the CPU
rf      - read/write rf register
saveenv - save environment variables to persistent storage
setenv  - set environment variables
sleep   - delay execution for some time
spi	- spi command
tftpboot- boot image via network using TFTP protocol
version - print monitor version
```

## U-Boot env
```
MT7628 # printenv
bootcmd=tftp
bootdelay=1
baudrate=115200
ethaddr="00:0A:EB:13:09:69"
ipaddr=192.168.0.2
serverip=192.168.0.225
stdin=serial
stdout=serial
stderr=serial
```

# U-Boot board info structure
```
MT7628 # bdinfo
boot_params = 0x83F53FB0
memstart    = 0x80000000
memsize     = 0x04000000
flashstart  = 0x00000000
flashsize   = 0x00800000
flashoffset = 0x00000000
ethaddr     = 00:00:0A:EB:13:09
ip_addr     = 192.168.0.2
baudrate    = 115200 bps
```
