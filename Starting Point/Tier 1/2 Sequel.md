# Sequel
## Q&A

We connect to the machine as usual by openvpn.

And here we got some questions to answer.

**What does the acronym SQL stand for?**
-*Structured Query Language*

**During our scan, which port running mysql do we find?**
-*3306*

**What community-developed MySQL version is the target running?**
-*MariaDB*

**What switch do we need to use in order to specify a login username for the MySQL service?**
-*"-u"*

**Which username allows us to log into MariaDB without providing a password?**
-*root*

**What symbol can we use to specify within the query that we want to display everything inside a table?**
-*

**What symbol do we need to end each query with?**
-*;*


## Actions

First we scan the machine at all ports

```sh
nmap -p- -Pn {IP}
```

And discover an open mysql port 

*3306/tcp open  mysql*

So we try to connect it

```sh
mysql -u root -h {IP}
```

And we successfully connect to the db
```
MariaDB [(none)]>
```

I tried to learn the help about 20 minutes and didn't get far, so I googled what commands are commonly used in MariaDB and found some (btw "help" didn't include them)

```sh
MariaDB [(none)]> show databases;
```

The console gives us a db list and one of them is called "htb" very familiar name
We need to choose it amongst the other, also let's see the tables

```sh
MariaDB [(none)]> use htb;
MariaDB [htb]>
MariaDB [htb]> show tables;
```

It gives us "config" and "users" tables, let's see what's hot in "config"

```sh
MariaDB [(none)]> select * from config;
```

After that we see some keys, one of them named *flag* with the flag value

I just paste the value and submit the flag ;)

## **Fin**

