
# Setting up this fucking bullshit

My ipv6 address ends with: ::6680:99FF:FE18:9664

It should start with fe80.

It shall be: `fe80::6680:99ff:fe18:9664` /64

Manually assign it with 

```
ip address add fe80::6680:99ff:fe18:9664/64 dev wlan0
```

PERMISSION FUCKING DENIED I"M FUCKING ROOT YOU PIECE OF SHIT

# Tools

- rdisc6 - router discovery
- ndisc6 - neighbor discovery
- traceroute6 - yep

# I found why permission denied

```
sudo sysctl -a | grep ipv6 | grep disable
```

reveals:

```
net.ipv6.conf.wlan0.disable_ipv6 = 1
```

WHY THE FUCK WAS THAT THERE?

```
sudo sysctl -a | grep net.ipv6.conf.wlan0.disable_ipv6
```

Turn it off with:

```
sudo sysctl -w net.ipv6.conf.wlan0.disable_ipv6=0
```

Cool! Now what?

# Ping my neighbors

```
ping ff02::1%wlan0
```

Fuck yeah, there's lots of ipv6 devices on the link. List them:

```
ip -6 neigh
```

rdisc6 says that there are no routers though.


> Enabled ipv6 connection sharing

IT"S ALIVE, THATS A WIN FOR THE E-DOG


