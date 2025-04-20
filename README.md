# ZLT-S12-Pro-Openwrt-Builds
Tozed S12 Plus (UNISOC) OpenWrt Test Builds


# Notice 
# ⚠️ Do anything at your own risk.
# ⚠️ I am not responsible for any router bricking cases.


Here's an OpenWrt test build for the Tozed S12 Plus (UNISOC) aka ZLT S12 Pro.

DISCLAIMER: Please note that I'm providing these builds WITHOUT WARRANTY OR SUPPORT. FLASH AT YOUR OWN RISK, I TAKE NO RESPONSIBILITY IF IT BREAKS YOUR DEVICE. (I have already flashed these in mine before I made it available.)

It is already implied that if you flash this, then you are also comfortable with unbricking the device, should anything go wrong. I'm providing these builds to aid in getting the modem fully supported in vanilla OpenWrt. If you find something is not working concerning the builds, then let me know and I'll see what I can do. For other inquiries like 'how do I install this <package>, how do I configure for <anything>...' then Google and the countless other forums are your bestfriends for those.

Now this doesn't come totally without support, and here are somethings you need to remember, so PLEASE READ CAREFULLY:

1. The unit can be directly flashed via sysupgrade. :D

2. In case you want to return to stock, then it is easy to do so via firmware dump restoration. This assumes that you have already taken a dump of the mtd3 partition of your unit from stock. Upload the dump via scp or whatever to /tmp, then run
```
mtd -r write /tmp/<filename> /dev/mtd3 # replace <filename>
```

3. I and many others would appreciate it if you can help get the WWAN module in this unit supported in OpenWrt. ;)

4. You can install packages from snapshot, or the 22.03-rc5 release, PROVIDED that the package you are installing DOES NOT INSTALL KERNEL MODULES. Those kernel modules would need to be integrated into my test builds. I have included kmod-wireguard for wireguard (installed) and kmod-tun for openvpn (not-installed). It will be much better if you install from the 22.03-rc5 release as this snapshot is a couple of commits ahead of 22.03-rc5 when it was branched off and tagged as rc5.

5. I have converted LAN1 on this unit into WAN, so you can use it as a router.

6. With this test build, it is based on vanilla OpenWrt. So apart from a very basic network setup of involving LAN and WAN, and disabled wireless interfaces, you will have to setup everything on your own. THIS IS NOT FOR THE FAINT OF HEART. You will need to put in your work, as I have put in mine into getting this unit supported under mainline OpenWrt. You will have to consult online documentation, or make your own researches, to do what it is you wish to do, you can start here: Documentation (https://openwrt.org/docs/start)

7. I have mentioned before that with the migration from stock firmware to OpenWrt, open-source wireless drivers are now available. It brings in Wi-Fi Wave2, WPA3, 802.11r (band-steering), and Mesh Wi-Fi improvements, to name a few. Have fun learning and getting these technologies to work within your network setup. Say goodbye to unstable 2.4GHz wireless.

I have already submitted patches in upstream OpenWrt. Let's wait until it is accepted, then it will be available for download from the site.

Without further ado, here's how you install OpenWrt:

Stock firmware runs an old OpenWrt SNAPSHOT release. Installation can be either via

a) sysupgrade (gain root shell access, run 'sysupgrade -n -F <sysupgrade.bin>'), or
b) tftpboot in the bootloader.

Instructions below are for b). Connect the USB-TTL serial converter as follows when facing the board upright on the side of the buttons and RJ45 ports, located under the WPS/Wi-Fi buttons from left to right:

(TX) (GND) (RX)

Baud rate is 115200.

1. Connect the computer to the device via ethernet cable. Set a static adddress of 10.10.10.3/24 to the wired interface.
2. Start the TFTP server, point it to where the initramfs image is located. Rename the image to 'test.bin'.
3. Turn on the device. There will be a three-second delay before the default 'Boot system code via flash' is selected.
4. Interrupt the boot process by pressing 1 to 'System Load Linux to SDRAM via TFTP'.
5. Press enter to accept the default 'Input device IP (10.10.10.123)'.
6. Press enter to accept the default 'Input server IP (10.10.10.3)'.
7. Press enter to accept the default 'Input Linux Kernel filename ()', or enter 'test.bin'.
8. Wait for the initramfs image to finish loading.
9. Reconnect the wired interface to any LAN ports of the device via DHCP.
9. Flash the sysupgrade image at http://192.168.1.1/cgi-bin/luci/admin/system/flash

Initramfs:https://github.com/speedforce-demo/ZLT-S12-Pro-Openwrt-Builds/raw/main/openwrt-ramips-mt7621-tozed_s12-unisoc-plus-initramfs-kernel.bin

Sysupgrade:https://github.com/speedforce-demo/ZLT-S12-Pro-Openwrt-Builds/raw/main/openwrt-ramips-mt7621-tozed_s12-unisoc-plus-squashfs-sysupgrade.bin


This is not My work , Original Work : https://phcorner.net/threads/tozed-s12-plus-unisoc-openwrt-test-builds.1428085/


<img src="https://github.com/speedforce-demo/ZLT-S12-Pro-Openwrt-Builds/blob/main/_20220720_201638.JPG?raw=true">
