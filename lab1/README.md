## Scheduling & QoS

Packet Scheduler, Queueing Discipline(QDisc)

https://openwrt.org/docs/guide-user/network/traffic-shaping/packet.scheduler.theory

https://openwrt.org/docs/guide-user/network/traffic-shaping/packet.scheduler

### Install
```
opkg update
opkg install tc iptables-mod-ipopt
```
### Command
```
tc qdisc show

tc -s qdisc show dev eth0
```

```
root@OpenWrt:~# tc qdisc show
qdisc noqueue 0: dev lo root refcnt 2
qdisc fq_codel 0: dev eth0 root refcnt 2 limit 10240p flows 1024 quantum 1522 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64
qdisc fq_codel 0: dev wlan0 root refcnt 2 limit 10240p flows 1024 quantum 1514 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64
qdisc noqueue 0: dev br-lan root refcnt 2
qdisc mq 0: dev wlan1 root
qdisc fq_codel 0: dev wlan1 parent :4 limit 10240p flows 1024 quantum 1514 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64
qdisc fq_codel 0: dev wlan1 parent :3 limit 10240p flows 1024 quantum 1514 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64
qdisc fq_codel 0: dev wlan1 parent :2 limit 10240p flows 1024 quantum 1514 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64
qdisc fq_codel 0: dev wlan1 parent :1 limit 10240p flows 1024 quantum 1514 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64

root@OpenWrt:~# tc qdisc add dev wlan0 root handle 1: htb default 20

root@OpenWrt:~# tc qdisc show
qdisc noqueue 0: dev lo root refcnt 2
qdisc fq_codel 0: dev eth0 root refcnt 2 limit 10240p flows 1024 quantum 1522 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64
qdisc htb 1: dev wlan0 root refcnt 2 r2q 10 default 0x20 direct_packets_stat 13 direct_qlen 1000
qdisc noqueue 0: dev br-lan root refcnt 2
qdisc mq 0: dev wlan1 root
qdisc fq_codel 0: dev wlan1 parent :4 limit 10240p flows 1024 quantum 1514 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64
qdisc fq_codel 0: dev wlan1 parent :3 limit 10240p flows 1024 quantum 1514 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64
qdisc fq_codel 0: dev wlan1 parent :2 limit 10240p flows 1024 quantum 1514 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64
qdisc fq_codel 0: dev wlan1 parent :1 limit 10240p flows 1024 quantum 1514 target 5ms interval 100ms memory_limit 4Mb ecn drop_batch 64

root@OpenWrt:~# tc -s qdisc show dev wlan0
qdisc htb 1: root refcnt 2 r2q 10 default 0x20 direct_packets_stat 88 direct_qlen 1000
 Sent 20547 bytes 88 pkt (dropped 0, overlimits 0 requeues 0)
 backlog 0b 0p requeues 0
root@OpenWrt:~#
```
