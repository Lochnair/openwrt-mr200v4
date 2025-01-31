# MR200v4 support for OpenWrt notes
### See the [mr200v4](https://github.com/Lochnair/openwrt/tree/mr200v4) branch on my OpenWrt repo for the code

## HW
* Soc: MT7628
* CPU freq: 580 MHZ
* RAM: 64 MB
* Flash: 8 MB W25Q64BV
* Modem: (?) (based on MDM9207 Soc)

## Status
* Installation: ✓
* Buttons: ✓
* LEDs: ✓
* Ethernet: ✓
* WLAN 2.4GHz: ✓
* WLAN 5GHz: ✓
* LTE Modem: ✕

## Installation
Easiest way of installation on OpenWrt is by using the TFTP recovery in U-Boot.
* Set your computers IP address to 192.168.0.225
* Copy the openwrt-ramips-mt76x8-ArcherMR200v4-squashfs-tftp-recovery.bin to your TFTP server root folder with the name `tp_recovery.bin`.
* Hold the reset button while you power up the device (keep it pressed for approx 10 sec).
* The device will write the image to flash and boot it.

## Revert to stock
Reverting to stock is relatively simple on this device. We must however cut out only the part we need from the stock FW image for U-Boot it to work. Luckily, unlike the MR200v1, the v4 does *not* flash the U-Boot partition with TFTP recovery. Therefore we only need to to this:
```
dd if='LTE_GATEWAYv3_1.6.0_0.9.1_up_boot(181022)_12.04.23.bin' of=tp_recovery.bin bs=512 skip=1 count=15616
```
Now follow the usual steps for TFTP recovery as described in [Installation](https://github.com/Lochnair/openwrt-mr200v4#installation).

## TFTP recovery
U-Boot runs the following commands when the reset button is held for 10-ish seconds upon boot:
```
set serverip 192.168.0.225
tftp 0x80060000 tp_recovery.bin
erase tplink 0x20000 0x7a0000
cp.b 0x80080000 0x20000 0x7a0000
reset
```


## Modem
I've gotten the modem to at least respond to uqmi commands by applying the SET_DTR quirk in the qmi_wwan driver. However I have not gotten it to connect, and commands can still just stall. The furthest I've gotten is to get it to search for a tower.

## UART shell login
* Username: admin
* Password: 1234

## GPL source
https://static.tp-link.com/resources/gpl/Archer_MR200V4_GPL.tar.gz

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
|  Name        |  GPIO | Polarity   |
|--------------|-------|------------|
| WLAN LED     | 4     | Active low |
| LAN LED      | 5     | Active low |
| Reset button | 38    | Active low |
| Power LED    | 39    | Active low |
| WAN LED      | 40    | Active low |
| Signal low   | 41    | Active low |
| Signal med   | 42    | Active low |
| Signal high  | 43    | Active low |
| WLAN button  | 46    | Active low |

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
