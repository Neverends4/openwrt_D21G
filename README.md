# openwrt_D21G

Adding dts and necessary files to support **Mercury D21G** router in openwrt

For personal record usage. If you bumped into this repo and want to use the patch, some hints below:

1. This patch only applies to **Mercury D21G**, an 802.11ac router with MT7621 CPU, MT7603N+MT7611EN wireless chips, 8M NOR ROM and 128M DDR3 RAM.
  
2. To flash openwrt on this router you need some knowledge on building openwrt, flashing SOP and building EEPROM, this is not for a faint of heart or a newbie, **YOU HAVE BEEN WARNED**.
  
3. There is no known bugs to exploit for enabling ssh with factory firmware, not that I know of at least. So to flash openwrt you need to tear down the unit, buy an SOP8 test clip and program the famous breed bootloader onto the ROM.
  
4. The breed to use is named **breed-mt7621-xunlei-timeplug.bin**
  
5. You need to backup factory firmware image of 8 MB using breed, and extract and build a 64k EEPROM compatible with openwrt, search online if you have no idea what it is.
  
  Mapping of EEPROM data between factory (0x7FFFFF) <--> 64k (0x10000) EEPROM:
  
  2.4G wifi art
  
  0x1E000,0x1E3FF <--> 0x0000,0x03FF
  
  5G wifi art
  
  0x1F000,0x1F3FF <--> 0x8000,0x83FF
  
  2.4G and 5G mac address
  
  0x1D80D, 0x1D80D value +2 <--> 0x4,0x8004
  
6. Only tested on the official openwrt 21.02 source code.
  

Do it at your own risk, no guarantee from me.

Usage:

Download the patch file to your local PC, openwrt 21.02 source code should be ready beforehand.

Apply the patch and compile.

`git am < D21G.patch`

`make menuconfig`

`make -j$(($(nproc) + 1)) V=s`
