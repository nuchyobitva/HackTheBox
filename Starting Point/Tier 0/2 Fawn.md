# Second step

We connect to the machine as usual by openvpn.

And here we got some questions to answer.

**What does the 3-letter acronym FTP stand for?**
-*File transfer protocol*

**Which port does the FTP service listen on usually?**
-*21*

**What acronym is used for the secure version of FTP?**
-*SFTP*

**What is the command we can use to send an ICMP echo request to test our connection to the target?**
-*ping*

**From your scans, what version is FTP running on the target?**
-*vsftpd 3.0.3*

**From your scans, what OS type is running on the target?**
-*Unix*

**What is the command we need to run in order to display the 'ftp' client help menu?**
-*ftp -h*

**What is username that is used over FTP when you want to log in without having an account?**
-*ANONYMOUS*

### Actions

First we scan the machine

```sh
nmap -sV {IP Machine}
```

And discover an open FTP port with its version

*21/tcp open  ftp     vsftpd 3.0.3*

After that you try to connect to machine

```sh
ftp -t {Machine IP}
```

Here we need to log in, so you can remember the lesson's topic and get it.
After that, we get into the FTP console and type **DIR** so we have the catalog.

```sh
-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
```

By **MGET** command we can easily extract the file from machine and submit the flag.

**Fin**
