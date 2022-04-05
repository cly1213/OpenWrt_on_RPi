## wifi wireless setting

```
arp
 
cat /tmp/dhcp.leases

iwinfo wlan0 assoclist

iw wlan0 station dump | grep Station
```

## MCS (Modulation and Coding Scheme)

https://en.wikipedia.org/wiki/IEEE_802.11n-2009

https://mcsindex.com/

```
iw dev [wlan0] set bitrates ht-mcs-2.4 [10]
```
