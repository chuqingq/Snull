# usage

## 0. env

    $ uname -a
    Linux chuqq-hp 4.4.0-21-generic #37-Ubuntu SMP Mon Apr 18 18:33:37 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

## 1. get idle ips

    ping 192.168.8.8 # failed
    ping 192.168.8.9 # failed
    ping 192.168.9.9 # failed
    ping 192.168.9.8 # failed

## 2. `/etc/networks`

no need to add in `/etc/networks`:

    #snullnet0 192.168.8.0
    #snullnet1 192.168.9.0

## 3. `/etc/hosts`

    192.168.8.8 local0
    192.168.8.9 remote0
    192.168.9.9 local1
    192.168.9.8 remote1

## 4. `./snull_load`

## 5. check ping

    ping 192.168.8.9 # success

## 6. check tcp

    nc -l 192.168.9.9 10000
    telnet 192.168.8.9 10000 # success

## 7. trace

    ping -c 192.168.8.9

log:

```
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836153] snull_tx: 0
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836156] snull_hw_tx: 0
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836158] len is 98
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836161] 192.168.8.8:02048 --> 192.168.8.9:25482
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836163] snull_regular_interrupt: 1
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836164] snull_rx: 1
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836167] snull_regular_interrupt: 0
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836179] snull_tx: 1
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836180] snull_hw_tx: 1
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836181] len is 98
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836184] 192.168.9.8:27530 <-- 192.168.9.9:00000
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836185] snull_regular_interrupt: 0
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836186] snull_rx: 0
Oct 26 09:43:53 chuqq-hp kernel: [1024478.836188] snull_regular_interrupt: 1
```

> sn0 send packet, and then invoke snull_regular_interrupt of sn1. so no real interrupt needed.

