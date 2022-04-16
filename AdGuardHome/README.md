# AdGuard Home

https://github.com/AdguardTeam/AdGuardHome

https://openwrt.org/toh/views/toh_extended_all

https://kb.adguard.com/en/general/dns-providers

## Install
```
opkg update && opkg install wget
mkdir /opt/ && cd /opt
wget -c https://static.adguard.com/adguardhome/beta/AdGuardHome_linux_arm64.tar.gz
tar xfvz AdGuardHome_linux_arm64.tar.gz
rm AdGuardHome_linux_arm64.tar.gz

/opt/AdGuardHome/AdGuardHome 
```

```
vim /etc/rc.local

#Add /opt/AdGuardHome/AdGuardHome
```

### ref
https://www.youtube.com/watch?v=yMcM40ipDlQ&ab_channel=VanTechCorner
