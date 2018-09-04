# CentOS is hard

### First, activate root:
```bash
sudo su
```

### Set ip:
```bash
ifconfig eno16777736 10.150.x.y netmask 255.255.255.0 up
```

### Set Gateway:
```bash
ip route add default via 10.150.x.254 dev eno16777736
```

### Set DNS:
```bash
vim /etc/resolv.conf
```

Add This Line:
`nameserver 8.8.8.8`

### Fix YUM:
```bash
yum clean all
yum --disablerepo=\* --enablerepo=base,extras,updates update
```

### SSH with X11 forwarding:
```bash
ssh -CY student@10.150.x.y
```
C enables compression, makes things faster  
Y enables X11 forwarding, trusted, no extra security.
