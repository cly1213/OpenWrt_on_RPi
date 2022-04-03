# OpenWrt_on_RPi  
## OpenWrt
https://openwrt.org/

## Turn Raspberry Pi into Router with OpenWrt
<img src="https://github.com/cly1213/OpenWrt_on_RPi/blob/main/Picture1.png"/>

```
BusyBox v1.33.2 (2022-02-16 20:29:10 UTC) built-in shell (ash)

  _______                     ________        __
 |       |.-----.-----.-----.|  |  |  |.----.|  |_
 |   -   ||  _  |  -__|     ||  |  |  ||   _||   _|
 |_______||   __|_____|__|__||________||__|  |____|
          |__| W I R E L E S S   F R E E D O M
 -----------------------------------------------------
 OpenWrt 21.02.2, r16495-bf0c965af0
 -----------------------------------------------------
=== WARNING! =====================================
There is no root password defined on this device!
Use the "passwd" command to set up a new password
in order to prevent unauthorized SSH logins.
--------------------------------------------------
root@OpenWrt:~#
```

```
root@OpenWrt:~# ls /etc/config/
dhcp             firewall.bk      network.bk       rpcd             uhttpd
dropbear         luci             openvpn          system           wireless
firewall         network          openvpn_recipes  ucitrack         wireless.bk
```

## Hardware
- Raspberry Pi 
- wifi adapter
  - MT7601 (doesn't support AP mode)
  - RT5370 (it works!)
- usb ethernet adapter
- ethernet cable
- PC(Windows)

## Firmware
https://openwrt.org/toh/raspberry_pi_foundation/raspberry_pi

## config

```
root@OpenWrt:~# ls /etc/config/
dhcp             firewall.bk      network.bk       rpcd             uhttpd
dropbear         luci             openvpn          system           wireless
firewall         network          openvpn_recipes  ucitrack         wireless.bk
```

### network
### firewall
### wireless

## command
```
$ lsusb

$ ifconfig wlan1 up

$ uci commit wireless

$ wifi
```

## ifconfig
```
root@OpenWrt:~# ifconfig
br-lan    Link encap:Ethernet  HWaddr B8:27:EB:51:76:3B
          inet addr:10.71.71.1  Bcast:10.71.71.255  Mask:255.255.255.0
          inet6 addr: fe80::ba27:ebff:fe51:763b/64 Scope:Link
          inet6 addr: fd59:46fa:8f0f::1/60 Scope:Global
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9784 errors:0 dropped:0 overruns:0 frame:0
          TX packets:15794 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:1095090 (1.0 MiB)  TX bytes:19044540 (18.1 MiB)

eth0      Link encap:Ethernet  HWaddr B8:27:EB:51:76:3B
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9784 errors:0 dropped:0 overruns:0 frame:0
          TX packets:15794 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:1232066 (1.1 MiB)  TX bytes:19044540 (18.1 MiB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:52 errors:0 dropped:0 overruns:0 frame:0
          TX packets:52 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:5649 (5.5 KiB)  TX bytes:5649 (5.5 KiB)

wlan0     Link encap:Ethernet  HWaddr B8:27:EB:04:23:6E
          inet addr:192.168.1.113  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::ba27:ebff:fe04:236e/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:15641 errors:0 dropped:0 overruns:0 frame:0
          TX packets:9342 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:18807992 (17.9 MiB)  TX bytes:1380188 (1.3 MiB)
```

```
root@OpenWrt:~# opkg install kmod-mt7601u
```

```
root@OpenWrt:~# ifconfig wlan1 up
root@OpenWrt:~# ifconfig
br-lan    Link encap:Ethernet  HWaddr B8:27:EB:51:76:3B
          inet addr:10.71.71.1  Bcast:10.71.71.255  Mask:255.255.255.0
          inet6 addr: fe80::ba27:ebff:fe51:763b/64 Scope:Link
          inet6 addr: fd59:46fa:8f0f::1/60 Scope:Global
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9913 errors:0 dropped:0 overruns:0 frame:0
          TX packets:15893 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:1108198 (1.0 MiB)  TX bytes:19058317 (18.1 MiB)

eth0      Link encap:Ethernet  HWaddr B8:27:EB:51:76:3B
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9913 errors:0 dropped:0 overruns:0 frame:0
          TX packets:15893 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:1246980 (1.1 MiB)  TX bytes:19058317 (18.1 MiB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:52 errors:0 dropped:0 overruns:0 frame:0
          TX packets:52 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:5649 (5.5 KiB)  TX bytes:5649 (5.5 KiB)

wlan0     Link encap:Ethernet  HWaddr B8:27:EB:04:23:6E
          inet addr:192.168.1.113  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::ba27:ebff:fe04:236e/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:15686 errors:0 dropped:0 overruns:0 frame:0
          TX packets:9394 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:18813983 (17.9 MiB)  TX bytes:1390542 (1.3 MiB)

wlan1     Link encap:Ethernet  HWaddr 1C:BF:CE:70:4D:7C
          UP BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

root@OpenWrt:~#
```

## Ref
https://elinux.org/RPi_USB_Wi-Fi_Adapters

## Test
RT5572
RT3070
MT7612U

