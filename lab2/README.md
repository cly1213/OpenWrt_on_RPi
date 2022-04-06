## 802.11 Packet Analysis

https://en.wikipedia.org/wiki/802.11_Frame_Types

https://documentation.meraki.com/General_Administration/Tools_and_Troubleshooting/Analyzing_Wireless_Packet_Captures

https://praveenkumar4blog.wordpress.com/category/802-11-packet-analysis/

### Install tcpdump
```
opkg update
opkg install tcpdump
```

### /etc/config/wireless
Add

```
config wifi-iface
        option device 'radio2'
        option mode 'monitor'
``` 

### command 

```
uci commit wireless

wifi

iwinfo
```

```
root@OpenWrt:~# iwinfo
wlan0     ESSID: "y13601"
          Access Point: B8:27:EB:04:23:6E
          Mode: Client  Channel: 11 (2.462 GHz)
          Center Channel 1: 11 2: unknown
          Tx-Power: 31 dBm  Link Quality: 61/70
          Signal: -49 dBm  Noise: -91 dBm
          Bit Rate: 54.0 MBit/s
          Encryption: WPA PSK (TKIP)
          Type: nl80211  HW Mode(s): 802.11nac
          Hardware: 02D0:A9A6 0000:0000 [Generic MAC80211]
          TX power offset: unknown
          Frequency offset: unknown
          Supports VAPs: no  PHY name: phy0

wlan1     ESSID: unknown
          Access Point: 38:A2:8C:92:00:38
          Mode: Monitor  Channel: unknown (unknown)
          Center Channel 1: unknown 2: unknown
          Tx-Power: 20 dBm  Link Quality: unknown/70
          Signal: unknown  Noise: unknown
          Bit Rate: unknown
          Encryption: unknown
          Type: nl80211  HW Mode(s): 802.11bgn
          Hardware: unknown [Generic MAC80211]
          TX power offset: unknown
          Frequency offset: unknown
          Supports VAPs: yes  PHY name: phy1

wlan1-1   ESSID: "OpenWrt_Leo"
          Access Point: 38:A2:8C:92:00:39
          Mode: Master  Channel: 1 (2.412 GHz)
          Center Channel 1: 1 2: unknown
          Tx-Power: 20 dBm  Link Quality: 55/70
          Signal: -55 dBm  Noise: unknown
          Bit Rate: 52.0 MBit/s
          Encryption: WPA2 PSK (CCMP)
          Type: nl80211  HW Mode(s): 802.11bgn
          Hardware: unknown [Generic MAC80211]
          TX power offset: unknown
          Frequency offset: unknown
          Supports VAPs: yes  PHY name: phy1

```

### Capture
```
tcpdump -ne -y ieee802_11_radio -i wlan1

tcpdump -ne -y ieee802_11_radio -i wlan1 -w capture_dump

time tcpdump -ne -y ieee802_11_radio -i wlan1 | grep 38:a2:8c:92:00:39
```

```
root@OpenWrt:~# tcpdump -ne -y ieee802_11_radio -i wlan1 -w capture_dump
tcpdump: data link type ieee802_11_radio
tcpdump: listening on wlan1, link-type IEEE802_11_RADIO (802.11 plus radiotap header), capture size 262144 bytes
^C1241 packets captured
1286 packets received by filter
0 packets dropped by kernel
```
