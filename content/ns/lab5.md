# Lab 5 - DNS

Mr. David Norse Soloman, founder of Double Neutron Star Digital Network Solutions, Son of Daniel N. Soloman (Department of Nuclear Safety) and Mrs. Daisy N. Soloman (Director of Nusing Services), has responded to our requests with "Do Not Survey" - and as such, his Data is Not Shown in our survey of Daily Nutritional Support.

Remember: Without proper Daily Nutritional Support, one could become a Drowning Non-Swimmer - and then who would manufacture the Doppler Navigation Systems?

# Activity 0

## Part 1 - Nuke past VMS

Delete all the clones, we're making fresh ones.

## Part 2 - New VMs

They're all going on the same network.

Name | Operating System | IP | Role
---|---
LambSauce | CentOS 7 | .2 | Linux DNS Server
Wisdom | Windows 2016 | .3 | Windows DNS Server
Lucy | CentOS 7 | .4 | Linux DNS Client
Wacco | Windows 7 | .5 | Windows DNS Client

## Part 3 - Config VMs

Config the IP of your bench machine.

See [Lab1 - Secret Commands to make CentOS not Terrible](./lab1.md) to config the CentOS vms.

The windows VMs are all GUI based. Setup IP, DNS, Default gateway, netmask, standard stuff.

You can do part 4 for windows while waiting for yum to update.

## Part 4 - Giving VMs Hostnames.

### Windows

If you're using windows 10, the lab will help you out.

[Setting hostname on windows server 2016](https://www.server-world.info/en/note?os=Windows_Server_2016&p=initial_conf&f=3)

Windows 7:  
- Start menu
- control panel
- System and Security
- "Set the name of this computer" under System
- Change Settings

**Restart the windows VMs**

### CentOS 7

Wait for Yum to update on the CentOS machines...

Use `hostnamectl set-hostname [name]`

## Part 5 - Setting SELinux to Permissive

### What *Should* Work (But Sometimes Doesn't)

1. `vim /etc/selinux/config`
2. set `SELINUX=permissive`
3. restart with `shutdown -r now`

### How to tell if it worked

`sestatus` will show you the current mode. We want "permissive", not "enforcing".

### What to do if it didn't work

Use `setenforce permissive`.

**You will have to do this again after *every* restart.**

## Part 6 - pre-launch checklist

- CentOS can ping google
- SELinux is set to permissive (`sestatus`)

# Activity 1 - Installing BIND

This website is great - keep it open somewhere.

[Zytrax - DNS for Rocket Scientists.](http://www.zytrax.com/books/dns/)

## 1.1 - Ah, Skip this.

We are not freshly installing CentOS onto anything, this section is useless.

## 1.2 - Installing BIND on CentOS 7

- Make sure you've updated YUM
- If you restarted after setting ip via ifoncfig, you have to set IP again and add the default gateway again.
- install bind with `yum -y install bind bind-utils`
- Firewall: `firewall-cmd --zone=public --permanent --add-service=dns`
- We've already set SELinux to permissive in Act 0.

## 1.3 - Config Zone Data Files

No actions, just info.

## 1.4 - Config zone data file

No actions, just info.

## 1.5 - Reverse Lookup

Lots of info for reference later

## 1.6 - Loopback zone

More info for reference

## 1.7 - Root hints

More info, not really needed

## 1.8 - named.conf

Real good reference info in here.

## 1.9 - other options

I'll update this later if we need these.

## Signoff

Now we use the above reference info to create the configs.

1. Use 1.8 to make a named.conf file
2. Use 1.4 to make a zone file
3. Test! With the above two, the service should start and run.
	- `named-checkconf`
	- `named-checkzone`
4. Use 1.5 to make a reverse lookup
5. Use 1.6 to make a loopback zone
6. add the reverse and loopback zones the named.conf
7. Test, start service, signoff.

> This is where I got to during the first lab session.

# Activity 2 - Does it Work?

# Bonus Content

## How long did this take me?

Data | Time Spent | Progress
---|---
First lab session | 2 hours | Finish act 1, got signoff 1.

## Storing VMs
- Shutdown All
- Connect Network Drive
- Copy all files over

## Reviving VMs
- Connect Network
- Copy Files
- Setup laptop, water bottle, etc.
- Open VMs
- Power Up VMs
- `setenforce permissive` on CentOS
- configure IP and default gateway on CentOS
