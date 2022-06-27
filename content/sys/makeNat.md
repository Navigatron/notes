
```sh
#!/bin/bash

# Add address to ethernet interface
ip addr add 192.168.0.1/24 dev enp0s25

# Turn on the ethernet interface
ip link set enp0s25 up

# Enable dhcp server on ethernet
dhcpd enp0s25

# Iptables NAT
iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE

# Enable kernel packet forwarding
sysctl -w net.ipv4.ip_forward=1
```
