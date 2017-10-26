# usage

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
    telnet 192.168.8.8 10000 # success


