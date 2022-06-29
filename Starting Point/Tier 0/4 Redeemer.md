# Back to Linux now

We connect to the machine as usual by openvpn.

And here we got some questions to answer.

**Which TCP port is open on the machine?**
-*6379*

**Which service is running on the port that is open on the machine?**
-*redis*

**What type of database is Redis?**
-*In-memory Database*

**Which command-line utility is used to interact with the Redis server?**
-*redis-cli*

**Which flag is used with the Redis command-line utility to specify the hostname?**
-*"-h"*

**Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server?**
-*info*

**What is the version of the Redis server being used on the target machine?**
-*5.0.7*

**Which command is used to select the desired database in Redis?**
-*select*

**How many keys are present inside the database with index 0?**
-*4*

**Which command is used to obtain all the keys in a database?**
-_keys *_

### Actions

First we scan the machine at all ports

```sh
nmap -p- -Pn {Machine IP}
```

And discover an open tcp port with redis service

*6379/tcp open  redis   Redis key-value store 5.0.7*

After that we try to connect to machine by *redis-cli* and get into redis shell

```sh
redis-cli -h {Machine IP}
```

Here we get the access to redis client shell and connect to the "0" db
After that we check the DB size, you can do it with both of this commands

```sh
index 0
dbsize     //this one
keys *     // or this one
```

We understand that there are only *4* elements and one of them is the flag
After we use *scan* command we can find the files names in db

```sh
scan 100
```

Here we get this response:
_1) "flag" 2) "temp" 3) "stor" 4) "numb"_

Here we use the simple *get* command and steal the flag content

```sh
get flag
```

Submit the flag from it and pwn the Redeemer!

**Fin**
