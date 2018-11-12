# Lab 5 - DNS

Mr. David Norse Soloman, founder of Double Neutron Star Digital Network Solutions, Son of Daniel N. Soloman (Department of Nuclear Safety) and Mrs. Daisy N. Soloman (Director of Nursing Services), has responded to our requests with "Do Not Survey" - and as such, his Data is Not Shown in our survey of Daily Nutritional Support.

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
7. make sure all configs are good via the above commands
8. Signoff!

> This is where I got to during the first lab session.

# Activity 2 - Does it Work?

## 2.1 - make errors and fix them

deleting a semicolon is all you really need to do.

## 2.2 - rndc and screenshots

Run the following command:

```
rndc status
```

Take a screenshot.

Change the debug level with:

```
rndc trace X
```

where X is the debug level you want. I used 71.

```
rndc status
```

Take a screenshot.

run:

```
rndc reload
```

Take a screenshot.

Just for fun, you may run `man rndc`, scroll to commands, and take a screenshot of the reload command description.

> Note - we never configured rndc to communicate with the server, this could be a problem later? Saving this link here just in case: [config rndc with bind](https://www.centos.org/docs/5/html/Deployment_Guide-en-US/s1-bind-rndc.html)

## 2.3

At this point, the instructions and the report diverge.

Here's my understanding of the report:

#### Question 9
- screenshot of command of choice - for me it's dig
- explain how it's output can be used in troubleshooting
- explain what debug levels are
- include a screenshot of nslookup
- include a screenshot of host

#### Question 10
using info from nslookup, dig, or host:
- explain args used, how useful in troubleshooting
- screenshot showing args used, info provided

Back to activity 2.3.

> This is as far as I've gotten in lab section 2, understanding this part, 2.3, really held me up a lot.

Question 9's requirements are easy, question ten requires the use of command line arguments.

Dig @server name type

type can be A, NS, ANY, whatever you're looking for

-4 forces ipv4, -6 forces ipv6, -p to specify port (53 is default), +trace enables tracing the delegation path, +norecurse turns off the recursive resolve bit

```
dig @10.150.71.2 lambsauce.myco.[name].com CNAME -4 +norecurse -p 53
```

# Activity 3 - Bring on the Clients

## 3.1 - /etc/resolv.conf

The instructions do not tell you how to do this. Fortunately, it's very easy.

Here's what mine looks like:
```
nameserver 10.150.71.2
```

Do that on both CentOS vms, the server and the client.

## 3.2

Set the windows VMs to use LambSauce as the DNS server. Easy.

## 3.3

Instructions don't specify which VMs to start wireshark on, nor which VM to run ping from.

This relates to question 12 on the report. Question 12 doesn't care which VM sends the requests, as long as we can see the request and reply. (One request reply pair, no need to ping every client.)

1. Start wireshark on Lucy
2. Ping wisdom: `ping wisdom.myco.[name].com`
3. stop wireshark - Save this trace to show the request reply pair in Question 12
4. `cat /etc/resolv.conf`

The signoff also wants to be able to resolve requests from windows.

1. Start wireshark on Wisdom
2. Ping Lucy
3. Stop wireshark - no need to save this trace
4. run `ipconfig /all`

Signoff!

> TODO: Save 3.3.reqrep.pcapng from Lucy

# Activity 4 - Second in Command

We're setting up a Windows DNS server as a secondary - in my case, Wisdom.

## 4.1 - Install

The instructions go step-by-step here. Follow those.

## 4.2 - Configure Server

The instructions go pretty much step by step.

For part E, use `myco.[name].com`

For part J, use the ip address as normal - `10.150.71`, it will reverse it on its own.

## 4.3 - Configure Clients

Gotta add `nameserver 10.150.71.3` to the CentOS VMs, and set the secondary on the windows VMs. Easy.

## 4.4 - The End is Near!

This works with questions 14 and 15 in the report.

For 14, we need a screenshot of the dig output showing if the second server is authoritative

For 15, we need a network trace of a zone transfer.

For the signoff, we need a network trace of a DNS request/reply on the secondary server, as well as the transfer trace for question 15.

Steps for capture 1:
1. Activate wireshark on Lucy
2. dig wisdom
3. stop wireshark
4. Save wireshark capture
5. Screenshot dig to show authoritativeness of secondary


Steps for capture 2:
1. Enable named on LambSauce
2. Disable dns on wisdom
3. Update zone file on lambsauce, increment serial number
4. Start wireshark on Wisdom
5. start dns on wisdom - this will check lambsauce, and due to serial number, initiate transfer.
6. stop wireshark, save trace

Signoff.

> At the end of the third lab session, I wrote the above steps but have yet to execute them.



# Bonus Content

## How long did this take me?

Data | Time Spent | Progress
---|---
First lab session | 2 hours | Finish act 1, got signoff 1.
Lab nov05 | 2 hours | Got signoff 2
Lab nov12 | 2 hours | Got signoff 3 - so close to signoff 4, but not close enough.

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
