# MR200v4 support for OpenWrt notes

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
