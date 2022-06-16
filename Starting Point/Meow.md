# The very start

Connect to Starting Point VPN before starting the machine

```sh
openvpn starting_point_nuchyobitva.ovpn 
```
After that we spawn the machine and answer some questions:

**What does the acronym VM stand for?**
-*Virtual machine*

**What tool do we use to interact with the operating system in order to issue commands via the command line, such as the one to start our VPN connection? It's also known as a console or shell.**
-*Terminal*

**What service do we use to form our VPN connection into HTB labs?**
-*Openvpn*

**What is the abbreviated name for a 'tunnel interface' in the output of your VPN boot-up sequence output?**
-*tun*

**What tool do we use to test our connection to the target with an ICMP echo request?**
-*ping*

**What is the name of the most common tool for finding open ports on a target?**
-*nmap*

**What username is able to log into the target over telnet with a blank password?**
-*root*

After that we get the access to enter the root flag, so we can submit the flag.
Let's penetrate the given machine by telnet.

```sh
nmap -sC -sV -v {machine IP}
telnet {machine IP}
dir
cat flag.txt
```

1. First we *nmap* the given machine and discover open 23 port.
2. Then we connect to this machine by telnet
3. Here we are already at the root user, so we just scan the directory
4. After that commands we get the flag.txt content and submit the flag

**Fin**
