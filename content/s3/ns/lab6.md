[up](./index.md)

# Network Services - Lab 6 - DNS part II

> TODO - tell about the DNSSEC time sink and how to avoid it.

# Activity Zero - VM setup

- LambSauce
	- CentOS
	- Primary for myco
	- On bench machine 1, the 71 network.
	- IP: 10.150.71.2
- Wisdom
	- Windows Server
	- Secondary for myco
	- On bench machine 2, the 72 network.
	- IP: 10.150.72.2

More VMS will be added later, throughout the lab.

# Activity 1 - Make Wisdom a Primary for theirco

## 1.1

The instructions go through this step-by-step - However, there are some clarifications:

- Step L
	- Use theirco instead of myco
	- Use any IP on your second network that does not cause conflicts.

## 1.2

Add the appropriate variant of the following to `/etc/named.conf`

```
zone "theirco.abc1234.com" {
	type slave;
	file "slaves/theirco.abc1234.com";
	masters{
		10.150.72.2;
	};
};
```

The instructions imply that something needs to be added to the `options` section. This is false.

> My option section contains only `directory "/var/named";` and not even that is needed.

## 1.3

The instructions here are incomplete and inefficient. Perform these steps:

- `systemctl stop named`
- `rm -rf /var/named/slaves/`
- start a wireshark capture
- `systemctl start named`
- When the transfer has appeared, stop wireshark and save.
- Have the wireshark open for the signoff.

Convert the binary file to text with the following command, replacing abc1234 where needed:

```
named-compilezone -f raw -F text -o /var/named/slaves/theirco.abc1234.com.dns theirco.abc1234.com /var/named/slaves/theirco.abc1234.com
```

- -f raw specifies the input is raw
- -F text specifies to create an output file in text
- -o (filename) is where to create the output file
- The FQDN is specified
- The final argument is the file to read

Finally, `cat /var/named/slaves/theirco.abc1234.com.dns`

### Signoff 1

- Have the wireshark of the transfer open
- Have the text zone file open

# Activity 2

## 2.1

Here we're creating another CentOS-BIND-DNS stack to serve a subdomain.

> The instructions have been using subnets

#### Create new VM

On bench machine 1 (the 71 network for me), Full-clone the base CentOS_7.3 VM.

The instructions will call it CentOS2.

I will call it LOOOP.

#### Configure Networking

Use the GUI to set the ip information. I placed LOOOP on 71.100

#### Update YUM:

```bash
yum clean all
yum --disablerepo=\* --enablerepo=base,extras,updates update
```

#### Set the Hostname:

`hostnamectl set-hostname [name]`

#### Disable SELinux:

1. `vim /etc/selinux/config`
2. set `SELINUX=permissive`
3. restart with `shutdown -r now`

Verify changes with `sestatus`

#### Install BIND:

```bash
yum -y install bind bind-utils
firewall-cmd --zone=public --permanent --add-service=dns
```

#### Configure bind

```
vim /etc/named.conf

options{
	directory "/var/named";
};
zone "mgmt.myco.abc1234.com" IN{
	type master;
	file "mgmt.myco.abc1234.com.dns";
};
# Reverse zone here.
```

#### Create Zone files.

The `mgmt` domain needs two fake entries. Almost everything needed can be copy/pasted from CentOS1, or LambSauce in my case.

#### Note on the reverse lookup file.

I don't have subnets, so whichever server is set as DNS for a host will be the one they ask for reverse lookup.

#### fin

- `named-checkconf`
- `named-checkzone`

If both check commands are fine, and it starts, and `systemctl status named -l` looks okay, then it's probably okay.

## 2.2 - Make sure it's okay.

This section has two parts

#### Table

While the report does ask for a DNS topology, nothing needs to be done *In Lab* to create this, as long as you have notes somewhere of what VMs do what job.

#### Network Traces

Report question 3.1 asks about these network traces. You need two:

- A client asking CentOS1 about a host in mgmt
	- This fails, because CentOS1 doesn't know about mgmt
- A client asking CentOS2 about a host in mgmt
	- This should work

> This is where I got in my second lab section.

# Informal, extra notes

## How long did this take me?

My first lab session was less productive than expected, due to a number of things I had to fix from lab5 and errors in the lab6 instructions. I hope those following my notes fare better.

Session | Time Spent | Progress
---|---
In Lab, Nov 19th | 2 Hours | Activity 1, signoff 1.
Lab Nov26th | 2 hours | Through 2.2, no signoff
